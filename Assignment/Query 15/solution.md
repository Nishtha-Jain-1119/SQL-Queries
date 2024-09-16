Find all the orders that have more than one return.

Solution
```SQL
select 
  ORDER_ID, 
  count(distinct RETURN_ID) as return_count 
from 
  return_item 
group by 
  ORDER_ID 
having 
  return_count > 1 
  and ORDER_ID is not null;
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/1c906c69-852c-433f-a127-853ac140ee0c)
