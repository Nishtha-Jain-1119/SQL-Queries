6. In the past month, which store has the highest number of one-day shipped orders?

Query using product store
```SQL
select 
  oh.PRODUCT_STORE_ID, 
  count(s.PRIMARY_ORDER_ID) shipped_order_count 
from 
  shipment s 
  join shipment_status ss on ss.SHIPMENT_ID = s.SHIPMENT_ID 
  join order_header oh on s.PRIMARY_ORDER_ID = oh.ORDER_ID 
where 
  s.SHIPMENT_METHOD_TYPE_ID = 'NEXT_DAY' 
  and ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
  and ss.STATUS_DATE >= curdate() - INTERVAL 1 month 
group by 
  oh.PRODUCT_STORE_ID;

```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/081d942d-c54a-4566-995f-28789deaf3a2)


Query using facility
```SQL
select 
  s.ORIGIN_FACILITY_ID, 
  f.FACILITY_TYPE_ID, 
  count(s.PRIMARY_ORDER_ID) shipped_order_count 
from 
  shipment s 
  join shipment_status ss on s.SHIPMENT_ID = ss.SHIPMENT_ID 
  join facility f on f.FACILITY_ID = s.ORIGIN_FACILITY_ID 
where 
  s.SHIPMENT_METHOD_TYPE_ID = 'NEXT_DAY' 
  and ss.STATUS_ID = 'SHIPMENT_SHIPPED' 
  and ss.STATUS_DATE >= curdate() - INTERVAL 1 month 
group by 
  s.ORIGIN_FACILITY_ID;
```

Result 

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/95b6c488-c98a-4ab6-b203-86ff613cb1a9)
