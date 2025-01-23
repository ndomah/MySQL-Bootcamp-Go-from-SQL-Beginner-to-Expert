# Window Functions
- Allow you to perform calculations across a subset of rows (a window) related to the current row, without collapsing the rows into a single aggregate result
- Unlike aggregate functions (e.g., SUM, AVG), window functions retain individual rows while providing calculated values across a defined set of data

**Key Features of Window Functions**:
- Operate on a "window" of rows that are related to the current row
- Do not group rows, meaning each row still appears in the result set
- Enable complex analytics, such as running totals, ranking, and moving averages
- Partitioning and ordering allow calculations over specific groups and sequences

## Using `OVER()`


## PARTITION BY


## ORDER BY with Windows


## `RANK()`


## `DENSE_RANK` & `ROW_NUMBER()`


## NTILE()


## FIRST_VALUE


## LEAD and LAG


