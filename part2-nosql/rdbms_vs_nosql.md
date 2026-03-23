## Database Recommendation

For a patient management system, I would strongly recommend MySQL over MongoDB. This decision is based on the core differences in how relational and NoSQL databases manage data consistency.



Healthcare data, including patient records, medication dosages, and allergy details, requires a very high level of accuracy. MySQL follows the ACID model (Atomicity, Consistency, Isolation, Durability), ensuring that all database transactions are executed reliably. For instance, when a doctor updates a patient’s record, the change is instantly reflected across the system, and there is no risk of incomplete or failed transactions.



On the other hand, MongoDB follows the BASE model (Basically Available, Soft state, Eventual consistency). As per the CAP theorem, a distributed database can only guarantee two out of three properties: Consistency, Availability, and Partition Tolerance. MongoDB prioritizes availability and partition tolerance, which means it may not provide immediate consistency. While eventual consistency works well for scenarios like product catalogs, it can be risky in healthcare. For example, a nurse accessing a patient’s record might not see the most recent medication update if the data has not yet synchronized.



That said, introducing a fraud detection module changes the architectural considerations. Fraud detection systems typically process large volumes of unstructured data at high speed, such as server logs or billing transactions. Traditional relational databases like MySQL are not well-suited for horizontal scaling in such high-throughput scenarios.



In this case, a hybrid approach would be most effective. Core patient data should remain in MySQL to ensure ACID compliance and data integrity. Meanwhile, high-volume data streams like logs and billing information can be handled by MongoDB. This allows fraud detection systems to take advantage of NoSQL scalability and flexibility, without affecting the reliability of critical healthcare data.

