- DELETE FROM hr.employees
  WHERE
    id IN (
    SELECT
        id
    FROM (
        SELECT
            id,
            ROW_NUMBER() OVER (
                PARTITION BY email
                ORDER BY email) AS row_num
        FROM
            hr.employees
       
    ) t
    WHERE row_num > 1
  );
-
- use join able:
-
- delete  t1  from hr.employees as t1
    inner join  hr.employees as t2
    where  t1.id > t2.id
        and t1.fullname = t2.fullname;