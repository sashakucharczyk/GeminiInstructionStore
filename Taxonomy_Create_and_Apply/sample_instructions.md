I have provided you with 5 files. 1 is a 1000 row CSV to be used as an input file for review. 4 are sets of instructions. Can you please do the following 4 activities in sequence and then provide me with an output csv?

**Activity 1**
Use the instructions found in `Data_Sampling.md` on `raw_input.csv`. Create a temporary file called `temp_sample.csv` with the results.

**Activity 2**
Use the instructions found in `Taxonomy_Create.md` on `temp_sample.csv` file. Create a file called `Created_Taxonomy.csv` with the results. It should have at least the following 3 colums: {`id`, `taxonomy_id`, `description`} where `id` is the row number and `taxonomy_id` is a unique identifier for the taxonomy (ex: c1 or c2).

**Activity 3**
Use the instructions founds in `Taxonomy_Review.md` to review the taxonomy created in the previous step that were stored in `Created_Taxonomy.csv`. If the instructions require it, loop back to `Activity 2`. Do not proceed to `Activity 4` until the results pass the review.

**Activity 4**
Use the instructions found in `Taxonomy_Apply.md` to apply the taxonomy to `raw_input.csv`. Provide the results as `Applied_Output.csv`.

Provide the final `Created_Taxonomy.csv` and `Applied_Output.csv` in chat