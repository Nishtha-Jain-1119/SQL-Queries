5. In New York, which product has the highest sales?

Query
```SQL
select 
  oi.PRODUCT_ID, 
  p.PRODUCT_TYPE_ID, 
  p.PRODUCT_NAME, 
  p.BRAND_NAME, 
  sum(oi.QUANTITY)  as product_cnt 
from 
  order_contact_mech ocm 
  join order_item oi on oi.ORDER_ID = ocm.ORDER_ID 
  join postal_address pa on pa.CONTACT_MECH_ID = ocm.CONTACT_MECH_ID 
  join product p on oi.PRODUCT_ID = p.PRODUCT_ID 
where 
  ocm.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION' 
  and pa.CITY = 'New York' 
  and oi.PRODUCT_ID is not null 
  and oi.STATUS_ID = 'ITEM_COMPLETED' 
group by 
  oi.PRODUCT_ID 
order by 
  product_cnt desc 
limit 
  1;

```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/874ac94b-f1a0-4ba4-8ad3-fdd231204303)
