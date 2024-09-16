8. How many orders with a single return were recorded in the last month?

Query
```SQL
select 
 count(tt.order_id) as order_count
from 
  (
    select 
      ri.RETURN_ID as return_id, 
      ri.order_id as order_id 
    from 
      return_item ri 
    group by 
      ri.ORDER_ID 
    having 
      count(distinct ri.RETURN_ID)= 1 
      and ri.ORDER_ID is not null
  ) as tt 
  join return_header rh on rh.return_id = tt.return_id 
where 
  rh.entry_date >= CURDATE() - INTERVAL 1 month;
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/df78212a-92ab-47e5-b007-0fdb7f8786c9)

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/d0aaa5f4-c65b-4d36-ae5f-4c28c00fc8e1)
