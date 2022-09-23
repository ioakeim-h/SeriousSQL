
## How many records

Use `COUNT` to count the number of records.

```
SELECT
    COUNT(*) AS row_count
FROM schema_name.table_name;
```
`COUNT(1)` is a common alternative to `COUNT(*)` and provides the same result.

Keyword `AS` is used as a "column alias" to specify a name for the `COUNT(*)` expression. Aliases vastly improve readability and can be used to name other SQL expressions.

<hr><hr>

## Show unique column values

Use `DISTINCT` to obtain unique values from a column.

```
SELECT DISTINCT
    column_name
FROM schema_name.table_name;
```
<hr>

## Count of unique values

Use `COUNT` and `DISTINCT` to get the number of unique values from a column.

```
SELECT
    COUNT(DISTINCT column_name) 
FROM schema_name.table_name;
```

<hr><hr>

## Group by counts

`GROUP BY` splits the dataset into groups based on the values of the selected columns.

Use `GROUP BY` with `COUNT` to generate a frequency value counts output.

```
SELECT
  column_name,
  COUNT(*) AS frequency
FROM schema_name.table_name
GROUP BY column_name
ORDER BY frequency DESC;
```

**Remember:** only 1 row will ever be returned for each individual group from a `GROUP BY` !

<br>

**Bonus:** Add a percentage column

```
SELECT
  column_name,
  COUNT(*) AS frequency,
  ROUND(
    100 * COUNT(*)::NUMERIC / SUM(COUNT(*)) OVER (),
    2
  ) AS percentage
FROM schema_name.table_name
GROUP BY column_name
ORDER BY frequency DESC;
```

```::NUMERIC``` right after the ```COUNT(*)``` is to avoid the dreaded integer floor division.

<hr>

## Group by counts for multiple column combinations

When analysing more than one column, we just need to specify the additional columns in the `GROUP BY`.

```
SELECT
  column_name1,
  column_name2,
  COUNT(*) AS frequency
FROM schema_name.table_name
GROUP BY column_name1, column_name2
ORDER BY frequency DESC
LIMIT 5;
```

<hr><hr>

## Exercises

1. Which actor_id has the most number of unique film_id records in the dvd_rentals.film_actor table?

```
SELECT
  actor_id,
  COUNT(DISTINCT film_id) AS unique_film_id
FROM 
  dvd_rentals.film_actor
GROUP BY
  actor_id
ORDER BY
  unique_film_id DESC
LIMIT 5;
```

2. How many distinct fid values are there for the 3rd most common price value in the dvd_rentals.nicer_but_slower_film_list table?

```
SELECT 
  price,
  COUNT (DISTINCT fid) AS unique_fid
FROM
  dvd_rentals.nicer_but_slower_film_list
GROUP BY
  price
ORDER BY
  unique_fid DESC;
```

3. How many unique country_id values exist in the dvd_rentals.city table?

```
SELECT
  COUNT(DISTINCT country_id)
FROM
  dvd_rentals.city;
```

4. What percentage of overall total_sales does the Sports category make up in the dvd_rentals.sales_by_film_category table?

```
SELECT
  category,
  ROUND(
    100 * total_sales::NUMERIC / SUM(total_sales) OVER (),
    2
  ) AS percentage
FROM 
  dvd_rentals.sales_by_film_category;
```

5. What percentage of unique fid values are in the Children category in the dvd_rentals.film_list table?

```
SELECT
  category,
  ROUND (
    100 * COUNT(DISTINCT fid)::NUMERIC / SUM(COUNT(DISTINCT fid)) OVER(),
    2
  ) AS percentage
FROM
  dvd_rentals.film_list
GROUP BY
  category;
  ```


