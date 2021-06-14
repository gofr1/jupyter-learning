# Best Practices

## PARTITION BY

Partition the table by a column which is used in the `WHERE` clause or `ON` clause (join). The most commonly used partition column is the **date**.

Use columns with **low cardinality**. If the cardinality of a column will be very high, do not use that column for partitioning. For example, if you partition by a column userId and if there can be 1M distinct user IDs, then that is a bad partitioning strategy.

**Amount of data in each partition**: You can partition by a column if you expect data in that partition to be **at least 1 GB**. Partitioning is not required for smaller tables.

`PARTITION BY` is done on **a single column only**.

## OPTIMIZE

`OPTIMIZE` is required for all tables to which we write data continuously on a daily basis.

`OPTIMIZE` **is not required** for tables that have **static data/reference data** which are rarely updated.

There is **a cost associated** with `OPTIMIZE`. We should run it **more often (daily)** if we want better end-user query performance. We should run it less often if we want to optimize costs.