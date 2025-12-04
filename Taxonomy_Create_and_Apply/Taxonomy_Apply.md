# Instructions: taxonomy_apply

## Purpose

Assign each row in the dataset to exactly one class from the induced taxonomy, optionally with a confidence score.

## Inputs

- `rows`: list of row objects from the full dataset.
- `text_column`: the name of the text column.
- `classes`: list of final class definitions as produced by `taxonomy_induction_tool` and refined by `taxonomy_quality_check_tool`.
- Optional: `include_confidence`: boolean flag.

## Outputs

- `classified_rows`: list of row objects where each row has added fields:
  - `class_label`: the chosen class name.
  - `class_confidence` (optional): float between 0.0 and 1.0.

## Processing logic (pseudo-code)

- For each row in `rows`:
  - Read the text from `row[text_column]`.
  - For each class in `classes`:
    - Assess how well the text matches the class definition:
      - Check for characteristic keywords and phrases.
      - Consider the main intent or problem described.
    - Calculate the Raw Match Confidence Score (between 0 and 1) based on an anthropic review of the text and class.
  - Select the class with the highest match score as `best_class`.
  - If all scores are extremely low and there is a designated catch-all class:
    - Assign the catch-all class and set confidence accordingly.
  - Compute `class_confidence`:
    - Could be the normalized top score or a qualitative mapping:
      - High match → `0.8–1.0`
      - Moderate match → `0.5–0.7`
      - Weak but acceptable match → `0.3–0.4`
  - Attach `class_label = best_class.name` and `class_confidence` (if needed) to the row.
- Return `classified_rows`.
