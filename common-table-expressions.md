# CTE

- Not stored on disk, only exist in duration of query.


```postgresql
WITH cte_name AS (
    SELECT ...
    FROM ...
    WHERE ...
)
SELECT ...
-- multiple select statements can be chained
```

### Table: `orders`

| order_id | customer_id | order_date | total_amount |
|----------|-------------|------------|--------------|
| 1        | 101         | 2023-10-01 | 100.00       |
| 2        | 102         | 2023-10-02 | 150.00       |
| 3        | 101         | 2023-10-03 | 200.00       |
| 4        | 103         | 2023-10-04 | 250.00       |
| 5        | 101         | 2023-10-05 | 300.00       |

### Task:
You are required to write a query using a CTE to find the total spending
of each customer. The output should include the `customer_id` and `total_spending`
and be ordered by `total_spending` in descending order.

### Expected Output:

| customer_id | total_spending |
|-------------|----------------|
| 101         | 600.00         |
| 103         | 250.00         |
| 102         | 150.00         |

### Solution:

```postgresql
WITH cte_table AS (
    SELECT 
        customer_id,
        SUM(total_amount) AS total_spending
    FROM orders
    GROUP BY customer_id
)
SELECT * FROM cte_table
ORDER BY total_spending DESC;
```

