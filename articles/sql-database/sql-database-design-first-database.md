---
title: Design your first Azure SQL database | Microsoft Docs
description: Learn to design your first Azure SQL database.
services: sql-database
documentationcenter: ''
author: janeng
manager: jstrauss
editor: ''
tags: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: ''
ms.date: 03/30/2017
ms.author: janeng
ms.openlocfilehash: ca51ee37801430d64581cbedfee4e3d612e40e48
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552146"
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="190d3-103">Design your first Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="190d3-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="190d3-104">In this tutorial, you build a database for a university to track student grades and courses enrollment.</span><span class="sxs-lookup"><span data-stu-id="190d3-104">In this tutorial, you build a database for a university to track student grades and courses enrollment.</span></span> <span data-ttu-id="190d3-105">This tutorial demonstrates how to use the [Azure portal](https://portal.azure.com/) and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to create an Azure SQL database on an Azure SQL Database logical server, add tables to the database, load data into the tables, and query the database.</span><span class="sxs-lookup"><span data-stu-id="190d3-105">This tutorial demonstrates how to use the [Azure portal](https://portal.azure.com/) and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to create an Azure SQL database on an Azure SQL Database logical server, add tables to the database, load data into the tables, and query the database.</span></span> <span data-ttu-id="190d3-106">It also demonstrates how to use SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities to restore the database to an earlier point in time.</span><span class="sxs-lookup"><span data-stu-id="190d3-106">It also demonstrates how to use SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities to restore the database to an earlier point in time.</span></span>

<span data-ttu-id="190d3-107">To complete this tutorial, make sure you have installed the newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="190d3-107">To complete this tutorial, make sure you have installed the newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span> 

## <a name="step-1-log-in-to-the-azure-portal"></a><span data-ttu-id="190d3-108">Step 1: Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="190d3-108">Step 1: Log in to the Azure portal</span></span>

<span data-ttu-id="190d3-109">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="190d3-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="step-2-create-a-blank-sql-database-in-azure"></a><span data-ttu-id="190d3-110">Step 2: Create a blank SQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="190d3-110">Step 2: Create a blank SQL database in Azure</span></span>

<span data-ttu-id="190d3-111">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="190d3-111">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="190d3-112">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="190d3-112">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="190d3-113">Follow these steps to create a blank SQL database.</span><span class="sxs-lookup"><span data-stu-id="190d3-113">Follow these steps to create a blank SQL database.</span></span> 

