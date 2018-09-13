---
title: 'Tutorial: Design your first Azure SQL database using SSMS | Microsoft Docs'
description: Learn to design your first Azure SQL database with SQL Server Management Studio.
services: sql-database
author: CarlRabeler
manager: craigg
ms.service: sql-database
ms.custom: mvc,develop databases
ms.topic: tutorial
ms.date: 07/16/2018
ms.author: carlrab
ms.openlocfilehash: ed2d4654163881b3258c4a98632d48acd0e80fb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808345"
---
# <a name="tutorial-design-your-first-azure-sql-database-using-ssms"></a><span data-ttu-id="a6253-103">Tutorial: Design your first Azure SQL database using SSMS</span><span class="sxs-lookup"><span data-stu-id="a6253-103">Tutorial: Design your first Azure SQL database using SSMS</span></span>

<span data-ttu-id="a6253-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud (Azure).</span><span class="sxs-lookup"><span data-stu-id="a6253-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud (Azure).</span></span> <span data-ttu-id="a6253-105">In this tutorial, you learn how to use the Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span><span class="sxs-lookup"><span data-stu-id="a6253-105">In this tutorial, you learn how to use the Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a6253-106">Create a database in the Azure portal\*</span><span class="sxs-lookup"><span data-stu-id="a6253-106">Create a database in the Azure portal\*</span></span>
> * <span data-ttu-id="a6253-107">Set up a server-level firewall rule in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a6253-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="a6253-108">Connect to the database with SSMS</span><span class="sxs-lookup"><span data-stu-id="a6253-108">Connect to the database with SSMS</span></span>
> * <span data-ttu-id="a6253-109">Create tables with SSMS</span><span class="sxs-lookup"><span data-stu-id="a6253-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="a6253-110">Bulk load data with BCP</span><span class="sxs-lookup"><span data-stu-id="a6253-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="a6253-111">Query that data with SSMS</span><span class="sxs-lookup"><span data-stu-id="a6253-111">Query that data with SSMS</span></span>

<span data-ttu-id="a6253-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a6253-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

   >[!NOTE]
   > <span data-ttu-id="a6253-113">For the purpose of this tutorial, we are using the [DTU-based purchasing model](sql-database-service-tiers-dtu.md), but you do have the option of choosing the [vCore-based purchasing model](sql-database-service-tiers-vcore.md).</span><span class="sxs-lookup"><span data-stu-id="a6253-113">For the purpose of this tutorial, we are using the [DTU-based purchasing model](sql-database-service-tiers-dtu.md), but you do have the option of choosing the [vCore-based purchasing model](sql-database-service-tiers-vcore.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a6253-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a6253-114">Prerequisites</span></span>

<span data-ttu-id="a6253-115">To complete this tutorial, make sure you have installed:</span><span class="sxs-lookup"><span data-stu-id="a6253-115">To complete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="a6253-116">The newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="a6253-116">The newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="a6253-117">The newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="a6253-117">The newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="a6253-118">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a6253-118">Log in to the Azure portal</span></span>

<span data-ttu-id="a6253-119">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6253-119">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="a6253-120">Create a blank SQL database</span><span class="sxs-lookup"><span data-stu-id="a6253-120">Create a blank SQL database</span></span>

<span data-ttu-id="a6253-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="a6253-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers-dtu.md).</span></span> <span data-ttu-id="a6253-122">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="a6253-122">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="a6253-123">Follow these steps to create a blank SQL database.</span><span class="sxs-lookup"><span data-stu-id="a6253-123">Follow these steps to create a blank SQL database.</span></span> 

