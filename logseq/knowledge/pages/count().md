- count(null)  是 0， count(constant ) will be only be 1.c
-
- count(1), count(* )  会计算Null值的 记录， count(colname) 不会计算
-
- 当用count(case when  ...   else null  end) 时也不会计算Null值的记录， 都是对列名计算。
-
- select count(1), count(* ), count(year),
  	count(case when quarter is not null  then 1 else null end ) as cnt_case
   from avenue;
- res: 10  10   8  8