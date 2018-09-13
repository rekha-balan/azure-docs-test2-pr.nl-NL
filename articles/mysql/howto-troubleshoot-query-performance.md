---
title: How To Troubleshoot Query Performance in Azure Database for MySQL
description: This article describes how to use EXPLAIN to troubleshoot query performance in Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 72b047c37ac88e4b33c8723f8df14c6794e84399
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968075"
---
# <a name="how-to-use-explain-to-profile-query-performance-in-azure-database-for-mysql"></a><span data-ttu-id="100be-103">How to use EXPLAIN to profile query performance in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="100be-103">How to use EXPLAIN to profile query performance in Azure Database for MySQL</span></span>
<span data-ttu-id="100be-104">**EXPLAIN** is a handy tool to optimize queries.</span><span class="sxs-lookup"><span data-stu-id="100be-104">**EXPLAIN** is a handy tool to optimize queries.</span></span> <span data-ttu-id="100be-105">EXPLAIN statement can be used to get information about how SQL statements are executed.</span><span class="sxs-lookup"><span data-stu-id="100be-105">EXPLAIN statement can be used to get information about how SQL statements are executed.</span></span> <span data-ttu-id="100be-106">The following output shows an example of the execution of an EXPLAIN statement.</span><span class="sxs-lookup"><span data-stu-id="100be-106">The following output shows an example of the execution of an EXPLAIN statement.</span></span>

```sql
mysql> EXPLAIN SELECT * FROM tb1 WHERE id=100\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 995789
     filtered: 10.00
        Extra: Using where
```

<span data-ttu-id="100be-107">As can be seen from this example, the value of *key* is NULL.</span><span class="sxs-lookup"><span data-stu-id="100be-107">As can be seen from this example, the value of *key* is NULL.</span></span> <span data-ttu-id="100be-108">This output means MySQL cannot find any indexes optimized for the query and it performs a full table scan.</span><span class="sxs-lookup"><span data-stu-id="100be-108">This output means MySQL cannot find any indexes optimized for the query and it performs a full table scan.</span></span> <span data-ttu-id="100be-109">Let's optimize this query by adding an index on the **ID** column.</span><span class="sxs-lookup"><span data-stu-id="100be-109">Let's optimize this query by adding an index on the **ID** column.</span></span>

```sql
mysql> ALTER TABLE tb1 ADD KEY (id);
mysql> EXPLAIN SELECT * FROM tb1 WHERE id=100\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: ref
possible_keys: id
          key: id
      key_len: 4
          ref: const
         rows: 1
     filtered: 100.00
        Extra: NULL
```

<span data-ttu-id="100be-110">The new EXPLAIN shows that MySQL now uses an index to limit the number of rows to 1, which in turn dramatically shortened the search time.</span><span class="sxs-lookup"><span data-stu-id="100be-110">The new EXPLAIN shows that MySQL now uses an index to limit the number of rows to 1, which in turn dramatically shortened the search time.</span></span>
 
## <a name="covering-index"></a><span data-ttu-id="100be-111">Covering index</span><span class="sxs-lookup"><span data-stu-id="100be-111">Covering index</span></span>
<span data-ttu-id="100be-112">A covering index consists of all columns of a query in the index to reduce value retrieval from data tables.</span><span class="sxs-lookup"><span data-stu-id="100be-112">A covering index consists of all columns of a query in the index to reduce value retrieval from data tables.</span></span> <span data-ttu-id="100be-113">Here's an illustration in the following **GROUP BY** statement.</span><span class="sxs-lookup"><span data-stu-id="100be-113">Here's an illustration in the following **GROUP BY** statement.</span></span>
 
```sql
mysql> EXPLAIN SELECT MAX(c1), c2 FROM tb1 WHERE c2 LIKE '%100' GROUP BY c1\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 995789
     filtered: 11.11
        Extra: Using where; Using temporary; Using filesort
```

<span data-ttu-id="100be-114">As can be seen from the output, MySQL does not use any indexes because no proper indexes are available.</span><span class="sxs-lookup"><span data-stu-id="100be-114">As can be seen from the output, MySQL does not use any indexes because no proper indexes are available.</span></span> <span data-ttu-id="100be-115">It also shows *Using temporary; Using file sort*, which means MySQL creates a temporary table to satisfy the **GROUP BY** clause.</span><span class="sxs-lookup"><span data-stu-id="100be-115">It also shows *Using temporary; Using file sort*, which means MySQL creates a temporary table to satisfy the **GROUP BY** clause.</span></span>
 
<span data-ttu-id="100be-116">Creating an index on column **c2** alone makes no difference, and MySQL still needs to create a temporary table:</span><span class="sxs-lookup"><span data-stu-id="100be-116">Creating an index on column **c2** alone makes no difference, and MySQL still needs to create a temporary table:</span></span>

```sql 
mysql> ALTER TABLE tb1 ADD KEY (c2);
mysql> EXPLAIN SELECT MAX(c1), c2 FROM tb1 WHERE c2 LIKE '%100' GROUP BY c1\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 995789
     filtered: 11.11
        Extra: Using where; Using temporary; Using filesort
```

