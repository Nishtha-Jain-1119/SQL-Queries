Fetch the following columns for completed return items of SM_STORE for ecom return channel.
- RETURN_ID 
- ORDER_ID
- PRODUCT_STORE_ID 
- STATUS_DATETIME
- ORDER_NAME 
- FROM_PARTY_ID 
- RETURN_DATE 
- ENTRY_DATE
- RETURN_CHANNEL_ENUM_ID

Solution
```SQL
select 
  rh.RETURN_ID, 
  ri.ORDER_ID, 
  oh.PRODUCT_STORE_ID, 
  rs.STATUS_DATETIME, 
  oh.ORDER_NAME, 
  rh.FROM_PARTY_ID, 
  rh.RETURN_DATE, 
  rh.ENTRY_DATE, 
  rh.RETURN_CHANNEL_ENUM_ID 
from 
  return_header rh 
  join return_item ri on rh.RETURN_ID = ri.RETURN_ID 
  join return_status rs on rs.RETURN_ID = ri.RETURN_ID 
  and rs.RETURN_ITEM_SEQ_ID = ri.RETURN_ITEM_SEQ_ID 
  join order_header oh on ri.ORDER_ID = oh.ORDER_ID 
where 
  rh.RETURN_CHANNEL_ENUM_ID = 'ECOM_RTN_CHANNEL' 
  and rs.STATUS_ID = 'RETURN_COMPLETED' 
  and oh.PRODUCT_STORE_ID = 'SM_STORE';
```
Result
![image](https://github.com/Nishtha-Jain-1119/SQL-Queries/assets/127538617/cc9dc72a-5759-48c5-a3c6-9daaa00c59ce)
