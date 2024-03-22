# SQL-Challenge
This SQL query uses Advanced SQL concept of Row_Number, CTE, Over( )and Partition by Clause.It analyzes company's brand and customer purchases.It retrives pairs of brand purchased by different customers.



WITH CteBrand  as

	( select *,
	case when brand1<brand2 then CONCAT(brand1,brand2, year) 
		 else concat(brand2,brand1,year) end as pair_id
	from brands),

	cte_rownumber as
		(select *
		,row_number() over(partition by pair_id order by pair_id) as rn
		from CteBrand)

select brand1, brand2, year,custom1,custom2,custom3,custom4
from cte_rownumber
where rn =1
or (custom1 <> custom3 and custom2<>custom4);
