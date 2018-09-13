---
title: Getting started with Azure SQL Data Sync (Preview) | Microsoft Docs
description: This tutorial helps you get started with the Azure SQL Data Sync (Preview).
services: sql-database
documentationcenter: ''
author: dearandyxu
manager: jhubbard
editor: ''
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: sync data
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: jhubbard
ms.openlocfilehash: b0f7ba85d6c95a7ad65391988a8ef9eb56766233
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554808"
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="913be-103">Getting Started with Azure SQL Data Sync (Preview)</span><span class="sxs-lookup"><span data-stu-id="913be-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="913be-104">In this tutorial, you learn the fundamentals of Azure SQL Data Sync using the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="913be-104">In this tutorial, you learn the fundamentals of Azure SQL Data Sync using the Azure Classic Portal.</span></span>

<span data-ttu-id="913be-105">This tutorial assumes minimal prior experience with SQL Server and Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="913be-105">This tutorial assumes minimal prior experience with SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="913be-106">In this tutorial, you create a hybrid (SQL Server and SQL Database instances) sync group fully configured and synchronizing on the schedule you set.</span><span class="sxs-lookup"><span data-stu-id="913be-106">In this tutorial, you create a hybrid (SQL Server and SQL Database instances) sync group fully configured and synchronizing on the schedule you set.</span></span>

> [!NOTE]
> <span data-ttu-id="913be-107">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .pdf.</span><span class="sxs-lookup"><span data-stu-id="913be-107">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .pdf.</span></span> <span data-ttu-id="913be-108">Download it [here](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf).</span><span class="sxs-lookup"><span data-stu-id="913be-108">Download it [here](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf).</span></span>
>
>

