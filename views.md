# Views

Preview of Example Table(s)

Students Table

| student\_id | first\_name | last\_name | birth\_date | enrolled\_year | gender | fav\_professor | completed\_credits | gpa |
|:------------|:------------|:-----------|:------------|:---------------|:-------|:---------------|:-------------------|:----|
| 1           | Alejandra   | Rodriguez  | 1995-04-08  | 2021           | F      | Dr. Martinez   | 9                  | 3.6 |
| 2           | Mohammad    | Ali        | 1993-10-12  | 2022           | M      | Dr. Wang       | 6                  | 3.8 |
| 3           | Ming        | Xu         | 1992-08-23  | 2021           | M      | Dr. Smith      | 15                 | 3.5 |
| 4           | Aarav       | Patel      | 1994-02-19  | 2023           | M      | Dr. Johnson    | 3                  | 4   |
| 5           | Fatima      | Khan       | 1995-01-14  | 2023           | F      | Dr. Lee        | 3                  | 3.7 |



### Create View

```postgresql
CREATE VIEW students_2022 AS 
    (
        SELECT * 
        FROM students
        WHERE enrolled_year = 2022
);
```

```postgresql
SELECT first_name 
FROM students_2022;
```


### Create or Replace View

```postgresql
CREATE OR REPLACE VIEW students_2022 
    AS (
        SELECT * 
        FROM students
        WHERE enrolled_year = 2023
);

ALTER VIEW students_2022 RENAME TO students_2023;
```

```postgresql
SELECT first_name, enrolled_year
FROM students_2023;
```

| first\_name | enrolled\_year |
|:------------|:---------------|
| Aarav       | 2023           |
| Fatima      | 2023           |
| Maria       | 2023           |
| Chen        | 2023           |


-------

### Northwinds Example

We will be using this view for window function examples in `window-functions.md`

```postgresql
CREATE VIEW northwinds_window_example_data AS 
    (
    SELECT product_id,
       category_id,
       supplier_id,
       unit_price,
       units_in_stock
    FROM products
    );
```

```postgresql
CREATE VIEW view_with_check_option AS
    (
    SELECT id, firstname, lastname
    FROM strings_record
    )
WITH CHECK OPTION;
```

```postgresql
SELECT id, firstname, lastname 
FROM view_with_check_option;
```

| id | firstname | lastname |
| :--- | :--- | :--- |
| 1 | John | Doe |
| 2 | Alice | Smith |
| 3 | Robert | Johnson |

```postgresql
ALTER TABLE strings_record
DROP COLUMN firstname;
```
??
SELECT * FROM view_with_check_option;
```

