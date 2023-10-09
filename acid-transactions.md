
# Postgres ACID Transactions

Notes:

- By default, PostgreSQL executes transactions in "auto commit" mode.
  - each SQL statement is a transaction
  - each SQL statement is committed when it completes 
  - each SQL statement is rolled back if it fails

----------------
## Summary
- Atomicity: A transaction is all or nothing. If it fails, changes are rolled back.
- Consistency: Transactions take a database from one valid state to another.
- Isolation: Transactions don't interfere with each other when executed concurrently.
- Durability: Once committed, transactions remain so, even after system failures.
----------------

The term "ACID" stands for Atomicity, Consistency, Isolation, and Durability. These are a set of properties that guarantee that database transactions are processed reliably, which is crucial for the smooth operation of many types of software and systems. Here's a breakdown of each component:

### Atomicity
Atomicity ensures that a transaction is treated as a single "unit of work," which either completes in its entirety or not at all. For example, if a transaction includes multiple SQL queries, either all queries will be executed, or none will. If something goes wrong during the transaction, any changes are rolled back to the previous state.

### Consistency
Consistency ensures that a transaction takes a database from one consistent state to another consistent state. **This means that all data in the database will be valid according to the predefined rules, constraints, and cascades.**

### Isolation
Isolation ensures that concurrent transactions are executed in such a way that their **interleaved** execution has the same effect as if they were executed sequentially. This is important to ensure that one transaction doesn't interfere with another.

### Durability
Durability ensures that once a transaction has been committed, it remains that way even in the face of system failures, crashes, or errors. This is usually achieved through the use of database logs and other mechanisms that can recover the database to the last known consistent state.

----------------

## PostgreSQL Transaction Syntax

- Transactions are managed using the `BEGIN`, `COMMIT`, and `ROLLBACK` statements. 
- The `BEGIN` statement marks the start of a transaction block, while the `COMMIT` or `ROLLBACK` statements mark the end of a transaction block.






