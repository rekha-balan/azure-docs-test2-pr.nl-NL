---
title: 'Migrate: Data Warehouse Migration Utility | Microsoft Docs'
description: Migrate to SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 0d607a0f4130dddc44aeaa3e63cee43643b68d1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662207"
---
# <a name="data-warehouse-migration-utility-preview"></a><span data-ttu-id="85801-103">Data Warehouse Migration Utility (Preview)</span><span class="sxs-lookup"><span data-stu-id="85801-103">Data Warehouse Migration Utility (Preview)</span></span>
> [!div class="op_single_selector"]
> * [Download Migration Utility][Download Migration Utility]
> 
> 

<span data-ttu-id="85801-105">The Data Warehouse Migration Utility is a tool designed to migrate schema and data from SQL Server and Azure SQL Database to Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="85801-105">The Data Warehouse Migration Utility is a tool designed to migrate schema and data from SQL Server and Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="85801-106">During schema migration, the tool automatically maps the corresponding schema from source to destination.</span><span class="sxs-lookup"><span data-stu-id="85801-106">During schema migration, the tool automatically maps the corresponding schema from source to destination.</span></span> <span data-ttu-id="85801-107">After the schema has been migrated, the tools provides the option to move data with automatically generated scripts.</span><span class="sxs-lookup"><span data-stu-id="85801-107">After the schema has been migrated, the tools provides the option to move data with automatically generated scripts.</span></span>

<span data-ttu-id="85801-108">In addition to schema and data migration, this tool gives you the option to generate compatibility reports which summarize incompatibilities between the target and source instances which would prevent streamlined migration.</span><span class="sxs-lookup"><span data-stu-id="85801-108">In addition to schema and data migration, this tool gives you the option to generate compatibility reports which summarize incompatibilities between the target and source instances which would prevent streamlined migration.</span></span>

## <a name="get-started"></a><span data-ttu-id="85801-109">Get started</span><span class="sxs-lookup"><span data-stu-id="85801-109">Get started</span></span>
<span data-ttu-id="85801-110">As a prerequisite for installation, you will need the BCP command-line utility to run migration scripts and Office to view the compatibility report.</span><span class="sxs-lookup"><span data-stu-id="85801-110">As a prerequisite for installation, you will need the BCP command-line utility to run migration scripts and Office to view the compatibility report.</span></span> <span data-ttu-id="85801-111">After launching the executable that is downloaded you will be prompted to accept a standard EULA before the tool will be installed.</span><span class="sxs-lookup"><span data-stu-id="85801-111">After launching the executable that is downloaded you will be prompted to accept a standard EULA before the tool will be installed.</span></span>

<span data-ttu-id="85801-112">In addition, to run the Migration Utiliy, you will need the one following permissions on the database that you are looking to migrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span><span class="sxs-lookup"><span data-stu-id="85801-112">In addition, to run the Migration Utiliy, you will need the one following permissions on the database that you are looking to migrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span></span>

### <a name="launching-the-tool-and-connecting"></a><span data-ttu-id="85801-113">Launching the tool and connecting</span><span class="sxs-lookup"><span data-stu-id="85801-113">Launching the tool and connecting</span></span>
<span data-ttu-id="85801-114">Launch the tool by clicking on the desktop icon which appears post install.</span><span class="sxs-lookup"><span data-stu-id="85801-114">Launch the tool by clicking on the desktop icon which appears post install.</span></span> <span data-ttu-id="85801-115">Upon opening the tool, you will be prompted with an initial connection page where you can choose your source and destination for the migration tool.</span><span class="sxs-lookup"><span data-stu-id="85801-115">Upon opening the tool, you will be prompted with an initial connection page where you can choose your source and destination for the migration tool.</span></span> <span data-ttu-id="85801-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span><span class="sxs-lookup"><span data-stu-id="85801-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span></span> <span data-ttu-id="85801-117">After selecting this you will be asked to connect to your source server by filling in server name and authenticating and then clicking ‘Connect’.</span><span class="sxs-lookup"><span data-stu-id="85801-117">After selecting this you will be asked to connect to your source server by filling in server name and authenticating and then clicking ‘Connect’.</span></span>

<span data-ttu-id="85801-118">After authenticating, the tool will show a list of databases that are present in the server which you are connected to.</span><span class="sxs-lookup"><span data-stu-id="85801-118">After authenticating, the tool will show a list of databases that are present in the server which you are connected to.</span></span> <span data-ttu-id="85801-119">You can begin the migration by selecting a database that you would like to migrate and then clicking on ‘Migrate selected’.</span><span class="sxs-lookup"><span data-stu-id="85801-119">You can begin the migration by selecting a database that you would like to migrate and then clicking on ‘Migrate selected’.</span></span>

