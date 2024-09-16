7. On a city-wise basis, what is the analysis of returns?

Query
```SQL
select 
  pa.CITY, 
  count(distinct rcm.RETURN_ID) as return_count 
from 
  return_contact_mech rcm 
  join postal_address pa on pa.CONTACT_MECH_ID = rcm.CONTACT_MECH_ID 
group by 
  pa.CITY;
```

Result

![image](https://github.com/Nishtha-Jain-1119/Training-Assignment/assets/127538617/16f71e3a-50e9-4ee7-98d4-8ab07accaa89)
