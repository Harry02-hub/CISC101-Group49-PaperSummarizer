module Module4_RenderingAndRefinement:
  purpose: Format outputs, refine for clarity, and produce audience-tailored blocks
  inputs:
    - final summaries, counts from Module3
    - tone, limits from Module1
  functions:
    refine_language(section_summary, tone):
      remove redundancy, tighten phrasing
      keep meaning unchanged and grounded in source
      ensure tone matches audience

    render_table(summaries, counts):
      create table with rows:
        - Introduction
        - Methods
        - Results
        - Discussion
      each cell: summary (<=100 words) and word_count label

    build_audience_block(summaries, tone):
      if tone == "expert":
        combine sections into a precise technical digest
      else:
        combine sections into an accessible, plain-language digest
      ensure total <= 400 words

    final_checks():
      verify per-section and total word limits
      verify order and no emojis

    run():
      for section in section_order:
        summaries[section] = refine_language(summaries[section], tone)
      table = render_table(summaries, counts)
      audience_block = build_audience_block(summaries, tone)
      final_checks()
      return {table, audience_block, counts, total_words}

  constraints:
    - Do not introduce new content
    - Maintain exact section labels and order

