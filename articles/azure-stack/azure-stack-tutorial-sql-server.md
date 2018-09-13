---
title: Make SQL databases available to your Azure Stack users | Microsoft Docs
description: Tutorial to install the SQL Server resource provider and create offers that let Azure Stack users create SQL databases.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: ''
ms.custom: mvc
ms.openlocfilehash: 35f4d2adfe3ca64496139cdd708fb5f52f8721ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865688"
---
# <a name="tutorial-make-sql-databases-available-to-your-azure-stack-users"></a><span data-ttu-id="ea26d-103">Tutorial: make SQL databases available to your Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="ea26d-103">Tutorial: make SQL databases available to your Azure Stack users</span></span>

<span data-ttu-id="ea26d-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span><span class="sxs-lookup"><span data-stu-id="ea26d-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="ea26d-105">By providing these custom, on-demand, cloud-based databases to your users, you can save them time and resources.</span><span class="sxs-lookup"><span data-stu-id="ea26d-105">By providing these custom, on-demand, cloud-based databases to your users, you can save them time and resources.</span></span> <span data-ttu-id="ea26d-106">To set this up, you will:</span><span class="sxs-lookup"><span data-stu-id="ea26d-106">To set this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea26d-107">Deploy the SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="ea26d-107">Deploy the SQL Server resource provider</span></span>
> * <span data-ttu-id="ea26d-108">Create an offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-108">Create an offer</span></span>
> * <span data-ttu-id="ea26d-109">Test the offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-109">Test the offer</span></span>

## <a name="deploy-the-sql-server-resource-provider"></a><span data-ttu-id="ea26d-110">Deploy the SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="ea26d-110">Deploy the SQL Server resource provider</span></span>