## <a name="migration-report"></a><span data-ttu-id="85801-120">Migration report</span><span class="sxs-lookup"><span data-stu-id="85801-120">Migration report</span></span>
<span data-ttu-id="85801-121">Selecting ‘Check Database Compatibility’ in the tool will generate a report summarizing all object incompatibilities in the database you requested to migrate.</span><span class="sxs-lookup"><span data-stu-id="85801-121">Selecting ‘Check Database Compatibility’ in the tool will generate a report summarizing all object incompatibilities in the database you requested to migrate.</span></span> <span data-ttu-id="85801-122">A broader list of some of the SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span><span class="sxs-lookup"><span data-stu-id="85801-122">A broader list of some of the SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span></span> <span data-ttu-id="85801-123">After the report is generated you will be able to save and open the report in Excel.</span><span class="sxs-lookup"><span data-stu-id="85801-123">After the report is generated you will be able to save and open the report in Excel.</span></span>

<span data-ttu-id="85801-124">Please note that when generating the migration schema, most issues identified as ‘Object’ will be adjusted in order to allow immediate migration of that data.</span><span class="sxs-lookup"><span data-stu-id="85801-124">Please note that when generating the migration schema, most issues identified as ‘Object’ will be adjusted in order to allow immediate migration of that data.</span></span> <span data-ttu-id="85801-125">Please review the changes to ensure you do not want to make additional adjustments before applying the schema.</span><span class="sxs-lookup"><span data-stu-id="85801-125">Please review the changes to ensure you do not want to make additional adjustments before applying the schema.</span></span>

## <a name="migrate-schema"></a><span data-ttu-id="85801-126">Migrate schema</span><span class="sxs-lookup"><span data-stu-id="85801-126">Migrate schema</span></span>
<span data-ttu-id="85801-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for the selected tables.</span><span class="sxs-lookup"><span data-stu-id="85801-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for the selected tables.</span></span> <span data-ttu-id="85801-128">This script ports the structure of the table, maps incompatible data types to more compatible forms, and creates security credentials and schema if this is indicated by the user in the migration settings.</span><span class="sxs-lookup"><span data-stu-id="85801-128">This script ports the structure of the table, maps incompatible data types to more compatible forms, and creates security credentials and schema if this is indicated by the user in the migration settings.</span></span> <span data-ttu-id="85801-129">This code can be run against the targeted SQL Data Warehouse instance, saved to a file, copied to your clipboard, or even edited in-line before taking further action.</span><span class="sxs-lookup"><span data-stu-id="85801-129">This code can be run against the targeted SQL Data Warehouse instance, saved to a file, copied to your clipboard, or even edited in-line before taking further action.</span></span>  

<span data-ttu-id="85801-130">As noted above, when migrating schema review the migration changes that the tool has made in order to ensure that that you fully understand them.</span><span class="sxs-lookup"><span data-stu-id="85801-130">As noted above, when migrating schema review the migration changes that the tool has made in order to ensure that that you fully understand them.</span></span>  

## <a name="migrate-data"></a><span data-ttu-id="85801-131">Migrate data</span><span class="sxs-lookup"><span data-stu-id="85801-131">Migrate data</span></span>
<span data-ttu-id="85801-132">By clicking the ‘Migrate Data’ option you can generate BCP scripts that will move your data first to flat files on your server, and then directly into your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="85801-132">By clicking the ‘Migrate Data’ option you can generate BCP scripts that will move your data first to flat files on your server, and then directly into your SQL Data Warehouse.</span></span> <span data-ttu-id="85801-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of the network connection.</span><span class="sxs-lookup"><span data-stu-id="85801-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of the network connection.</span></span> <span data-ttu-id="85801-134">In order to run this, you will need to have the BCP command-line utility installed and the schema for the data must already have been created.</span><span class="sxs-lookup"><span data-stu-id="85801-134">In order to run this, you will need to have the BCP command-line utility installed and the schema for the data must already have been created.</span></span>

<span data-ttu-id="85801-135">After you have filled out the parameters above you simply need to click run migration and a set of two packages will be generated to your specified location.</span><span class="sxs-lookup"><span data-stu-id="85801-135">After you have filled out the parameters above you simply need to click run migration and a set of two packages will be generated to your specified location.</span></span> <span data-ttu-id="85801-136">Run the export file in order to export data from your migration source into flat files, and run the import file in order to import your data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="85801-136">Run the export file in order to export data from your migration source into flat files, and run the import file in order to import your data into SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85801-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="85801-137">Next steps</span></span>
<span data-ttu-id="85801-138">Now that you've migrated some data, check out how to [develop][develop].</span><span class="sxs-lookup"><span data-stu-id="85801-138">Now that you've migrated some data, check out how to [develop][develop].</span></span>

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
