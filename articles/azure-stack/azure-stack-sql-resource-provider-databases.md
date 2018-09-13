---
title: Using databases provided by the SQL Adapter Resource provider on Azure Stack | Microsoft Docs
description: How to create and manage SQL databases provisioned by using the SQL Adapter Resource provider
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 2f286c48822956c82f99808092c26f6637be5cb1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857325"
---
# <a name="create-sql-databases"></a><span data-ttu-id="c5749-103">Create SQL databases</span><span class="sxs-lookup"><span data-stu-id="c5749-103">Create SQL databases</span></span>

<span data-ttu-id="c5749-104">You can create and manage self-service databases in the user portal.</span><span class="sxs-lookup"><span data-stu-id="c5749-104">You can create and manage self-service databases in the user portal.</span></span> <span data-ttu-id="c5749-105">An Azure Stack user needs a subscription with an offer that includes the  SQL database service.</span><span class="sxs-lookup"><span data-stu-id="c5749-105">An Azure Stack user needs a subscription with an offer that includes the  SQL database service.</span></span>

1. <span data-ttu-id="c5749-106">Sign in to the [Azure Stack](azure-stack-poc.md) user portal.</span><span class="sxs-lookup"><span data-stu-id="c5749-106">Sign in to the [Azure Stack](azure-stack-poc.md) user portal.</span></span>

2. <span data-ttu-id="c5749-107">Select **+ New** &gt;**Data + Storage** &gt; **SQL Server Database** &gt; **Add**.</span><span class="sxs-lookup"><span data-stu-id="c5749-107">Select **+ New** &gt;**Data + Storage** &gt; **SQL Server Database** &gt; **Add**.</span></span>

3. <span data-ttu-id="c5749-108">Under **Create Database**, enter the required information, such as **Database Name** and **Max Size in MB**.</span><span class="sxs-lookup"><span data-stu-id="c5749-108">Under **Create Database**, enter the required information, such as **Database Name** and **Max Size in MB**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="c5749-109">The database size must be at least 64 MB, which you can increase after you deploy the database.</span><span class="sxs-lookup"><span data-stu-id="c5749-109">The database size must be at least 64 MB, which you can increase after you deploy the database.</span></span>

   <span data-ttu-id="c5749-110">Configure the other settings as required for your environment.</span><span class="sxs-lookup"><span data-stu-id="c5749-110">Configure the other settings as required for your environment.</span></span>

4. <span data-ttu-id="c5749-111">Under **Create Database**, select **SKU**.</span><span class="sxs-lookup"><span data-stu-id="c5749-111">Under **Create Database**, select **SKU**.</span></span> <span data-ttu-id="c5749-112">Under **Select a SKU**, select the SKU for your database.</span><span class="sxs-lookup"><span data-stu-id="c5749-112">Under **Select a SKU**, select the SKU for your database.</span></span>

   ![Create Database](./media/azure-stack-sql-rp-deploy/newsqldb.png)

   >[!NOTE]
   ><span data-ttu-id="c5749-114">As hosting servers are added to Azure Stack, they're assigned a SKU.</span><span class="sxs-lookup"><span data-stu-id="c5749-114">As hosting servers are added to Azure Stack, they're assigned a SKU.</span></span> <span data-ttu-id="c5749-115">Databases are created in the pool of hosting servers in a SKU.</span><span class="sxs-lookup"><span data-stu-id="c5749-115">Databases are created in the pool of hosting servers in a SKU.</span></span>

5. <span data-ttu-id="c5749-116">Select **Login**.</span><span class="sxs-lookup"><span data-stu-id="c5749-116">Select **Login**.</span></span>
6. <span data-ttu-id="c5749-117">Under **Select a Login**, choose an existing login, or select **+ Create a new login**.</span><span class="sxs-lookup"><span data-stu-id="c5749-117">Under **Select a Login**, choose an existing login, or select **+ Create a new login**.</span></span>
7. <span data-ttu-id="c5749-118">Under **New Login**, enter a name for **Database login** and a **Password**.</span><span class="sxs-lookup"><span data-stu-id="c5749-118">Under **New Login**, enter a name for **Database login** and a **Password**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="c5749-119">These settings are the SQL Authentication credential that's created for your access to this database only.</span><span class="sxs-lookup"><span data-stu-id="c5749-119">These settings are the SQL Authentication credential that's created for your access to this database only.</span></span> <span data-ttu-id="c5749-120">The login user name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="c5749-120">The login user name must be globally unique.</span></span> <span data-ttu-id="c5749-121">You can reuse login settings for other databases that use the same SKU.</span><span class="sxs-lookup"><span data-stu-id="c5749-121">You can reuse login settings for other databases that use the same SKU.</span></span>

   ![Create a new database login](./media/azure-stack-sql-rp-deploy/create-new-login.png)

