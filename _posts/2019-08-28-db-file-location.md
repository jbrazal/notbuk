---
title: SQL Server Database File Locations
category: SQL
tags: ["sql server", "meta"]
is_angular: false
---

```sql
SELECT name, physical_name AS current_file_location
FROM sys.master_files
```