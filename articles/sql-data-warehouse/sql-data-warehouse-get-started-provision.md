---
title: Create a SQL Data Warehouse in the Azure portal | Microsoft Docs
description: Learn how to create an Azure SQL Data Warehouse in the Azure portal
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 67933cfec879ac3b23c88107fc29f55812e946d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550193"
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="6a24e-103">Create an Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6a24e-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="6a24e-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span><span class="sxs-lookup"><span data-stu-id="6a24e-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a24e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a24e-108">Prerequisites</span></span>
<span data-ttu-id="6a24e-109">To get started, you need:</span><span class="sxs-lookup"><span data-stu-id="6a24e-109">To get started, you need:</span></span>

* <span data-ttu-id="6a24e-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span><span class="sxs-lookup"><span data-stu-id="6a24e-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="6a24e-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span><span class="sxs-lookup"><span data-stu-id="6a24e-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> Creating a SQL Data Warehouse might result in a new billable service.  See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="6a24e-114">Create a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="6a24e-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="6a24e-115">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a24e-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6a24e-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="6a24e-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="6a24e-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span><span class="sxs-lookup"><span data-stu-id="6a24e-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![Create database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="6a24e-120">**Server**: We recommend you select your server first.</span><span class="sxs-lookup"><span data-stu-id="6a24e-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="6a24e-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a24e-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="6a24e-122">It must be unique to the server.</span><span class="sxs-lookup"><span data-stu-id="6a24e-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="6a24e-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span><span class="sxs-lookup"><span data-stu-id="6a24e-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="6a24e-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span><span class="sxs-lookup"><span data-stu-id="6a24e-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="6a24e-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="6a24e-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="6a24e-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span><span class="sxs-lookup"><span data-stu-id="6a24e-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="6a24e-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span><span class="sxs-lookup"><span data-stu-id="6a24e-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="6a24e-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a24e-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="6a24e-129">**Select source**: Click **Select source** > **Sample**.</span><span class="sxs-lookup"><span data-stu-id="6a24e-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="6a24e-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="6a24e-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS. If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.
   >
   >

1. <span data-ttu-id="6a24e-133">Click **Create** to create your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a24e-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="6a24e-134">Wait for a few minutes.</span><span class="sxs-lookup"><span data-stu-id="6a24e-134">Wait for a few minutes.</span></span> <span data-ttu-id="6a24e-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a24e-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6a24e-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span><span class="sxs-lookup"><span data-stu-id="6a24e-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![portal view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="6a24e-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a24e-138">Next steps</span></span>
<span data-ttu-id="6a24e-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span><span class="sxs-lookup"><span data-stu-id="6a24e-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="6a24e-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="6a24e-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="6a24e-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="6a24e-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="6a24e-142">Firewall rules can also be configured using Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="6a24e-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="6a24e-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="6a24e-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="6a24e-144">It's also a great idea to look at the [Best practices][Best practices].</span><span class="sxs-lookup"><span data-stu-id="6a24e-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[subscription]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F



