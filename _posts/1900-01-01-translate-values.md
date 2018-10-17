---
layout: post
title: Translate Values
category: SQL
tags: [peopletools, peoplesoft]
is_angular: false
---

Record: PSXLATITEM

```sql
select X.FIELDNAME
, X.FIELDVALUE
, X.XLATLONGNAME
FROM PSXLATITEM X
WHERE X.EFFDT = (select max(X2.EFFDT) 
                from PSXLATITEM X2 
                WHERE X2.FIELDNAME = X.FIELDNAME)
```