Find all the orders whose two or more items are canceled but the orders are still in the approved status.

Solution
```SQL
SELECT 
  oh.order_id, 
  oh.STATUS_ID, 
  COUNT(ORDER_ITEM_SEQ_ID) AS canceled_items_count 
FROM 
  order_header oh 
  JOIN order_item oi on (oh.ORDER_ID = oi.ORDER_ID
    AND oh.STATUS_ID = 'ORDER_APPROVED' 
    AND oi.STATUS_ID = 'ITEM_CANCELLED')
group by 
  ORDER_ID 
having 
  count(ORDER_ITEM_SEQ_ID)>= 2;
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/55774865-b32b-4528-be23-d4e15ec03ae1)

