module Module2_SectionLoops:
  purpose: Summarize each section independently with tone and word limits
  inputs:
    - config from Module1
    - paper_sections
  functions:
    summarize_section(section_text, tone, limit):
      use only content from section_text
      for "general public": plain language, minimal jargon, short sentences
      for "expert": preserve domain terms, methods, statistics if present
      condense to <= limit words
      return {summary, word_count}

    run():
      for section in config.section_order:
        text = paper_sections[section]
        {summary, count} = summarize_section(text, config.tone, config.per_section_limit)
        store summaries[section] = summary
        store counts[section] = count
      return {summaries, counts}

  constraints:
    - No cross-section borrowing
    - No invented data, numbers, or claims
    - <= 100 words per section

if summary_level == "short": 
    produce 1–2 sentence summary
if summary_level == "detailed":
    produce paragraph and 3–5 bullets

