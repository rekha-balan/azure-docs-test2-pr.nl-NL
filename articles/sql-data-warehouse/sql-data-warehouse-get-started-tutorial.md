---
title: Azure SQL Data Warehouse - get started tutorial | Microsoft Docs
description: This tutorial teaches you how to provision and load data into Azure SQL Data Warehouse. You’ll also learn the basics about scaling, pausing, and tuning.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 53ea61c23d53101b159d78b9b8770d9936d8bdad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661183"
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="c897c-104">Get started with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c897c-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="c897c-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-105">This tutorial shows how to provision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c897c-106">You’ll also learn the basics about scaling, pausing, and tuning.</span><span class="sxs-lookup"><span data-stu-id="c897c-106">You’ll also learn the basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="c897c-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-107">When you’re finished, you’ll be ready to query and explore your data warehouse.</span></span>

<span data-ttu-id="c897c-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="c897c-108">**Estimated time to complete:** This is an end-to-end tutorial with example code that takes about 30 minutes to complete once you have met the prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c897c-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c897c-109">Prerequisites</span></span>

<span data-ttu-id="c897c-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span><span class="sxs-lookup"><span data-stu-id="c897c-110">The tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="c897c-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="c897c-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="c897c-112">Sign up for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c897c-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="c897c-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span><span class="sxs-lookup"><span data-stu-id="c897c-113">If you don't already have a Microsoft Azure account, you need to sign up for one to use this service.</span></span> <span data-ttu-id="c897c-114">If you already have an account, you may skip this step.</span><span class="sxs-lookup"><span data-stu-id="c897c-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="c897c-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="c897c-115">Navigate to the account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="c897c-116">Create a free Azure account, or purchase an account.</span><span class="sxs-lookup"><span data-stu-id="c897c-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="c897c-117">Follow the instructions</span><span class="sxs-lookup"><span data-stu-id="c897c-117">Follow the instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="c897c-118">Install appropriate SQL client drivers and tools</span><span class="sxs-lookup"><span data-stu-id="c897c-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="c897c-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="c897c-119">Most SQL client tools can connect to SQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="c897c-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-120">Due to the large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="c897c-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="c897c-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="c897c-122">Create a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c897c-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="c897c-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span><span class="sxs-lookup"><span data-stu-id="c897c-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="c897c-124">The database is distributed across multiple nodes and processes queries in parallel.</span><span class="sxs-lookup"><span data-stu-id="c897c-124">The database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="c897c-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span><span class="sxs-lookup"><span data-stu-id="c897c-125">SQL Data Warehouse has a control node that orchestrates the activities of all the nodes.</span></span> <span data-ttu-id="c897c-126">The nodes themselves use SQL Database to manage your data.</span><span class="sxs-lookup"><span data-stu-id="c897c-126">The nodes themselves use SQL Database to manage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="c897c-127">Creating a SQL Data Warehouse might result in a new billable service.</span><span class="sxs-lookup"><span data-stu-id="c897c-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="c897c-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="c897c-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="c897c-129">Create a data warehouse</span><span class="sxs-lookup"><span data-stu-id="c897c-129">Create a data warehouse</span></span>

