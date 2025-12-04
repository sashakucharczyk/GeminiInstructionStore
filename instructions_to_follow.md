Use the following files to implement these instructions. One is a .CSV input file and the other four are instructions for specific tasks.

`root` = `https://github.com/sashakucharczyk/GeminiInstructionStore`
`raw_input.csv` = `root/raw_input.csv`
`Data_Sampling.md` = `root/Data_Sampling.md`
`Taxonomy_Create.md` = `root/Taxonomy_Create.md`
`Taxonomy_Review.md` = `root/Taxonomy_Review.md`
`Taxonomy_Apply.md` = `root/Taxonomy_Apply.md`

Can you please do the following 4 activities in sequence and then provide me with an output csv?

**Activity 1**
Use the instructions found in `Data_Sampling.md` on `raw_input.csv`. Create a temporary file called `temp_sample.csv` with the results.

**Activity 2**
Use the instructions found in `Taxonomy_Create.md` on `temp_sample.csv` file. Create a file called `Created_Taxonomy.csv` with the results. It should have at least the following 3 colums: {`id`, `taxonomy_id`, `description`} where `id` is the row number and `taxonomy_id` is a unique identifier for the taxonomy (ex: c1 or c2).

**Activity 3**
Use the instructions founds in `Taxonomy_Review.md` to review the taxonomy created in the previous step that were stored in `Created_Taxonomy.csv`. If the instructions require it, loop back to `Activity 2`. Do not proceed to `Activity 4` until the results pass the review.

**Activity 4**
Use the instructions found in `Taxonomy_Apply.md` to apply the taxonomy to `raw_input.csv`. Provide the results as `Applied_Output.csv`.

Provide the final `Created_Taxonomy.csv` and `Applied_Output.csv` in chat