## <a name="step-1-connect-to-the-azure-sql-database"></a><span data-ttu-id="913be-109">Step 1: Connect to the Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="913be-109">Step 1: Connect to the Azure SQL Database</span></span>
1. <span data-ttu-id="913be-110">Sign in to the [Classic Portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="913be-110">Sign in to the [Classic Portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="913be-111">Click **SQL DATABASES** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="913be-111">Click **SQL DATABASES** in the left pane.</span></span>
3. <span data-ttu-id="913be-112">Click **SYNC** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="913be-112">Click **SYNC** at the bottom of the page.</span></span> <span data-ttu-id="913be-113">When you click SYNC, a list appears showing the things you can add - **New Sync Group** and **New Sync Agent**.</span><span class="sxs-lookup"><span data-stu-id="913be-113">When you click SYNC, a list appears showing the things you can add - **New Sync Group** and **New Sync Agent**.</span></span>
4. <span data-ttu-id="913be-114">To launch the New SQL Data Sync Agent wizard, click **New Sync Agent**.</span><span class="sxs-lookup"><span data-stu-id="913be-114">To launch the New SQL Data Sync Agent wizard, click **New Sync Agent**.</span></span>
5. <span data-ttu-id="913be-115">If you haven't added an agent before, **click download it here**.</span><span class="sxs-lookup"><span data-stu-id="913be-115">If you haven't added an agent before, **click download it here**.</span></span>

    ![Image1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/SQLDatabaseScreen-Figure1.PNG)

## <a name="step-2-add-a-client-agent"></a><span data-ttu-id="913be-117">Step 2: Add a Client Agent</span><span class="sxs-lookup"><span data-stu-id="913be-117">Step 2: Add a Client Agent</span></span>
<span data-ttu-id="913be-118">This step is required only if you are going to have an on-premises SQL Server database included in your sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-118">This step is required only if you are going to have an on-premises SQL Server database included in your sync group.</span></span>
<span data-ttu-id="913be-119">Skip to Step 4 if your sync group has only SQL Database instances.</span><span class="sxs-lookup"><span data-stu-id="913be-119">Skip to Step 4 if your sync group has only SQL Database instances.</span></span>

<a id="InstallRequiredSoftware"></a>

### <a name="step-2a-install-the-required-software"></a><span data-ttu-id="913be-120">Step 2a: Install the required software</span><span class="sxs-lookup"><span data-stu-id="913be-120">Step 2a: Install the required software</span></span>
<span data-ttu-id="913be-121">Be sure that you have the following installed on the computer where you install the Client Agent.</span><span class="sxs-lookup"><span data-stu-id="913be-121">Be sure that you have the following installed on the computer where you install the Client Agent.</span></span>

* <span data-ttu-id="913be-122">**.NET Framework 4.0**</span><span class="sxs-lookup"><span data-stu-id="913be-122">**.NET Framework 4.0**</span></span>

  <span data-ttu-id="913be-123">Install .NET Framework 4.0 from [here](http://go.microsoft.com/fwlink/?linkid=205836).</span><span class="sxs-lookup"><span data-stu-id="913be-123">Install .NET Framework 4.0 from [here](http://go.microsoft.com/fwlink/?linkid=205836).</span></span>
* <span data-ttu-id="913be-124">**Microsoft SQL Server 2008 R2 SP1 System CLR Types (x86)**</span><span class="sxs-lookup"><span data-stu-id="913be-124">**Microsoft SQL Server 2008 R2 SP1 System CLR Types (x86)**</span></span>

  <span data-ttu-id="913be-125">Install the Microsoft SQL Server 2008 R2 SP1 System CLR Types (x86) from  [here](http://www.microsoft.com/download/en/details.aspx?id=26728)</span><span class="sxs-lookup"><span data-stu-id="913be-125">Install the Microsoft SQL Server 2008 R2 SP1 System CLR Types (x86) from  [here](http://www.microsoft.com/download/en/details.aspx?id=26728)</span></span>
* <span data-ttu-id="913be-126">**Microsoft SQL Server 2008 R2 SP1 Shared Management Objects (x86)**</span><span class="sxs-lookup"><span data-stu-id="913be-126">**Microsoft SQL Server 2008 R2 SP1 Shared Management Objects (x86)**</span></span>

  <span data-ttu-id="913be-127">Install the Microsoft SQL Server 2008 R2 SP1 Shared Management Objects (x86) from [here](http://www.microsoft.com/download/en/details.aspx?id=26728)</span><span class="sxs-lookup"><span data-stu-id="913be-127">Install the Microsoft SQL Server 2008 R2 SP1 Shared Management Objects (x86) from [here](http://www.microsoft.com/download/en/details.aspx?id=26728)</span></span>

<a id="InstallClient"></a>

### <a name="step-2b-install-a-new-client-agent"></a><span data-ttu-id="913be-128">Step 2b: Install a new Client Agent</span><span class="sxs-lookup"><span data-stu-id="913be-128">Step 2b: Install a new Client Agent</span></span>
<span data-ttu-id="913be-129">Follow the instructions in [Install a Client Agent (SQL Data Sync)](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf) to install the agent.</span><span class="sxs-lookup"><span data-stu-id="913be-129">Follow the instructions in [Install a Client Agent (SQL Data Sync)](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf) to install the agent.</span></span>

<a id="RegisterSSDb"></a>

### <a name="step-2c-finish-the-new-sql-data-sync-agent-wizard"></a><span data-ttu-id="913be-130">Step 2c: Finish the New SQL Data Sync Agent wizard</span><span class="sxs-lookup"><span data-stu-id="913be-130">Step 2c: Finish the New SQL Data Sync Agent wizard</span></span>
1. <span data-ttu-id="913be-131">Return to the New SQL Data Sync Agent wizard.</span><span class="sxs-lookup"><span data-stu-id="913be-131">Return to the New SQL Data Sync Agent wizard.</span></span>
2. <span data-ttu-id="913be-132">Give the agent a meaningful name.</span><span class="sxs-lookup"><span data-stu-id="913be-132">Give the agent a meaningful name.</span></span>
3. <span data-ttu-id="913be-133">From the dropdown, select the **REGION** (data center) to host this agent.</span><span class="sxs-lookup"><span data-stu-id="913be-133">From the dropdown, select the **REGION** (data center) to host this agent.</span></span>
4. <span data-ttu-id="913be-134">From the dropdown, select the **SUBSCRIPTION** to host this agent.</span><span class="sxs-lookup"><span data-stu-id="913be-134">From the dropdown, select the **SUBSCRIPTION** to host this agent.</span></span>
5. <span data-ttu-id="913be-135">Click the right-arrow.</span><span class="sxs-lookup"><span data-stu-id="913be-135">Click the right-arrow.</span></span>

## <a name="step-3-register-a-sql-server-database-with-the-client-agent"></a><span data-ttu-id="913be-136">Step 3: Register a SQL Server database with the Client Agent</span><span class="sxs-lookup"><span data-stu-id="913be-136">Step 3: Register a SQL Server database with the Client Agent</span></span>
<span data-ttu-id="913be-137">After the Client Agent is installed, register every on-premises SQL Server database that you intend to include in a sync group with the agent.</span><span class="sxs-lookup"><span data-stu-id="913be-137">After the Client Agent is installed, register every on-premises SQL Server database that you intend to include in a sync group with the agent.</span></span>
<span data-ttu-id="913be-138">To register a database with the agent, follow the instructions at [Register a SQL Server Database with a Client Agent](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf).</span><span class="sxs-lookup"><span data-stu-id="913be-138">To register a database with the agent, follow the instructions at [Register a SQL Server Database with a Client Agent](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf).</span></span>

## <a name="step-4-create-a-sync-group"></a><span data-ttu-id="913be-139">Step 4: Create a sync group</span><span class="sxs-lookup"><span data-stu-id="913be-139">Step 4: Create a sync group</span></span>
<a id="StartNewSGWizard"></a>

### <a name="step-4a-start-the-new-sync-group-wizard"></a><span data-ttu-id="913be-140">Step 4a: Start the New Sync Group wizard</span><span class="sxs-lookup"><span data-stu-id="913be-140">Step 4a: Start the New Sync Group wizard</span></span>
1. <span data-ttu-id="913be-141">Return to the [Classic Portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="913be-141">Return to the [Classic Portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="913be-142">Click **SQL DATABASES**.</span><span class="sxs-lookup"><span data-stu-id="913be-142">Click **SQL DATABASES**.</span></span>
3. <span data-ttu-id="913be-143">Click **ADD SYNC** at the bottom of the page then select New Sync Group from the drawer.</span><span class="sxs-lookup"><span data-stu-id="913be-143">Click **ADD SYNC** at the bottom of the page then select New Sync Group from the drawer.</span></span>

   ![Image2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/NewSyncGroup-Figure2.png)

<a id=""></a>

### <a name="step-4b-enter-the-basic-settings"></a><span data-ttu-id="913be-145">Step 4b: Enter the basic settings</span><span class="sxs-lookup"><span data-stu-id="913be-145">Step 4b: Enter the basic settings</span></span>
1. <span data-ttu-id="913be-146">Enter a meaningful name for the sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-146">Enter a meaningful name for the sync group.</span></span>
2. <span data-ttu-id="913be-147">From the dropdown, select the **REGION** (Data Center) to host this sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-147">From the dropdown, select the **REGION** (Data Center) to host this sync group.</span></span>
3. <span data-ttu-id="913be-148">Click the right-arrow.</span><span class="sxs-lookup"><span data-stu-id="913be-148">Click the right-arrow.</span></span>

    ![Image3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/NewSyncGroupName-Figure3.PNG)

<a id="DefineHubDB"></a>

### <a name="step-4c-define-the-sync-hub"></a><span data-ttu-id="913be-150">Step 4c: Define the sync hub</span><span class="sxs-lookup"><span data-stu-id="913be-150">Step 4c: Define the sync hub</span></span>
1. <span data-ttu-id="913be-151">From the dropdown, select the SQL Database instance to serve as the sync group hub.</span><span class="sxs-lookup"><span data-stu-id="913be-151">From the dropdown, select the SQL Database instance to serve as the sync group hub.</span></span>
2. <span data-ttu-id="913be-152">Enter the credentials for this SQL Database instance - **HUB USERNAME** and **HUB PASSWORD**.</span><span class="sxs-lookup"><span data-stu-id="913be-152">Enter the credentials for this SQL Database instance - **HUB USERNAME** and **HUB PASSWORD**.</span></span>
3. <span data-ttu-id="913be-153">Wait for SQL Data Sync to confirm the USERNAME and PASSWORD.</span><span class="sxs-lookup"><span data-stu-id="913be-153">Wait for SQL Data Sync to confirm the USERNAME and PASSWORD.</span></span> <span data-ttu-id="913be-154">You will see a green check mark appear to the right of the PASSWORD when the credentials are confirmed.</span><span class="sxs-lookup"><span data-stu-id="913be-154">You will see a green check mark appear to the right of the PASSWORD when the credentials are confirmed.</span></span>
4. <span data-ttu-id="913be-155">From the dropdown, select the **CONFLICT RESOLUTION** policy.</span><span class="sxs-lookup"><span data-stu-id="913be-155">From the dropdown, select the **CONFLICT RESOLUTION** policy.</span></span>

   <span data-ttu-id="913be-156">**Hub Wins** - any change written to the hub database write to the reference databases, overwriting changes in the same reference database record.</span><span class="sxs-lookup"><span data-stu-id="913be-156">**Hub Wins** - any change written to the hub database write to the reference databases, overwriting changes in the same reference database record.</span></span> <span data-ttu-id="913be-157">Functionally, this means that the first change written to the hub propagates to the other databases.</span><span class="sxs-lookup"><span data-stu-id="913be-157">Functionally, this means that the first change written to the hub propagates to the other databases.</span></span>

 <span data-ttu-id="913be-158">**Client Wins** - changes written to the hub are overwritten by changes in reference databases.</span><span class="sxs-lookup"><span data-stu-id="913be-158">**Client Wins** - changes written to the hub are overwritten by changes in reference databases.</span></span> <span data-ttu-id="913be-159">Functionally, this means that the last change written to the hub is the one kept and propagated to the other databases.</span><span class="sxs-lookup"><span data-stu-id="913be-159">Functionally, this means that the last change written to the hub is the one kept and propagated to the other databases.</span></span>

1. <span data-ttu-id="913be-160">Click the right-arrow.</span><span class="sxs-lookup"><span data-stu-id="913be-160">Click the right-arrow.</span></span>

   ![Image4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/NewSyncGroupHub-Figure4.PNG)

<a id="AddRefDB"></a>

### <a name="step-4d-add-a-reference-database"></a><span data-ttu-id="913be-162">Step 4d: Add a reference database</span><span class="sxs-lookup"><span data-stu-id="913be-162">Step 4d: Add a reference database</span></span>
<span data-ttu-id="913be-163">Repeat this step for each additional database you want to add to the sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-163">Repeat this step for each additional database you want to add to the sync group.</span></span>

1. <span data-ttu-id="913be-164">From the dropdown, select the database to add.</span><span class="sxs-lookup"><span data-stu-id="913be-164">From the dropdown, select the database to add.</span></span>

    <span data-ttu-id="913be-165">Databases in the dropdown include both SQL Server databases that have been registered with the agent and SQL Database instances.</span><span class="sxs-lookup"><span data-stu-id="913be-165">Databases in the dropdown include both SQL Server databases that have been registered with the agent and SQL Database instances.</span></span>
2. <span data-ttu-id="913be-166">Enter credentials for this database - **USERNAME** and **PASSWORD**.</span><span class="sxs-lookup"><span data-stu-id="913be-166">Enter credentials for this database - **USERNAME** and **PASSWORD**.</span></span>
3. <span data-ttu-id="913be-167">From the dropdown, select the **SYNC DIRECTION** for this database.</span><span class="sxs-lookup"><span data-stu-id="913be-167">From the dropdown, select the **SYNC DIRECTION** for this database.</span></span>

   <span data-ttu-id="913be-168">**Bi-directional** - changes in the reference database are written to the hub database, and changes to the hub database are written to the reference database.</span><span class="sxs-lookup"><span data-stu-id="913be-168">**Bi-directional** - changes in the reference database are written to the hub database, and changes to the hub database are written to the reference database.</span></span>

   <span data-ttu-id="913be-169">**Sync from the Hub** - The database receives updates from the Hub.</span><span class="sxs-lookup"><span data-stu-id="913be-169">**Sync from the Hub** - The database receives updates from the Hub.</span></span> <span data-ttu-id="913be-170">It does not send changes to the Hub.</span><span class="sxs-lookup"><span data-stu-id="913be-170">It does not send changes to the Hub.</span></span>

   <span data-ttu-id="913be-171">**Sync to the Hub** - The database sends updates to the Hub.</span><span class="sxs-lookup"><span data-stu-id="913be-171">**Sync to the Hub** - The database sends updates to the Hub.</span></span> <span data-ttu-id="913be-172">Changes in the Hub are not written to this database.</span><span class="sxs-lookup"><span data-stu-id="913be-172">Changes in the Hub are not written to this database.</span></span>
4. <span data-ttu-id="913be-173">To finish creating the sync group, click the check mark in the lower right of the wizard.</span><span class="sxs-lookup"><span data-stu-id="913be-173">To finish creating the sync group, click the check mark in the lower right of the wizard.</span></span> <span data-ttu-id="913be-174">Wait for the SQL Data Sync to confirm the credentials.</span><span class="sxs-lookup"><span data-stu-id="913be-174">Wait for the SQL Data Sync to confirm the credentials.</span></span> <span data-ttu-id="913be-175">A green check indicates that the credentials are confirmed.</span><span class="sxs-lookup"><span data-stu-id="913be-175">A green check indicates that the credentials are confirmed.</span></span>
5. <span data-ttu-id="913be-176">Click the check mark a second time.</span><span class="sxs-lookup"><span data-stu-id="913be-176">Click the check mark a second time.</span></span> <span data-ttu-id="913be-177">This returns you to the **SYNC** page under SQL Databases.</span><span class="sxs-lookup"><span data-stu-id="913be-177">This returns you to the **SYNC** page under SQL Databases.</span></span> <span data-ttu-id="913be-178">This sync group is now listed with your other sync groups and agents.</span><span class="sxs-lookup"><span data-stu-id="913be-178">This sync group is now listed with your other sync groups and agents.</span></span>

   ![Image5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/NewSyncGroupReference-Figure5.PNG)

## <a name="step-5-define-the-data-to-sync"></a><span data-ttu-id="913be-180">Step 5: Define the data to sync</span><span class="sxs-lookup"><span data-stu-id="913be-180">Step 5: Define the data to sync</span></span>
<span data-ttu-id="913be-181">Azure SQL Data Sync allows you to select tables and columns to synchronize.</span><span class="sxs-lookup"><span data-stu-id="913be-181">Azure SQL Data Sync allows you to select tables and columns to synchronize.</span></span> <span data-ttu-id="913be-182">If you also want to filter a column so that only rows with specific values (such as, Age>=65) synchronize, use the SQL Data Sync portal at Azure and the documentation at Select the Tables, Columns, and Rows to Synchronize to define the data to sync.</span><span class="sxs-lookup"><span data-stu-id="913be-182">If you also want to filter a column so that only rows with specific values (such as, Age>=65) synchronize, use the SQL Data Sync portal at Azure and the documentation at Select the Tables, Columns, and Rows to Synchronize to define the data to sync.</span></span>

1. <span data-ttu-id="913be-183">Return to the [Classic Portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="913be-183">Return to the [Classic Portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="913be-184">Click **SQL DATABASES**.</span><span class="sxs-lookup"><span data-stu-id="913be-184">Click **SQL DATABASES**.</span></span>
3. <span data-ttu-id="913be-185">Click the **SYNC** tab.</span><span class="sxs-lookup"><span data-stu-id="913be-185">Click the **SYNC** tab.</span></span>
4. <span data-ttu-id="913be-186">Click the name of this sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-186">Click the name of this sync group.</span></span>
5. <span data-ttu-id="913be-187">Click the **SYNC RULES** tab.</span><span class="sxs-lookup"><span data-stu-id="913be-187">Click the **SYNC RULES** tab.</span></span>
6. <span data-ttu-id="913be-188">Select the database you want to provide the sync group schema.</span><span class="sxs-lookup"><span data-stu-id="913be-188">Select the database you want to provide the sync group schema.</span></span>
7. <span data-ttu-id="913be-189">Click the right-arrow.</span><span class="sxs-lookup"><span data-stu-id="913be-189">Click the right-arrow.</span></span>
8. <span data-ttu-id="913be-190">Click **REFRESH SCHEMA**.</span><span class="sxs-lookup"><span data-stu-id="913be-190">Click **REFRESH SCHEMA**.</span></span>
9. <span data-ttu-id="913be-191">For each table in the database, select the columns to include in the synchronizations.</span><span class="sxs-lookup"><span data-stu-id="913be-191">For each table in the database, select the columns to include in the synchronizations.</span></span>
   * <span data-ttu-id="913be-192">Columns with unsupported data types cannot be selected.</span><span class="sxs-lookup"><span data-stu-id="913be-192">Columns with unsupported data types cannot be selected.</span></span>
   * <span data-ttu-id="913be-193">If no columns in a table are selected, the table is not included in the sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-193">If no columns in a table are selected, the table is not included in the sync group.</span></span>
   * <span data-ttu-id="913be-194">To select/unselect all the tables, click SELECT at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="913be-194">To select/unselect all the tables, click SELECT at the bottom of the screen.</span></span>
10. <span data-ttu-id="913be-195">Click **SAVE**, then wait for the sync group to finish provisioning.</span><span class="sxs-lookup"><span data-stu-id="913be-195">Click **SAVE**, then wait for the sync group to finish provisioning.</span></span>
11. <span data-ttu-id="913be-196">To return to the Data Sync landing page, click the back-arrow in the upper left of the screen (above the sync group's name).</span><span class="sxs-lookup"><span data-stu-id="913be-196">To return to the Data Sync landing page, click the back-arrow in the upper left of the screen (above the sync group's name).</span></span>

    ![Image6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/NewSyncGroupSyncRules-Figure6.PNG)

## <a name="step-6-configure-your-sync-group"></a><span data-ttu-id="913be-198">Step 6: Configure your sync group</span><span class="sxs-lookup"><span data-stu-id="913be-198">Step 6: Configure your sync group</span></span>
<span data-ttu-id="913be-199">You can always synchronize a sync group by clicking SYNC at the bottom of the Data Sync landing page.</span><span class="sxs-lookup"><span data-stu-id="913be-199">You can always synchronize a sync group by clicking SYNC at the bottom of the Data Sync landing page.</span></span>
<span data-ttu-id="913be-200">To synchronize on a schedule, you configure the sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-200">To synchronize on a schedule, you configure the sync group.</span></span>

1. <span data-ttu-id="913be-201">Return to the [Classic Portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="913be-201">Return to the [Classic Portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="913be-202">Click **SQL DATABASES**.</span><span class="sxs-lookup"><span data-stu-id="913be-202">Click **SQL DATABASES**.</span></span>
3. <span data-ttu-id="913be-203">Click the **SYNC** tab.</span><span class="sxs-lookup"><span data-stu-id="913be-203">Click the **SYNC** tab.</span></span>
4. <span data-ttu-id="913be-204">Click the name of this sync group.</span><span class="sxs-lookup"><span data-stu-id="913be-204">Click the name of this sync group.</span></span>
5. <span data-ttu-id="913be-205">Click the **CONFIGURE** tab.</span><span class="sxs-lookup"><span data-stu-id="913be-205">Click the **CONFIGURE** tab.</span></span>
6. <span data-ttu-id="913be-206">**AUTOMATIC SYNC**</span><span class="sxs-lookup"><span data-stu-id="913be-206">**AUTOMATIC SYNC**</span></span>
   * <span data-ttu-id="913be-207">To configure the sync group to sync on a set frequency, click **ON**.</span><span class="sxs-lookup"><span data-stu-id="913be-207">To configure the sync group to sync on a set frequency, click **ON**.</span></span> <span data-ttu-id="913be-208">You can still sync on demand by clicking SYNC.</span><span class="sxs-lookup"><span data-stu-id="913be-208">You can still sync on demand by clicking SYNC.</span></span>
   * <span data-ttu-id="913be-209">Click **OFF** to configure the sync group to sync only when you click SYNC.</span><span class="sxs-lookup"><span data-stu-id="913be-209">Click **OFF** to configure the sync group to sync only when you click SYNC.</span></span>
7. <span data-ttu-id="913be-210">**SYNC FREQUENCY**</span><span class="sxs-lookup"><span data-stu-id="913be-210">**SYNC FREQUENCY**</span></span>
   * <span data-ttu-id="913be-211">If AUTOMATIC SYNC is ON, set the synchronization frequency.</span><span class="sxs-lookup"><span data-stu-id="913be-211">If AUTOMATIC SYNC is ON, set the synchronization frequency.</span></span> <span data-ttu-id="913be-212">The frequency must be between 5 Minutes and 1 Month.</span><span class="sxs-lookup"><span data-stu-id="913be-212">The frequency must be between 5 Minutes and 1 Month.</span></span>
8. <span data-ttu-id="913be-213">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="913be-213">Click **SAVE**.</span></span>

![Image7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-sql-data-sync/NewSyncGroupConfigure-Figure7.PNG)

<span data-ttu-id="913be-215">Congratulations.</span><span class="sxs-lookup"><span data-stu-id="913be-215">Congratulations.</span></span> <span data-ttu-id="913be-216">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="913be-216">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="913be-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="913be-217">Next steps</span></span>
<span data-ttu-id="913be-218">For additional information on SQL Database and SQL Data Sync see:</span><span class="sxs-lookup"><span data-stu-id="913be-218">For additional information on SQL Database and SQL Data Sync see:</span></span>

* [<span data-ttu-id="913be-219">Download the complete SQL Data Sync technical documentation</span><span class="sxs-lookup"><span data-stu-id="913be-219">Download the complete SQL Data Sync technical documentation</span></span>](http://download.microsoft.com/download/4/E/3/4E394315-A4CB-4C59-9696-B25215A19CEF/SQL_Data_Sync_Preview.pdf)
* [<span data-ttu-id="913be-220">SQL Database Overview</span><span class="sxs-lookup"><span data-stu-id="913be-220">SQL Database Overview</span></span>](sql-database-technical-overview.md)
* [<span data-ttu-id="913be-221">Database Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="913be-221">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)







