---
title: Getting Started with Temporal Tables in Azure SQL Database | Microsoft Docs
description: Learn how to get started with using Temporal Tables in Azure SQL Database.
services: sql-database
documentationcenter: ''
author: bonova
manager: jhubbard
editor: ''
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: development
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 03aac8e8e4f28f9d0300faccf05e5d7970de1641
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660627"
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="2c26a-103">Getting Started with Temporal Tables in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="2c26a-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="2c26a-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span><span class="sxs-lookup"><span data-stu-id="2c26a-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="2c26a-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span><span class="sxs-lookup"><span data-stu-id="2c26a-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="2c26a-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span><span class="sxs-lookup"><span data-stu-id="2c26a-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="2c26a-107">Temporal Scenario</span><span class="sxs-lookup"><span data-stu-id="2c26a-107">Temporal Scenario</span></span>
<span data-ttu-id="2c26a-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span><span class="sxs-lookup"><span data-stu-id="2c26a-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="2c26a-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span><span class="sxs-lookup"><span data-stu-id="2c26a-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="2c26a-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2c26a-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="2c26a-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span><span class="sxs-lookup"><span data-stu-id="2c26a-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="2c26a-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span><span class="sxs-lookup"><span data-stu-id="2c26a-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="2c26a-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span><span class="sxs-lookup"><span data-stu-id="2c26a-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![Schema](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="2c26a-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span><span class="sxs-lookup"><span data-stu-id="2c26a-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="2c26a-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span><span class="sxs-lookup"><span data-stu-id="2c26a-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="2c26a-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="2c26a-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="2c26a-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span><span class="sxs-lookup"><span data-stu-id="2c26a-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="2c26a-119">Step 1: Configure tables as temporal</span><span class="sxs-lookup"><span data-stu-id="2c26a-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="2c26a-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span><span class="sxs-lookup"><span data-stu-id="2c26a-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="2c26a-121">In general case, your scenario can be a mix of these two options.</span><span class="sxs-lookup"><span data-stu-id="2c26a-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="2c26a-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span><span class="sxs-lookup"><span data-stu-id="2c26a-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c26a-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2c26a-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="2c26a-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c26a-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="2c26a-125">Create new table</span><span class="sxs-lookup"><span data-stu-id="2c26a-125">Create new table</span></span>
<span data-ttu-id="2c26a-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span><span class="sxs-lookup"><span data-stu-id="2c26a-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="2c26a-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span><span class="sxs-lookup"><span data-stu-id="2c26a-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="2c26a-129">That will open table designer and enable you to easily specify the table layout:</span><span class="sxs-lookup"><span data-stu-id="2c26a-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="2c26a-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="2c26a-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="2c26a-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span><span class="sxs-lookup"><span data-stu-id="2c26a-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="2c26a-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span><span class="sxs-lookup"><span data-stu-id="2c26a-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="2c26a-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span><span class="sxs-lookup"><span data-stu-id="2c26a-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="2c26a-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="2c26a-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="2c26a-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span><span class="sxs-lookup"><span data-stu-id="2c26a-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="2c26a-137">A clustered columnstore provides very good compression and performance for analytical queries.</span><span class="sxs-lookup"><span data-stu-id="2c26a-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="2c26a-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span><span class="sxs-lookup"><span data-stu-id="2c26a-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="2c26a-139">Columnstore indexes are only available in the premium service tier.</span><span class="sxs-lookup"><span data-stu-id="2c26a-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="2c26a-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span><span class="sxs-lookup"><span data-stu-id="2c26a-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="2c26a-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span><span class="sxs-lookup"><span data-stu-id="2c26a-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="2c26a-143">Alter existing table to temporal</span><span class="sxs-lookup"><span data-stu-id="2c26a-143">Alter existing table to temporal</span></span>
<span data-ttu-id="2c26a-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span><span class="sxs-lookup"><span data-stu-id="2c26a-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="2c26a-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2c26a-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="2c26a-146">Step 2: Run your workload regularly</span><span class="sxs-lookup"><span data-stu-id="2c26a-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="2c26a-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span><span class="sxs-lookup"><span data-stu-id="2c26a-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="2c26a-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span><span class="sxs-lookup"><span data-stu-id="2c26a-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="2c26a-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span><span class="sxs-lookup"><span data-stu-id="2c26a-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="2c26a-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span><span class="sxs-lookup"><span data-stu-id="2c26a-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="2c26a-151">Both aspects are automatically handled by the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="2c26a-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="2c26a-152">The following diagram illustrates how history data is being generated on every update.</span><span class="sxs-lookup"><span data-stu-id="2c26a-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="2c26a-154">Step 3: Perform historical data analysis</span><span class="sxs-lookup"><span data-stu-id="2c26a-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="2c26a-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span><span class="sxs-lookup"><span data-stu-id="2c26a-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="2c26a-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span><span class="sxs-lookup"><span data-stu-id="2c26a-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="2c26a-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span><span class="sxs-lookup"><span data-stu-id="2c26a-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="2c26a-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span><span class="sxs-lookup"><span data-stu-id="2c26a-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="2c26a-159">To perform basic statistical analysis for the previous day, use the following example:</span><span class="sxs-lookup"><span data-stu-id="2c26a-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="2c26a-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span><span class="sxs-lookup"><span data-stu-id="2c26a-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="2c26a-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span><span class="sxs-lookup"><span data-stu-id="2c26a-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="2c26a-163">Evolving table schema</span><span class="sxs-lookup"><span data-stu-id="2c26a-163">Evolving table schema</span></span>
<span data-ttu-id="2c26a-164">Typically, you will need to change the temporal table schema while you are doing app development.</span><span class="sxs-lookup"><span data-stu-id="2c26a-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="2c26a-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span><span class="sxs-lookup"><span data-stu-id="2c26a-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="2c26a-166">The following script shows how you can add additional attribute for tracking:</span><span class="sxs-lookup"><span data-stu-id="2c26a-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="2c26a-167">Similarly, you can change column definition while your workload is active:</span><span class="sxs-lookup"><span data-stu-id="2c26a-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="2c26a-168">Finally, you can remove a column that you do not need anymore.</span><span class="sxs-lookup"><span data-stu-id="2c26a-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="2c26a-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span><span class="sxs-lookup"><span data-stu-id="2c26a-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="2c26a-170">Controlling retention of historical data</span><span class="sxs-lookup"><span data-stu-id="2c26a-170">Controlling retention of historical data</span></span>
<span data-ttu-id="2c26a-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span><span class="sxs-lookup"><span data-stu-id="2c26a-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="2c26a-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span><span class="sxs-lookup"><span data-stu-id="2c26a-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="2c26a-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span><span class="sxs-lookup"><span data-stu-id="2c26a-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="2c26a-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span><span class="sxs-lookup"><span data-stu-id="2c26a-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="2c26a-175">Table Partitioning</span><span class="sxs-lookup"><span data-stu-id="2c26a-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="2c26a-176">Custom Cleanup Script</span><span class="sxs-lookup"><span data-stu-id="2c26a-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="2c26a-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c26a-177">Next steps</span></span>
<span data-ttu-id="2c26a-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c26a-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="2c26a-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="2c26a-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>







