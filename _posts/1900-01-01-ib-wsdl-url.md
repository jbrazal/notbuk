---
layout: post
title: IB Service WSDL URL
category: SQL
tags: [peoplesoft, meta, web service]
is_angular: false
---

```sql
select W.IB_SERVICENAME, (X.IB_TGTLOCATION + '/' + W.IB_WSDLNAME + '.wsdl')  'WSDL URL'
    from PSIBWSDL2_VW W
    , PSIBSVCSETUP X
where W.IB_SERVICENAME IN 
('SCC_USERREG')
```