1. <span data-ttu-id="c897c-130">Sign into the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c897c-130">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c897c-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="c897c-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="c897c-132">![NewBlade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="c897c-132">![NewBlade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="c897c-133">Fill out deployment details</span><span class="sxs-lookup"><span data-stu-id="c897c-133">Fill out deployment details</span></span>

    <span data-ttu-id="c897c-134">**Database Name**: Pick anything you'd like.</span><span class="sxs-lookup"><span data-stu-id="c897c-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="c897c-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="c897c-135">If you have multiple data warehouses, we recommend your names include details such as the region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="c897c-136">**Subscription**: Your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="c897c-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="c897c-137">**Resource Group**: Create a resource group or use an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="c897c-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="c897c-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span><span class="sxs-lookup"><span data-stu-id="c897c-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="c897c-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span><span class="sxs-lookup"><span data-stu-id="c897c-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="c897c-140">**Source**: Blank Database</span><span class="sxs-lookup"><span data-stu-id="c897c-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="c897c-141">**Server**: Select the server you created in [Prerequisites].</span><span class="sxs-lookup"><span data-stu-id="c897c-141">**Server**: Select the server you created in [Prerequisites].</span></span>

    <span data-ttu-id="c897c-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="c897c-142">**Collation**: Leave the default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="c897c-143">**Select performance**: We recommend starting with the standard 400DWU.</span><span class="sxs-lookup"><span data-stu-id="c897c-143">**Select performance**: We recommend starting with the standard 400DWU.</span></span>

4. <span data-ttu-id="c897c-144">Choose **Pin to dashboard** ![Pin To Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="c897c-144">Choose **Pin to dashboard** ![Pin To Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="c897c-145">Sit back and wait for your data warehouse to deploy!</span><span class="sxs-lookup"><span data-stu-id="c897c-145">Sit back and wait for your data warehouse to deploy!</span></span> <span data-ttu-id="c897c-146">It's normal for this process to take several minutes.</span><span class="sxs-lookup"><span data-stu-id="c897c-146">It's normal for this process to take several minutes.</span></span> <span data-ttu-id="c897c-147">The portal notifies you when your data warehouse is ready to use.</span><span class="sxs-lookup"><span data-stu-id="c897c-147">The portal notifies you when your data warehouse is ready to use.</span></span> 

## <a name="connect-to-sql-data-warehouse"></a><span data-ttu-id="c897c-148">Connect to SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c897c-148">Connect to SQL Data Warehouse</span></span>

<span data-ttu-id="c897c-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-149">This tutorial uses SQL Server Management Studio (SSMS) to connect to the data warehouse.</span></span> <span data-ttu-id="c897c-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span><span class="sxs-lookup"><span data-stu-id="c897c-150">You can connect to SQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="c897c-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c897c-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="c897c-152">Get connection information</span><span class="sxs-lookup"><span data-stu-id="c897c-152">Get connection information</span></span>

<span data-ttu-id="c897c-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span><span class="sxs-lookup"><span data-stu-id="c897c-153">To connect to your data warehouse, you need to connect through the logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="c897c-154">Select your data warehouse from the dashboard or search for it in your resources.</span><span class="sxs-lookup"><span data-stu-id="c897c-154">Select your data warehouse from the dashboard or search for it in your resources.</span></span>

    ![SQL Data Warehouse Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="c897c-156">Find the full name for the logical SQL server.</span><span class="sxs-lookup"><span data-stu-id="c897c-156">Find the full name for the logical SQL server.</span></span>

    ![Select Server Name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="c897c-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span><span class="sxs-lookup"><span data-stu-id="c897c-158">Open SSMS and use object explorer to connect to this server using the server admin credentials you created in [Prerequisites]</span></span>

    ![Connect with SSMS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="c897c-160">If all goes correctly, you should now be connected to your logical SQL server.</span><span class="sxs-lookup"><span data-stu-id="c897c-160">If all goes correctly, you should now be connected to your logical SQL server.</span></span> <span data-ttu-id="c897c-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span><span class="sxs-lookup"><span data-stu-id="c897c-161">Since you logged in as the server admin, you can connect to any database hosted by the server, including the master database.</span></span> 

<span data-ttu-id="c897c-162">There is only one server admin account and it has the most privileges of any user.</span><span class="sxs-lookup"><span data-stu-id="c897c-162">There is only one server admin account and it has the most privileges of any user.</span></span> <span data-ttu-id="c897c-163">Be careful not to allow too many people in your organization to know the admin password.</span><span class="sxs-lookup"><span data-stu-id="c897c-163">Be careful not to allow too many people in your organization to know the admin password.</span></span> 

<span data-ttu-id="c897c-164">You can also have an Azure active directory admin account.</span><span class="sxs-lookup"><span data-stu-id="c897c-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="c897c-165">We don't provide the details here.</span><span class="sxs-lookup"><span data-stu-id="c897c-165">We don't provide the details here.</span></span> <span data-ttu-id="c897c-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="c897c-166">If you want to learn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="c897c-167">Next, we explore creating additional logins and users.</span><span class="sxs-lookup"><span data-stu-id="c897c-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="c897c-168">Create a database user</span><span class="sxs-lookup"><span data-stu-id="c897c-168">Create a database user</span></span>

<span data-ttu-id="c897c-169">In this step, you create a user account to access your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-169">In this step, you create a user account to access your data warehouse.</span></span> <span data-ttu-id="c897c-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span><span class="sxs-lookup"><span data-stu-id="c897c-170">We also show you how to give that user the ability to run queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-to-queries"></a><span data-ttu-id="c897c-171">Notes about resource classes for allocating resources to queries</span><span class="sxs-lookup"><span data-stu-id="c897c-171">Notes about resource classes for allocating resources to queries</span></span>

- <span data-ttu-id="c897c-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span><span class="sxs-lookup"><span data-stu-id="c897c-172">To keep your data safe, don't use the server admin to run queries on your production databases.</span></span> <span data-ttu-id="c897c-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span><span class="sxs-lookup"><span data-stu-id="c897c-173">It has the most privileges of any user and using it to perform operations on user data puts your data at risk.</span></span> <span data-ttu-id="c897c-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span><span class="sxs-lookup"><span data-stu-id="c897c-174">Also, since the server admin is meant to perform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="c897c-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span><span class="sxs-lookup"><span data-stu-id="c897c-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, to allocate different amounts of memory, CPU resources, and concurrency slots to users.</span></span> <span data-ttu-id="c897c-176">Each user can belong to a small, medium, large, or extra-large resource class.</span><span class="sxs-lookup"><span data-stu-id="c897c-176">Each user can belong to a small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="c897c-177">The user's resource class determines the resources the user has to run queries and load operations.</span><span class="sxs-lookup"><span data-stu-id="c897c-177">The user's resource class determines the resources the user has to run queries and load operations.</span></span>

- <span data-ttu-id="c897c-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span><span class="sxs-lookup"><span data-stu-id="c897c-178">For optimal data compression, the user may need to load with large or extra large resource allocations.</span></span> <span data-ttu-id="c897c-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="c897c-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="c897c-180">Create an account that can control a database</span><span class="sxs-lookup"><span data-stu-id="c897c-180">Create an account that can control a database</span></span>

<span data-ttu-id="c897c-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span><span class="sxs-lookup"><span data-stu-id="c897c-181">Since you are currently logged in as the server admin you have permissions to create logins and users.</span></span>

1. <span data-ttu-id="c897c-182">Using SSMS or another query client, open a new query for **master**.</span><span class="sxs-lookup"><span data-stu-id="c897c-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![New Query on Master](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![New Query on Master1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="c897c-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="c897c-185">In the query window, run this T-SQL command to create a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="c897c-186">This login can connect to the logical SQL server.</span><span class="sxs-lookup"><span data-stu-id="c897c-186">This login can connect to the logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="c897c-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span><span class="sxs-lookup"><span data-stu-id="c897c-187">Now querying the *SQL Data Warehouse database*, create a database user based on the login you created to access and perform operations on the database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="c897c-188">Give the database user control permissions to the database called NYT.</span><span class="sxs-lookup"><span data-stu-id="c897c-188">Give the database user control permissions to the database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] to LoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="c897c-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span><span class="sxs-lookup"><span data-stu-id="c897c-189">If your database name has hyphens in it, be sure to wrap it in brackets!</span></span> 
    >

### <a name="give-the-user-medium-resource-allocations"></a><span data-ttu-id="c897c-190">Give the user medium resource allocations</span><span class="sxs-lookup"><span data-stu-id="c897c-190">Give the user medium resource allocations</span></span>

1. <span data-ttu-id="c897c-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span><span class="sxs-lookup"><span data-stu-id="c897c-191">Run this T-SQL command to make it a member of the medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="c897c-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span><span class="sxs-lookup"><span data-stu-id="c897c-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) to learn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="c897c-193">Connect to the logical server with the new credentials</span><span class="sxs-lookup"><span data-stu-id="c897c-193">Connect to the logical server with the new credentials</span></span>

    ![Log in With New Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="c897c-195">Load data from Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="c897c-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="c897c-196">You are now ready to load data into your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-196">You are now ready to load data into your data warehouse.</span></span> <span data-ttu-id="c897c-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span><span class="sxs-lookup"><span data-stu-id="c897c-197">This step shows you how to load New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="c897c-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-198">A common way to load data into SQL Data Warehouse is to first move the data to Azure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="c897c-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span><span class="sxs-lookup"><span data-stu-id="c897c-199">To make it easier to understand how to load, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="c897c-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="c897c-200">For future reference, to learn how to get your data to Azure blob storage or to load it directly from your source into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="c897c-201">Define external data</span><span class="sxs-lookup"><span data-stu-id="c897c-201">Define external data</span></span>

1. <span data-ttu-id="c897c-202">Create a master key.</span><span class="sxs-lookup"><span data-stu-id="c897c-202">Create a master key.</span></span> <span data-ttu-id="c897c-203">You only need to create a master key once per database.</span><span class="sxs-lookup"><span data-stu-id="c897c-203">You only need to create a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="c897c-204">Define the location of the Azure blob that contains the taxi cab data.</span><span class="sxs-lookup"><span data-stu-id="c897c-204">Define the location of the Azure blob that contains the taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="c897c-205">Define the external file formats</span><span class="sxs-lookup"><span data-stu-id="c897c-205">Define the external file formats</span></span>

    <span data-ttu-id="c897c-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span><span class="sxs-lookup"><span data-stu-id="c897c-206">The ```CREATE EXTERNAL FILE FORMAT``` command is used to specify the format of files that contain the external data.</span></span> <span data-ttu-id="c897c-207">They contain text separated by one or more characters called delimiters.</span><span class="sxs-lookup"><span data-stu-id="c897c-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="c897c-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span><span class="sxs-lookup"><span data-stu-id="c897c-208">For demonstration purposes, the taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="c897c-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span><span class="sxs-lookup"><span data-stu-id="c897c-209">Run these T-SQL commands to define two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="c897c-210">Create a schema for your external file format.</span><span class="sxs-lookup"><span data-stu-id="c897c-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="c897c-211">Create the external tables.</span><span class="sxs-lookup"><span data-stu-id="c897c-211">Create the external tables.</span></span> <span data-ttu-id="c897c-212">These tables reference data stored in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="c897c-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="c897c-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span><span class="sxs-lookup"><span data-stu-id="c897c-213">Run the following T-SQL commands to create several external tables that all point to the Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-the-data-from-azure-blob-storage"></a><span data-ttu-id="c897c-214">Import the data from Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="c897c-214">Import the data from Azure blob storage.</span></span>

<span data-ttu-id="c897c-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="c897c-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="c897c-216">This statement creates a new table based on the results of a select statement.</span><span class="sxs-lookup"><span data-stu-id="c897c-216">This statement creates a new table based on the results of a select statement.</span></span> <span data-ttu-id="c897c-217">The new table has the same columns and data types as the results of the select statement.</span><span class="sxs-lookup"><span data-stu-id="c897c-217">The new table has the same columns and data types as the results of the select statement.</span></span>  <span data-ttu-id="c897c-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-218">This is an elegant way to import data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="c897c-219">Run this script to import your data.</span><span class="sxs-lookup"><span data-stu-id="c897c-219">Run this script to import your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="c897c-220">View your data as it loads.</span><span class="sxs-lookup"><span data-stu-id="c897c-220">View your data as it loads.</span></span>

   <span data-ttu-id="c897c-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span><span class="sxs-lookup"><span data-stu-id="c897c-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="c897c-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span><span class="sxs-lookup"><span data-stu-id="c897c-222">Run the following query that uses a dynamic management views (DMVs) to show the status of the load.</span></span> <span data-ttu-id="c897c-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span><span class="sxs-lookup"><span data-stu-id="c897c-223">After starting the query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="c897c-224">View all system queries.</span><span class="sxs-lookup"><span data-stu-id="c897c-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="c897c-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![See Data Loaded](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="c897c-227">Improve query performance</span><span class="sxs-lookup"><span data-stu-id="c897c-227">Improve query performance</span></span>

<span data-ttu-id="c897c-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span><span class="sxs-lookup"><span data-stu-id="c897c-228">There are several ways to improve query performance and to achieve the high-speed performance that SQL Data Warehouse is designed to provide.</span></span>  

### <a name="see-the-effect-of-scaling-on-query-performance"></a><span data-ttu-id="c897c-229">See the effect of scaling on query performance</span><span class="sxs-lookup"><span data-stu-id="c897c-229">See the effect of scaling on query performance</span></span> 

<span data-ttu-id="c897c-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-230">One way to improve query performance is to scale resources by changing the DWU service level for your data warehouse.</span></span> <span data-ttu-id="c897c-231">Each service level costs more, but you can scale back or pause resources at any time.</span><span class="sxs-lookup"><span data-stu-id="c897c-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="c897c-232">In this step, you compare performance at two different DWU settings.</span><span class="sxs-lookup"><span data-stu-id="c897c-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="c897c-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span><span class="sxs-lookup"><span data-stu-id="c897c-233">First, let's scale the sizing down to 100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="c897c-234">Go to the portal and select your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-234">Go to the portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="c897c-235">Select scale in the SQL Data Warehouse blade.</span><span class="sxs-lookup"><span data-stu-id="c897c-235">Select scale in the SQL Data Warehouse blade.</span></span> 

    ![Scale DW From portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="c897c-237">Scale down the performance bar to 100 DWU and hit save.</span><span class="sxs-lookup"><span data-stu-id="c897c-237">Scale down the performance bar to 100 DWU and hit save.</span></span>

    ![Scale and save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="c897c-239">Wait for your scale operation to finish.</span><span class="sxs-lookup"><span data-stu-id="c897c-239">Wait for your scale operation to finish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c897c-240">Queries cannot run while changing the scale.</span><span class="sxs-lookup"><span data-stu-id="c897c-240">Queries cannot run while changing the scale.</span></span> <span data-ttu-id="c897c-241">Scaling **kills** your currently running queries.</span><span class="sxs-lookup"><span data-stu-id="c897c-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="c897c-242">You can restart them when the operation is finished.</span><span class="sxs-lookup"><span data-stu-id="c897c-242">You can restart them when the operation is finished.</span></span>
    >
    
5. <span data-ttu-id="c897c-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span><span class="sxs-lookup"><span data-stu-id="c897c-243">Do a scan operation on the trip data, selecting the top million entries for all the columns.</span></span> <span data-ttu-id="c897c-244">If you're eager to move on quickly, feel free to select fewer rows.</span><span class="sxs-lookup"><span data-stu-id="c897c-244">If you're eager to move on quickly, feel free to select fewer rows.</span></span> <span data-ttu-id="c897c-245">Take note of the time it takes to run this operation.</span><span class="sxs-lookup"><span data-stu-id="c897c-245">Take note of the time it takes to run this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="c897c-246">Scale your data warehouse back to 400 DWU.</span><span class="sxs-lookup"><span data-stu-id="c897c-246">Scale your data warehouse back to 400 DWU.</span></span> <span data-ttu-id="c897c-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-247">Remember, each 100 DWU is adding another compute node to your Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="c897c-248">Run the query again!</span><span class="sxs-lookup"><span data-stu-id="c897c-248">Run the query again!</span></span> <span data-ttu-id="c897c-249">You should notice a significant difference.</span><span class="sxs-lookup"><span data-stu-id="c897c-249">You should notice a significant difference.</span></span> 

> [!NOTE]
> <span data-ttu-id="c897c-250">Since SQL Data Warehouse uses massively parallel processing.</span><span class="sxs-lookup"><span data-stu-id="c897c-250">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="c897c-251">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c897c-251">Queries that scan or perform analytic functions on millions of rows experience the true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-the-effect-of-statistics-on-query-performance"></a><span data-ttu-id="c897c-252">See the effect of statistics on query performance</span><span class="sxs-lookup"><span data-stu-id="c897c-252">See the effect of statistics on query performance</span></span>

1. <span data-ttu-id="c897c-253">Run a query that joins the Date table with the Trip table</span><span class="sxs-lookup"><span data-stu-id="c897c-253">Run a query that joins the Date table with the Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="c897c-254">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span><span class="sxs-lookup"><span data-stu-id="c897c-254">This query takes a while because SQL Data Warehouse has to shuffle data before it can perform the join.</span></span> <span data-ttu-id="c897c-255">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span><span class="sxs-lookup"><span data-stu-id="c897c-255">Joins do not have to shuffle data if they are designed to join data in the same way it is distributed.</span></span> <span data-ttu-id="c897c-256">That's a deeper subject.</span><span class="sxs-lookup"><span data-stu-id="c897c-256">That's a deeper subject.</span></span> 

2. <span data-ttu-id="c897c-257">Statistics make a difference.</span><span class="sxs-lookup"><span data-stu-id="c897c-257">Statistics make a difference.</span></span> 
3. <span data-ttu-id="c897c-258">Run this statement to create statistics on the join columns.</span><span class="sxs-lookup"><span data-stu-id="c897c-258">Run this statement to create statistics on the join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="c897c-259">SQL DW does not automatically manage statistics for you.</span><span class="sxs-lookup"><span data-stu-id="c897c-259">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="c897c-260">Statistics are important for query performance and it is highly recommended you create and update statistics.</span><span class="sxs-lookup"><span data-stu-id="c897c-260">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="c897c-261">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="c897c-261">**You gain the most benefit by having statistics on columns involved in joins, columns used in the WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="c897c-262">Run the query from Prerequisites again and observe any performance differences.</span><span class="sxs-lookup"><span data-stu-id="c897c-262">Run the query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="c897c-263">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span><span class="sxs-lookup"><span data-stu-id="c897c-263">While the differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c897c-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="c897c-264">Next steps</span></span>

<span data-ttu-id="c897c-265">You're now ready to query and explore.</span><span class="sxs-lookup"><span data-stu-id="c897c-265">You're now ready to query and explore.</span></span> <span data-ttu-id="c897c-266">Check out our best practices or tips.</span><span class="sxs-lookup"><span data-stu-id="c897c-266">Check out our best practices or tips.</span></span>

<span data-ttu-id="c897c-267">If you're done exploring for the day, make sure to pause your instance!</span><span class="sxs-lookup"><span data-stu-id="c897c-267">If you're done exploring for the day, make sure to pause your instance!</span></span> <span data-ttu-id="c897c-268">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span><span class="sxs-lookup"><span data-stu-id="c897c-268">In production, you can experience enormous savings by pausing and scaling to meet your business needs.</span></span>

![Pause](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="c897c-270">Useful readings</span><span class="sxs-lookup"><span data-stu-id="c897c-270">Useful readings</span></span>

<span data-ttu-id="c897c-271">[Concurrency and Workload Management][]</span><span class="sxs-lookup"><span data-stu-id="c897c-271">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="c897c-272">[Best practices for Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="c897c-272">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="c897c-273">[Query Monitoring][]</span><span class="sxs-lookup"><span data-stu-id="c897c-273">[Query Monitoring][]</span></span>

<span data-ttu-id="c897c-274">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="c897c-274">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="c897c-275">[Migrating Data to Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="c897c-275">[Migrating Data to Azure SQL Data Warehouse][]</span></span>

[Concurrency and Workload Management]: sql-data-warehouse-develop-concurrency.md#change-a-user-resource-class-example
[Best practices for Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Query Monitoring]: sql-data-warehouse-manage-monitor.md
[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[Migrating Data to Azure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[Prerequisites]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx













