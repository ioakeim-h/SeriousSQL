

## Select all columns

Use `*` to display all columns in a table. Useful when **unfamiliar with a dataset**.

```
SELECT * FROM schema_name.table_name;
```
<hr>

## Select specific columns

```
SELECT
  column_name_1,
  column_name_2
FROM schema_name.table_name;
```
Be wary of the commas used to separate columns. Use `control-f` to quickly highlight and inspect them.

<hr>

## Limit output rows

Use `LIMIT` to restrict the output to the first few rows. This can be important when dealing with unknown data - running `select * from some_big_data_table` can crash entire systems!

```
SELECT * FROM schema_name.table_name
LIMIT 10;
```

<hr><hr>

## Sorting query results

Exploring a dataset usually involves sorting data. This is done with the `ORDER BY` clause which accepts more than one column and sorts data in ascending order by default.

A note on null values: PostgreSQL places null values last unless specified with a `NULLS FIRST`.

<hr>

## Sort by text column

```
SELECT text_column
FROM schema_name.table_name
ORDER BY text_column
LIMIT 5;
```

<hr>

## Sort by numeric/date column

Sorting of this kind is done from lowest to highest for numeric columns or latest to earliest for datetime columns.

```
SELECT numeric_column
FROM schema_name.table_name
ORDER BY 1 DESC
LIMIT 5;
```

We can refer to the `ORDER BY` column by its name or position (also known as index). In the above example, the column was at index 1 and we sorted with descending order using keyword `DESC`.

<hr>

## Sort by multiple columns

Perform a multi-level sort by specifying 2 or more columns with the `ORDER BY` clause.

Multi-level sort both ascending:

```
SELECT * FROM schema_name.table_name
ORDER BY column_a, column_b;
```

Multi-level sort descending & ascending:

```
SELECT * FROM schema_name.table_name
ORDER BY column_a DESC, column_b;
```

Multi-level sort both descending:

```
SELECT * FROM schema_name.table_name
ORDER BY column_a DESC, column_b DESC;
```

<hr>

## Different column order

The output will differ based on which column was provided first to the `ORDER BY` clause.

```
SELECT * FROM schema_name.table_name
ORDER BY column_a DESC, column_b;
```

```
SELECT * FROM schema_name.table_name
ORDER BY column_b, column_a DESC;
```
The above examples produce different outputs. If you specify multiple columns, the result set is sorted by the first column and then that sorted result set is sorted by the second column, and so on. 

<hr><hr>

## Sorting exercises

1. Which customer_id had the latest rental_date for inventory_id = 1 and 2?

```
SELECT 
    customer_id, 
    rental_date,
    inventory_id
FROM dvd_rentals.rental
ORDER BY inventory_id, rental_date DESC
LIMIT 10;
```

2. In the `dvd_rentals.sales_by_film_category` table, which category has the highest total_sales?

```
SELECT * 
FROM dvd_rentals.sales_by_film_category
ORDER BY total_sales DESC
LIMIT 10;
```

3. What is the name of the category with the highest category_id in the dvd_rentals.category table?

```
SELECT
  name,
  category_id
FROM dvd_rentals.category
ORDER BY category_id DESC
LIMIT 5;
```

4. For the films with the longest length, what is the title of the “R” rated film with the lowest replacement_cost in dvd_rentals.film table?

```
SELECT
  title,
  replacement_cost,
  length,
  rating
FROM dvd_rentals.film
ORDER BY length DESC, replacement_cost
LIMIT 10;
```

5. Who was the manager of the store with the highest total_sales in the dvd_rentals.sales_by_store table?

```
SELECT
  manager,
  total_sales
FROM dvd_rentals.sales_by_store
ORDER BY total_sales DESC;
```

6. What is the postal_code of the city with the 5th highest city_id in the dvd_rentals.address table?

```
SELECT 
  postal_code,
  city_id
FROM dvd_rentals.address
ORDER BY city_id DESC
LIMIT 5;
```
