module Module5_Terminology:
  purpose: Extract and define key terms present in the source, tailored to audience
  inputs:
    - paper_sections
    - tone
  functions:
    extract_terms(texts):
      scan for explicitly present domain terms, abbreviations, acronyms
      return unique term list

    define_terms(terms, tone):
      for each term:
        if tone == "general public":
          create one-sentence plain-English definition grounded in context
        else:
          create concise technical clarification or expansion
      return terminology_list

    run():
      terms = extract_terms(paper_sections)
      terminology = define_terms(terms, tone)
      return terminology

  rules:
    - Only define terms found in the source
    - One sentence per term

