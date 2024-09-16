Fetch the following columns for completed order items for sales orders of SM_STORE product store and that are physical items.
 - ORDER_ID
 - ORDER_ITEM_SEQ_ID
 - PRODUCT_ID
 - PRODUCT_TYPE_ID
 - IS_PHYSICAL
 - IS_DIGITAL
 - SALES_CHANNEL_ENUM_ID
 - ORDER_DATE
 - ENTRY_DATE
 - STATUS_ID
 - STATUS_DATETIME
 - ORDER_TYPE_ID
 - PRODUCT_STORE_ID 

Solution
```SQL
select 
  oh.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oi.PRODUCT_ID, 
  p.PRODUCT_TYPE_ID, 
  pt.IS_PHYSICAL, 
  pt.IS_DIGITAL, 
  oh.SALES_CHANNEL_ENUM_ID, 
  oh.ORDER_DATE, 
  oh.ENTRY_DATE, 
  os.STATUS_ID, 
  os.STATUS_DATETIME, 
  oh.ORDER_TYPE_ID, 
  oh.PRODUCT_STORE_ID 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
  join order_status os on oi.order_id = os.ORDER_ID 
  and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID 
  join product p on oi.PRODUCT_ID = p.PRODUCT_ID 
  join product_type pt on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID 
where 
  os.STATUS_ID = 'ITEM_COMPLETED' 
  and oh.ORDER_TYPE_ID = 'SALES_ORDER' 
  and oh.PRODUCT_STORE_ID = 'SM_STORE' 
  and pt.IS_PHYSICAL = 'Y';
```
Result
![image](https://github.com/Nishtha-Jain-1119/SQL-Queries/assets/127538617/7422f2e8-88e1-4e60-ae43-e99ff8fa6264)
