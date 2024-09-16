Fetch the order id and contact mech id for the shipping address of the orders completed in October of 2023.

Solution
```SQL
select 
  os.ORDER_ID, 
  ocm.CONTACT_MECH_ID 
from 
  order_status os 
  join order_contact_mech ocm on os.ORDER_ID = ocm.ORDER_ID 
where 
  os.STATUS_ID = 'ORDER_COMPLETED' 
  and (
    os.STATUS_DATETIME between '2023-10-01' 
    and '2023-10-31'
  ) 
  and ocm.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION';

```
Result

![image](https://github.com/Nishtha-Jain-1119/SQL-Queries/assets/127538617/b5bb57d9-1dab-44be-8c35-3c608f63bacb)
