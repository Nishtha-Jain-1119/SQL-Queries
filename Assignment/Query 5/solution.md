Fetch the following data for completed order items in July of 2023
- ORDER_ID
- ORDER_ITEM_SEQ_ID
- SHOPIFY_ORDER_ID
- SHOPIFY_PRODUCT_ID

Solution
```SQL
select 
  oi.ORDER_ID, 
  oi.ORDER_ITEM_SEQ_ID, 
  oid.ID_VALUE as SHOPIFY_ORD_ID, 
  gi.ID_VALUE as SHOPIFY_PRODUCT_ID 
from 
  order_item oi 
  join order_status os on (
    oi.order_id = os.ORDER_ID 
    and oi.ORDER_ITEM_SEQ_ID = os.ORDER_ITEM_SEQ_ID
  ) 
  left join order_identification oid on oi.ORDER_ID = oid.ORDER_ID 
  left join good_identification gi on gi.PRODUCT_ID = oi.PRODUCT_ID 
where 
  os.STATUS_ID = 'ITEM_COMPLETED' 
  and (
    os.STATUS_DATETIME between '2023-07-01' 
    and '2023-07-31'
  ) 
  and oid.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_ID' and gi.GOOD_IDENTIFICATION_TYPE_ID = 'SHOPIFY_PROD_ID';
```

Result

![image](https://github.com/Nishtha-Jain-1119/SQL-Queries/assets/127538617/7a55ebcd-6acc-49f5-a3a2-d6ad396de2c3)