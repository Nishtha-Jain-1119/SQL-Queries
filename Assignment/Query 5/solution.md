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
  left join order_identification oid on (
    oi.ORDER_ID = oid.ORDER_ID 
    and (
      oid.THRU_DATE is null 
      or oid.THRU_DATE > curdate()
    )
  ) 
  left join good_identification gi on (
    gi.PRODUCT_ID = oi.PRODUCT_ID 
    and (
      gi.THRU_DATE is null 
      or gi.THRU_DATE > curdate()
    )
  ) 
where 
  os.STATUS_ID = 'ITEM_COMPLETED' 
  and (
    year(os.STATUS_DATETIME)= 2023 
    and month(os.STATUS_DATETIME)= 7
  ) 
  and oid.ORDER_IDENTIFICATION_TYPE_ID = 'SHOPIFY_ORD_ID' 
  and gi.GOOD_IDENTIFICATION_TYPE_ID = 'SHOPIFY_PROD_ID';


```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/ecff599e-0e1e-4e69-a546-92c2cff2224f)
