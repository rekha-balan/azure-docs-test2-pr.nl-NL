---
title: Make web, and API apps available to your Azure Stack users | Microsoft Docs
description: Tutorial to install the App Service resource provider and create offers that give your Azure Stack users the ability to create web, and API apps.
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
ms.date: 06/05/2018
ms.author: jeffgilb
ms.reviewer: ''
ms.custom: mvc
ms.openlocfilehash: 0171dba639e480a04cdd1c7f23d546d01121fb42
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871566"
---
# <a name="tutorial-make-web-and-api-apps-available-to-your-azure-stack-users"></a><span data-ttu-id="e1abc-103">Tutorial: make web and API apps available to your Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="e1abc-103">Tutorial: make web and API apps available to your Azure Stack users</span></span>

<span data-ttu-id="e1abc-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, and API applications.</span><span class="sxs-lookup"><span data-stu-id="e1abc-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, and API applications.</span></span> <span data-ttu-id="e1abc-105">By giving your users access to these on-demand, cloud-based apps, you can save them time and resources.</span><span class="sxs-lookup"><span data-stu-id="e1abc-105">By giving your users access to these on-demand, cloud-based apps, you can save them time and resources.</span></span>

<span data-ttu-id="e1abc-106">To set this up, you will:</span><span class="sxs-lookup"><span data-stu-id="e1abc-106">To set this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1abc-107">Deploy the App Service resource provider</span><span class="sxs-lookup"><span data-stu-id="e1abc-107">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="e1abc-108">Create an offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-108">Create an offer</span></span>
> * <span data-ttu-id="e1abc-109">Test the offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-109">Test the offer</span></span>

## <a name="deploy-the-app-service-resource-provider"></a><span data-ttu-id="e1abc-110">Deploy the App Service resource provider</span><span class="sxs-lookup"><span data-stu-id="e1abc-110">Deploy the App Service resource provider</span></span>

