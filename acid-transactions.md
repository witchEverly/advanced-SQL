
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

*Transactions are independent of each other: 
When there are several transactions happen concurrently, 
users should be able to understand a transaction without 
considering the effect of other concurrently existing transaction.*

### Durability
Durability ensures that once a transaction has been committed, it remains that way even in the face of system failures, crashes, or errors. This is usually achieved through the use of database logs and other mechanisms that can recover the database to the last known consistent state.

----------------

# PostgreSQL Transactions

## Syntax

- Transactions are managed using the `BEGIN`, `COMMIT`, and `ROLLBACK` statements. 
- The `BEGIN` statement marks the start of a transaction block, while the `COMMIT` or `ROLLBACK` statements mark the end of a transaction block.

```postgresql
BEGIN TRANSACTION -- start a transaction;
-- queries
-- updates
-- inserts
-- deletes
COMMIT -- commit a transaction;
ROLLBACK -- rollback a transaction;
```

## Four Types of Isolation Levels



### Read Committed

```postgresql
-- postgres default
BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED
    SELECT COUNT(*) FROM table
    SELECT COUNT(*) FROM table;

-- Equailent to READ COMMITTED
BEGIN
    SELECT COUNT(*) FROM table;
    SELECT COUNT(*) FROM table;
```


### Read Uncommitted
```postgresql
BEGIN TRANSACTION 
    ISOLATION LEVEL 
    READ UNCOMMITTED;
```



###  Serializable
> until the first transaction completes, the second transaction cannot start. 
```postgresql
BEGIN TRANSACTION 
    ISOLATION LEVEL 
    SERIALIZABLE;
```


### Repeatable Read
> Allows for insert 
```postgresql
BEGIN TRANSACTION 
    ISOLATION LEVEL 
    REPEATABLE READ;
```




