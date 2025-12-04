# Instructions: taxonomy_create

## Purpose

Induce a set of candidate classes (topics) from a sample of text rows and generate initial names and definitions.

## Inputs

- `sampled_rows`: a list of row objects sampled from the dataset.
- `text_column`: the name of the text column.
- `min_classes`: target minimum number of classes (default: 5).
- `max_classes`: target maximum number of classes (default: 15).

## Outputs

- `classes`: a list of class objects, where each class has:
  - `name`: short string label.
  - `description`: 1–3 sentence description.
  - `example_ids`: list of example row ids or indices.
  - Optional: `keywords`: list of characteristic words/phrases.

## Processing logic (pseudo-code)

- Extract the text from `sampled_rows[text_column]`.
- Preprocess texts:
  - Lowercase.
  - Remove extra whitespace.
  - Optionally remove very common stopwords.
- Compute pairwise or embedded similarities between texts (conceptually; the LLM can approximate by reading and grouping).
- Cluster texts into an initial number of groups:
  - Start with a number of clusters `k_initial` slightly higher than `max_classes` (for example, `max_classes + 3`).
  - Group texts that clearly talk about similar topics into the same cluster.
- For each cluster:
  - Identify common themes and terms.
  - Propose a tentative class name (e.g., `"Billing and refunds"`, `"Login / password issues"`).
  - Write a short description specifying:
    - What kinds of issues belong in this class.
    - What similar but distinct issues belong elsewhere.
- If the number of clusters is greater than `max_classes`:
  - Merge the most similar clusters with overlapping themes until the number of classes is between `min_classes` and `max_classes`.
- If the number of clusters is less than `min_classes`:
  - Split broad clusters into more specific sub-classes where it makes sense.
- Return the list of `classes`.
