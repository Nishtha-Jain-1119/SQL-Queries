Fetch all the order items that are in the created status and the order type should be a sales order
- ORDER_ID
- PRODUCT_TYPE_ID
- ORDER_LINE_ID
- EXTERNAL_ID
- SALES_CHANNEL
- QUANTITY
- ITEM_STATUS 
- PRODUCT_ID
- BILL_CITY
- BILL_COUNTRY
- BILL_POSTALCODE
- BILL_ADDRESS1
- BILL_ADDRESS2
- SHIP_CITY
- SHIP_COUNTRY
- SHIP_POSTALCODE
- SHIP_ADDRESS1
- SHIP_ADDRESS2

Solution
```SQL
select 
  oi.ORDER_ID, 
  p.PRODUCT_TYPE_ID, 
  oi.ORDER_ITEM_SEQ_ID as ORDER_LINE_ID, 
  oi.EXTERNAL_ID, 
  oh.SALES_CHANNEL_ENUM_ID, 
  oi.QUANTITY, 
  oi.STATUS_ID as ITEM_STATUS, 
  oi.PRODUCT_ID, 
  pa_b.CITY as BILL_CITY, 
  pa_b.COUNTRY_GEO_ID as BILL_COUNTRY, 
  pa_b.POSTAL_CODE as BILL_POSTALCODE, 
  pa_b.ADDRESS1 as BILL_ADDRESS1, 
  pa_b.ADDRESS2 as BILL_ADDRESS2, 
  pa_s.CITY as SHIP_CITY, 
  pa_s.COUNTRY_GEO_ID as SHIP_COUNTRY, 
  pa_s.POSTAL_CODE as SHIP_POSTALCODE, 
  pa_s.ADDRESS1 as SHIP_ADDRESS1, 
  pa_s.ADDRESS2 as SHIP_ADDRESS2 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
  join product p on p.PRODUCT_ID = oi.PRODUCT_ID 
  join order_contact_mech ocm_s on (
    ocm_s.ORDER_ID = oh.ORDER_ID 
    and ocm_s.CONTACT_MECH_PURPOSE_TYPE_ID = 'SHIPPING_LOCATION'
  ) 
  join order_contact_mech ocm_b on (
    ocm_b.ORDER_ID = oh.ORDER_ID 
    and ocm_b.CONTACT_MECH_PURPOSE_TYPE_ID = 'BILLING_LOCATION'
  ) 
  join postal_address pa_s on pa_s.CONTACT_MECH_ID = ocm_s.CONTACT_MECH_ID 
  join postal_address pa_b on pa_b.CONTACT_MECH_ID = ocm_b.CONTACT_MECH_ID 
where 
  oi.STATUS_ID = 'ITEM_CREATED' 
  and oh.ORDER_TYPE_ID = 'SALES_ORDER';
```

Result
![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/2f41f3a9-6b78-47ae-bb0f-7d07e7eaad16)
![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/3c83a8da-9e78-417d-aea8-9eaf239549c5)



