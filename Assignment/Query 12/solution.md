Get all the appeasements in July month.
1. How do we differentiate between returns and appeasements?
-  <b>Return</b> result in a reversal of the original transaction, either through a refund, replacement, or exchange.
-  <b>Appeasement</b> aim to satisfy the customer without necessarily undoing the original transaction.
-  <b>Difference</b> In Return_Adjustment entity there is no return_item for appeasement type.
2. Get all the below fields 
- RETURN_ID
- ENTRY_DATE 
- RETURN_ADJUSTMENT_TYPE_ID
- AMOUNT
- COMMENTS 
- ORDER_ID
- ORDER_DATE 
- RETURN_DATE
- PRODUCT_STORE_ID

Solution
```SQL
select 
  rh.RETURN_ID, 
  rh.ENTRY_DATE, 
  ra.RETURN_ADJUSTMENT_TYPE_ID, 
  ra.AMOUNT, 
  ra.COMMENTS, 
  ra.ORDER_ID, 
  oh.ORDER_DATE, 
  rh.RETURN_DATE, 
  oh.PRODUCT_STORE_ID 
from 
  return_header rh 
  join return_adjustment ra on rh.RETURN_ID = ra.RETURN_ID 
  join order_header oh on ra.ORDER_ID = oh.ORDER_ID 
where 
  RETURN_ADJUSTMENT_TYPE_ID = 'APPEASEMENT' 
  and rh.RETURN_DATE between '2023-07-01' 
  and '2023-07-31';
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/2e3fbd5b-32ba-4afe-9894-4313d15a1750)
