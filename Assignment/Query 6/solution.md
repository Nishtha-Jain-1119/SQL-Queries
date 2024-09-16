Fetch all the physical items completed from Warehouse in September of 2023.

Solution
```SQL
select 
  oi.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oisg.SHIP_GROUP_SEQ_ID,
  oi.PRODUCT_ID,
  p.PRODUCT_NAME,
  f.FACILITY_ID, 
  f.FACILITY_TYPE_ID, 
  os.STATUS_ID, 
  os.STATUS_DATETIME, 
  pt.IS_PHYSICAL 
from 
  order_item oi 
  join order_item_ship_group_assoc oisga on (
    oisga.ORDER_ID = oi.order_id 
    and oi.ORDER_ITEM_SEQ_ID = oisga.ORDER_ITEM_SEQ_ID
  ) 
  join order_item_ship_group oisg on (
    oisg.ORDER_ID = oisga.ORDER_ID 
    and oisg.SHIP_GROUP_SEQ_ID = oisga.SHIP_GROUP_SEQ_ID
  ) 
  join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
  join facility_type ft on f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
  join order_status os on oi.order_id = os.ORDER_ID 
  and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
  join product p on oi.PRODUCT_ID = p.PRODUCT_ID 
  join product_type pt on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID 
where 
  ft.PARENT_TYPE_ID = 'DISTRIBUTION_CENTER' 
  and os.STATUS_ID = 'ITEM_COMPLETED' 
  and (
    os.STATUS_DATETIME between '2023-09-01' 
    and '2023-09-30'
  ) 
  and pt.IS_PHYSICAL = 'Y';
```
Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/0440f7e6-4546-41db-8ad2-f541d5b3f3a9)


