3. In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?

Query

```SQL
select 
  count(distinct s.PRIMARY_ORDER_ID) as SHIPPED_ORDERS_COUNT 
from 
  shipment s 
  join facility f on f.FACILITY_ID = s.ORIGIN_FACILITY_ID 
  join facility_type ft on (
    f.FACILITY_TYPE_ID = ft.FACILITY_TYPE_ID 
    and ft.PARENT_TYPE_ID = 'PHYSICAL_STORE'
  ) 
  join shipment_status ss on (
    ss.SHIPMENT_ID = s.SHIPMENT_ID 
    and ss.STATUS_ID = 'SHIPMENT_SHIPPED'
  ) 
where 
  ss.STATUS_DATE >= '2024-01-01' 
  AND ss.STATUS_DATE < '2024-01-01' + INTERVAL 25 day;

```
**Query cost: 5163.57**

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/c3c6b850-c7ad-4dd3-9289-51c277d38e89)
