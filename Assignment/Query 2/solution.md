2. Leading up to the New Year, what is the count of orders shipped from stores in the 25 days preceding the New Year?

Query:

**Query cost: 5163.57**
```sql
select 
  count(distinct s.PRIMARY_ORDER_ID) as SHIPPED_ORDERS_COUNT 
  from shipment s 
  join facility f on f.FACILITY_ID = s.ORIGIN_FACILITY_ID
  join facility_type ft on (f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID and ft.PARENT_TYPE_ID = 'PHYSICAL_STORE')
  join shipment_status ss on (ss.SHIPMENT_ID = s.SHIPMENT_ID and ss.STATUS_ID = 'SHIPMENT_SHIPPED')
  where 
  ss.STATUS_DATE >= '2024-01-01' - INTERVAL 25 day 
  AND ss.STATUS_DATE < '2024-01-01';
```
Query with alternate approach

**Query cost: 6203.63**
```SQL
select 
  count(distinct s.PRIMARY_ORDER_ID) as SHIPPED_ORDERS_COUNT 
from 
  order_item_ship_group oisg 
  join facility f on f.FACILITY_ID = oisg.FACILITY_ID 
  join facility_type ft on f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
  join shipment s on oisg.ORDER_ID = s.PRIMARY_ORDER_ID 
  and s.PRIMARY_SHIP_GROUP_SEQ_ID = oisg.SHIP_GROUP_SEQ_ID 
  join shipment_status ss on ss.SHIPMENT_ID = s.SHIPMENT_ID 
where 
  ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
  AND ft.PARENT_TYPE_ID = 'PHYSICAL_STORE' 
  AND ss.STATUS_DATE >= '2024-01-01' - INTERVAL 25 day 
  AND ss.STATUS_DATE < '2024-01-01';
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/436dff83-6ad6-4b08-b77e-2e80e83d43ad)

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/cec9c57d-5eb1-4e86-a444-86facde5be40)


Note: Count of orders shipped is - 7 but count of shipment for those orders is 12 because one order can have multiple shipments.
