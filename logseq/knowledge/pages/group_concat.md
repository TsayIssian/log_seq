- ```
  SELECT col1, col2, ..., colN
  GROUP_CONCAT ( [DISTINCT] col_name1 
  [ORDER BY clause]  [SEPARATOR str_val] ) 
  FROM table_name GROUP BY col_name2;
  - **col1, col2, ...colN : **These are the column names of table.
  **col_name1: **Column of the table whose values are concatenated into a single field for each group.
  **table_name: **Name of table.
  **col_name2: **Column of the table according to which grouping is done.
  ```
-
- used to concatenate data from multiple rows into one field
- Using simple GROUP_CONCAT() function-
- ```
  SELECT emp_id, fname, lname, dept_id, 
  GROUP_CONCAT ( strength ) as "strengths" 
  FROM employee group by emp_id;
  ```
- **Output:**
	- | emp_id | fname | lname | dept_id | strengths |
	  | ---- | ---- | ---- |
	  | 1 | mukesh | gupta | 2 | Leadership, Responsible, Quick-learner |
	  | 2 | devesh | tyagi | 2 | Punctuality, Quick-learner |
	  | 3 | neelam | sharma | 3 | Hard-working, Self-motivated |
	  | 4 | keshav | singhal | 3 | Listening, Critical thinking |
	  | 5 | tanya | jain | 1 | Hard-working, Goal-oriented |