<span data-ttu-id="ea26d-111">The deployment process is described in detail in the [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and consists of the following primary steps:</span><span class="sxs-lookup"><span data-stu-id="ea26d-111">The deployment process is described in detail in the [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and consists of the following primary steps:</span></span>

1. <span data-ttu-id="ea26d-112">[Deploy the SQL resource provider](azure-stack-sql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ea26d-112">[Deploy the SQL resource provider](azure-stack-sql-resource-provider-deploy.md).</span></span>
2. <span data-ttu-id="ea26d-113">[Verify the deployment](azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span><span class="sxs-lookup"><span data-stu-id="ea26d-113">[Verify the deployment](azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span></span>
3. <span data-ttu-id="ea26d-114">Provide capacity by connecting to a hosting SQL server.</span><span class="sxs-lookup"><span data-stu-id="ea26d-114">Provide capacity by connecting to a hosting SQL server.</span></span> <span data-ttu-id="ea26d-115">For more information, see [Add hosting servers](azure-stack-sql-resource-provider-hosting-servers.md)</span><span class="sxs-lookup"><span data-stu-id="ea26d-115">For more information, see [Add hosting servers](azure-stack-sql-resource-provider-hosting-servers.md)</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="ea26d-116">Create an offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-116">Create an offer</span></span>

1.  <span data-ttu-id="ea26d-117">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span><span class="sxs-lookup"><span data-stu-id="ea26d-117">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span></span> <span data-ttu-id="ea26d-118">Select **Microsoft.SQLAdapter** for the **Namespace** field.</span><span class="sxs-lookup"><span data-stu-id="ea26d-118">Select **Microsoft.SQLAdapter** for the **Namespace** field.</span></span>
2.  <span data-ttu-id="ea26d-119">[Create a plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="ea26d-119">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="ea26d-120">Name it *TestSQLServerPlan*, select the **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span><span class="sxs-lookup"><span data-stu-id="ea26d-120">Name it *TestSQLServerPlan*, select the **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ea26d-121">To let users create other apps, other services might be required in the plan.</span><span class="sxs-lookup"><span data-stu-id="ea26d-121">To let users create other apps, other services might be required in the plan.</span></span> <span data-ttu-id="ea26d-122">For example, Azure Functions requires the **Microsoft.Storage** service in the plan, while Wordpress requires **Microsoft.MySQLAdapter**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-122">For example, Azure Functions requires the **Microsoft.Storage** service in the plan, while Wordpress requires **Microsoft.MySQLAdapter**.</span></span>

3.  <span data-ttu-id="ea26d-123">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select the **TestSQLServerPlan** plan.</span><span class="sxs-lookup"><span data-stu-id="ea26d-123">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select the **TestSQLServerPlan** plan.</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="ea26d-124">Test the offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-124">Test the offer</span></span>

<span data-ttu-id="ea26d-125">Now that you've deployed the SQL Server resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create a database.</span><span class="sxs-lookup"><span data-stu-id="ea26d-125">Now that you've deployed the SQL Server resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create a database.</span></span>

### <a name="subscribe-to-the-offer"></a><span data-ttu-id="ea26d-126">Subscribe to the offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-126">Subscribe to the offer</span></span>

1. <span data-ttu-id="ea26d-127">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span><span class="sxs-lookup"><span data-stu-id="ea26d-127">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="ea26d-128">Select **Get a subscription** and then enter  **TestSQLServerSubscription** under **Display Name**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-128">Select **Get a subscription** and then enter  **TestSQLServerSubscription** under **Display Name**.</span></span>
3. <span data-ttu-id="ea26d-129">Select **Select an offer** > **TestSQLServerOffer** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-129">Select **Select an offer** > **TestSQLServerOffer** > **Create**.</span></span>
4. <span data-ttu-id="ea26d-130">Select **All services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-130">Select **All services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span></span>
5. <span data-ttu-id="ea26d-131">Select **Register** next to the **Microsoft.SQLAdapter** provider.</span><span class="sxs-lookup"><span data-stu-id="ea26d-131">Select **Register** next to the **Microsoft.SQLAdapter** provider.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="ea26d-132">Create a SQL database</span><span class="sxs-lookup"><span data-stu-id="ea26d-132">Create a SQL database</span></span>

1. <span data-ttu-id="ea26d-133">Select **+** > **Data + Storage** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-133">Select **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="ea26d-134">Keep the default values or use these examples for the following fields:</span><span class="sxs-lookup"><span data-stu-id="ea26d-134">Keep the default values or use these examples for the following fields:</span></span>
    - <span data-ttu-id="ea26d-135">**Database Name**: SQLdb</span><span class="sxs-lookup"><span data-stu-id="ea26d-135">**Database Name**: SQLdb</span></span>
    - <span data-ttu-id="ea26d-136">**Max Size in MB**: 100</span><span class="sxs-lookup"><span data-stu-id="ea26d-136">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="ea26d-137">**Subscription**: TestSQLOffer</span><span class="sxs-lookup"><span data-stu-id="ea26d-137">**Subscription**: TestSQLOffer</span></span>
    - <span data-ttu-id="ea26d-138">**Resource Group**: SQL-RG</span><span class="sxs-lookup"><span data-stu-id="ea26d-138">**Resource Group**: SQL-RG</span></span>
3. <span data-ttu-id="ea26d-139">Select **Login Settings**, enter credentials for the database, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-139">Select **Login Settings**, enter credentials for the database, and then select **OK**.</span></span>
4. <span data-ttu-id="ea26d-140">Select **SKU** > select the SQL SKU that you created for the SQL Hosting Server > and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-140">Select **SKU** > select the SQL SKU that you created for the SQL Hosting Server > and then select **OK**.</span></span>
5. <span data-ttu-id="ea26d-141">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea26d-141">Select **Create**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea26d-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea26d-142">Next steps</span></span>

<span data-ttu-id="ea26d-143">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="ea26d-143">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea26d-144">Deploy the SQL Server resource provider</span><span class="sxs-lookup"><span data-stu-id="ea26d-144">Deploy the SQL Server resource provider</span></span>
> * <span data-ttu-id="ea26d-145">Create an offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-145">Create an offer</span></span>
> * <span data-ttu-id="ea26d-146">Test the offer</span><span class="sxs-lookup"><span data-stu-id="ea26d-146">Test the offer</span></span>

<span data-ttu-id="ea26d-147">Advance to the next tutorial to learn how to:</span><span class="sxs-lookup"><span data-stu-id="ea26d-147">Advance to the next tutorial to learn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea26d-148">Make web, mobile, and API apps available to your users</span><span class="sxs-lookup"><span data-stu-id="ea26d-148">Make web, mobile, and API apps available to your users</span></span>]( azure-stack-tutorial-app-service.md)