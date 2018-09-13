---
title: Set up Azure SQL Data Sync | Microsoft Docs
description: This tutorial shows you how to set up Azure SQL Data Sync
services: sql-database
author: allenwux
manager: craigg
ms.service: sql-database
ms.custom: load & move data
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: xiwu
ms.reviewer: douglasl
ms.openlocfilehash: ccdffaf0c224cc4579f24ca5f3ca60a6c53f3bd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782735"
---
# <a name="set-up-sql-data-sync"></a><span data-ttu-id="eca08-103">Set up SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="eca08-103">Set up SQL Data Sync</span></span>
<span data-ttu-id="eca08-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span><span class="sxs-lookup"><span data-stu-id="eca08-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="eca08-105">The new sync group is fully configured and synchronizes on the schedule you set.</span><span class="sxs-lookup"><span data-stu-id="eca08-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="eca08-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eca08-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="eca08-107">For an overview of SQL Data Sync, see [Sync data across multiple cloud and on-premises databases with Azure SQL Data Sync](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="eca08-107">For an overview of SQL Data Sync, see [Sync data across multiple cloud and on-premises databases with Azure SQL Data Sync](sql-database-sync-data.md).</span></span>

<span data-ttu-id="eca08-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="eca08-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="eca08-109">Use PowerShell to sync between multiple Azure SQL databases</span><span class="sxs-lookup"><span data-stu-id="eca08-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="eca08-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span><span class="sxs-lookup"><span data-stu-id="eca08-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

## <a name="step-1---create-sync-group"></a><span data-ttu-id="eca08-111">Step 1 - Create sync group</span><span class="sxs-lookup"><span data-stu-id="eca08-111">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="eca08-112">Locate the Data Sync settings</span><span class="sxs-lookup"><span data-stu-id="eca08-112">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="eca08-113">In your browser, navigate to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eca08-113">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="eca08-114">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="eca08-114">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![List of Azure SQL databases](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="eca08-116">On the **SQL databases** page, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-116">On the **SQL databases** page, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database page opens.</span></span>

    <span data-ttu-id="eca08-117">The hub database is the central endpoint of the sync topology, in which a sync group has multiple database endpoints.</span><span class="sxs-lookup"><span data-stu-id="eca08-117">The hub database is the central endpoint of the sync topology, in which a sync group has multiple database endpoints.</span></span> <span data-ttu-id="eca08-118">All other database endpoints in the same sync group - that is, all member databases - sync with the hub database.</span><span class="sxs-lookup"><span data-stu-id="eca08-118">All other database endpoints in the same sync group - that is, all member databases - sync with the hub database.</span></span>

4.  <span data-ttu-id="eca08-119">On the SQL database page for the selected database, select **Sync to other databases**.</span><span class="sxs-lookup"><span data-stu-id="eca08-119">On the SQL database page for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="eca08-120">The Data Sync page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-120">The Data Sync page opens.</span></span>

    ![Sync to other databases option](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="eca08-122">Create a new Sync Group</span><span class="sxs-lookup"><span data-stu-id="eca08-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="eca08-123">On the Data Sync page, select **New Sync Group**.</span><span class="sxs-lookup"><span data-stu-id="eca08-123">On the Data Sync page, select **New Sync Group**.</span></span> <span data-ttu-id="eca08-124">The **New sync group** page opens with Step 1, **Create sync group**, highlighted.</span><span class="sxs-lookup"><span data-stu-id="eca08-124">The **New sync group** page opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="eca08-125">The **Create Data Sync Group** page also opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-125">The **Create Data Sync Group** page also opens.</span></span>

2.  <span data-ttu-id="eca08-126">On the **Create Data Sync Group** page, do the following things:</span><span class="sxs-lookup"><span data-stu-id="eca08-126">On the **Create Data Sync Group** page, do the following things:</span></span>

    1.  <span data-ttu-id="eca08-127">In the **Sync Group Name** field, enter a name for the new sync group.</span><span class="sxs-lookup"><span data-stu-id="eca08-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="eca08-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span><span class="sxs-lookup"><span data-stu-id="eca08-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="eca08-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span><span class="sxs-lookup"><span data-stu-id="eca08-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="eca08-130">Data Sync creates tables in this database and runs a frequent workload.</span><span class="sxs-lookup"><span data-stu-id="eca08-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="eca08-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span><span class="sxs-lookup"><span data-stu-id="eca08-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="eca08-132">You can't change the Sync Metadata Database or its name without dropping it.</span><span class="sxs-lookup"><span data-stu-id="eca08-132">You can't change the Sync Metadata Database or its name without dropping it.</span></span>

        <span data-ttu-id="eca08-133">If you chose **New database**, select **Create new database.**</span><span class="sxs-lookup"><span data-stu-id="eca08-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="eca08-134">The **SQL Database** page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-134">The **SQL Database** page opens.</span></span> <span data-ttu-id="eca08-135">On the **SQL Database** page, name and configure the new database.</span><span class="sxs-lookup"><span data-stu-id="eca08-135">On the **SQL Database** page, name and configure the new database.</span></span> <span data-ttu-id="eca08-136">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="eca08-136">Then select **OK**.</span></span>

        <span data-ttu-id="eca08-137">If you chose **Use existing database**, select the database from the list.</span><span class="sxs-lookup"><span data-stu-id="eca08-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="eca08-138">In the **Automatic Sync** section, first select **On** or **Off**.</span><span class="sxs-lookup"><span data-stu-id="eca08-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="eca08-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span><span class="sxs-lookup"><span data-stu-id="eca08-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Specify sync frequency](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="eca08-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span><span class="sxs-lookup"><span data-stu-id="eca08-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        <span data-ttu-id="eca08-142">"Hub wins" means that, when a conflict occurs, the data in the hub database overwrites the conflicting data in the member database.</span><span class="sxs-lookup"><span data-stu-id="eca08-142">"Hub wins" means that, when a conflict occurs, the data in the hub database overwrites the conflicting data in the member database.</span></span> <span data-ttu-id="eca08-143">"Member wins" means that, when a conflict occurs, the data in the member database overwrites the conflicting data in the hub database.</span><span class="sxs-lookup"><span data-stu-id="eca08-143">"Member wins" means that, when a conflict occurs, the data in the member database overwrites the conflicting data in the hub database.</span></span> 

        ![Specify how conflicts are resolved](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="eca08-145">Select **OK** and wait for the new sync group to be created and deployed.</span><span class="sxs-lookup"><span data-stu-id="eca08-145">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="eca08-146">Step 2 - Add sync members</span><span class="sxs-lookup"><span data-stu-id="eca08-146">Step 2 - Add sync members</span></span>

<span data-ttu-id="eca08-147">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** page.</span><span class="sxs-lookup"><span data-stu-id="eca08-147">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** page.</span></span>

<span data-ttu-id="eca08-148">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span><span class="sxs-lookup"><span data-stu-id="eca08-148">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="eca08-149">Don't enter *new* credentials in this section.</span><span class="sxs-lookup"><span data-stu-id="eca08-149">Don't enter *new* credentials in this section.</span></span>

![Hub database has been added to sync group](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

### <a name="add-an-azure-sql-database"></a><span data-ttu-id="eca08-151">Add an Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="eca08-151">Add an Azure SQL Database</span></span>

<span data-ttu-id="eca08-152">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span><span class="sxs-lookup"><span data-stu-id="eca08-152">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="eca08-153">The **Configure Azure Database** page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-153">The **Configure Azure Database** page opens.</span></span>

<span data-ttu-id="eca08-154">On the **Configure Azure Database** page, do the following things:</span><span class="sxs-lookup"><span data-stu-id="eca08-154">On the **Configure Azure Database** page, do the following things:</span></span>

1.  <span data-ttu-id="eca08-155">In the **Sync Member Name** field, provide a name for the new sync member.</span><span class="sxs-lookup"><span data-stu-id="eca08-155">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="eca08-156">This name is distinct from the name of the database itself.</span><span class="sxs-lookup"><span data-stu-id="eca08-156">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="eca08-157">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span><span class="sxs-lookup"><span data-stu-id="eca08-157">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="eca08-158">In the **Azure SQL Server** field, select the existing SQL database server.</span><span class="sxs-lookup"><span data-stu-id="eca08-158">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="eca08-159">In the **Azure SQL Database** field, select the existing SQL database.</span><span class="sxs-lookup"><span data-stu-id="eca08-159">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="eca08-160">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span><span class="sxs-lookup"><span data-stu-id="eca08-160">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![Adding a new SQL Database sync member](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="eca08-162">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span><span class="sxs-lookup"><span data-stu-id="eca08-162">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="eca08-163">Don't enter *new* credentials in this section.</span><span class="sxs-lookup"><span data-stu-id="eca08-163">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="eca08-164">Select **OK** and wait for the new sync member to be created and deployed.</span><span class="sxs-lookup"><span data-stu-id="eca08-164">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![New SQL Database sync member has been added](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

### <a name="add-on-prem"></a> <span data-ttu-id="eca08-166">Add an on-premises SQL Server database</span><span class="sxs-lookup"><span data-stu-id="eca08-166">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="eca08-167">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span><span class="sxs-lookup"><span data-stu-id="eca08-167">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="eca08-168">The **Configure On-Premises** page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-168">The **Configure On-Premises** page opens.</span></span>

<span data-ttu-id="eca08-169">On the **Configure On-Premises** page, do the following things:</span><span class="sxs-lookup"><span data-stu-id="eca08-169">On the **Configure On-Premises** page, do the following things:</span></span>

1.  <span data-ttu-id="eca08-170">Select **Choose the Sync Agent Gateway**.</span><span class="sxs-lookup"><span data-stu-id="eca08-170">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="eca08-171">The **Select Sync Agent** page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-171">The **Select Sync Agent** page opens.</span></span>

    ![Choose the sync agent gateway](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="eca08-173">On the **Choose the Sync Agent Gateway** page, choose whether to use an existing agent or create a new agent.</span><span class="sxs-lookup"><span data-stu-id="eca08-173">On the **Choose the Sync Agent Gateway** page, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="eca08-174">If you chose **Existing agents**, select the existing agent from the list.</span><span class="sxs-lookup"><span data-stu-id="eca08-174">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="eca08-175">If you chose **Create a new agent**, do the following things:</span><span class="sxs-lookup"><span data-stu-id="eca08-175">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="eca08-176">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span><span class="sxs-lookup"><span data-stu-id="eca08-176">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="eca08-177">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span><span class="sxs-lookup"><span data-stu-id="eca08-177">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="eca08-178">Enter a name for the agent.</span><span class="sxs-lookup"><span data-stu-id="eca08-178">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="eca08-179">Select **Create and Generate Key**.</span><span class="sxs-lookup"><span data-stu-id="eca08-179">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="eca08-180">Copy the agent key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="eca08-180">Copy the agent key to the clipboard.</span></span>
        
        ![Creating a new sync agent](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="eca08-182">Select **OK** to close the **Select Sync Agent** page.</span><span class="sxs-lookup"><span data-stu-id="eca08-182">Select **OK** to close the **Select Sync Agent** page.</span></span>

    6.  <span data-ttu-id="eca08-183">On the SQL Server computer, locate and run the Client Sync Agent app.</span><span class="sxs-lookup"><span data-stu-id="eca08-183">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![The data sync client agent app](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="eca08-185">In the sync agent app, select **Submit Agent Key**.</span><span class="sxs-lookup"><span data-stu-id="eca08-185">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="eca08-186">The **Sync Metadata Database Configuration** dialog box opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-186">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="eca08-187">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eca08-187">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="eca08-188">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span><span class="sxs-lookup"><span data-stu-id="eca08-188">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="eca08-189">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span><span class="sxs-lookup"><span data-stu-id="eca08-189">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![Enter the agent key and server credentials](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="eca08-191">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span><span class="sxs-lookup"><span data-stu-id="eca08-191">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="eca08-192">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="eca08-192">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="eca08-193">In SSMS, try to connect to the hub database on Azure.</span><span class="sxs-lookup"><span data-stu-id="eca08-193">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="eca08-194">Enter its name as <hub_database_name>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="eca08-194">Enter its name as <hub_database_name>.database.windows.net.</span></span> <span data-ttu-id="eca08-195">To configure the Azure firewall rule, follow the steps in the dialog box.</span><span class="sxs-lookup"><span data-stu-id="eca08-195">To configure the Azure firewall rule, follow the steps in the dialog box.</span></span> <span data-ttu-id="eca08-196">Then return to the Client Sync Agent app.</span><span class="sxs-lookup"><span data-stu-id="eca08-196">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="eca08-197">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span><span class="sxs-lookup"><span data-stu-id="eca08-197">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="eca08-198">The **SQL Server Configuration** dialog box opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-198">The **SQL Server Configuration** dialog box opens.</span></span>

        ![Add and configure a SQL Server database](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="eca08-200">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="eca08-200">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="eca08-201">If you chose SQL Server authentication, enter the existing credentials.</span><span class="sxs-lookup"><span data-stu-id="eca08-201">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="eca08-202">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span><span class="sxs-lookup"><span data-stu-id="eca08-202">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="eca08-203">Then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="eca08-203">Then select **Save**.</span></span> <span data-ttu-id="eca08-204">The registered database appears in the list.</span><span class="sxs-lookup"><span data-stu-id="eca08-204">The registered database appears in the list.</span></span>

        ![SQL Server database is now registered](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="eca08-206">You can now close the Client Sync Agent app.</span><span class="sxs-lookup"><span data-stu-id="eca08-206">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="eca08-207">In the portal, on the **Configure On-Premises** page, select **Select the Database.**</span><span class="sxs-lookup"><span data-stu-id="eca08-207">In the portal, on the **Configure On-Premises** page, select **Select the Database.**</span></span> <span data-ttu-id="eca08-208">The **Select Database** page opens.</span><span class="sxs-lookup"><span data-stu-id="eca08-208">The **Select Database** page opens.</span></span>

    13. <span data-ttu-id="eca08-209">On the **Select Database** page, in the **Sync Member Name** field, provide a name for the new sync member.</span><span class="sxs-lookup"><span data-stu-id="eca08-209">On the **Select Database** page, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="eca08-210">This name is distinct from the name of the database itself.</span><span class="sxs-lookup"><span data-stu-id="eca08-210">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="eca08-211">Select the database from the list.</span><span class="sxs-lookup"><span data-stu-id="eca08-211">Select the database from the list.</span></span> <span data-ttu-id="eca08-212">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span><span class="sxs-lookup"><span data-stu-id="eca08-212">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![Select the on premises database](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="eca08-214">Select **OK** to close the **Select Database** page.</span><span class="sxs-lookup"><span data-stu-id="eca08-214">Select **OK** to close the **Select Database** page.</span></span> <span data-ttu-id="eca08-215">Then select **OK** to close the **Configure On-Premises** page and wait for the new sync member to be created and deployed.</span><span class="sxs-lookup"><span data-stu-id="eca08-215">Then select **OK** to close the **Configure On-Premises** page and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="eca08-216">Finally, click **OK** to close the **Select sync members** page.</span><span class="sxs-lookup"><span data-stu-id="eca08-216">Finally, click **OK** to close the **Select sync members** page.</span></span>

        ![On premises database added to sync group](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="eca08-218">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="eca08-218">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="eca08-219">Data Sync creates this role on the SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="eca08-219">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="eca08-220">Step 3 - Configure sync group</span><span class="sxs-lookup"><span data-stu-id="eca08-220">Step 3 - Configure sync group</span></span>

<span data-ttu-id="eca08-221">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** page.</span><span class="sxs-lookup"><span data-stu-id="eca08-221">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** page.</span></span>

1.  <span data-ttu-id="eca08-222">On the **Tables** page, select a database from the list of sync group members, and then select **Refresh schema**.</span><span class="sxs-lookup"><span data-stu-id="eca08-222">On the **Tables** page, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="eca08-223">From the list of available tables, select the tables that you want to sync.</span><span class="sxs-lookup"><span data-stu-id="eca08-223">From the list of available tables, select the tables that you want to sync.</span></span>

    ![Select tables to sync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="eca08-225">By default, all columns in the table are selected.</span><span class="sxs-lookup"><span data-stu-id="eca08-225">By default, all columns in the table are selected.</span></span> <span data-ttu-id="eca08-226">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span><span class="sxs-lookup"><span data-stu-id="eca08-226">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![Select fields to sync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="eca08-228">Finally, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="eca08-228">Finally, select **Save**.</span></span>

## <a name="faq-about-setup-and-configuration"></a><span data-ttu-id="eca08-229">FAQ about setup and configuration</span><span class="sxs-lookup"><span data-stu-id="eca08-229">FAQ about setup and configuration</span></span>

### <a name="how-frequently-can-data-sync-synchronize-my-data"></a><span data-ttu-id="eca08-230">How frequently can Data Sync synchronize my data?</span><span class="sxs-lookup"><span data-stu-id="eca08-230">How frequently can Data Sync synchronize my data?</span></span> 
<span data-ttu-id="eca08-231">The minimum frequency is every five minutes.</span><span class="sxs-lookup"><span data-stu-id="eca08-231">The minimum frequency is every five minutes.</span></span>

### <a name="does-sql-data-sync-fully-create-and-provision-tables"></a><span data-ttu-id="eca08-232">Does SQL Data Sync fully create and provision tables?</span><span class="sxs-lookup"><span data-stu-id="eca08-232">Does SQL Data Sync fully create and provision tables?</span></span>

<span data-ttu-id="eca08-233">If the sync schema tables are not already created in the destination database, SQL Data Sync creates them with the columns that you selected.</span><span class="sxs-lookup"><span data-stu-id="eca08-233">If the sync schema tables are not already created in the destination database, SQL Data Sync creates them with the columns that you selected.</span></span> <span data-ttu-id="eca08-234">However, this behavior does not result in a full fidelity schema, for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="eca08-234">However, this behavior does not result in a full fidelity schema, for the following reasons:</span></span>

-   <span data-ttu-id="eca08-235">Only the columns that you selected are created in the destination table.</span><span class="sxs-lookup"><span data-stu-id="eca08-235">Only the columns that you selected are created in the destination table.</span></span> <span data-ttu-id="eca08-236">If some columns in the source tables are not part of the sync group, those columns are not provisioned in the destination tables.</span><span class="sxs-lookup"><span data-stu-id="eca08-236">If some columns in the source tables are not part of the sync group, those columns are not provisioned in the destination tables.</span></span>

-   <span data-ttu-id="eca08-237">Indexes are created only for the selected columns.</span><span class="sxs-lookup"><span data-stu-id="eca08-237">Indexes are created only for the selected columns.</span></span> <span data-ttu-id="eca08-238">If the source table index has columns that are not part of the sync group, those indexes are not provisioned in the destination tables.</span><span class="sxs-lookup"><span data-stu-id="eca08-238">If the source table index has columns that are not part of the sync group, those indexes are not provisioned in the destination tables.</span></span>

-   <span data-ttu-id="eca08-239">Indexes on XML type columns are not provisioned.</span><span class="sxs-lookup"><span data-stu-id="eca08-239">Indexes on XML type columns are not provisioned.</span></span>

-   <span data-ttu-id="eca08-240">CHECK constraints are not provisioned.</span><span class="sxs-lookup"><span data-stu-id="eca08-240">CHECK constraints are not provisioned.</span></span>

-   <span data-ttu-id="eca08-241">Existing triggers on the source tables are not provisioned.</span><span class="sxs-lookup"><span data-stu-id="eca08-241">Existing triggers on the source tables are not provisioned.</span></span>

-   <span data-ttu-id="eca08-242">Views and Stored Procedures are not created on the destination database.</span><span class="sxs-lookup"><span data-stu-id="eca08-242">Views and Stored Procedures are not created on the destination database.</span></span>

<span data-ttu-id="eca08-243">Because of these limitations, we recommend the following things:</span><span class="sxs-lookup"><span data-stu-id="eca08-243">Because of these limitations, we recommend the following things:</span></span>
-   <span data-ttu-id="eca08-244">For production environments, provision the full-fidelity schema yourself.</span><span class="sxs-lookup"><span data-stu-id="eca08-244">For production environments, provision the full-fidelity schema yourself.</span></span>
-   <span data-ttu-id="eca08-245">For trying out the service, the auto-provisioning feature of SQL Data Sync works well.</span><span class="sxs-lookup"><span data-stu-id="eca08-245">For trying out the service, the auto-provisioning feature of SQL Data Sync works well.</span></span>

### <a name="why-do-i-see-tables-that-i-did-not-create"></a><span data-ttu-id="eca08-246">Why do I see tables that I did not create?</span><span class="sxs-lookup"><span data-stu-id="eca08-246">Why do I see tables that I did not create?</span></span>  
<span data-ttu-id="eca08-247">Data Sync creates side tables in your database for change tracking.</span><span class="sxs-lookup"><span data-stu-id="eca08-247">Data Sync creates side tables in your database for change tracking.</span></span> <span data-ttu-id="eca08-248">Don't delete them or Data Sync stops working.</span><span class="sxs-lookup"><span data-stu-id="eca08-248">Don't delete them or Data Sync stops working.</span></span>

### <a name="is-my-data-convergent-after-a-sync"></a><span data-ttu-id="eca08-249">Is my data convergent after a sync?</span><span class="sxs-lookup"><span data-stu-id="eca08-249">Is my data convergent after a sync?</span></span>

<span data-ttu-id="eca08-250">Not necessarily.</span><span class="sxs-lookup"><span data-stu-id="eca08-250">Not necessarily.</span></span> <span data-ttu-id="eca08-251">In a sync group with a hub and three spokes (A, B, and C), the synchronizations are Hub to A, Hub to B, and Hub to C. If a change is made to database A *after* the Hub to A sync, that change is not written to either database B or database C until the next sync task.</span><span class="sxs-lookup"><span data-stu-id="eca08-251">In a sync group with a hub and three spokes (A, B, and C), the synchronizations are Hub to A, Hub to B, and Hub to C. If a change is made to database A *after* the Hub to A sync, that change is not written to either database B or database C until the next sync task.</span></span>

### <a name="how-do-i-get-schema-changes-into-a-sync-group"></a><span data-ttu-id="eca08-252">How do I get schema changes into a sync group?</span><span class="sxs-lookup"><span data-stu-id="eca08-252">How do I get schema changes into a sync group?</span></span>

<span data-ttu-id="eca08-253">You have to make and propagate all schema changes manually.</span><span class="sxs-lookup"><span data-stu-id="eca08-253">You have to make and propagate all schema changes manually.</span></span>
1. <span data-ttu-id="eca08-254">Replicate the schema changes manually to the hub and to all sync members.</span><span class="sxs-lookup"><span data-stu-id="eca08-254">Replicate the schema changes manually to the hub and to all sync members.</span></span>
2. <span data-ttu-id="eca08-255">Update the sync schema.</span><span class="sxs-lookup"><span data-stu-id="eca08-255">Update the sync schema.</span></span>

<span data-ttu-id="eca08-256">**Adding new tables and columns**.</span><span class="sxs-lookup"><span data-stu-id="eca08-256">**Adding new tables and columns**.</span></span> <span data-ttu-id="eca08-257">New tables and columns don't impact the current sync. Data Sync ignores the new tables and columns until you add them to the sync schema.</span><span class="sxs-lookup"><span data-stu-id="eca08-257">New tables and columns don't impact the current sync. Data Sync ignores the new tables and columns until you add them to the sync schema.</span></span> <span data-ttu-id="eca08-258">When you add new database objects, this is the best sequence to follow:</span><span class="sxs-lookup"><span data-stu-id="eca08-258">When you add new database objects, this is the best sequence to follow:</span></span>
1. <span data-ttu-id="eca08-259">Add the new tables or columns to the hub and to all sync members.</span><span class="sxs-lookup"><span data-stu-id="eca08-259">Add the new tables or columns to the hub and to all sync members.</span></span>
2. <span data-ttu-id="eca08-260">Add the new tables or columns to the sync schema.</span><span class="sxs-lookup"><span data-stu-id="eca08-260">Add the new tables or columns to the sync schema.</span></span>
3. <span data-ttu-id="eca08-261">Start to insert values into the new tables and columns.</span><span class="sxs-lookup"><span data-stu-id="eca08-261">Start to insert values into the new tables and columns.</span></span>

<span data-ttu-id="eca08-262">**Changing the data type of a column**.</span><span class="sxs-lookup"><span data-stu-id="eca08-262">**Changing the data type of a column**.</span></span> <span data-ttu-id="eca08-263">When you change the data type of an existing column, Data Sync continues to work as long as the new values fit the original data type defined in the sync schema.</span><span class="sxs-lookup"><span data-stu-id="eca08-263">When you change the data type of an existing column, Data Sync continues to work as long as the new values fit the original data type defined in the sync schema.</span></span> <span data-ttu-id="eca08-264">For example, if you change the type in the source database from **int** to **bigint**, Data Sync continues to work until you insert a value that's too large for the **int** data type.</span><span class="sxs-lookup"><span data-stu-id="eca08-264">For example, if you change the type in the source database from **int** to **bigint**, Data Sync continues to work until you insert a value that's too large for the **int** data type.</span></span> <span data-ttu-id="eca08-265">To complete the change, replicate the schema change manually to the hub and to all sync members, and then update the sync schema.</span><span class="sxs-lookup"><span data-stu-id="eca08-265">To complete the change, replicate the schema change manually to the hub and to all sync members, and then update the sync schema.</span></span>

### <a name="how-can-i-export-and-import-a-database-with-data-sync"></a><span data-ttu-id="eca08-266">How can I export and import a database with Data Sync?</span><span class="sxs-lookup"><span data-stu-id="eca08-266">How can I export and import a database with Data Sync?</span></span>
<span data-ttu-id="eca08-267">After you export a database as a `.bacpac` file and import the file to create a new database, you have to do the following two things to use Data Sync in the new database:</span><span class="sxs-lookup"><span data-stu-id="eca08-267">After you export a database as a `.bacpac` file and import the file to create a new database, you have to do the following two things to use Data Sync in the new database:</span></span>
1.  <span data-ttu-id="eca08-268">Clean up the Data Sync objects and side tables on the **new database** by using [this script](https://github.com/vitomaz-msft/DataSyncMetadataCleanup/blob/master/Data%20Sync%20complete%20cleanup.sql).</span><span class="sxs-lookup"><span data-stu-id="eca08-268">Clean up the Data Sync objects and side tables on the **new database** by using [this script](https://github.com/vitomaz-msft/DataSyncMetadataCleanup/blob/master/Data%20Sync%20complete%20cleanup.sql).</span></span> <span data-ttu-id="eca08-269">This script deletes all of the required Data Sync objects from the database.</span><span class="sxs-lookup"><span data-stu-id="eca08-269">This script deletes all of the required Data Sync objects from the database.</span></span>
2.  <span data-ttu-id="eca08-270">Recreate the sync group with the new database.</span><span class="sxs-lookup"><span data-stu-id="eca08-270">Recreate the sync group with the new database.</span></span> <span data-ttu-id="eca08-271">If you no longer need the old sync group, delete it.</span><span class="sxs-lookup"><span data-stu-id="eca08-271">If you no longer need the old sync group, delete it.</span></span>

## <a name="faq-about-the-client-agent"></a><span data-ttu-id="eca08-272">FAQ about the client agent</span><span class="sxs-lookup"><span data-stu-id="eca08-272">FAQ about the client agent</span></span>

### <a name="why-do-i-need-a-client-agent"></a><span data-ttu-id="eca08-273">Why do I need a client agent?</span><span class="sxs-lookup"><span data-stu-id="eca08-273">Why do I need a client agent?</span></span>

<span data-ttu-id="eca08-274">The SQL Data Sync service communicates with SQL Server databases via the client agent.</span><span class="sxs-lookup"><span data-stu-id="eca08-274">The SQL Data Sync service communicates with SQL Server databases via the client agent.</span></span> <span data-ttu-id="eca08-275">This security feature prevents direct communication with databases behind a firewall.</span><span class="sxs-lookup"><span data-stu-id="eca08-275">This security feature prevents direct communication with databases behind a firewall.</span></span> <span data-ttu-id="eca08-276">When the SQL Data Sync service communicates with the agent, it does so using encrypted connections and a unique token or *agent key*.</span><span class="sxs-lookup"><span data-stu-id="eca08-276">When the SQL Data Sync service communicates with the agent, it does so using encrypted connections and a unique token or *agent key*.</span></span> <span data-ttu-id="eca08-277">The SQL Server databases authenticate the agent using the connection string and agent key.</span><span class="sxs-lookup"><span data-stu-id="eca08-277">The SQL Server databases authenticate the agent using the connection string and agent key.</span></span> <span data-ttu-id="eca08-278">This design provides a high level of security for your data.</span><span class="sxs-lookup"><span data-stu-id="eca08-278">This design provides a high level of security for your data.</span></span>

### <a name="how-many-instances-of-the-local-agent-ui-can-be-run"></a><span data-ttu-id="eca08-279">How many instances of the local agent UI can be run?</span><span class="sxs-lookup"><span data-stu-id="eca08-279">How many instances of the local agent UI can be run?</span></span>

<span data-ttu-id="eca08-280">Only one instance of the UI can be run.</span><span class="sxs-lookup"><span data-stu-id="eca08-280">Only one instance of the UI can be run.</span></span>

### <a name="how-can-i-change-my-service-account"></a><span data-ttu-id="eca08-281">How can I change my service account?</span><span class="sxs-lookup"><span data-stu-id="eca08-281">How can I change my service account?</span></span>

<span data-ttu-id="eca08-282">After you install a client agent, the only way to change the service account is to uninstall it and install a new client agent with the new service account.</span><span class="sxs-lookup"><span data-stu-id="eca08-282">After you install a client agent, the only way to change the service account is to uninstall it and install a new client agent with the new service account.</span></span>

### <a name="how-do-i-change-my-agent-key"></a><span data-ttu-id="eca08-283">How do I change my agent key?</span><span class="sxs-lookup"><span data-stu-id="eca08-283">How do I change my agent key?</span></span>

<span data-ttu-id="eca08-284">An agent key can only be used once by an agent.</span><span class="sxs-lookup"><span data-stu-id="eca08-284">An agent key can only be used once by an agent.</span></span> <span data-ttu-id="eca08-285">It cannot be reused when you remove then reinstall a new agent, nor can it be used by multiple agents.</span><span class="sxs-lookup"><span data-stu-id="eca08-285">It cannot be reused when you remove then reinstall a new agent, nor can it be used by multiple agents.</span></span> <span data-ttu-id="eca08-286">If you need to create a new key for an existing agent, you must be sure that the same key is recorded with the client agent and with the SQL Data Sync service.</span><span class="sxs-lookup"><span data-stu-id="eca08-286">If you need to create a new key for an existing agent, you must be sure that the same key is recorded with the client agent and with the SQL Data Sync service.</span></span>

### <a name="how-do-i-retire-a-client-agent"></a><span data-ttu-id="eca08-287">How do I retire a client agent?</span><span class="sxs-lookup"><span data-stu-id="eca08-287">How do I retire a client agent?</span></span>

<span data-ttu-id="eca08-288">To immediately invalidate or retire an agent, regenerate its key in the portal but do not submit it in the Agent UI.</span><span class="sxs-lookup"><span data-stu-id="eca08-288">To immediately invalidate or retire an agent, regenerate its key in the portal but do not submit it in the Agent UI.</span></span> <span data-ttu-id="eca08-289">Regenerating a key invalidates the previous key irrespective if the corresponding agent is online or offline.</span><span class="sxs-lookup"><span data-stu-id="eca08-289">Regenerating a key invalidates the previous key irrespective if the corresponding agent is online or offline.</span></span>

### <a name="how-do-i-move-a-client-agent-to-another-computer"></a><span data-ttu-id="eca08-290">How do I move a client agent to another computer?</span><span class="sxs-lookup"><span data-stu-id="eca08-290">How do I move a client agent to another computer?</span></span>

<span data-ttu-id="eca08-291">If you want to run the local agent from a different computer than it is currently on, do the following things:</span><span class="sxs-lookup"><span data-stu-id="eca08-291">If you want to run the local agent from a different computer than it is currently on, do the following things:</span></span>

1. <span data-ttu-id="eca08-292">Install the agent on desired computer.</span><span class="sxs-lookup"><span data-stu-id="eca08-292">Install the agent on desired computer.</span></span>

2. <span data-ttu-id="eca08-293">Log in to the SQL Data Sync portal and regenerate an agent key for the new agent.</span><span class="sxs-lookup"><span data-stu-id="eca08-293">Log in to the SQL Data Sync portal and regenerate an agent key for the new agent.</span></span>

3. <span data-ttu-id="eca08-294">Use the new agent's UI to submit the new agent key.</span><span class="sxs-lookup"><span data-stu-id="eca08-294">Use the new agent's UI to submit the new agent key.</span></span>

4. <span data-ttu-id="eca08-295">Wait while the client agent downloads the list of on-premises databases that were registered earlier.</span><span class="sxs-lookup"><span data-stu-id="eca08-295">Wait while the client agent downloads the list of on-premises databases that were registered earlier.</span></span>

5. <span data-ttu-id="eca08-296">Provide database credentials for all databases that display as unreachable.</span><span class="sxs-lookup"><span data-stu-id="eca08-296">Provide database credentials for all databases that display as unreachable.</span></span> <span data-ttu-id="eca08-297">These databases must be reachable from the new computer on which the agent is installed.</span><span class="sxs-lookup"><span data-stu-id="eca08-297">These databases must be reachable from the new computer on which the agent is installed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eca08-298">Next steps</span><span class="sxs-lookup"><span data-stu-id="eca08-298">Next steps</span></span>
<span data-ttu-id="eca08-299">Congratulations.</span><span class="sxs-lookup"><span data-stu-id="eca08-299">Congratulations.</span></span> <span data-ttu-id="eca08-300">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="eca08-300">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="eca08-301">For more info about SQL Data Sync, see:</span><span class="sxs-lookup"><span data-stu-id="eca08-301">For more info about SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="eca08-302">Sync data across multiple cloud and on-premises databases with Azure SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="eca08-302">Sync data across multiple cloud and on-premises databases with Azure SQL Data Sync</span></span>](sql-database-sync-data.md)
-   [<span data-ttu-id="eca08-303">Best practices for Azure SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="eca08-303">Best practices for Azure SQL Data Sync</span></span>](sql-database-best-practices-data-sync.md)
-   [<span data-ttu-id="eca08-304">Monitor Azure SQL Data Sync with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="eca08-304">Monitor Azure SQL Data Sync with Log Analytics</span></span>](sql-database-sync-monitor-oms.md)
-   [<span data-ttu-id="eca08-305">Troubleshoot issues with Azure SQL Data Sync</span><span class="sxs-lookup"><span data-stu-id="eca08-305">Troubleshoot issues with Azure SQL Data Sync</span></span>](sql-database-troubleshoot-data-sync.md)

-   <span data-ttu-id="eca08-306">Complete PowerShell examples that show how to configure SQL Data Sync:</span><span class="sxs-lookup"><span data-stu-id="eca08-306">Complete PowerShell examples that show how to configure SQL Data Sync:</span></span>
    -   [<span data-ttu-id="eca08-307">Use PowerShell to sync between multiple Azure SQL databases</span><span class="sxs-lookup"><span data-stu-id="eca08-307">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
    -   [<span data-ttu-id="eca08-308">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span><span class="sxs-lookup"><span data-stu-id="eca08-308">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

-   [<span data-ttu-id="eca08-309">Download the SQL Data Sync REST API documentation</span><span class="sxs-lookup"><span data-stu-id="eca08-309">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)

<span data-ttu-id="eca08-310">For more info about SQL Database, see:</span><span class="sxs-lookup"><span data-stu-id="eca08-310">For more info about SQL Database, see:</span></span>

-   [<span data-ttu-id="eca08-311">SQL Database Overview</span><span class="sxs-lookup"><span data-stu-id="eca08-311">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="eca08-312">Database Lifecycle Management</span><span class="sxs-lookup"><span data-stu-id="eca08-312">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
