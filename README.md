# Developer Coding Test Instructions

## Files Provided

You are provided with the following five files:

- **README.md** – This document.
- **desired_output.json** – The expected output. Your program must produce JSON that exactly matches this file.
- **movies.csv** – Contains movie records with various fields.
- **genre.json** – Contains genre mappings.
- **writters.json** – Contains writer information. 

## Task Overview

Write a Python program to:

1. Read and process the input files.
2. Produce an output JSON file that matches `desired_output.json`.

**Important**: Do not use hard-coded values from the desired output. Your solution should work consistently with the provided input files and any other datasets that follow the same structure.

## Data Processing Requirements

### 1. Read and Convert Data

**CSV Parsing and Conversions**

- Read `movies.csv`.
- Convert these fields to numeric types:
  - `rank` → integer
  - `year` → integer
  - `imbd_votes` → integer
  - `imdb_rating` → float
  - `duration` → integer
- Retain other string fields as provided.

**Array Fields**

Split and pair comma-separated fields:

- `cast_id` and `cast_name`
  - Create arrays of objects with keys `"id"` and `"name"`.
- `writter_id` and `writter_name`
  - Create arrays of objects with keys `"id"`, `"name"`, and `"valid"`.

### 2. Enrich Data with External Datasets

**Extra Genres**

- Load `datasets/genre.json`.
- For each movie, add an `extra_genres` array:
  - Include a genre if the movie's ID appears in that genre mapping.

**Writers Validation**

- Load `datasets/writters.json`.
- For each writer, add a boolean field `"valid"`:
  - Set to `true` only if the writer's ID and name match exactly in `writters.json`.

### 3. Calculate Additional Fields (Per-Movie)

For each movie record, compute:

- **rating_percentage**: `imdb_rating × 10`, rounded to two decimals.
- **popularity_score**:
  - Formula: (imdb_rating * imbd_votes) / 1000.0
  - Round to two decimal places.
- **duration_hours**: Convert `duration` to hours, rounded to two decimals.
- **release_date**: Format as `"YYYY-MM-DD"` using January 1st of the movie's year.
- **reception**:
  - Group movies by year.
  - Compute the year average of `imdb_rating`.
  - Calculate `rating_difference` for each movie.
  - Determine `category`:
    - "Above Average" if `rating_difference > 0.5`
    - "Below Average" if `rating_difference < −0.5`
    - "Average" otherwise

Include these in a `"reception"` object with keys: `"year_average_rating"`, `"rating_difference"`, `"category"`.

### 4. Produce the Final Output

- JSON output must be an array containing all enriched movie objects.
- The JSON structure and calculated values must exactly match `desired_output.json`.

## Submission Guidelines

- **Language**: Use Python.
- **Packages**: You may use Python standard libraries (e.g., `csv`, `json`, `datetime`)
- **Execution**: Provide clear instructions on running your program.
- **Evaluation**: Your solution’s final JSON output will be compared with `desired_output.json`.
- **Delivery**: Provide a link to a private Gist on Github

## Context

The reference solution reads and processes data, enriches it, calculates fields, and writes the enhanced array to `output.json`. Your Python implementation must meet the same specifications.

**Good luck!**