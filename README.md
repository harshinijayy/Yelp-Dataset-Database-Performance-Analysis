# Yelp-Dataset-Database-Performance-Analysis
Comparative analysis of PostgreSQL and MongoDB performance on 1.15M+ records from the Yelp Academic Dataset, using complex queries and benchmarking.
*Data 101 Optional Final Project – UC Berkeley*

## Authors
Harshini Jayaprakash  
Malavika Sushil  
Diya Patil

## Objective
Evaluate the usability, efficiency, and performance of PostgreSQL and MongoDB by running equivalent queries on both platforms and benchmarking:
- Query execution time
- Query complexity and readability
- Schema design and data modeling
- Handling of joins, aggregations, and window functions

## Tools and Technologies
- PostgreSQL  
- MongoDB (PyMongo)  
- SQLAlchemy  
- Jupyter Notebook  
- Python (Pandas, NumPy)  
- Yelp Academic Dataset

## Dataset
We worked with:
- ~150,000 business records
- 500,000 reviews
- 500,000 users  
A total of 1.15M records, cleaned and preprocessed using **reservoir sampling** and loaded into both systems to ensure a fair comparison.

## System Setup
- Created PostgreSQL tables (`business`, `user`, `review`) with proper schema, foreign keys, and optimized indexing.
- Created MongoDB collections with equivalent structures and imported JSON documents after sampling.
- Ensured structural parity between both systems to minimize schema bias during query comparisons.

## Key Queries
We implemented five core queries across both systems:

1. **Top Reviewers Across Cities**  
   Identified top 10 users by review count across multiple cities using SQL joins and MongoDB `$lookup` + `$group`.

2. **Top Monthly Reviewers (Post-2019)**  
   Used SQL `ROW_NUMBER()` and MongoDB `$setWindowFields` to rank top monthly contributors by review volume.

3. **Business + Review Joins**  
   Compared join strategies using SQL `JOIN` vs MongoDB `$lookup`, focusing on review context and business metadata.

4. **User Review Activity Over Time**  
   Aggregated yearly user activity to understand long-term review trends and active users.

5. **Top “Useful” Reviewers**  
   Ranked users by total “useful” votes on reviews, combining review and user tables/collections.

## Results Summary
| Criteria            | PostgreSQL                       | MongoDB                          |
|---------------------|----------------------------------|----------------------------------|
| Query Readability   | Clear, concise (SQL syntax)      | Verbose, pipeline-heavy          |
| Join Operations     | Fast with foreign keys           | Requires `$lookup` + `$unwind`   |
| Performance         | < 1 second (avg.)                | 3–6 seconds (avg.)               |
| Flexibility         | Strict schema, easier debugging  | Flexible schema, harder to tune  |

- **PostgreSQL** was faster, more transparent, and easier to debug—ideal for structured datasets.
- **MongoDB** was more flexible but required complex pipelines and indexing to reach comparable speed.

## Conclusions
- PostgreSQL outperformed MongoDB in most tasks, especially for joins, grouping, and sorting operations.
- MongoDB pipelines are powerful but require more setup and suffer in performance without indexing.
- Relational databases remain ideal for structured analytics, while NoSQL systems may be better for nested, frequently updated data.


