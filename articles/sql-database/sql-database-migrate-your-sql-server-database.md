---
title: Migrate SQL Server DB to Azure SQL Database | Microsoft Docs
description: Learn to migrate your SQL Server database to Azure SQL Database.
services: sql-database
documentationcenter: ''
author: janeng
manager: jstrauss
editor: ''
tags: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: tutorial-migrate
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: ''
ms.date: 04/04/2017
ms.author: janeng
ms.openlocfilehash: 5afe40308725285e3af82d2931c9d8d3d4604ecf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551890"
---
# <a name="migrate-your-sql-server-database-to-azure-sql-database"></a><span data-ttu-id="d2920-103">Migrate your SQL Server database to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d2920-103">Migrate your SQL Server database to Azure SQL Database</span></span>

<span data-ttu-id="d2920-104">In this tutorial, you migrate an existing SQL Server database to Azure SQL Database using the Microsoft Data Migration Assistant and go through the required steps from preparing for migration to performing the actual data migration, and connecting to the migrated database after completed migration.</span><span class="sxs-lookup"><span data-stu-id="d2920-104">In this tutorial, you migrate an existing SQL Server database to Azure SQL Database using the Microsoft Data Migration Assistant and go through the required steps from preparing for migration to performing the actual data migration, and connecting to the migrated database after completed migration.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d2920-105">To fix compatibility issues, use [Visual Studio Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span><span class="sxs-lookup"><span data-stu-id="d2920-105">To fix compatibility issues, use [Visual Studio Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).</span></span> 
>

<span data-ttu-id="d2920-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="d2920-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="d2920-107">To complete this tutorial, make sure you have:</span><span class="sxs-lookup"><span data-stu-id="d2920-107">To complete this tutorial, make sure you have:</span></span>

