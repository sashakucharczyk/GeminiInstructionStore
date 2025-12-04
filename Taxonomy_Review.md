# Instructions: taxonomy_review

## Purpose

Check the induced taxonomy for overlaps, ambiguity, and poor coverage, then suggest merges or refinements.

## Inputs

- `classes`: list of class objects (name, description, example_ids, keywords).
- `sampled_rows`: list of representative rows with their current tentative class assignments (if available).
- `text_column`: the name of the text column.

## Outputs

- `refined_classes`: updated list of class objects with clearer, non-overlapping definitions.
- Optional: `change_log`: a description of merges, splits, renames, or definition tweaks.

## Processing logic (pseudo-code)

- For each pair of classes `(A, B)`:
  - Compare names and descriptions.
  - If they describe essentially the same topic, mark them as candidates for merging.
- For each class:
  - Check if its description is too broad or vague (e.g., "general issues").
  - Check examples assigned to it:
    - If many examples could equally belong to another class, identify the conflicting class and note the overlap.
- Resolve issues:
  - Merge classes that are clearly redundant or extremely similar.
  - If a class is too broad, consider:
    - Splitting it into two more precise classes, **only if** you still stay within the overall class count constraints (5–15).
  - Tighten descriptions:
    - Explicitly state what **does not** belong in a class.
- Verify coverage:
  - Ensure that most sampled rows can be assigned to a specific, meaningful class.
  - If many rows do not fit any existing class:
    - Either introduce a new class capturing that theme, or use a catch-all class.
- Return the updated `refined_classes` and a brief `change_log`.
