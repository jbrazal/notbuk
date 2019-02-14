---
title: Return Boolean Expression
category: PeopleCode
tags: [peoplesoft, peoplecode]
---

For quick logical comparisons, enclose the expression in parenthesis instead of using conditional statements.

```cs

method IsEqual
/+
    &var1 as number
    &var2 as number
+/

/*
    if &var1 = &var2 then
        return true;
    else
        return false;
    end-if;
*/
    return (&var1 = &var2);

end-method;

```