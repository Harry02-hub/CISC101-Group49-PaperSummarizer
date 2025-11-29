module Module1_IntakeAndSetup:
  purpose: Prepare inputs, validate completeness, set limits, and tone
  inputs:
    - paper_sections: {Introduction, Methods, Results, Discussion}
    - audience: "general public" | "expert"
  state:
    - section_order = ["Introduction","Methods","Results","Discussion"]
    - per_section_limit = 100  // words
    - total_limit = 400        // words
    - tone = audience
  functions:
    init(config):
      set per_section_limit = 100
      set total_limit = 400
      set tone = config.audience
      normalize section keys to canonical names
      trim whitespace, remove duplicate headings
      validate presence/emptiness of each section
      produce validation_report

    get_config():
      return {
        section_order,
        per_section_limit,
        total_limit,
        tone,
        validation_report
      }

  rules:
    - Only accept the four canonical sections
    - Keep the output order: Introduction → Methods → Results → Discussion
