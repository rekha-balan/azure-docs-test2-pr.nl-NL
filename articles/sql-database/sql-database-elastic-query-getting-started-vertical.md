---
title: Get started with cross-database queries (vertical partitioning) | Microsoft Docs
description: how to use elastic database query with vertically partitioned databases
services: sql-database
documentationcenter: ''
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 594760d5c52ac3724a0b8dd882e76ca3302ee8ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556344"
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="af629-103">Get started with cross-database queries (vertical partitioning) (preview)</span><span class="sxs-lookup"><span data-stu-id="af629-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="af629-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span><span class="sxs-lookup"><span data-stu-id="af629-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="af629-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="af629-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="af629-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span><span class="sxs-lookup"><span data-stu-id="af629-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="af629-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af629-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="af629-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af629-108">Prerequisites</span></span>

<span data-ttu-id="af629-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span><span class="sxs-lookup"><span data-stu-id="af629-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="af629-110">This permission is included with the ALTER DATABASE permission.</span><span class="sxs-lookup"><span data-stu-id="af629-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="af629-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span><span class="sxs-lookup"><span data-stu-id="af629-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="af629-112">Create the sample databases</span><span class="sxs-lookup"><span data-stu-id="af629-112">Create the sample databases</span></span>
<span data-ttu-id="af629-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span><span class="sxs-lookup"><span data-stu-id="af629-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="af629-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span><span class="sxs-lookup"><span data-stu-id="af629-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="af629-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span><span class="sxs-lookup"><span data-stu-id="af629-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="af629-116">Create database objects</span><span class="sxs-lookup"><span data-stu-id="af629-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="af629-117">Database scoped master key and credentials</span><span class="sxs-lookup"><span data-stu-id="af629-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="af629-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af629-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="af629-119">Connect to the Orders database and execute the following T-SQL commands:</span><span class="sxs-lookup"><span data-stu-id="af629-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="af629-120">The "username" and "password" should be the username and password used to login into the Customers database.</span><span class="sxs-lookup"><span data-stu-id="af629-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="af629-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="af629-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="af629-122">External data sources</span><span class="sxs-lookup"><span data-stu-id="af629-122">External data sources</span></span>
<span data-ttu-id="af629-123">To create an external data source, execute the following command on the Orders database:</span><span class="sxs-lookup"><span data-stu-id="af629-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="af629-124">External tables</span><span class="sxs-lookup"><span data-stu-id="af629-124">External tables</span></span>
<span data-ttu-id="af629-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span><span class="sxs-lookup"><span data-stu-id="af629-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="af629-126">Execute a sample elastic database T-SQL query</span><span class="sxs-lookup"><span data-stu-id="af629-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="af629-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span><span class="sxs-lookup"><span data-stu-id="af629-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="af629-128">Execute this query on the Orders database:</span><span class="sxs-lookup"><span data-stu-id="af629-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="af629-129">Cost</span><span class="sxs-lookup"><span data-stu-id="af629-129">Cost</span></span>
<span data-ttu-id="af629-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="af629-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="af629-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="af629-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af629-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="af629-132">Next steps</span></span>

* <span data-ttu-id="af629-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af629-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="af629-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="af629-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="af629-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="af629-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="af629-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="af629-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="af629-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="af629-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>