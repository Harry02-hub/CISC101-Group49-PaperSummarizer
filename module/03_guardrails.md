module Module3_Guardrails:
  purpose: Prevent hallucinations, handle missing/empty sections, enforce limits
  inputs:
    - summaries, counts from Module2
    - validation_report, limits from Module1
    - paper_sections
  functions:
    source_fidelity_check(section, summary):
      verify every claim is present in paper_sections[section]
      if mismatch: trim or remove unsupported content

    handle_missing_or_empty(section, text):
      if text is missing:
        return "Section not provided by source.", word_count <= 10
      if text is empty or too short:
        return "Insufficient content in source.", word_count <= 7
      else:
        return null

    enforce_limits():
      for each section:
        if counts[section] > per_section_limit: refine to meet limit
      compute total = sum(counts)
      if total > total_limit: proportionally trim lowest-value sentences

    run():
      for section in section_order:
        placeholder = handle_missing_or_empty(section, paper_sections[section])
        if placeholder:
          summaries[section] = placeholder.text
          counts[section] = placeholder.word_count
        else:
          source_fidelity_check(section, summaries[section])
      enforce_limits()
      ensure final order is correct and tone matches audience
      return {summaries, counts, compliance_report}

  rules:
    - Never add facts beyond source
    - Keep section order intact

