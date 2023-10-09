# Functions

--------------


```postgresql
CREATE OR REPLACE FUNCTION product_info(PRODUCT_ID)
RETURNS numeric AS
    $$
    SELECT 
    units_in_stock - units_on_order
    FROM products
    WHERE product_id = product_id
    $$
LANGUAGE sql;
```

--------------

```postgresql
DROP FUNCTION IF EXISTS concat(a TEXT, b TEXT);

CREATE OR REPLACE FUNCTION concat(a TEXT,b TEXT)
RETURNS TEXT AS 
    $$  
    SELECT a || b
    $$
LANGUAGE sql;
```

```postgresql
SELECT concat('hello', ' world! ');
```

---------------

```postgresql
DROP FUNCTION IF EXISTS time_until_exam();

CREATE OR REPLACE FUNCTION time_until_exam()
RETURNS interval AS
    $$
    SELECT 
        TO_TIMESTAMP('2023-10-10 09:00', 'YYYY-MM-DD HH24:MI') - CURRENT_TIMESTAMP
    $$
LANGUAGE sql;
```

```postgresql
SELECT time_until_exam();
```

--------------------
