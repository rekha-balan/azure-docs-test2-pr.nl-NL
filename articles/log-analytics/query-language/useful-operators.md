---
title: Useful operators in Azure Log Analytics queries | Microsoft Docs
description: Common functions to use for different scenarios in Log Analytics queries.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: ce397b1ba8d77d2916caa2798c0161ba55f51dbb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856593"
---
# <a name="useful-operators-in-log-analytics-queries"></a>Useful operators in Log Analytics queries

The table below provides some common functions to use for different scenarios in Log Analytics queries.

## <a name="useful-operators"></a>Useful operators

Category                                |Relevant Analytics Function
----------------------------------------|----------------------------------------
Selection and Column aliases            |`project`, `project-away`, `extend`
Temporary tables and constants          |`let scalar_alias_name = …;` <br> `let table_alias_name = (){ … &#124; … &#124; … };`
Comparison and String Operators         |`startswith`, `!startswith`, `has`, `!has` <br> `contains`, `!contains`, `containscs` <br> `hasprefix`, `!hasprefix`, `hassuffix`, `!hassuffix`, `in`, `!in` <br> `matches regex` <br> `==`, `=~`, `!=`, `!~`
Common string functions                 |`strcat()`, `replace()`, `tolower()`, `toupper()`, `substring()`, `strlen()`
Common math functions                   |`sqrt()`, `abs()` <br> `exp()`, `exp2()`, `exp10()`, `log()`, `log2()`, `log10()`, `pow()` <br> `gamma()`, `gammaln()`
Parsing text                            |`extract()`, `extractjson()`, `parse`, `split()`
Limiting output                         |`take`, `limit`, `top`, `sample`
Date functions                          |`now()`, `ago()` <br> `datetime()`, `datepart()`, `timespan` <br> `startofday()`, `startofweek()`, `startofmonth()`, `startofyear()` <br> `endofday()`, `endofweek()`, `endofmonth()`, `endofyear()` <br> `dayofweek()`, `dayofmonth()`, `dayofyear()` <br> `getmonth()`, `getyear()`, `weekofyear()`, `monthofyear()`
Grouping and aggregation                |`summarize by` <br> `max()`, `min()`, `count()`, `dcount()`, `avg()`, `sum()` <br> `stddev()`, `countif()`, `dcountif()`, `argmax()`, `argmin()` <br> `percentiles()`, `percentile_array()`
Joins and Unions                        |`join kind=leftouter`, `inner`, `rightouter`, `fullouter`, `leftanti` <br> `union`
Sort, order                             |`sort`, `order` 
Dynamic object (JSON and array)         |`parsejson()` <br> `makeset()`, `makelist()` <br> `split()`, `arraylength()` <br> `zip()`, `pack()`
Logical operators                       |`and`, `or`, `iff(condition, value_t, value_f)` <br> `binary_and()`, `binary_or()`, `binary_not()`, `binary_xor()`
Machine learning                        |`evaluate autocluster`, `basket`, `diffpatterns`, `extractcolumns`


## <a name="next-steps"></a>Next steps

- Go through a lesson on the [writing queries in Log Analytics](get-started-queries.md).