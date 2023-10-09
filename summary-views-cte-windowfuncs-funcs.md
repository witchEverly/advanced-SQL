# VIEWS

```postgresql
/*

----------------------------
CREATE VIEW <view_name> AS
    <query>;
-----------------------------
CREATE OR REPLACE VIEW <view_name> AS
    <query>;
-----------------------------
CREATE OR REPLACE VIEW <view_name> AS
    <query>
WITH CHECK OPTION;
-----------------------------

 */
 
CREATE VIEW view_name AS
    SELECT * FROM table_name;
SELECT * FROM view_name;
```

# FUNCTION

```postgresql
/* 
---------------------------- 
CREATE OR REPLACE FUNCTION <func_name>()
RETURNS <return_dtype> AS 
$$
    <query>
$$ 
LANGUAGE SQL;
-----------------------------
*/ 

CREATE OR REPLACE FUCNTION func_name()
RETURNS int 
    (
    SELECT col from table
    )
    
SELECT func_name();
```


# CTE (Common Table Expression)
- Can't be indexed
- Temporary

```postgresql
/*
----------------------------
WITH <cte_name> AS (<query>)
SELECT * FROM <cte_name>
-----------------------------
*/


WITH newtable AS 
    (
    SELECT 
        depname, 
        empno, 
        salary, 
        avg(salary) 
            OVER (PARTITION BY depname)
    FROM empsalary
    )

SELECT empno, salary
FROM newtable
WHERE avg > 6500;
```


| empno | salary |
|:------|:-------|
| 6     | 8000   |
| 7     | 8500   |
| 2     | 7500   |
| 3     | 6200   |
| 1     | 7000   |




# WINDOW FUNCTION

##### `OVER()`

```postgresql
SELECT order_id,
       order_date OVER()
FROM orders
```

##### `OVER(PARTITION BY)`

```postgresql

```

##### `OVER(PARTITION BY ORDER BY)`

```postgresql

```

##### `OVER(PARTITION BY ORDER BY ROWS BETWEEN)`

```postgresql

```

##### `OVER(PARTITION BY ORDER BY ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)`

```postgresql

```



```postgresql

```

