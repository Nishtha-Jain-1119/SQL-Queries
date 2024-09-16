Fetch all the customers created in June 2023.

Solution
```SQL
select 
  p.PARTY_ID, 
  pr.ROLE_TYPE_ID 
from 
  party p 
  join party_role pr on p.PARTY_ID = pr.PARTY_ID 
where 
  (
    p.CREATED_DATE between '2023-06-01' 
    and '2023-06-30'
  ) 
  and p.STATUS_ID = 'PARTY_ENABLED' 
  and pr.ROLE_TYPE_ID = 'CUSTOMER';

```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/3cce8f10-568b-4fed-b250-90a433824962)
