# Taxonomy_Create_and_Apply


## What this skill does

This skill takes a CSV file with a free-text column (for example, support tickets, survey responses, product descriptions) and:

1. Creates a **compact taxonomy** of **5 to 15 classes** that:
   - Are mutually exclusive (no overlapping meanings).
   - Are reasonably interpretable by humans.
   - Cover the majority of the dataset.

2. Assigns exactly **one class per row**, so each entry ends up in a single bucket.

3. Outputs:
   - The original CSV with new columns containing the class label and optional confidence.
   - A separate summary of the taxonomy itself (names and definitions) can be produced by the calling agent if desired.

This is useful when you have unstructured text and you need a small, clean set of categories for reporting, dashboards, or downstream models.

## When to use it

Use this skill when:

- You have a CSV with one column of text that describes something: tickets, comments, product info, etc.
- You **don’t already have** a fixed label set and want the classes to emerge from the data.
- You need a small number of non-overlapping classes (5–15) for:
  - KPIs and dashboards
  - Simple supervised models
  - Operational triage flows

Do **not** use this skill when:

- You already have a stable taxonomy and just need classification. (Use a classification-only skill instead.)
- You need very granular, multi-label tags. This skill forces exactly one class per row.

## Inputs

- **File type:** CSV
- **Required information from caller/agent:**
  - `{{FILENAME}}`: path to the input CSV.
  - `{{ID_COLUMN}}`: optional but recommended; unique row identifier (e.g. `id`, `ticket_id`).
  - `{{TEXT_COLUMN}}`: name of the text column used to induce the taxonomy (for example, `description`, `body`, `comment`).
  - `{{OUTPUT_CLASS_COLUMN}}`: name of the new class label column to add (for example, `taxonomy_class`).
  - Optional:
    - `{{OUTPUT_CONFIDENCE_COLUMN}}`: for numeric confidence scores (0–1).
    - `{{MIN_CLASSES}}` and `{{MAX_CLASSES}}` if you want to override defaults (default: 5 and 15).

## Outputs

- **Primary output CSV** (same shape as input, with extra columns):
  - Original columns unchanged.
  - `{{OUTPUT_CLASS_COLUMN}}`:
    - A string label representing the assigned taxonomy class.
    - Each row has exactly one non-empty class label.
  - Optional `{{OUTPUT_CONFIDENCE_COLUMN}}`:
    - A float between 0 and 1 representing how confident the agent is about the class assignment.

- **Implicit taxonomy definition** (not a separate file by default, but easy to derive):
  - A list of all distinct values in `{{OUTPUT_CLASS_COLUMN}}`.
  - For each class, the agent is expected (in `instructions.md`) to maintain internal definitions / criteria.

## Key assumptions & constraints

- The text is in a single language (or at least mostly).
- Each row should be mapped to the **single best** class for its main theme.
- The taxonomy:
  - Has between 5 and 15 classes.
  - Can optionally include a catch-all like `"Other / Misc"` if required to avoid ugly overlaps.
- Classes must be **mutually exclusive in definition**:
  - For example, avoid having both `"Billing issues"` and `"Payment problems"` if they mean the same thing.
  - Avoid ambiguous classes like `"General"` unless used purely as a catch-all.

## Limitations

- The taxonomy is inferred from the dataset; if the dataset is tiny or wildly mixed, the classes may be coarse.
- This skill does **not** guarantee long-term stability of the taxonomy across unrelated datasets.
- Class names and counts can vary depending on the data and the agent’s judgment.

## Known issues

- Confidence is currently a single value, need to rework on a per row
- Output on Gemini gets slow at large file sizes, need to chunk to about 500 per chunk (max)
