---
layout: post
title: Change User Password
category: SQL
is_angluar: false
tags: [dms, peopletools]
---

## Old Tools
```sql
set log = 'C:/temp/output.log';

update PSOPRDEFN
set OPERPSWD  = 'Test@123'
, ENCRYPTED  = 0
where OPRID = 'JBrazal';

ENCRYPT_PASSWORD JBrazal;    		
```

## Ptools 8.54 

## Ptools 8.55

## Ptools 8.56 


