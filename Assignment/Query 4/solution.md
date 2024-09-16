4. What is the total number of orders originating from New York?

Query
```SQL
select 
  distinct oh.ORDER_ID 
from 
  order_header oh 
  join order_role or2 on (
    or2.ORDER_ID = oh.ORDER_ID 
    and or2.ROLE_TYPE_ID = 'PLACING_CUSTOMER'
  ) 
  join party_contact_mech_purpose pcmp on (
    or2.PARTY_ID = pcmp.PARTY_ID 
    and pcmp.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
  ) 
  join postal_address pa on (
    pa.CONTACT_MECH_ID = pcmp.CONTACT_MECH_ID 
    and pa.city = 'New York'
  )
where 
  oh.STATUS_ID != 'ORDER_CANCELLED' 
  or oh.STATUS_ID != 'ORDER_REJECTED';

```
**Query cost: 330.67**

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/34756e90-f0ee-4ca7-94bf-4fb6dc0aae63)

Query with different approach
```SQL
select 
  count(distinct s.PRIMARY_ORDER_ID) as orders_count 
from 
  shipment s 
  join postal_address pa on s.ORIGIN_CONTACT_MECH_ID = pa.CONTACT_MECH_ID 
where 
  (
    s.SHIPMENT_TYPE_ID = 'SALES_SHIPMENT' 
    or s.SHIPMENT_TYPE_ID = 'PURCHASE_SHIPMENT'
  ) 
  and (
    s.STATUS_ID = 'PURCH_SHIP_SHIPPED' 
    or s.STATUS_ID = 'SHIPMENT_SHIPPED'
  ) 
  and pa.CITY = 'New York';
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/d4f93db1-0e65-40fa-9c1f-638f38ee2ae2)
