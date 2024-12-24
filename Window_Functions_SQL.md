
#Key Window Functions
- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- NTILE()
- SUM(), AVG(), MIN(), MAX() (Aggregate functions used as window functions)
- LAG()
- LEAD()
- FIRST_VALUE()
- LAST_VALUE()

## 1. ROW_NUMBER()
Purpose: Assigns a unique, sequential number to each row in the result set or partition.

Example:

sql
Copy code
SELECT employee_id, department_id, salary,
       ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS row_number
FROM employees;
Explanation:

Numbers rows within each department_id partition, ordered by salary DESC.
Output:

employee_id	department_id	salary	row_number
1	101	100000	1
2	101	90000	2
3	102	120000	1

## 2. RANK()
Purpose: Assigns a rank to each row within a partition. Ties receive the same rank, but gaps appear in ranking for tied values.

Example:

sql
Copy code
SELECT employee_id, department_id, salary,
       RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank
FROM employees;
Explanation:

Employees with the same salary receive the same rank.
Gaps exist in ranks after ties.
Output:

employee_id	department_id	salary	rank
1	101	100000	1
2	101	90000	2
3	101	90000	2
4	101	80000	4

## 3. DENSE_RANK()
Purpose: Similar to RANK(), but without gaps in ranks for tied values.

Example:

sql
Copy code
SELECT employee_id, department_id, salary,
       DENSE_RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS dense_rank
FROM employees;
Output:

employee_id	department_id	salary	dense_rank
1	101	100000	1
2	101	90000	2
3	101	90000	2
4	101	80000	3

##4. NTILE(n)
Purpose: Divides rows into n roughly equal-sized groups and assigns a bucket number to each row.

Example:

sql
Copy code
SELECT employee_id, salary,
       NTILE(3) OVER (ORDER BY salary DESC) AS bucket
FROM employees;
Explanation:

Divides rows into 3 groups based on salary in descending order.
Output:

employee_id	salary	bucket
1	100000	1
2	90000	1
3	80000	2
4	70000	2
5	60000	3

## 5. Aggregate Functions as Window Functions
Purpose: Perform aggregate calculations (e.g., SUM, AVG, MIN, MAX) over a window of rows.

Example:

sql
Copy code
SELECT employee_id, department_id, salary,
       SUM(salary) OVER (PARTITION BY department_id) AS total_salary,
       AVG(salary) OVER (PARTITION BY department_id) AS avg_salary
FROM employees;
Output:

employee_id	department_id	salary	total_salary	avg_salary
1	101	100000	270000	90000
2	101	90000	270000	90000
3	101	80000	270000	90000

## 6. LAG()
Purpose: Retrieves the value of a column from the previous row in the same partition.

Example:

sql
Copy code
SELECT employee_id, salary,
       LAG(salary) OVER (ORDER BY salary DESC) AS previous_salary
FROM employees;
Output:

employee_id	salary	previous_salary
1	100000	NULL
2	90000	100000
3	80000	90000

## 7. LEAD()
Purpose: Retrieves the value of a column from the next row in the same partition.

Example:

sql
Copy code
SELECT employee_id, salary,
       LEAD(salary) OVER (ORDER BY salary DESC) AS next_salary
FROM employees;
Output:

employee_id	salary	next_salary
1	100000	90000
2	90000	80000
3	80000	NULL

## 8. FIRST_VALUE()
Purpose: Retrieves the first value in the window.

Example:

sql
Copy code
SELECT employee_id, salary,
       FIRST_VALUE(salary) OVER (PARTITION BY department_id ORDER BY salary DESC) AS highest_salary
FROM employees;
Output:

employee_id	salary	highest_salary
1	100000	100000
2	90000	100000
3	80000	100000

##9. LAST_VALUE()
Purpose: Retrieves the last value in the window.

Example:

sql
Copy code
SELECT employee_id, salary,
       LAST_VALUE(salary) OVER (PARTITION BY department_id ORDER BY salary DESC ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS lowest_salary
FROM employees;
Explanation:

The ROWS clause ensures the window spans all rows in the partition.
Output:

employee_id	salary	lowest_salary
1	100000	80000
2	90000	80000
3	80000	80000

## Summary Table
Function	Purpose	Use Case Example
ROW_NUMBER()	Assigns a unique number to each row.	Pagination, deduplication.
RANK()	Ranks rows with gaps for ties.	Competition ranking (e.g., sports scores).
DENSE_RANK()	Ranks rows without gaps for ties.	Sequential ranking without gaps.
NTILE()	Divides rows into equal buckets.	Distributing data into groups (e.g., quartiles).
SUM()	Calculates running totals.	Sales analysis, cumulative data.
LAG()	Retrieves value from the previous row.	Comparing current vs. previous values.
LEAD()	Retrieves value from the next row.	Anticipating trends or future comparisons.
FIRST_VALUE()	Retrieves the first value in the window.	Finding top values in groups.
LAST_VALUE()	Retrieves the last value in the window.	Finding bottom values in groups.