1. <span data-ttu-id="190d3-114">Click the **New** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="190d3-114">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="190d3-115">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span><span class="sxs-lookup"><span data-stu-id="190d3-115">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span> 

    ![create empty-database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="190d3-117">Fill out the SQL Database form with the following information, as shown on the preceding image:</span><span class="sxs-lookup"><span data-stu-id="190d3-117">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>     

   - <span data-ttu-id="190d3-118">Database name: **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="190d3-118">Database name: **mySampleDatabase**</span></span>
   - <span data-ttu-id="190d3-119">Resource group: **myResourceGroup**</span><span class="sxs-lookup"><span data-stu-id="190d3-119">Resource group: **myResourceGroup**</span></span>
   - <span data-ttu-id="190d3-120">Source: **Blank database**</span><span class="sxs-lookup"><span data-stu-id="190d3-120">Source: **Blank database**</span></span>

4. <span data-ttu-id="190d3-121">Click **Server** to create and configure a new server for your new database.</span><span class="sxs-lookup"><span data-stu-id="190d3-121">Click **Server** to create and configure a new server for your new database.</span></span> <span data-ttu-id="190d3-122">Fill out the **New server form** specifying a globally unique server name, provide a name for the Server admin login, and then specify the password of your choice.</span><span class="sxs-lookup"><span data-stu-id="190d3-122">Fill out the **New server form** specifying a globally unique server name, provide a name for the Server admin login, and then specify the password of your choice.</span></span> 

    ![create database-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-database-server.png)
5. <span data-ttu-id="190d3-124">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="190d3-124">Click **Select**.</span></span>

6. <span data-ttu-id="190d3-125">Click **Pricing tier** to specify the service tier and performance level for your new database.</span><span class="sxs-lookup"><span data-stu-id="190d3-125">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="190d3-126">For this tutorial, select **20 DTUs** and **250** GB of storage.</span><span class="sxs-lookup"><span data-stu-id="190d3-126">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

    ![create database-s1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="190d3-128">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="190d3-128">Click **Apply**.</span></span>  

8. <span data-ttu-id="190d3-129">Click **Create** to provision the database.</span><span class="sxs-lookup"><span data-stu-id="190d3-129">Click **Create** to provision the database.</span></span> <span data-ttu-id="190d3-130">Provisioning takes about a minute and a half to complete.</span><span class="sxs-lookup"><span data-stu-id="190d3-130">Provisioning takes about a minute and a half to complete.</span></span> 

9. <span data-ttu-id="190d3-131">On the toolbar, click **Notifications** to monitor the deployment process.</span><span class="sxs-lookup"><span data-stu-id="190d3-131">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

    ![notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/notification.png)


## <a name="step-3-create-a-server-level-firewall-rule"></a><span data-ttu-id="190d3-133">Step 3: Create a server-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="190d3-133">Step 3: Create a server-level firewall rule</span></span>

<span data-ttu-id="190d3-134">Azure SQL Databases are protected by a firewall.</span><span class="sxs-lookup"><span data-stu-id="190d3-134">Azure SQL Databases are protected by a firewall.</span></span> <span data-ttu-id="190d3-135">By default, all connections to the server and the databases inside the server are rejected.</span><span class="sxs-lookup"><span data-stu-id="190d3-135">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="190d3-136">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from your client's IP address.</span><span class="sxs-lookup"><span data-stu-id="190d3-136">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from your client's IP address.</span></span> 

1. <span data-ttu-id="190d3-137">After the deployment completes, click **SQL databases** from the left-hand menu and click your new database, **mySampleDatabase**, on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="190d3-137">After the deployment completes, click **SQL databases** from the left-hand menu and click your new database, **mySampleDatabase**, on the **SQL databases** page.</span></span> <span data-ttu-id="190d3-138">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span><span class="sxs-lookup"><span data-stu-id="190d3-138">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.</span></span>

      ![server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/server-firewall-rule.png) 

2. <span data-ttu-id="190d3-140">Click **Set server firewall** on the toolbar as shown in the previous image.</span><span class="sxs-lookup"><span data-stu-id="190d3-140">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="190d3-141">The **Firewall settings** page for the SQL Database server opens.</span><span class="sxs-lookup"><span data-stu-id="190d3-141">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="190d3-142">Click **Add client IP** on the toolbar and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="190d3-142">Click **Add client IP** on the toolbar and then click **Save**.</span></span> <span data-ttu-id="190d3-143">A server-level firewall rule is created for your current IP address.</span><span class="sxs-lookup"><span data-stu-id="190d3-143">A server-level firewall rule is created for your current IP address.</span></span>

      ![set server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/server-firewall-rule-set.png) 

4. <span data-ttu-id="190d3-145">Click **OK** and then click the **X** to close the **Firewall settings** page.</span><span class="sxs-lookup"><span data-stu-id="190d3-145">Click **OK** and then click the **X** to close the **Firewall settings** page.</span></span>

<span data-ttu-id="190d3-146">You can now connect to the database and its server using SQL Server Management Studio or another tool of your choice.</span><span class="sxs-lookup"><span data-stu-id="190d3-146">You can now connect to the database and its server using SQL Server Management Studio or another tool of your choice.</span></span>

> [!NOTE]
> <span data-ttu-id="190d3-147">SQL Database communicates over port 1433.</span><span class="sxs-lookup"><span data-stu-id="190d3-147">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="190d3-148">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span><span class="sxs-lookup"><span data-stu-id="190d3-148">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="190d3-149">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span><span class="sxs-lookup"><span data-stu-id="190d3-149">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="step-4---get-connection-information"></a><span data-ttu-id="190d3-150">Step 4 - Get connection information</span><span class="sxs-lookup"><span data-stu-id="190d3-150">Step 4 - Get connection information</span></span>

<span data-ttu-id="190d3-151">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="190d3-151">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span></span> <span data-ttu-id="190d3-152">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="190d3-152">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="190d3-153">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="190d3-153">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="190d3-154">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="190d3-154">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="190d3-155">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span><span class="sxs-lookup"><span data-stu-id="190d3-155">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span></span>

    ![connection information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connection-information.png) 

## <a name="step-5---connect-to-your-database-using-sql-server-management-studio"></a><span data-ttu-id="190d3-157">Step 5 - Connect to your database using SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="190d3-157">Step 5 - Connect to your database using SQL Server Management Studio</span></span>

<span data-ttu-id="190d3-158">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="190d3-158">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span></span>

1. <span data-ttu-id="190d3-159">Open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="190d3-159">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="190d3-160">In the **Connect to Server** dialog box, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="190d3-160">In the **Connect to Server** dialog box, enter the following information:</span></span>
   - <span data-ttu-id="190d3-161">**Server type**: Specify Database engine</span><span class="sxs-lookup"><span data-stu-id="190d3-161">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="190d3-162">**Server name**: Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="190d3-162">**Server name**: Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**</span></span>
   - <span data-ttu-id="190d3-163">**Authentication**: Specify SQL Server Authentication</span><span class="sxs-lookup"><span data-stu-id="190d3-163">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="190d3-164">**Login**: Enter your server admin account</span><span class="sxs-lookup"><span data-stu-id="190d3-164">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="190d3-165">**Password**: Enter the password for your server admin account</span><span class="sxs-lookup"><span data-stu-id="190d3-165">**Password**: Enter the password for your server admin account</span></span>


   <img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connect.png" alt="connect to server" style="width: 780px;" />

3. <span data-ttu-id="190d3-166">Click **Options** in the **Connect to server** dialog box.</span><span class="sxs-lookup"><span data-stu-id="190d3-166">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="190d3-167">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span><span class="sxs-lookup"><span data-stu-id="190d3-167">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![connect to db on server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="190d3-169">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="190d3-169">Click **Connect**.</span></span> <span data-ttu-id="190d3-170">The Object Explorer window opens in SSMS.</span><span class="sxs-lookup"><span data-stu-id="190d3-170">The Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="190d3-171">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span><span class="sxs-lookup"><span data-stu-id="190d3-171">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

   ![database objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connected.png)  

## <a name="step-6---create-tables-in-the-database"></a><span data-ttu-id="190d3-173">Step 6 - Create tables in the database</span><span class="sxs-lookup"><span data-stu-id="190d3-173">Step 6 - Create tables in the database</span></span> 

<span data-ttu-id="190d3-174">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span><span class="sxs-lookup"><span data-stu-id="190d3-174">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="190d3-175">Person</span><span class="sxs-lookup"><span data-stu-id="190d3-175">Person</span></span>
- <span data-ttu-id="190d3-176">Course</span><span class="sxs-lookup"><span data-stu-id="190d3-176">Course</span></span>
- <span data-ttu-id="190d3-177">Student</span><span class="sxs-lookup"><span data-stu-id="190d3-177">Student</span></span>
- <span data-ttu-id="190d3-178">Credit that model a student management system for universities</span><span class="sxs-lookup"><span data-stu-id="190d3-178">Credit that model a student management system for universities</span></span>

<span data-ttu-id="190d3-179">The following diagram shows how these tables are related to each other.</span><span class="sxs-lookup"><span data-stu-id="190d3-179">The following diagram shows how these tables are related to each other.</span></span> <span data-ttu-id="190d3-180">Some of these tables reference columns in other tables.</span><span class="sxs-lookup"><span data-stu-id="190d3-180">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="190d3-181">For example, the Student table references the **PersonId** column of the **Person** table.</span><span class="sxs-lookup"><span data-stu-id="190d3-181">For example, the Student table references the **PersonId** column of the **Person** table.</span></span> <span data-ttu-id="190d3-182">Study the diagram to understand how the tables in this tutorial are related to one another.</span><span class="sxs-lookup"><span data-stu-id="190d3-182">Study the diagram to understand how the tables in this tutorial are related to one another.</span></span> <span data-ttu-id="190d3-183">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span><span class="sxs-lookup"><span data-stu-id="190d3-183">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="190d3-184">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="190d3-184">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="190d3-185">You can also use the [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) to create and design your tables.</span><span class="sxs-lookup"><span data-stu-id="190d3-185">You can also use the [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) to create and design your tables.</span></span> 

![Table relationships](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="190d3-187">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="190d3-187">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="190d3-188">A blank query window opens that is connected to your database.</span><span class="sxs-lookup"><span data-stu-id="190d3-188">A blank query window opens that is connected to your database.</span></span>

2. <span data-ttu-id="190d3-189">In the query window, execute the following query to create four tables in your database:</span><span class="sxs-lookup"><span data-stu-id="190d3-189">In the query window, execute the following query to create four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

    CREATE TABLE Person
    (
      PersonId      INT IDENTITY PRIMARY KEY,
      FirstName     NVARCHAR(128) NOT NULL,
      MiddelInitial NVARCHAR(10),
      LastName      NVARCHAR(128) NOT NULL,
      DateOfBirth   DATE NOT NULL
    )
   
   -- Create Student table
 
    CREATE TABLE Student
    (
      StudentId INT IDENTITY PRIMARY KEY,
      PersonId  INT REFERENCES Person (PersonId),
      Email     NVARCHAR(256)
    )
    
   -- Create Course table
 
    CREATE TABLE Course
    (
      CourseId  INT IDENTITY PRIMARY KEY,
      Name      NVARCHAR(50) NOT NULL,
      Teacher   NVARCHAR(256) NOT NULL
    ) 

   -- Create Credit table
 
    CREATE TABLE Credit
    (
      StudentId   INT REFERENCES Student (StudentId),
      CourseId    INT REFERENCES Course (CourseId),
      Grade       DECIMAL(5,2) CHECK (Grade <= 100.00),
      Attempt     TINYINT,
      CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
      (
        StudentId, CourseId, Grade, Attempt
      )
    )
   ```

![Create tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="190d3-191">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span><span class="sxs-lookup"><span data-stu-id="190d3-191">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span></span>

   ![ssms tables-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="step-7---load-data-into-the-tables"></a><span data-ttu-id="190d3-193">Step 7 - Load data into the tables</span><span class="sxs-lookup"><span data-stu-id="190d3-193">Step 7 - Load data into the tables</span></span>

1. <span data-ttu-id="190d3-194">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span><span class="sxs-lookup"><span data-stu-id="190d3-194">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span></span> 

2. <span data-ttu-id="190d3-195">Right-click the following links and save them into the **SampleTableData** folder.</span><span class="sxs-lookup"><span data-stu-id="190d3-195">Right-click the following links and save them into the **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="190d3-196">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="190d3-196">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="190d3-197">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="190d3-197">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="190d3-198">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="190d3-198">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="190d3-199">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="190d3-199">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="190d3-200">Open a command prompt window and navigate to the SampleTableData folder.</span><span class="sxs-lookup"><span data-stu-id="190d3-200">Open a command prompt window and navigate to the SampleTableData folder.</span></span>

4. <span data-ttu-id="190d3-201">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span><span class="sxs-lookup"><span data-stu-id="190d3-201">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="190d3-202">You have now loaded sample data into the tables you created earlier.</span><span class="sxs-lookup"><span data-stu-id="190d3-202">You have now loaded sample data into the tables you created earlier.</span></span>

## <a name="step-8---query-the-tables"></a><span data-ttu-id="190d3-203">Step 8 - Query the tables</span><span class="sxs-lookup"><span data-stu-id="190d3-203">Step 8 - Query the tables</span></span>

<span data-ttu-id="190d3-204">Execute the following queries to retrieve information from the database tables.</span><span class="sxs-lookup"><span data-stu-id="190d3-204">Execute the following queries to retrieve information from the database tables.</span></span> <span data-ttu-id="190d3-205">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span><span class="sxs-lookup"><span data-stu-id="190d3-205">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span></span> <span data-ttu-id="190d3-206">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span><span class="sxs-lookup"><span data-stu-id="190d3-206">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="190d3-207">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span><span class="sxs-lookup"><span data-stu-id="190d3-207">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="190d3-208">In a SQL Server Management Studio query window, execute the following query:</span><span class="sxs-lookup"><span data-stu-id="190d3-208">In a SQL Server Management Studio query window, execute the following query:</span></span>

   ```sql 
   -- Find the students taught by Dominick Pope who have a grade higher than 75%

    SELECT  person.FirstName,
        person.LastName,
        course.Name,
        credit.Grade
    FROM  Person AS person
        INNER JOIN Student AS student ON person.PersonId = student.PersonId
        INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
        INNER JOIN Course AS course ON credit.CourseId = course.courseId
    WHERE course.Teacher = 'Dominick Pope' 
        AND Grade > 75
   ```

2. <span data-ttu-id="190d3-209">In a SQL Server Management Studio query window, execute following query:</span><span class="sxs-lookup"><span data-stu-id="190d3-209">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all the courses in which Noe Coleman has ever enrolled

    SELECT  course.Name,
        course.Teacher,
        credit.Grade
    FROM  Course AS course
        INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
        INNER JOIN Student AS student ON student.StudentId = credit.StudentId
        INNER JOIN Person AS person ON person.PersonId = student.PersonId
    WHERE person.FirstName = 'Noe'
        AND person.LastName = 'Coleman'
   ```

## <a name="step-9---restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="190d3-210">Step 9 - Restore a database to a previous point in time</span><span class="sxs-lookup"><span data-stu-id="190d3-210">Step 9 - Restore a database to a previous point in time</span></span> 

<span data-ttu-id="190d3-211">Imagine you have accidentally deleted a table.</span><span class="sxs-lookup"><span data-stu-id="190d3-211">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="190d3-212">This is something you cannot easily recover from.</span><span class="sxs-lookup"><span data-stu-id="190d3-212">This is something you cannot easily recover from.</span></span> <span data-ttu-id="190d3-213">Azure SQL Database allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new database.</span><span class="sxs-lookup"><span data-stu-id="190d3-213">Azure SQL Database allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new database.</span></span> <span data-ttu-id="190d3-214">You can you this database to recover your deleted data.</span><span class="sxs-lookup"><span data-stu-id="190d3-214">You can you this database to recover your deleted data.</span></span> <span data-ttu-id="190d3-215">The following steps restore the sample database to a point before the tables were added.</span><span class="sxs-lookup"><span data-stu-id="190d3-215">The following steps restore the sample database to a point before the tables were added.</span></span>

1. <span data-ttu-id="190d3-216">On the SQL Database page for your database, click **Restore** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="190d3-216">On the SQL Database page for your database, click **Restore** on the toolbar.</span></span> <span data-ttu-id="190d3-217">The **Restore** page opens.</span><span class="sxs-lookup"><span data-stu-id="190d3-217">The **Restore** page opens.</span></span>

   ![restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="190d3-219">Fill out the **Restore** form with the required information:</span><span class="sxs-lookup"><span data-stu-id="190d3-219">Fill out the **Restore** form with the required information:</span></span>
    * <span data-ttu-id="190d3-220">Database name: Provide a database name</span><span class="sxs-lookup"><span data-stu-id="190d3-220">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="190d3-221">Point-in-time: Select the **Point-in-time** tab on the Restore form</span><span class="sxs-lookup"><span data-stu-id="190d3-221">Point-in-time: Select the **Point-in-time** tab on the Restore form</span></span> 
    * <span data-ttu-id="190d3-222">Restore point: Select a time that occurs before the database was changed</span><span class="sxs-lookup"><span data-stu-id="190d3-222">Restore point: Select a time that occurs before the database was changed</span></span>
    * <span data-ttu-id="190d3-223">Target server: You cannot change this value when restoring a database</span><span class="sxs-lookup"><span data-stu-id="190d3-223">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="190d3-224">Elastic database pool: Select **None**</span><span class="sxs-lookup"><span data-stu-id="190d3-224">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="190d3-225">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span><span class="sxs-lookup"><span data-stu-id="190d3-225">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![restore-point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="190d3-227">Click **OK** to restore the database to [restore to a point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before the tables were added.</span><span class="sxs-lookup"><span data-stu-id="190d3-227">Click **OK** to restore the database to [restore to a point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before the tables were added.</span></span> <span data-ttu-id="190d3-228">Restoring a database to a different point in time creates a duplicate database in the same server as the original database as of the point in time you specify, provided that it is within the retention period for your [service tier](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="190d3-228">Restoring a database to a different point in time creates a duplicate database in the same server as the original database as of the point in time you specify, provided that it is within the retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="190d3-229">Next Steps</span><span class="sxs-lookup"><span data-stu-id="190d3-229">Next Steps</span></span> 

<span data-ttu-id="190d3-230">For PowerShell samples for common tasks, see [SQL Database PowerShell samples](sql-database-powershell-samples.md)</span><span class="sxs-lookup"><span data-stu-id="190d3-230">For PowerShell samples for common tasks, see [SQL Database PowerShell samples](sql-database-powershell-samples.md)</span></span>















