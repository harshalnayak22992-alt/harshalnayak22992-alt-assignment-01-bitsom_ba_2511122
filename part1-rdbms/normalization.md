## Anomaly Analysis

1.Insert Anomaly

Example: Since the structure is based on order\_id, it is not possible to insert a new product unless there is an associated order. This creates a dependency that restricts independent data entry.

Rows/Columns Cited: For instance, a value cannot be inserted in product\_name (Column G, e.g., G188) without a corresponding order\_id, as the dependency enforces the presence of an order record.



2.Update Anomaly

Example: Office addresses are duplicated across multiple rows for different orders. If an update is made in one row but missed in another, it results in inconsistency and data anomalies.

Rows/Columns Cited: For example, updating the Delhi office address in O2 but missing the same update in O4 leads to two different address values for the same office. Therefore, updates in Column O (office\_address) must be consistently applied across all related rows.



3.Delete Anomaly

Example: The product\_name column (Column G) stores product details only in the context of orders. If a row is deleted and no other record of that product exists, all related product information is permanently lost.

Rows/Columns Cited: For instance, G13 contains the product “Webcam,” which appears only once in the dataset. Deleting row 13 removes not only the order but also the only record of the product. This results in the loss of associated details such as product\_id (Column F).

## Normalization Justification

While keeping everything in one flat table looks simple at first glance, it is actually a ticking time bomb for data integrity rather than an example of over-engineering. If we continue with a flat CSV structure, we are forced to manage a significant amount of redundant data, which increases the likelihood of errors as the business scales.



Take our sales representative, Deepak Joshi, for instance. His name, email, and Mumbai HQ address are repeated across 83 separate rows in the original dataset. If his office location or email address changes, each of those 83 records must be manually updated. Missing even a single record would result in inconsistent and conflicting contact information for the same individual. In contrast, a normalized SalesReps table allows us to update his details in a single location, ensuring consistency across the system.



The flat table structure also makes catalog management inefficient. For example, if the business wants to introduce a new model of a Standing Desk, the current structure requires an order\_id for every row. As a result, it is not possible to add the new product to the database until a customer places an order, which is a clear limitation.



An even more critical issue is the risk of accidental data loss. The dataset shows only one order (ORD1185) for the Webcam. If Amit Verma cancels this order and the corresponding row is deleted, not only is the transaction removed, but all associated product information—such as product ID, category, and price—is also lost. Through normalization, this data is separated into distinct Products and Orders tables. This ensures that deleting a transaction does not affect the integrity of the product catalog.



Therefore, separating these entities is not over-engineering; rather, it is a fundamental design principle that safeguards data integrity and supports scalability.

