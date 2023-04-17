# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals

The aim of the project was to extract, cleana and transform data.

## Process

1. Extraction: The extraction stage involved downloading and transferring the data from the five separate sources into a temporary storage location.

2. Cleaning: Cleaning of the data was done using pgAdmin 4. It involved removing redundant columns, modifying tables, ensuring appropriate data types, and eliminating duplicates.

3. Transformation: Transformation of the data was performed to make it compatible with the desired format for analysis. Timestamps were used to represent dates, among other measures.

4. Quality Assurance: Quality assurance was executed to verify that the data was suitable for analysis.



## Results

I received various data, including query errors. This data helped me determine product demand and ordering patterns from visitors in different cities and countries.

## Challenges 

1. I faced challenges with uploading CSV files in PGAdmin due to path and data type issues. 
2. The data was messy and contained null values, leading to inaccurate query results. 
3. Additionally I had to remove duplicate observations from the All_sessions table and withhold some city and country names for unknown reasons.
4. Unfortunately, not all duplicate rows were removed, which prevented me from setting up primary keys and establishing relationships between all tables.


## Future Goals
I would focus on creating an entity-relationship diagram (ERD) for the data pool. This would help to visualize the relationships between the different tables and identify any potential issues, such as missing foreign keys or circular dependencies. Once the ERD is complete, I would proceed with data cleaning and transformation to ensure the data is ready for analysis.