8. <span data-ttu-id="c5749-123">Select **OK** to finish deploying the database.</span><span class="sxs-lookup"><span data-stu-id="c5749-123">Select **OK** to finish deploying the database.</span></span>

<span data-ttu-id="c5749-124">Under **Essentials**, which is shown after the database is deployed, take note of the **Connection string**.</span><span class="sxs-lookup"><span data-stu-id="c5749-124">Under **Essentials**, which is shown after the database is deployed, take note of the **Connection string**.</span></span> <span data-ttu-id="c5749-125">You can use this string in any application that needs to access the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="c5749-125">You can use this string in any application that needs to access the SQL Server database.</span></span>

![Retrieve the connection string](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="sql-always-on-databases"></a><span data-ttu-id="c5749-127">SQL Always On databases</span><span class="sxs-lookup"><span data-stu-id="c5749-127">SQL Always On databases</span></span>

<span data-ttu-id="c5749-128">By design, Always On databases are handled differently than in a standalone server environment.</span><span class="sxs-lookup"><span data-stu-id="c5749-128">By design, Always On databases are handled differently than in a standalone server environment.</span></span> <span data-ttu-id="c5749-129">For more information, see [Introducing SQL Server Always On availability groups on Azure virtual machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-overview).</span><span class="sxs-lookup"><span data-stu-id="c5749-129">For more information, see [Introducing SQL Server Always On availability groups on Azure virtual machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-availability-group-overview).</span></span>

### <a name="verify-sql-always-on-databases"></a><span data-ttu-id="c5749-130">Verify SQL Always On databases</span><span class="sxs-lookup"><span data-stu-id="c5749-130">Verify SQL Always On databases</span></span>

<span data-ttu-id="c5749-131">The following screen capture shows how you can use SQL Server Management Studio to look at database status in SQL Always On.</span><span class="sxs-lookup"><span data-stu-id="c5749-131">The following screen capture shows how you can use SQL Server Management Studio to look at database status in SQL Always On.</span></span>

![AlwaysOn database status](./media/azure-stack-sql-rp-deploy/verifyalwayson.png)

<span data-ttu-id="c5749-133">Always On databases should show as Synchronized and available on all the SQL instances and appear in Availability Groups.</span><span class="sxs-lookup"><span data-stu-id="c5749-133">Always On databases should show as Synchronized and available on all the SQL instances and appear in Availability Groups.</span></span> <span data-ttu-id="c5749-134">In the previous screen capture, the database example is newdb1 and its status is **newdb1 (Synchronized)**.</span><span class="sxs-lookup"><span data-stu-id="c5749-134">In the previous screen capture, the database example is newdb1 and its status is **newdb1 (Synchronized)**.</span></span>

### <a name="delete-an-alwayson-database"></a><span data-ttu-id="c5749-135">Delete an AlwaysOn database</span><span class="sxs-lookup"><span data-stu-id="c5749-135">Delete an AlwaysOn database</span></span>

<span data-ttu-id="c5749-136">When you delete a SQL AlwaysOn database from the resource provider, SQL deletes database from the Primary replica and from the availability group.</span><span class="sxs-lookup"><span data-stu-id="c5749-136">When you delete a SQL AlwaysOn database from the resource provider, SQL deletes database from the Primary replica and from the availability group.</span></span>

<span data-ttu-id="c5749-137">SQL then puts the database into the Restoring state on the other replicas and doesn't drop the database unless triggered.</span><span class="sxs-lookup"><span data-stu-id="c5749-137">SQL then puts the database into the Restoring state on the other replicas and doesn't drop the database unless triggered.</span></span> <span data-ttu-id="c5749-138">If the database isn't dropped, the secondary replicas go into a Not Synchronizing state.</span><span class="sxs-lookup"><span data-stu-id="c5749-138">If the database isn't dropped, the secondary replicas go into a Not Synchronizing state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5749-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5749-139">Next steps</span></span>

[<span data-ttu-id="c5749-140">Maintain the SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="c5749-140">Maintain the SQL Server resource provider</span></span>](azure-stack-sql-resource-provider-maintain.md)