<span data-ttu-id="100be-117">In this case, a **covered index** on both **c1** and **c2** can be created, whereby adding the value of **c2**" directly in the index to eliminate further data lookup.</span><span class="sxs-lookup"><span data-stu-id="100be-117">In this case, a **covered index** on both **c1** and **c2** can be created, whereby adding the value of **c2**" directly in the index to eliminate further data lookup.</span></span>

```sql 
mysql> ALTER TABLE tb1 ADD KEY covered(c1,c2);
mysql> EXPLAIN SELECT MAX(c1), c2 FROM tb1 WHERE c2 LIKE '%100' GROUP BY c1\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: index
possible_keys: covered
          key: covered
      key_len: 108
          ref: NULL
         rows: 995789
     filtered: 11.11
        Extra: Using where; Using index
```

<span data-ttu-id="100be-118">As the above EXPLAIN shows, MySQL now uses the covered index and avoid creating a temporary table.</span><span class="sxs-lookup"><span data-stu-id="100be-118">As the above EXPLAIN shows, MySQL now uses the covered index and avoid creating a temporary table.</span></span> 

## <a name="combined-index"></a><span data-ttu-id="100be-119">Combined index</span><span class="sxs-lookup"><span data-stu-id="100be-119">Combined index</span></span>
<span data-ttu-id="100be-120">A combined index consists values from multiple columns and can be considered an array of rows that are sorted by concatenating values of the indexed columns.</span><span class="sxs-lookup"><span data-stu-id="100be-120">A combined index consists values from multiple columns and can be considered an array of rows that are sorted by concatenating values of the indexed columns.</span></span> <span data-ttu-id="100be-121">This method can be useful in a **GROUP BY** statement.</span><span class="sxs-lookup"><span data-stu-id="100be-121">This method can be useful in a **GROUP BY** statement.</span></span>

```sql
mysql> EXPLAIN SELECT c1, c2 from tb1 WHERE c2 LIKE '%100' ORDER BY c1 DESC LIMIT 10\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 995789
     filtered: 11.11
        Extra: Using where; Using filesort
```

<span data-ttu-id="100be-122">MySQL performs a *file sort* operation that is fairly slow, especially when it has to sort many rows.</span><span class="sxs-lookup"><span data-stu-id="100be-122">MySQL performs a *file sort* operation that is fairly slow, especially when it has to sort many rows.</span></span> <span data-ttu-id="100be-123">To optimize this query, a combined index can be created on both columns that are being sorted.</span><span class="sxs-lookup"><span data-stu-id="100be-123">To optimize this query, a combined index can be created on both columns that are being sorted.</span></span>

```sql 
mysql> ALTER TABLE tb1 ADD KEY my_sort2 (c1, c2);
mysql> EXPLAIN SELECT c1, c2 from tb1 WHERE c2 LIKE '%100' ORDER BY c1 DESC LIMIT 10\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: tb1
   partitions: NULL
         type: index
possible_keys: NULL
          key: my_sort2
      key_len: 108
          ref: NULL
         rows: 10
     filtered: 11.11
        Extra: Using where; Using index
```

<span data-ttu-id="100be-124">The EXPLAIN now shows that MySQL is able to use combined index to avoid additional sorting since the index is already sorted.</span><span class="sxs-lookup"><span data-stu-id="100be-124">The EXPLAIN now shows that MySQL is able to use combined index to avoid additional sorting since the index is already sorted.</span></span>
 
## <a name="conclusion"></a><span data-ttu-id="100be-125">Conclusion</span><span class="sxs-lookup"><span data-stu-id="100be-125">Conclusion</span></span>
 
<span data-ttu-id="100be-126">Using EXPLAIN and different type of Indexes can increase performance significantly.</span><span class="sxs-lookup"><span data-stu-id="100be-126">Using EXPLAIN and different type of Indexes can increase performance significantly.</span></span> <span data-ttu-id="100be-127">Just because you have an index on the table does not necessarily mean MySQL would be able to use it for your queries.</span><span class="sxs-lookup"><span data-stu-id="100be-127">Just because you have an index on the table does not necessarily mean MySQL would be able to use it for your queries.</span></span> <span data-ttu-id="100be-128">Always validate your assumptions using EXPLAIN and optimize your queries using indexes.</span><span class="sxs-lookup"><span data-stu-id="100be-128">Always validate your assumptions using EXPLAIN and optimize your queries using indexes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="100be-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="100be-129">Next steps</span></span>
- <span data-ttu-id="100be-130">To find peer answers to your most concerned questions or post a new question/answer, visit [MSDN forum](https://social.msdn.microsoft.com/forums/security/en-US/home?forum=AzureDatabaseforMySQL) or [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-database-mysql).</span><span class="sxs-lookup"><span data-stu-id="100be-130">To find peer answers to your most concerned questions or post a new question/answer, visit [MSDN forum](https://social.msdn.microsoft.com/forums/security/en-US/home?forum=AzureDatabaseforMySQL) or [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-database-mysql).</span></span>
