## ETL Decisions

### Decision 1 – Ensuring Consistent Date Formats and Implementing Surrogate Keys



Problem: The raw date column contained highly inconsistent string formats, mixing DD/MM/YYYY , DD-MM-YYYY , and YYYY-MM-DD . If loaded directly, time-series analysis would be impossible because the database wouldn't recognize the strings as chronologically ordered dates.
Resolution: During extraction, the dates were parsed into standard Python datetime objects to ensure uniformity. For the load phase into the data warehouse, the dates were formatted into a strict YYYY-MM-DD string for the full\_date attribute, and transformed into an integer format ( YYYYMMDD ) to serve as an optimized, non-null surrogate primary key ( date\_id ) for the dim\_date table.



### Decision 2 – Handling Missing Store Location Data Through Imputation



Problem: The store\_city column had 19 explicit NULL values in the raw dataset. Leaving these as NULL would break the NOT NULL constraint of our dimension tables and cause issues for regional sales reporting.
Resolution: I analyzed the dataset and identified that store\_city could be directly derived from store\_name (e.g., “Chennai Anna” consistently maps to Chennai). Based on this, I created a mapping dictionary from complete records and used it to fill the 19 missing store\_city values before generating the dim\_store table.



### Decision 3 – Standardizing Product Category Naming and Casing



Problem: The category column suffered from free-text data entry issues. It contained a mix of lowercase and title case ("electronics" vs "Electronics"), as well as singular and plural forms ("Grocery" vs "Groceries"). This fragmentation would cause aggregate queries to split revenue across identical categories.
Resolution: I applied string transformations to remove extra whitespace and convert all category values to Title Case. Additionally, I mapped “Grocery” to “Groceries” to ensure consistent categorization and proper aggregation under a single unified dimension

