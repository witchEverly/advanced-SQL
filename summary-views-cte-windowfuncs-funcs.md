
# CTE

```postgresql
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

```postgresql
```

# FUNCTION

```postgresql
CREATE OR REPLACE FUCNTION func_name()
RETURNS int 
    (
    SELECT col from table
    )
    
SELECT func_name();
```

# WINDOW FUNCTION

### `OVER()`

```postgresql

```

### `OVER(PARTITION BY)`

```postgresql

```

### `OVER(PARTITION BY ORDER BY)`

```postgresql

```

### `OVER(PARTITION BY ORDER BY ROWS BETWEEN)`

```postgresql

```

### `OVER(PARTITION BY ORDER BY ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)`

```postgresql

```



```postgresql
select version();
```

