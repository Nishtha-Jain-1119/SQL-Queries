Fetch the inventory variances of the products where the reason is ‘VAR_LOST’ or VAR_DAMAGED.

Solution
```SQL
select 
  ii.PRODUCT_ID, 
  ii.INVENTORY_ITEM_ID, 
  iiv.VARIANCE_REASON_ID 
from 
  inventory_item ii 
  join inventory_item_variance iiv on ii.INVENTORY_ITEM_ID = iiv.INVENTORY_ITEM_ID 
where 
  iiv.VARIANCE_REASON_ID = 'VAR_LOST' 
  or iiv.VARIANCE_REASON_ID = 'VAR_DAMAGED';
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/daf45f76-8778-42ef-90f2-e431e7002a6d)
