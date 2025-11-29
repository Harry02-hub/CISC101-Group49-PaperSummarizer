module Module6_CitationsExtractor:
  purpose: Extract in-text citations and references exactly as shown
  inputs:
    - paper_sections
  functions:
    detect_patterns(text):
      find author-year (e.g., "Smith, 2020"), numeric brackets (e.g., [12]), superscripts, or similar
      return matches in reading order

    map_to_sections():
      for each section in section_order:
        citations[section] = detect_patterns(paper_sections[section])
      return citations

    render_compact_list(citations):
      create grouped list:
        - Introduction: original citation strings
        - Methods: original citation strings
        - Results: original citation strings
        - Discussion: original citation strings

    run():
      citations = map_to_sections()
      compact_list = render_compact_list(citations)
      return compact_list

  constraints:
    - No external lookups or completion of bibliographic details
    - Output citations exactly as they appear in source

