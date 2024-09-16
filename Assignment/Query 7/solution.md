Fetch all the physical items ordered in the month of September 2023.

Solution
```SQL
select 
  oi.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID,
  oi.PRODUCT_ID,
  p.PRODUCT_NAME,
  pt.IS_PHYSICAL, 
  os.STATUS_ID, 
  oh.ORDER_DATE 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
  join order_status os on oi.order_id = os.ORDER_ID 
  and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
  join product p on oi.PRODUCT_ID = p.PRODUCT_ID 
  join product_type pt on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID 
where 
  pt.IS_PHYSICAL = 'Y' 
  and os.STATUS_ID = 'ITEM_CREATED' 
  and (
    oh.ORDER_DATE between '2023-09-01' 
    and '2023-09-30'
  );
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/4f3da532-9661-4b64-8612-f81b02b35039)