1. <span data-ttu-id="a6253-124">Click **Create a resource** in the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a6253-124">Click **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="a6253-125">On the **New** page, select **Databases** in the Azure Marketplace section, and then click **SQL Database** in the **Featured** section.</span><span class="sxs-lookup"><span data-stu-id="a6253-125">On the **New** page, select **Databases** in the Azure Marketplace section, and then click **SQL Database** in the **Featured** section.</span></span>

   ![create empty-database](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="a6253-127">Fill out the SQL Database form with the following information, as shown on the preceding image:</span><span class="sxs-lookup"><span data-stu-id="a6253-127">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="a6253-128">Setting</span><span class="sxs-lookup"><span data-stu-id="a6253-128">Setting</span></span>       | <span data-ttu-id="a6253-129">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a6253-129">Suggested value</span></span> | <span data-ttu-id="a6253-130">Description</span><span class="sxs-lookup"><span data-stu-id="a6253-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="a6253-131">**Database name**</span><span class="sxs-lookup"><span data-stu-id="a6253-131">**Database name**</span></span> | <span data-ttu-id="a6253-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="a6253-132">mySampleDatabase</span></span> | <span data-ttu-id="a6253-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="a6253-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="a6253-134">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="a6253-134">**Subscription**</span></span> | <span data-ttu-id="a6253-135">Your subscription</span><span class="sxs-lookup"><span data-stu-id="a6253-135">Your subscription</span></span>  | <span data-ttu-id="a6253-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="a6253-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="a6253-137">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="a6253-137">**Resource group**</span></span> | <span data-ttu-id="a6253-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a6253-138">myResourceGroup</span></span> | <span data-ttu-id="a6253-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="a6253-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="a6253-140">**Select source**</span><span class="sxs-lookup"><span data-stu-id="a6253-140">**Select source**</span></span> | <span data-ttu-id="a6253-141">Blank database</span><span class="sxs-lookup"><span data-stu-id="a6253-141">Blank database</span></span> | <span data-ttu-id="a6253-142">Specifies that a blank database should be created.</span><span class="sxs-lookup"><span data-stu-id="a6253-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="a6253-143">Click **Server** to create and configure a new server for your new database.</span><span class="sxs-lookup"><span data-stu-id="a6253-143">Click **Server** to create and configure a new server for your new database.</span></span> <span data-ttu-id="a6253-144">Fill out the **New server form** with the following information:</span><span class="sxs-lookup"><span data-stu-id="a6253-144">Fill out the **New server form** with the following information:</span></span> 

   | <span data-ttu-id="a6253-145">Setting</span><span class="sxs-lookup"><span data-stu-id="a6253-145">Setting</span></span>       | <span data-ttu-id="a6253-146">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a6253-146">Suggested value</span></span> | <span data-ttu-id="a6253-147">Description</span><span class="sxs-lookup"><span data-stu-id="a6253-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="a6253-148">**Server name**</span><span class="sxs-lookup"><span data-stu-id="a6253-148">**Server name**</span></span> | <span data-ttu-id="a6253-149">Any globally unique name</span><span class="sxs-lookup"><span data-stu-id="a6253-149">Any globally unique name</span></span> | <span data-ttu-id="a6253-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="a6253-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="a6253-151">**Server admin login**</span><span class="sxs-lookup"><span data-stu-id="a6253-151">**Server admin login**</span></span> | <span data-ttu-id="a6253-152">Any valid name</span><span class="sxs-lookup"><span data-stu-id="a6253-152">Any valid name</span></span> | <span data-ttu-id="a6253-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="a6253-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="a6253-154">**Password**</span><span class="sxs-lookup"><span data-stu-id="a6253-154">**Password**</span></span> | <span data-ttu-id="a6253-155">Any valid password</span><span class="sxs-lookup"><span data-stu-id="a6253-155">Any valid password</span></span> | <span data-ttu-id="a6253-156">Your password must have at least eight characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="a6253-156">Your password must have at least eight characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="a6253-157">**Location**</span><span class="sxs-lookup"><span data-stu-id="a6253-157">**Location**</span></span> | <span data-ttu-id="a6253-158">Any valid location</span><span class="sxs-lookup"><span data-stu-id="a6253-158">Any valid location</span></span> | <span data-ttu-id="a6253-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="a6253-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![create database-server](./media/sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="a6253-161">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="a6253-161">Click **Select**.</span></span>

6. <span data-ttu-id="a6253-162">Click **Pricing tier** to specify the service tier, the number of DTUs or vCores, and the amount of storage.</span><span class="sxs-lookup"><span data-stu-id="a6253-162">Click **Pricing tier** to specify the service tier, the number of DTUs or vCores, and the amount of storage.</span></span> <span data-ttu-id="a6253-163">Explore the options for the number of DTUs/vCores and storage that is available to you for each service tier.</span><span class="sxs-lookup"><span data-stu-id="a6253-163">Explore the options for the number of DTUs/vCores and storage that is available to you for each service tier.</span></span> <span data-ttu-id="a6253-164">For the purpose of this tutorial, we are using the [DTU-based purchasing model](sql-database-service-tiers-dtu.md), but you do have the option of choosing the [vCore-based purchasing model](sql-database-service-tiers-vcore.md).</span><span class="sxs-lookup"><span data-stu-id="a6253-164">For the purpose of this tutorial, we are using the [DTU-based purchasing model](sql-database-service-tiers-dtu.md), but you do have the option of choosing the [vCore-based purchasing model](sql-database-service-tiers-vcore.md).</span></span> 

7. <span data-ttu-id="a6253-165">For this tutorial, select the **Standard** service tier and then use the slider to select **100 DTUs (S3)** and **400** GB of storage.</span><span class="sxs-lookup"><span data-stu-id="a6253-165">For this tutorial, select the **Standard** service tier and then use the slider to select **100 DTUs (S3)** and **400** GB of storage.</span></span>

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

8. <span data-ttu-id="a6253-167">Accept the preview terms to use the **Add-on Storage** option.</span><span class="sxs-lookup"><span data-stu-id="a6253-167">Accept the preview terms to use the **Add-on Storage** option.</span></span> 

   > [!IMPORTANT]
   > <span data-ttu-id="a6253-168">More than 1 TB of storage in the Premium tier is currently available in all regions except the following: UK North, West Central US, UK South2, China East, USDoDCentral, Germany Central, USDoDEast, US Gov Southwest, US Gov South Central, Germany Northeast,  China North, US Gov East.</span><span class="sxs-lookup"><span data-stu-id="a6253-168">More than 1 TB of storage in the Premium tier is currently available in all regions except the following: UK North, West Central US, UK South2, China East, USDoDCentral, Germany Central, USDoDEast, US Gov Southwest, US Gov South Central, Germany Northeast,  China North, US Gov East.</span></span> <span data-ttu-id="a6253-169">In other regions, the storage max in the Premium tier is limited to 1 TB.</span><span class="sxs-lookup"><span data-stu-id="a6253-169">In other regions, the storage max in the Premium tier is limited to 1 TB.</span></span> <span data-ttu-id="a6253-170">See [P11-P15 Current Limitations]( sql-database-dtu-resource-limits-single-databases.md#single-database-limitations-of-p11-and-p15-when-the-maximum-size-greater-than-1-tb).</span><span class="sxs-lookup"><span data-stu-id="a6253-170">See [P11-P15 Current Limitations]( sql-database-dtu-resource-limits-single-databases.md#single-database-limitations-of-p11-and-p15-when-the-maximum-size-greater-than-1-tb).</span></span>

9. <span data-ttu-id="a6253-171">After selecting the server tier, the number of DTUs, and the amount of storage, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="a6253-171">After selecting the server tier, the number of DTUs, and the amount of storage, click **Apply**.</span></span>  

10. <span data-ttu-id="a6253-172">Select a **collation** for the blank database (for this tutorial, use the default value).</span><span class="sxs-lookup"><span data-stu-id="a6253-172">Select a **collation** for the blank database (for this tutorial, use the default value).</span></span> <span data-ttu-id="a6253-173">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span><span class="sxs-lookup"><span data-stu-id="a6253-173">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

11. <span data-ttu-id="a6253-174">Now that you have completed the SQL Database form, click **Create** to provision the database.</span><span class="sxs-lookup"><span data-stu-id="a6253-174">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="a6253-175">Provisioning takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="a6253-175">Provisioning takes a few minutes.</span></span> 

12. <span data-ttu-id="a6253-176">On the toolbar, click **Notifications** to monitor the deployment process.</span><span class="sxs-lookup"><span data-stu-id="a6253-176">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>
    
     ![notification](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="a6253-178">Create a server-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="a6253-178">Create a server-level firewall rule</span></span>

<span data-ttu-id="a6253-179">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a6253-179">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="a6253-180">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span><span class="sxs-lookup"><span data-stu-id="a6253-180">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="a6253-181">SQL Database communicates over port 1433.</span><span class="sxs-lookup"><span data-stu-id="a6253-181">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="a6253-182">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span><span class="sxs-lookup"><span data-stu-id="a6253-182">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="a6253-183">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span><span class="sxs-lookup"><span data-stu-id="a6253-183">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="a6253-184">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="a6253-184">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="a6253-185">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170824.database.windows.net**) and provides options for further configuration.</span><span class="sxs-lookup"><span data-stu-id="a6253-185">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170824.database.windows.net**) and provides options for further configuration.</span></span> 

2. <span data-ttu-id="a6253-186">Copy this fully qualified server name for use to connect to your server and its databases in subsequent tutorials and quickstarts.</span><span class="sxs-lookup"><span data-stu-id="a6253-186">Copy this fully qualified server name for use to connect to your server and its databases in subsequent tutorials and quickstarts.</span></span> 

   ![server name](./media/sql-database-get-started-portal/server-name.png) 

3. <span data-ttu-id="a6253-188">Click **Set server firewall** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="a6253-188">Click **Set server firewall** on the toolbar.</span></span> <span data-ttu-id="a6253-189">The **Firewall settings** page for the SQL Database server opens.</span><span class="sxs-lookup"><span data-stu-id="a6253-189">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![server firewall rule](./media/sql-database-get-started-portal/server-firewall-rule.png) 

4. <span data-ttu-id="a6253-191">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span><span class="sxs-lookup"><span data-stu-id="a6253-191">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="a6253-192">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a6253-192">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

5. <span data-ttu-id="a6253-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6253-193">Click **Save**.</span></span> <span data-ttu-id="a6253-194">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span><span class="sxs-lookup"><span data-stu-id="a6253-194">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

6. <span data-ttu-id="a6253-195">Click **OK** and then close the **Firewall settings** page.</span><span class="sxs-lookup"><span data-stu-id="a6253-195">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="a6253-196">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span><span class="sxs-lookup"><span data-stu-id="a6253-196">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6253-197">By default, access through the SQL Database firewall is enabled for all Azure services.</span><span class="sxs-lookup"><span data-stu-id="a6253-197">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="a6253-198">Click **OFF** on this page to disable for all Azure services.</span><span class="sxs-lookup"><span data-stu-id="a6253-198">Click **OFF** on this page to disable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="a6253-199">SQL server connection information</span><span class="sxs-lookup"><span data-stu-id="a6253-199">SQL server connection information</span></span>

<span data-ttu-id="a6253-200">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a6253-200">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span></span> <span data-ttu-id="a6253-201">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="a6253-201">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="a6253-202">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6253-202">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a6253-203">Select **SQL Databases** from the left-hand menu and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="a6253-203">Select **SQL Databases** from the left-hand menu and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="a6253-204">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span><span class="sxs-lookup"><span data-stu-id="a6253-204">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span></span>

   ![connection information](./media/sql-database-get-started-portal/server-name.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="a6253-206">Connect to the database with SSMS</span><span class="sxs-lookup"><span data-stu-id="a6253-206">Connect to the database with SSMS</span></span>

<span data-ttu-id="a6253-207">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="a6253-207">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span></span>

1. <span data-ttu-id="a6253-208">Open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="a6253-208">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="a6253-209">In the **Connect to Server** dialog box, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="a6253-209">In the **Connect to Server** dialog box, enter the following information:</span></span>

   | <span data-ttu-id="a6253-210">Setting</span><span class="sxs-lookup"><span data-stu-id="a6253-210">Setting</span></span>       | <span data-ttu-id="a6253-211">Suggested value</span><span class="sxs-lookup"><span data-stu-id="a6253-211">Suggested value</span></span> | <span data-ttu-id="a6253-212">Description</span><span class="sxs-lookup"><span data-stu-id="a6253-212">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="a6253-213">Server type</span><span class="sxs-lookup"><span data-stu-id="a6253-213">Server type</span></span> | <span data-ttu-id="a6253-214">Database engine</span><span class="sxs-lookup"><span data-stu-id="a6253-214">Database engine</span></span> | <span data-ttu-id="a6253-215">This value is required</span><span class="sxs-lookup"><span data-stu-id="a6253-215">This value is required</span></span> |
   | <span data-ttu-id="a6253-216">Server name</span><span class="sxs-lookup"><span data-stu-id="a6253-216">Server name</span></span> | <span data-ttu-id="a6253-217">The fully qualified server name</span><span class="sxs-lookup"><span data-stu-id="a6253-217">The fully qualified server name</span></span> | <span data-ttu-id="a6253-218">The name should be something like this: **mynewserver20170824.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="a6253-218">The name should be something like this: **mynewserver20170824.database.windows.net**.</span></span> |
   | <span data-ttu-id="a6253-219">Authentication</span><span class="sxs-lookup"><span data-stu-id="a6253-219">Authentication</span></span> | <span data-ttu-id="a6253-220">SQL Server Authentication</span><span class="sxs-lookup"><span data-stu-id="a6253-220">SQL Server Authentication</span></span> | <span data-ttu-id="a6253-221">SQL Authentication is the only authentication type that we have configured in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a6253-221">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="a6253-222">Login</span><span class="sxs-lookup"><span data-stu-id="a6253-222">Login</span></span> | <span data-ttu-id="a6253-223">The server admin account</span><span class="sxs-lookup"><span data-stu-id="a6253-223">The server admin account</span></span> | <span data-ttu-id="a6253-224">This is the account that you specified when you created the server.</span><span class="sxs-lookup"><span data-stu-id="a6253-224">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="a6253-225">Password</span><span class="sxs-lookup"><span data-stu-id="a6253-225">Password</span></span> | <span data-ttu-id="a6253-226">The password for your server admin account</span><span class="sxs-lookup"><span data-stu-id="a6253-226">The password for your server admin account</span></span> | <span data-ttu-id="a6253-227">This is the password that you specified when you created the server.</span><span class="sxs-lookup"><span data-stu-id="a6253-227">This is the password that you specified when you created the server.</span></span> |

   ![connect to server](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="a6253-229">Click **Options** in the **Connect to server** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a6253-229">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="a6253-230">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span><span class="sxs-lookup"><span data-stu-id="a6253-230">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![connect to db on server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="a6253-232">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a6253-232">Click **Connect**.</span></span> <span data-ttu-id="a6253-233">The Object Explorer window opens in SSMS.</span><span class="sxs-lookup"><span data-stu-id="a6253-233">The Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="a6253-234">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span><span class="sxs-lookup"><span data-stu-id="a6253-234">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

   ![database objects](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-the-database"></a><span data-ttu-id="a6253-236">Create tables in the database</span><span class="sxs-lookup"><span data-stu-id="a6253-236">Create tables in the database</span></span> 

<span data-ttu-id="a6253-237">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span><span class="sxs-lookup"><span data-stu-id="a6253-237">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="a6253-238">Person</span><span class="sxs-lookup"><span data-stu-id="a6253-238">Person</span></span>
- <span data-ttu-id="a6253-239">Course</span><span class="sxs-lookup"><span data-stu-id="a6253-239">Course</span></span>
- <span data-ttu-id="a6253-240">Student</span><span class="sxs-lookup"><span data-stu-id="a6253-240">Student</span></span>
- <span data-ttu-id="a6253-241">Credit that model a student management system for universities</span><span class="sxs-lookup"><span data-stu-id="a6253-241">Credit that model a student management system for universities</span></span>

<span data-ttu-id="a6253-242">The following diagram shows how these tables are related to each other.</span><span class="sxs-lookup"><span data-stu-id="a6253-242">The following diagram shows how these tables are related to each other.</span></span> <span data-ttu-id="a6253-243">Some of these tables reference columns in other tables.</span><span class="sxs-lookup"><span data-stu-id="a6253-243">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="a6253-244">For example, the Student table references the **PersonId** column of the **Person** table.</span><span class="sxs-lookup"><span data-stu-id="a6253-244">For example, the Student table references the **PersonId** column of the **Person** table.</span></span> <span data-ttu-id="a6253-245">Study the diagram to understand how the tables in this tutorial are related to one another.</span><span class="sxs-lookup"><span data-stu-id="a6253-245">Study the diagram to understand how the tables in this tutorial are related to one another.</span></span> <span data-ttu-id="a6253-246">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6253-246">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="a6253-247">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="a6253-247">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="a6253-248">You can also use the [table designer in SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/visual-db-tools/design-database-diagrams-visual-database-tools) to create and design your tables.</span><span class="sxs-lookup"><span data-stu-id="a6253-248">You can also use the [table designer in SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/visual-db-tools/design-database-diagrams-visual-database-tools) to create and design your tables.</span></span> 

![Table relationships](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="a6253-250">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="a6253-250">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="a6253-251">A blank query window opens that is connected to your database.</span><span class="sxs-lookup"><span data-stu-id="a6253-251">A blank query window opens that is connected to your database.</span></span>

2. <span data-ttu-id="a6253-252">In the query window, execute the following query to create four tables in your database:</span><span class="sxs-lookup"><span data-stu-id="a6253-252">In the query window, execute the following query to create four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Create tables](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="a6253-254">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span><span class="sxs-lookup"><span data-stu-id="a6253-254">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span></span>

   ![ssms tables-created](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-the-tables"></a><span data-ttu-id="a6253-256">Load data into the tables</span><span class="sxs-lookup"><span data-stu-id="a6253-256">Load data into the tables</span></span>

1. <span data-ttu-id="a6253-257">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span><span class="sxs-lookup"><span data-stu-id="a6253-257">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span></span> 

2. <span data-ttu-id="a6253-258">Right-click the following links and save them into the **SampleTableData** folder.</span><span class="sxs-lookup"><span data-stu-id="a6253-258">Right-click the following links and save them into the **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="a6253-259">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="a6253-259">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="a6253-260">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="a6253-260">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="a6253-261">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="a6253-261">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="a6253-262">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="a6253-262">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="a6253-263">Open a command prompt window and navigate to the SampleTableData folder.</span><span class="sxs-lookup"><span data-stu-id="a6253-263">Open a command prompt window and navigate to the SampleTableData folder.</span></span>

4. <span data-ttu-id="a6253-264">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span><span class="sxs-lookup"><span data-stu-id="a6253-264">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="a6253-265">You have now loaded sample data into the tables you created earlier.</span><span class="sxs-lookup"><span data-stu-id="a6253-265">You have now loaded sample data into the tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="a6253-266">Query data</span><span class="sxs-lookup"><span data-stu-id="a6253-266">Query data</span></span>

<span data-ttu-id="a6253-267">Execute the following queries to retrieve information from the database tables.</span><span class="sxs-lookup"><span data-stu-id="a6253-267">Execute the following queries to retrieve information from the database tables.</span></span> <span data-ttu-id="a6253-268">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span><span class="sxs-lookup"><span data-stu-id="a6253-268">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span></span> <span data-ttu-id="a6253-269">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span><span class="sxs-lookup"><span data-stu-id="a6253-269">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="a6253-270">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span><span class="sxs-lookup"><span data-stu-id="a6253-270">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="a6253-271">In a SQL Server Management Studio query window, execute the following query:</span><span class="sxs-lookup"><span data-stu-id="a6253-271">In a SQL Server Management Studio query window, execute the following query:</span></span>

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

2. <span data-ttu-id="a6253-272">In a SQL Server Management Studio query window, execute following query:</span><span class="sxs-lookup"><span data-stu-id="a6253-272">In a SQL Server Management Studio query window, execute following query:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a6253-273">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6253-273">Next steps</span></span> 
<span data-ttu-id="a6253-274">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span><span class="sxs-lookup"><span data-stu-id="a6253-274">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="a6253-275">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="a6253-275">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a6253-276">Create a database</span><span class="sxs-lookup"><span data-stu-id="a6253-276">Create a database</span></span>
> * <span data-ttu-id="a6253-277">Set up a firewall rule</span><span class="sxs-lookup"><span data-stu-id="a6253-277">Set up a firewall rule</span></span>
> * <span data-ttu-id="a6253-278">Connect to the database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span><span class="sxs-lookup"><span data-stu-id="a6253-278">Connect to the database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="a6253-279">Create tables</span><span class="sxs-lookup"><span data-stu-id="a6253-279">Create tables</span></span>
> * <span data-ttu-id="a6253-280">Bulk load data</span><span class="sxs-lookup"><span data-stu-id="a6253-280">Bulk load data</span></span>
> * <span data-ttu-id="a6253-281">Query that data</span><span class="sxs-lookup"><span data-stu-id="a6253-281">Query that data</span></span>

<span data-ttu-id="a6253-282">Advance to the next tutorial to learn about designing a database using Visual Studio and C#.</span><span class="sxs-lookup"><span data-stu-id="a6253-282">Advance to the next tutorial to learn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="a6253-283">Design an Azure SQL database and connect with C# and ADO.NET</span><span class="sxs-lookup"><span data-stu-id="a6253-283">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
