---
title: Record Field Properties
category: SQL
tags: [peoplesoft, peopletools, meta]
is_angular: false
--- 

```sql
/*
    Source: http://peoplesoftdotnet.blogspot.ca/2015/02/how-to-use-useedit-field-to-find-out.html
   MSSSQL DB

    Description:  Record Field properties
*/

SELECT A.RECNAME,        A.FIELDNAME,
       CASE
         WHEN B.FIELDTYPE = 0 THEN 'CHAR'
         WHEN B.FIELDTYPE = 1 THEN 'LONG CHAR'
         WHEN B.FIELDTYPE = 2 THEN 'NUMBER'
         WHEN B.FIELDTYPE = 3 THEN 'SIGNED NBR'
         WHEN B.FIELDTYPE = 4 THEN 'DATE'
         WHEN B.FIELDTYPE = 5 THEN 'TIME'
         WHEN B.FIELDTYPE = 6 THEN 'DATETIME'
         WHEN B.FIELDTYPE = 7
               OR B.FIELDTYPE = 8 THEN 'IMAGE'
         ELSE NULL
       END           AS FIELDTYPE,
       CASE
         WHEN B.FIELDTYPE = 2   OR B.FIELDTYPE = 3 THEN RTRIM(cast(B.LENGTH AS CHAR))  + '.' + CAST(B.DECIMALPOS AS CHAR)
         ELSE CAST(B.LENGTH AS CHAR)
       END           AS FLDLEN,
       CASE
         WHEN (A.USEEDIT & 256) > 0 THEN 'YES'
         ELSE 'NO'
       END           AS REQ,
       CASE
         WHEN (A.USEEDIT & 1) > 0 THEN 'KEY'
         WHEN (A.USEEDIT & 2) > 0 THEN 'DUP'
         WHEN (A.USEEDIT & 16) > 0 THEN 'ALT'
         ELSE NULL 
       END           AS KEY_TYPE, 
       CASE 
         WHEN (A.USEEDIT & 64) > 0 THEN 'DESC' 
         WHEN ( (A.USEEDIT & 1) > 0 
                 OR (A.USEEDIT & 2) > 0 
                 OR (A.USEEDIT & 16) > 0 ) 
              AND (A.USEEDIT & 64) = 0 THEN 'ASC' 
         ELSE NULL 
       END           AS DIR, 
       CASE 
         WHEN (A.USEEDIT & 2048) > 0 THEN 'YES' 
         ELSE 'NO' 
       END           AS SRCH, 
       CASE 
         WHEN (A.USEEDIT & 32) > 0 THEN 'YES' 
         ELSE 'NO' 
       END           AS LIST, 
       CASE 
         WHEN (A.USEEDIT & 4) > 0 THEN 'YES' 
         ELSE 'NO' 
       END           AS SYS, 
       CASE 
         WHEN RTRIM(A.DEFRECNAME) = '' THEN A.DEFFIELDNAME 
         ELSE RTRIM(A.DEFRECNAME) 
              + '.' 
              + A.DEFFIELDNAME 
       END           AS DEFAULT_VALUE, 
       CASE 
         WHEN (A.USEEDIT & 8) > 0 
              AND (A.USEEDIT & 128) = 0 
              AND (A.USEEDIT & 1024) = 0 THEN 'A' 
         WHEN (A.USEEDIT & 8) > 0 
              AND (A.USEEDIT & 128) > 0 
              AND (A.USEEDIT & 1024) = 0 THEN 'AC' 
         WHEN (A.USEEDIT & 8) > 0 
              AND (A.USEEDIT & 128) > 0 
              AND (A.USEEDIT & 1024) > 0 THEN 'ACD' 
         WHEN (A.USEEDIT & 8) = 0 
              AND (A.USEEDIT & 128) > 0 
              AND (A.USEEDIT & 1024) = 0 THEN 'C' 
         WHEN (A.USEEDIT & 8) = 0 
              AND (A.USEEDIT & 128) > 0 
              AND (A.USEEDIT & 1024) > 0 THEN 'CD' 
         WHEN (A.USEEDIT & 8) = 0 
              AND (A.USEEDIT & 128) = 0 
              AND (A.USEEDIT & 1024) > 0 THEN 'D' 
         ELSE NULL 
       END           AS AUDT, 
       CASE 
         WHEN (A.USEEDIT & 16384) > 0 THEN 'PROMPT' 
         WHEN (A.USEEDIT & 512) > 0 THEN 'XLAT' 
         WHEN (A.USEEDIT & 8192) > 0 THEN 'Y/N' 
         ELSE NULL 
       END           AS EDIT, 
       A.EDITTABLE   AS PROMPT_TABLE, 
       A.SETCNTRLFLD AS SET_CONTROL_FLD, 
       CASE 
         WHEN (A.USEEDIT & 4096) > 0 THEN 'YES' 
         ELSE 'NO' 
       END           AS REASONABLE_DT, 
       CASE 
         WHEN (A.USEEDIT & 32768) > 0 THEN 'YES' 
         ELSE 'NO' 
       END           AS AUTO_UPDT, 
       CASE 
         WHEN (A.USEEDIT & 262144) > 0 THEN 'FROM' 
         WHEN (A.USEEDIT & 524288) > 0 THEN 'THROUGH' 
         ELSE NULL 
       END           AS SEARCH_FIELD, 
       CASE 
         WHEN A.SUBRECORD = 'Y' THEN 'YES' 
         ELSE 'NO' 
       END           AS SUBRECORD, 
       A.LASTUPDDTTM, 
       A.LASTUPDOPRID 
FROM   PSRECFIELD A, 
       PSDBFIELD B 
WHERE  A.RECNAME = 'VOUCHER' --PASTE RECNAME HERE 
       AND A.FIELDNAME = B.FIELDNAME 
ORDER  BY FIELDNUM; 
```