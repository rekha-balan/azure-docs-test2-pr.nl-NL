---
title: Connect to Azure SQL Data Warehouse sqlcmd | Microsoft Docs
description: Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 3508cdf6dcfa3d7122e1e3b635f3cd37863dbf62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553770"
---
# <a name="connect-to-sql-data-warehouse-with-sqlcmd"></a><span data-ttu-id="82068-103">Connect to SQL Data Warehouse with sqlcmd</span><span class="sxs-lookup"><span data-stu-id="82068-103">Connect to SQL Data Warehouse with sqlcmd</span></span>
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="82068-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="82068-109">Use [sqlcmd][sqlcmd] command-line utility to connect to and query an Azure SQL Data Warehouse.</span></span>  

## <a name="1-connect"></a><span data-ttu-id="82068-110">1. Connect</span><span class="sxs-lookup"><span data-stu-id="82068-110">1. Connect</span></span>
<span data-ttu-id="82068-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="82068-111">To get started with [sqlcmd][sqlcmd], open the command prompt and enter **sqlcmd** followed by the connection string for your SQL Data Warehouse database.</span></span> <span data-ttu-id="82068-112">The connection string requires the following parameters:</span><span class="sxs-lookup"><span data-stu-id="82068-112">The connection string requires the following parameters:</span></span>

* <span data-ttu-id="82068-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="82068-113">**Server (-S):** Server in the form `<`Server Name`>`.database.windows.net</span></span>
* <span data-ttu-id="82068-114">**Database (-d):** Database name.</span><span class="sxs-lookup"><span data-stu-id="82068-114">**Database (-d):** Database name.</span></span>
* <span data-ttu-id="82068-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span><span class="sxs-lookup"><span data-stu-id="82068-115">**Enable Quoted Identifiers (-I):** Quoted identifiers must be enabled to connect to a SQL Data Warehouse instance.</span></span>

<span data-ttu-id="82068-116">To use SQL Server Authentication, you need to add the username/password parameters:</span><span class="sxs-lookup"><span data-stu-id="82068-116">To use SQL Server Authentication, you need to add the username/password parameters:</span></span>

* <span data-ttu-id="82068-117">**User (-U):** Server user in the form `<`User`>`</span><span class="sxs-lookup"><span data-stu-id="82068-117">**User (-U):** Server user in the form `<`User`>`</span></span>
* <span data-ttu-id="82068-118">**Password (-P):** Password associated with the user.</span><span class="sxs-lookup"><span data-stu-id="82068-118">**Password (-P):** Password associated with the user.</span></span>

<span data-ttu-id="82068-119">For example, your connection string might look like the following:</span><span class="sxs-lookup"><span data-stu-id="82068-119">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

<span data-ttu-id="82068-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span><span class="sxs-lookup"><span data-stu-id="82068-120">To use Azure Active Directory Integrated authentication, you need to add the Azure Active Directory parameters:</span></span>

* <span data-ttu-id="82068-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span><span class="sxs-lookup"><span data-stu-id="82068-121">**Azure Active Directory Authentication (-G):** use Azure Active Directory for authentication</span></span>

<span data-ttu-id="82068-122">For example, your connection string might look like the following:</span><span class="sxs-lookup"><span data-stu-id="82068-122">For example, your connection string might look like the following:</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> You need to [enable Azure Active Directory Authentication](sql-data-warehouse-authentication.md) to authenticate using Active Directory.
> 
> 

## <a name="2-query"></a><span data-ttu-id="82068-124">2. Query</span><span class="sxs-lookup"><span data-stu-id="82068-124">2. Query</span></span>
<span data-ttu-id="82068-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span><span class="sxs-lookup"><span data-stu-id="82068-125">After connection, you can issue any supported Transact-SQL statements against the instance.</span></span>  <span data-ttu-id="82068-126">In this example, queries are submitted in interactive mode.</span><span class="sxs-lookup"><span data-stu-id="82068-126">In this example, queries are submitted in interactive mode.</span></span>

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

<span data-ttu-id="82068-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="82068-127">These next examples show how you can run your queries in batch mode using the -Q option or piping your SQL to sqlcmd.</span></span>

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a><span data-ttu-id="82068-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="82068-128">Next steps</span></span>
<span data-ttu-id="82068-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span><span class="sxs-lookup"><span data-stu-id="82068-129">See [sqlcmd documentation][sqlcmd] for more about details about the options available in sqlcmd.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