1. <span data-ttu-id="e1abc-111">[Prepare the Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e1abc-111">[Prepare the Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="e1abc-112">This includes deploying the SQL Server resource provider, which is required for creating some apps.</span><span class="sxs-lookup"><span data-stu-id="e1abc-112">This includes deploying the SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="e1abc-113">[Download the installer and helper scripts](azure-stack-app-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e1abc-113">[Download the installer and helper scripts](azure-stack-app-service-deploy.md).</span></span>
3. <span data-ttu-id="e1abc-114">[Run the helper script to create required certificates](azure-stack-app-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e1abc-114">[Run the helper script to create required certificates](azure-stack-app-service-deploy.md).</span></span>
4. <span data-ttu-id="e1abc-115">[Install the App Service resource provider](azure-stack-app-service-deploy.md) (It will take a couple hours to install and for all the worker roles to appear.)</span><span class="sxs-lookup"><span data-stu-id="e1abc-115">[Install the App Service resource provider](azure-stack-app-service-deploy.md) (It will take a couple hours to install and for all the worker roles to appear.)</span></span>
5. <span data-ttu-id="e1abc-116">[Validate the installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span><span class="sxs-lookup"><span data-stu-id="e1abc-116">[Validate the installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="e1abc-117">Create an offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-117">Create an offer</span></span>

<span data-ttu-id="e1abc-118">As an example, you can create an offer that lets users create DNN web content management systems.</span><span class="sxs-lookup"><span data-stu-id="e1abc-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="e1abc-119">It requires the SQL Server service which you already enabled by installing the SQL Server resource provider.</span><span class="sxs-lookup"><span data-stu-id="e1abc-119">It requires the SQL Server service which you already enabled by installing the SQL Server resource provider.</span></span>

1.  <span data-ttu-id="e1abc-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span><span class="sxs-lookup"><span data-stu-id="e1abc-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="e1abc-121">Select **Microsoft.Web** for the **Namespace** field.</span><span class="sxs-lookup"><span data-stu-id="e1abc-121">Select **Microsoft.Web** for the **Namespace** field.</span></span>
2.  <span data-ttu-id="e1abc-122">[Create a plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="e1abc-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="e1abc-123">Name it *TestAppServicePlan*, select the **Microsoft.SQL** service and the **AppService Quota** quota.</span><span class="sxs-lookup"><span data-stu-id="e1abc-123">Name it *TestAppServicePlan*, select the **Microsoft.SQL** service and the **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1abc-124">To let users create other apps, other services might be required in the plan.</span><span class="sxs-lookup"><span data-stu-id="e1abc-124">To let users create other apps, other services might be required in the plan.</span></span> <span data-ttu-id="e1abc-125">For example, Azure Functions requires the **Microsoft.Storage** service in the plan, while Wordpress requires **Microsoft.MySQL**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-125">For example, Azure Functions requires the **Microsoft.Storage** service in the plan, while Wordpress requires **Microsoft.MySQL**.</span></span>

3.  <span data-ttu-id="e1abc-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select the **TestAppServicePlan** plan.</span><span class="sxs-lookup"><span data-stu-id="e1abc-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select the **TestAppServicePlan** plan.</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="e1abc-127">Test the offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-127">Test the offer</span></span>

<span data-ttu-id="e1abc-128">Now that you've deployed the App Service resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create an app.</span><span class="sxs-lookup"><span data-stu-id="e1abc-128">Now that you've deployed the App Service resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create an app.</span></span>

<span data-ttu-id="e1abc-129">For this example, we'll create a DNN Platform content management system.</span><span class="sxs-lookup"><span data-stu-id="e1abc-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="e1abc-130">First, you create a SQL database and then the DNN web app.</span><span class="sxs-lookup"><span data-stu-id="e1abc-130">First, you create a SQL database and then the DNN web app.</span></span>

### <a name="subscribe-to-the-offer"></a><span data-ttu-id="e1abc-131">Subscribe to the offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-131">Subscribe to the offer</span></span>

1. <span data-ttu-id="e1abc-132">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span><span class="sxs-lookup"><span data-stu-id="e1abc-132">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="e1abc-133">Select **Get a subscription** >, enter **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-133">Select **Get a subscription** >, enter **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="e1abc-134">Create a SQL database</span><span class="sxs-lookup"><span data-stu-id="e1abc-134">Create a SQL database</span></span>

1. <span data-ttu-id="e1abc-135">Select **+** > **Data + Storage** > **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-135">Select **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="e1abc-136">Keep the default values, except for the following fields:</span><span class="sxs-lookup"><span data-stu-id="e1abc-136">Keep the default values, except for the following fields:</span></span>

    - <span data-ttu-id="e1abc-137">**Database Name**: DNNdb</span><span class="sxs-lookup"><span data-stu-id="e1abc-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="e1abc-138">**Max Size in MB**: 100</span><span class="sxs-lookup"><span data-stu-id="e1abc-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="e1abc-139">**Subscription**: TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="e1abc-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="e1abc-140">**Resource Group**: DNN-RG</span><span class="sxs-lookup"><span data-stu-id="e1abc-140">**Resource Group**: DNN-RG</span></span>

3. <span data-ttu-id="e1abc-141">Select **Login Settings**, enter credentials for the database, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-141">Select **Login Settings**, enter credentials for the database, and then select **OK**.</span></span> <span data-ttu-id="e1abc-142">You'll use these credentials later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e1abc-142">You'll use these credentials later in this tutorial.</span></span>
4. <span data-ttu-id="e1abc-143">Under **SKU** > select the SQL SKU that you created for the SQL Hosting Server > and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-143">Under **SKU** > select the SQL SKU that you created for the SQL Hosting Server > and then select **OK**.</span></span>
5. <span data-ttu-id="e1abc-144">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-144">Select **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="e1abc-145">Create a DNN app</span><span class="sxs-lookup"><span data-stu-id="e1abc-145">Create a DNN app</span></span>

1. <span data-ttu-id="e1abc-146">Select **+** > **See all** > **DNN Platform preview** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-146">Select **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="e1abc-147">Enter *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-147">Enter *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="e1abc-148">Select **Configure required settings** > **Create New** > to enter an **App Service plan** name.</span><span class="sxs-lookup"><span data-stu-id="e1abc-148">Select **Configure required settings** > **Create New** > to enter an **App Service plan** name.</span></span>
4. <span data-ttu-id="e1abc-149">Select **Pricing tier** > **F1 Free** > **Select** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-149">Select **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="e1abc-150">Select **Database** and enter the credentials for the SQL database you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e1abc-150">Select **Database** and enter the credentials for the SQL database you created earlier.</span></span>
6. <span data-ttu-id="e1abc-151">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1abc-151">Select **Create**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1abc-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1abc-152">Next steps</span></span>

<span data-ttu-id="e1abc-153">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="e1abc-153">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1abc-154">Deploy the App Service resource provider</span><span class="sxs-lookup"><span data-stu-id="e1abc-154">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="e1abc-155">Create an offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-155">Create an offer</span></span>
> * <span data-ttu-id="e1abc-156">Test the offer</span><span class="sxs-lookup"><span data-stu-id="e1abc-156">Test the offer</span></span>

<span data-ttu-id="e1abc-157">Advance to the next tutorial to learn how to:</span><span class="sxs-lookup"><span data-stu-id="e1abc-157">Advance to the next tutorial to learn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e1abc-158">Deploy apps to Azure and Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e1abc-158">Deploy apps to Azure and Azure Stack</span></span>](user/azure-stack-solution-pipeline.md)
