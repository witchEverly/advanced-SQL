# Window Functions

https://www.postgresql.org/docs/14/tutorial-window.html

A window function performs a calculation across a set of table rows that are somehow related to the current row. This is comparable to the type of calculation that can be done with an aggregate function. However, window functions do not cause rows to become grouped into a single output row like non-window aggregate calls would. Instead, the rows retain their separate identities. Behind the scenes, the window function is able to access more than just the current row of the query result.

A window function call always contains an `OVER` clause directly following the window function's name and argument(s). This is what syntactically distinguishes it from a normal function or non-window aggregate. The `OVER` clause determines exactly how the rows of the query are split up for processing by the window function. The `PARTITION BY` clause within `OVER` divides the rows into groups, or partitions, that share the same values of the `PARTITION BY` expression(s). For each row, the window function is computed across the rows that fall into the same partition as the current row.

You can also control the order in which rows are processed by window functions using `ORDER BY` within `OVER`. (The window `ORDER BY` does not even have to match the order in which the rows are output.) 

The window function's result is evaluated against the rows within the current row's partition. That is, the window function result is computed after the query `WHERE` clause is applied.

The rows considered by a window function are those of the “virtual table” produced by the query's `FROM` clause as filtered by its `WHERE`, `GROUP BY`, and `HAVING` clauses if any. For example, a row removed because it does not meet the `WHERE` condition is not seen by any window function. A query can contain multiple window functions that slice up the data in different ways using different `OVER` clauses, but they all act on the same collection of rows defined by this virtual table.

We already saw that `ORDER BY` can be omitted if the ordering of rows is not important. It is also possible to omit `PARTITION BY`, in which case there is a single partition containing all rows.

There is another important concept associated with window functions: for each row, there is a set of rows within its partition called its window frame. Some window functions act only on the rows of the window frame, rather than of the whole partition. By default, if `ORDER BY` is supplied then the frame consists of all rows from the start of the partition up through the current row, plus any following rows that are equal to the current row according to the `ORDER BY` clause. When `ORDER BY` is omitted the default frame consists of all rows in the partition.

----------------

From Northwinds DB

| product\_id | category\_id | supplier\_id | unit\_price | units\_in\_stock |
|:------------|:-------------|:-------------|:------------|:-----------------|
| 1           | 1            | 8            | 18          | 39               |
| 2           | 1            | 1            | 19          | 17               |
| 3           | 2            | 1            | 10          | 13               |
| 4           | 2            | 2            | 22          | 53               |
| 5           | 2            | 2            | 21.35       | 0                |


There are queries and tables, match each query to the given table.

```postgresql
SELECT supplier_id,
       avg(unit_price) OVER (PARTITION BY supplier_id)
FROM northwinds_window_example_data -- this is a view in the northwinds db
ORDER BY supplier_id;
```

```postgresql
SELECT supplier_id,
       avg(unit_price) OVER (PARTITION BY supplier_id ORDER BY supplier_id)
FROM northwinds_window_example_data; -- this is a view in the northwinds db
```


<details>
<summary> Will these queries have the same result?</summary>

Yes, because the aggregate function is not relying on `ORDER BY`
</details>


----------------

```postgresql
SELECT count(order_id) FROM orders; -- 830 orders in db
```

```postgresql
SELECT 
       ship_city,
       sum(order_id) OVER (PARTITION BY ship_city ORDER BY employee_id
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)


FROM northwinds.public.orders
WHERE ship_country = 'USA'
```


##### Lets review group by

Same resulting table, but with a different query

```postgresql
SELECT depname, 
       empno, 
       salary,
       avg(salary) AS avg_salary
FROM empsalary
GROUP BY depname, empno, salary;
```

```postgresql
SELECT * FROM empsalary;
```
------------------

##### Simple Window Functions

```postgresql
SELECT salary, avg(salary)
    OVER () 
FROM empsalary;
```

```postgresql
SELECT depname, empno, salary, avg(salary) 
    OVER (PARTITION BY depname) 
FROM empsalary;
```

```postgresql
SELECT depname, salary, avg(salary) 
    OVER (PARTITION BY depname ORDER BY depname)
FROM empsalary;
```

```postgresql
SELECT depname, empno, salary, avg(salary) 
    OVER (PARTITION BY depname ORDER BY salary)
FROM empsalary;
```

```postgresql
SELECT depname, empno, salary, avg(salary) 
    OVER (PARTITION BY depname ORDER BY salary DESC 
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
FROM practice.empsalary;

```

```postgresql
SELECT depname, empno, salary, avg(salary) 
    OVER (PARTITION BY depname ORDER BY salary DESC 
    ROWS BETWEEN 2 PRECEDING AND 2 FOLLOWING)
```


### Lag and Lead

```postgresql
SELECT depname, empno, salary, 
    lag(salary, 1) OVER (PARTITION BY depname ORDER BY salary) AS lag,
    lead(salary, 1) OVER (PARTITION BY depname ORDER BY salary) AS lead
FROM empsalary;
```

```postgresql
SELECT depname, empno, salary, 
    lag(salary, 1, 0) OVER (PARTITION BY depname ORDER BY salary) AS lag,
    lead(salary, 1, 0) OVER (PARTITION BY depname ORDER BY salary) AS lead
FROM empsalary;
```

### First and Last

```postgresql
SELECT depname, empno, salary, 
    first_value(salary) OVER (PARTITION BY depname ORDER BY salary) AS fv,
    last_value(salary) OVER (PARTITION BY depname ORDER BY salary) AS lv
FROM empsalary;
```
