# instructions: data_sampling

## Purpose

Select a representative, diverse subset of rows from a CSV text column to use for discovering themes and inducing a taxonomy.

## Inputs

- `rows`: a list of row objects (dict-like) from the CSV.
- `text_column`: the name of the text column to analyze.
- `max_samples` (optional, default: 200): maximum number of rows to keep in the sample.

## Outputs

- `sampled_rows`: a list of row objects representing a diverse sample of the original data.

## Processing logic (pseudo-code)

- Extract `(row_id, text)` pairs from `rows`, focusing on `text_column`.
- Clean each text minimally:
  - Strip leading/trailing whitespace.
  - Convert multiple spaces to single spaces.
- Remove obvious duplicates:
  - Use a case-insensitive set on the cleaned text.
- If the number of unique texts is less than or equal to `max_samples`:
  - Return all unique rows.
- Otherwise:
  - Compute a simple text length metric (short, medium, long) and stratify by length.
  - Optionally, compute a very rough similarity measure (e.g., bag-of-words overlap).
  - Select samples such that:
    - You cover short, medium, and long texts.
    - You avoid picking many near-identical entries.
- Return the selected `sampled_rows`.