- <span data-ttu-id="d2920-108">The newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="d2920-108">The newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="d2920-109">Installing SSMS also installs the newest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span><span class="sxs-lookup"><span data-stu-id="d2920-109">Installing SSMS also installs the newest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span> 
- <span data-ttu-id="d2920-110">The [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span><span class="sxs-lookup"><span data-stu-id="d2920-110">The [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span></span>
- <span data-ttu-id="d2920-111">A database to migrate.</span><span class="sxs-lookup"><span data-stu-id="d2920-111">A database to migrate.</span></span> <span data-ttu-id="d2920-112">This tutorial uses the [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span><span class="sxs-lookup"><span data-stu-id="d2920-112">This tutorial uses the [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span></span> 

## <a name="step-1---prepare-for-migration"></a><span data-ttu-id="d2920-113">Step 1 - Prepare for migration</span><span class="sxs-lookup"><span data-stu-id="d2920-113">Step 1 - Prepare for migration</span></span>

<span data-ttu-id="d2920-114">You are ready to prepare for migration.</span><span class="sxs-lookup"><span data-stu-id="d2920-114">You are ready to prepare for migration.</span></span> <span data-ttu-id="d2920-115">Follow these steps to use the **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** to assess the readiness of your database for migration to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d2920-115">Follow these steps to use the **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** to assess the readiness of your database for migration to Azure SQL Database.</span></span>

1. <span data-ttu-id="d2920-116">Open the **Data Migration Assistant**.</span><span class="sxs-lookup"><span data-stu-id="d2920-116">Open the **Data Migration Assistant**.</span></span> <span data-ttu-id="d2920-117">You can run DMA on any computer with connectivity to the SQL Server instance containing the database that you plan to migrate, you do not need to install it on the computer hosting the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="d2920-117">You can run DMA on any computer with connectivity to the SQL Server instance containing the database that you plan to migrate, you do not need to install it on the computer hosting the SQL Server instance.</span></span>

     ![open data migration assistant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. <span data-ttu-id="d2920-119">In the left-hand menu, click **+ New** to create an **Assessment** project.</span><span class="sxs-lookup"><span data-stu-id="d2920-119">In the left-hand menu, click **+ New** to create an **Assessment** project.</span></span> <span data-ttu-id="d2920-120">Fill in the form with a **Project name** (all other values should be left at their default values) and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2920-120">Fill in the form with a **Project name** (all other values should be left at their default values) and click **Create**.</span></span> <span data-ttu-id="d2920-121">The **Options** page opens.</span><span class="sxs-lookup"><span data-stu-id="d2920-121">The **Options** page opens.</span></span>

     ![new data migration assistant project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. <span data-ttu-id="d2920-123">On the **Options** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d2920-123">On the **Options** page, click **Next**.</span></span> <span data-ttu-id="d2920-124">The **Select sources** page opens.</span><span class="sxs-lookup"><span data-stu-id="d2920-124">The **Select sources** page opens.</span></span>

     ![new data migration options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. <span data-ttu-id="d2920-126">On the **Select sources** page, enter the name of SQL Server instance containing the server you plan to migrate.</span><span class="sxs-lookup"><span data-stu-id="d2920-126">On the **Select sources** page, enter the name of SQL Server instance containing the server you plan to migrate.</span></span> <span data-ttu-id="d2920-127">Change the other values on this page if necessary.</span><span class="sxs-lookup"><span data-stu-id="d2920-127">Change the other values on this page if necessary.</span></span> <span data-ttu-id="d2920-128">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d2920-128">Click **Connect**.</span></span>

     ![new data migration select sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. <span data-ttu-id="d2920-130">In the **Add sources** portion of the **Select sources** page, select the checkboxes for the databases to be tested for compatibility.</span><span class="sxs-lookup"><span data-stu-id="d2920-130">In the **Add sources** portion of the **Select sources** page, select the checkboxes for the databases to be tested for compatibility.</span></span> <span data-ttu-id="d2920-131">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d2920-131">Click **Add**.</span></span>

     ![new data migration select sources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. <span data-ttu-id="d2920-133">Click **Start Assessment**.</span><span class="sxs-lookup"><span data-stu-id="d2920-133">Click **Start Assessment**.</span></span>

     ![new data migration start assessment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. <span data-ttu-id="d2920-135">When the assessment completes, first look to see if the database is sufficiently compatible to migrate.</span><span class="sxs-lookup"><span data-stu-id="d2920-135">When the assessment completes, first look to see if the database is sufficiently compatible to migrate.</span></span> <span data-ttu-id="d2920-136">Look for the checkmark in a green circle.</span><span class="sxs-lookup"><span data-stu-id="d2920-136">Look for the checkmark in a green circle.</span></span>

     ![new data migration assessment results compatible](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. <span data-ttu-id="d2920-138">Review the results, beginning with **SQL Server feature parity**.</span><span class="sxs-lookup"><span data-stu-id="d2920-138">Review the results, beginning with **SQL Server feature parity**.</span></span> <span data-ttu-id="d2920-139">Specifically review the information about unsupported and partially supported features, and the provided information about recommended actions.</span><span class="sxs-lookup"><span data-stu-id="d2920-139">Specifically review the information about unsupported and partially supported features, and the provided information about recommended actions.</span></span> 

     ![new data migration assessment parity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. <span data-ttu-id="d2920-141">Click **Compatibility issues**.</span><span class="sxs-lookup"><span data-stu-id="d2920-141">Click **Compatibility issues**.</span></span> <span data-ttu-id="d2920-142">Specifically review the information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span><span class="sxs-lookup"><span data-stu-id="d2920-142">Specifically review the information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span></span> <span data-ttu-id="d2920-143">For the AdventureWorks2008R2 database, review the changes to Full-Text Search since SQL Server 2008 and the changes to SERVERPROPERTY('LCID') since SQL Server 2000.</span><span class="sxs-lookup"><span data-stu-id="d2920-143">For the AdventureWorks2008R2 database, review the changes to Full-Text Search since SQL Server 2008 and the changes to SERVERPROPERTY('LCID') since SQL Server 2000.</span></span> <span data-ttu-id="d2920-144">For details on these changes, links for more information is provided.</span><span class="sxs-lookup"><span data-stu-id="d2920-144">For details on these changes, links for more information is provided.</span></span> <span data-ttu-id="d2920-145">Many search options and settings for Full-Text Search have changed</span><span class="sxs-lookup"><span data-stu-id="d2920-145">Many search options and settings for Full-Text Search have changed</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="d2920-146">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span><span class="sxs-lookup"><span data-stu-id="d2920-146">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="d2920-147">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="d2920-147">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="d2920-148">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span><span class="sxs-lookup"><span data-stu-id="d2920-148">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>
   >

10. <span data-ttu-id="d2920-149">Optionally, click **Export report** to save the report as a JSON file.</span><span class="sxs-lookup"><span data-stu-id="d2920-149">Optionally, click **Export report** to save the report as a JSON file.</span></span>
11. <span data-ttu-id="d2920-150">Close the Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="d2920-150">Close the Data Migration Assistant.</span></span>

## <a name="step-2---export-to-bacpac-file"></a><span data-ttu-id="d2920-151">Step 2 - Export to BACPAC file</span><span class="sxs-lookup"><span data-stu-id="d2920-151">Step 2 - Export to BACPAC file</span></span> 

<span data-ttu-id="d2920-152">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d2920-152">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="d2920-153">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d2920-153">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server to Azure SQL Database.</span></span> <span data-ttu-id="d2920-154">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export.</span><span class="sxs-lookup"><span data-stu-id="d2920-154">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export.</span></span>

<span data-ttu-id="d2920-155">Follow these steps to use the SQLPackage command-line utility to export the AdventureWorks2008R2 database to local storage.</span><span class="sxs-lookup"><span data-stu-id="d2920-155">Follow these steps to use the SQLPackage command-line utility to export the AdventureWorks2008R2 database to local storage.</span></span>

1. <span data-ttu-id="d2920-156">Open a Windows command prompt and change your directory to a folder in which you have the **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span><span class="sxs-lookup"><span data-stu-id="d2920-156">Open a Windows command prompt and change your directory to a folder in which you have the **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span></span>

2. <span data-ttu-id="d2920-157">Execute the following SQLPackage command at the command prompt to export the **AdventureWorks2008R2** database from **localhost** to **AdventureWorks2008R2.bacpac**.</span><span class="sxs-lookup"><span data-stu-id="d2920-157">Execute the following SQLPackage command at the command prompt to export the **AdventureWorks2008R2** database from **localhost** to **AdventureWorks2008R2.bacpac**.</span></span> <span data-ttu-id="d2920-158">Change any of these values as appropriate to your environment.</span><span class="sxs-lookup"><span data-stu-id="d2920-158">Change any of these values as appropriate to your environment.</span></span>

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

<span data-ttu-id="d2920-160">Once the execution is complete the generated BCPAC file is stored in the directory where the sqlpackage executable is located.</span><span class="sxs-lookup"><span data-stu-id="d2920-160">Once the execution is complete the generated BCPAC file is stored in the directory where the sqlpackage executable is located.</span></span> <span data-ttu-id="d2920-161">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span><span class="sxs-lookup"><span data-stu-id="d2920-161">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span></span> 

## <a name="step-3-log-in-to-the-azure-portal"></a><span data-ttu-id="d2920-162">Step 3: Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d2920-162">Step 3: Log in to the Azure portal</span></span>

<span data-ttu-id="d2920-163">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2920-163">Log in to the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d2920-164">Logging on from the computer from which you are running the SQLPackage command-line utility eases the creation of the firewall rule in step 5.</span><span class="sxs-lookup"><span data-stu-id="d2920-164">Logging on from the computer from which you are running the SQLPackage command-line utility eases the creation of the firewall rule in step 5.</span></span>

## <a name="step-4-create-a-sql-database-logical-server"></a><span data-ttu-id="d2920-165">Step 4: Create a SQL Database logical server</span><span class="sxs-lookup"><span data-stu-id="d2920-165">Step 4: Create a SQL Database logical server</span></span>

<span data-ttu-id="d2920-166">An [Azure SQL Database logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span><span class="sxs-lookup"><span data-stu-id="d2920-166">An [Azure SQL Database logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span></span> <span data-ttu-id="d2920-167">Follow these steps to create a SQL Database logical server to contain the migrated Adventure Works OLTP SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="d2920-167">Follow these steps to create a SQL Database logical server to contain the migrated Adventure Works OLTP SQL Server database.</span></span> 

1. <span data-ttu-id="d2920-168">Click the **New** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d2920-168">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="d2920-169">Type **server** in the search window on the **New** page, and select **SQL database (logical server)** from the filtered list.</span><span class="sxs-lookup"><span data-stu-id="d2920-169">Type **server** in the search window on the **New** page, and select **SQL database (logical server)** from the filtered list.</span></span>

    ![select logical server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. <span data-ttu-id="d2920-171">On the **Everything** page, click **SQL server (logical server)** and then click **Create** on the **SQL Server (logical server)** page.</span><span class="sxs-lookup"><span data-stu-id="d2920-171">On the **Everything** page, click **SQL server (logical server)** and then click **Create** on the **SQL Server (logical server)** page.</span></span>

    ![create logical server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. <span data-ttu-id="d2920-173">Fill out the SQL server (logical server) form with the following information, as shown on the preceding image:</span><span class="sxs-lookup"><span data-stu-id="d2920-173">Fill out the SQL server (logical server) form with the following information, as shown on the preceding image:</span></span>     

   - <span data-ttu-id="d2920-174">Server name: Specify a globally unique server name</span><span class="sxs-lookup"><span data-stu-id="d2920-174">Server name: Specify a globally unique server name</span></span>
   - <span data-ttu-id="d2920-175">Server admin login: Provide a name for the Server admin login</span><span class="sxs-lookup"><span data-stu-id="d2920-175">Server admin login: Provide a name for the Server admin login</span></span>
   - <span data-ttu-id="d2920-176">Password: Specify the password of your choice</span><span class="sxs-lookup"><span data-stu-id="d2920-176">Password: Specify the password of your choice</span></span>
   - <span data-ttu-id="d2920-177">Resource group: Select **Create new** and specify **myResourceGroup**</span><span class="sxs-lookup"><span data-stu-id="d2920-177">Resource group: Select **Create new** and specify **myResourceGroup**</span></span>
   - <span data-ttu-id="d2920-178">Location: Select a data center location</span><span class="sxs-lookup"><span data-stu-id="d2920-178">Location: Select a data center location</span></span>

    ![create logical server completed form](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. <span data-ttu-id="d2920-180">Click **Create** to provision the logical server.</span><span class="sxs-lookup"><span data-stu-id="d2920-180">Click **Create** to provision the logical server.</span></span> <span data-ttu-id="d2920-181">Provisioning takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="d2920-181">Provisioning takes a few minutes.</span></span> 

## <a name="step-5-create-a-server-level-firewall-rule"></a><span data-ttu-id="d2920-182">Step 5: Create a server-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="d2920-182">Step 5: Create a server-level firewall rule</span></span>

<span data-ttu-id="d2920-183">The SQL Database service creates a [firewall at the server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span><span class="sxs-lookup"><span data-stu-id="d2920-183">The SQL Database service creates a [firewall at the server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="d2920-184">Follow these steps to create a SQL Database server-level firewall rule for the IP address of the computer from which you are running the SQLPackage command-line utility.</span><span class="sxs-lookup"><span data-stu-id="d2920-184">Follow these steps to create a SQL Database server-level firewall rule for the IP address of the computer from which you are running the SQLPackage command-line utility.</span></span> <span data-ttu-id="d2920-185">This enables SQLPackage to connect to the SQL Database logical server through the Azure SQL Database firewall.</span><span class="sxs-lookup"><span data-stu-id="d2920-185">This enables SQLPackage to connect to the SQL Database logical server through the Azure SQL Database firewall.</span></span> 

1. <span data-ttu-id="d2920-186">Click **All resources** from the left-hand menu and click your new server on the **All resources** page.</span><span class="sxs-lookup"><span data-stu-id="d2920-186">Click **All resources** from the left-hand menu and click your new server on the **All resources** page.</span></span> <span data-ttu-id="d2920-187">The overview page for your server opens, showing you the fully qualified server name (such as **mynewserver20170403.database.windows.net**) and provides options for further configuration.</span><span class="sxs-lookup"><span data-stu-id="d2920-187">The overview page for your server opens, showing you the fully qualified server name (such as **mynewserver20170403.database.windows.net**) and provides options for further configuration.</span></span>

     ![logical server overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="d2920-189">Click **Firewall** in the left-hand menu under **Settings** on the overview page.</span><span class="sxs-lookup"><span data-stu-id="d2920-189">Click **Firewall** in the left-hand menu under **Settings** on the overview page.</span></span> <span data-ttu-id="d2920-190">The **Firewall settings** page for the SQL Database server opens.</span><span class="sxs-lookup"><span data-stu-id="d2920-190">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="d2920-191">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d2920-191">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="d2920-192">A server-level firewall rule is created for this IP address.</span><span class="sxs-lookup"><span data-stu-id="d2920-192">A server-level firewall rule is created for this IP address.</span></span>

     ![set server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. <span data-ttu-id="d2920-194">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2920-194">Click **OK**.</span></span>

<span data-ttu-id="d2920-195">You can now connect to all databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span><span class="sxs-lookup"><span data-stu-id="d2920-195">You can now connect to all databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!NOTE]
> <span data-ttu-id="d2920-196">SQL Database communicates over port 1433.</span><span class="sxs-lookup"><span data-stu-id="d2920-196">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="d2920-197">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span><span class="sxs-lookup"><span data-stu-id="d2920-197">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d2920-198">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span><span class="sxs-lookup"><span data-stu-id="d2920-198">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="step-6---import-bacpac-file-to-azure-sql-database"></a><span data-ttu-id="d2920-199">Step 6 - Import BACPAC file to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d2920-199">Step 6 - Import BACPAC file to Azure SQL Database</span></span> 

<span data-ttu-id="d2920-200">The newest versions of the SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-200">The newest versions of the SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span></span> <span data-ttu-id="d2920-201">For best performance during import, select a high service tier and performance level and then scale down after import if the service tier and performance level is higher than you need immediately.</span><span class="sxs-lookup"><span data-stu-id="d2920-201">For best performance during import, select a high service tier and performance level and then scale down after import if the service tier and performance level is higher than you need immediately.</span></span>

<span data-ttu-id="d2920-202">Follow these steps use the SQLPackage command-line utility to import the AdventureWorks2008R2 database to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d2920-202">Follow these steps use the SQLPackage command-line utility to import the AdventureWorks2008R2 database to Azure SQL Database.</span></span>

- <span data-ttu-id="d2920-203">Execute the following SQLPackage command at the command prompt to import the **AdventureWorks2008R2** database from local storage to the Azure SQL Database logical server that you previously created with a database name of **myMigratedDatabase**, a service tier of **Premium**, and a Service Objective of **P6**.</span><span class="sxs-lookup"><span data-stu-id="d2920-203">Execute the following SQLPackage command at the command prompt to import the **AdventureWorks2008R2** database from local storage to the Azure SQL Database logical server that you previously created with a database name of **myMigratedDatabase**, a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="d2920-204">Change any of these three values as appropriate to your environment.</span><span class="sxs-lookup"><span data-stu-id="d2920-204">Change any of these three values as appropriate to your environment.</span></span>

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage import](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="d2920-206">An Azure SQL Database logical server listens on port 1433.</span><span class="sxs-lookup"><span data-stu-id="d2920-206">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="d2920-207">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span><span class="sxs-lookup"><span data-stu-id="d2920-207">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

## <a name="step-7---connect-using-sql-server-management-studio-ssms"></a><span data-ttu-id="d2920-208">Step 7 - Connect using SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="d2920-208">Step 7 - Connect using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="d2920-209">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server and newly migrated database.</span><span class="sxs-lookup"><span data-stu-id="d2920-209">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server and newly migrated database.</span></span> <span data-ttu-id="d2920-210">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using the steps in the previous procedure.</span><span class="sxs-lookup"><span data-stu-id="d2920-210">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using the steps in the previous procedure.</span></span>

1. <span data-ttu-id="d2920-211">Open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d2920-211">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="d2920-212">In the **Connect to Server** dialog box, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="d2920-212">In the **Connect to Server** dialog box, enter the following information:</span></span>
   - <span data-ttu-id="d2920-213">**Server type**: Specify Database engine</span><span class="sxs-lookup"><span data-stu-id="d2920-213">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="d2920-214">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="d2920-214">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span></span>
   - <span data-ttu-id="d2920-215">**Authentication**: Specify SQL Server Authentication</span><span class="sxs-lookup"><span data-stu-id="d2920-215">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="d2920-216">**Login**: Enter your server admin account</span><span class="sxs-lookup"><span data-stu-id="d2920-216">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="d2920-217">**Password**: Enter the password for your server admin account</span><span class="sxs-lookup"><span data-stu-id="d2920-217">**Password**: Enter the password for your server admin account</span></span>
 
    ![connect with ssms](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. <span data-ttu-id="d2920-219">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d2920-219">Click **Connect**.</span></span> <span data-ttu-id="d2920-220">The Object Explorer window opens.</span><span class="sxs-lookup"><span data-stu-id="d2920-220">The Object Explorer window opens.</span></span> 

4. <span data-ttu-id="d2920-221">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** to view the objects in the sample database.</span><span class="sxs-lookup"><span data-stu-id="d2920-221">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** to view the objects in the sample database.</span></span>

## <a name="step-8---change-database-properties"></a><span data-ttu-id="d2920-222">Step 8 - Change database properties</span><span class="sxs-lookup"><span data-stu-id="d2920-222">Step 8 - Change database properties</span></span>

<span data-ttu-id="d2920-223">You can change the service tier, performance level, and compatibility level using SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d2920-223">You can change the service tier, performance level, and compatibility level using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="d2920-224">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="d2920-224">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span></span> <span data-ttu-id="d2920-225">A query window opens connected to your database.</span><span class="sxs-lookup"><span data-stu-id="d2920-225">A query window opens connected to your database.</span></span>

2. <span data-ttu-id="d2920-226">Execute the following command to set the service tier to **Standard** and the performance level to **S1**.</span><span class="sxs-lookup"><span data-stu-id="d2920-226">Execute the following command to set the service tier to **Standard** and the performance level to **S1**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![change service tier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. <span data-ttu-id="d2920-228">Execute the following command to change the database compatibility level to **130**.</span><span class="sxs-lookup"><span data-stu-id="d2920-228">Execute the following command to change the database compatibility level to **130**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![change compatibility level](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a><span data-ttu-id="d2920-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2920-230">Next steps</span></span> 

- <span data-ttu-id="d2920-231">For an overview of migration, see [Database migration](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-231">For an overview of migration, see [Database migration](sql-database-cloud-migrate.md).</span></span>
- <span data-ttu-id="d2920-232">For a discussion of T-SQL differences, see [Resolving Transact-SQL differences during migration to SQL Database](sql-database-transact-sql-information.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-232">For a discussion of T-SQL differences, see [Resolving Transact-SQL differences during migration to SQL Database](sql-database-transact-sql-information.md).</span></span>
- <span data-ttu-id="d2920-233">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-233">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="d2920-234">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-234">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="d2920-235">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-235">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="d2920-236">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-236">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="d2920-237">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-237">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="d2920-238">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-238">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="d2920-239">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="d2920-239">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>



















