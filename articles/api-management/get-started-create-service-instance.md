---
title: Create an Azure API Management instance | Microsoft Docs
description: Follow the steps of this tutorial to create a new Azure API Management instance.
services: api-management
documentationcenter: ''
author: vladvino
manager: cflower
editor: ''
ms.service: api-management
ms.workload: integration
ms.topic: quickstart
ms.custom: mvc
ms.date: 11/28/2017
ms.author: apimpm
ms.openlocfilehash: 7fb4182c0b5149a9006a30ad34782ad968e16758
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870383"
---
# <a name="create-a-new-azure-api-management-service-instance"></a><span data-ttu-id="7b3af-103">Create a new Azure API Management service instance</span><span class="sxs-lookup"><span data-stu-id="7b3af-103">Create a new Azure API Management service instance</span></span>

<span data-ttu-id="7b3af-104">Azure API Management (APIM) helps organizations publish APIs to external, partner, and internal developers to unlock the potential of their data and services.</span><span class="sxs-lookup"><span data-stu-id="7b3af-104">Azure API Management (APIM) helps organizations publish APIs to external, partner, and internal developers to unlock the potential of their data and services.</span></span> <span data-ttu-id="7b3af-105">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security, and protection.</span><span class="sxs-lookup"><span data-stu-id="7b3af-105">API Management provides the core competencies to ensure a successful API program through developer engagement, business insights, analytics, security, and protection.</span></span> <span data-ttu-id="7b3af-106">APIM  enables you to create and manage modern API gateways for existing backend services hosted anywhere.</span><span class="sxs-lookup"><span data-stu-id="7b3af-106">APIM  enables you to create and manage modern API gateways for existing backend services hosted anywhere.</span></span> <span data-ttu-id="7b3af-107">For more information, see the [Overview](api-management-key-concepts.md) topic.</span><span class="sxs-lookup"><span data-stu-id="7b3af-107">For more information, see the [Overview](api-management-key-concepts.md) topic.</span></span>

<span data-ttu-id="7b3af-108">This quickstart describes the steps for creating a new API Management instance using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b3af-108">This quickstart describes the steps for creating a new API Management instance using the Azure portal.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

![new instance](./media/get-started-create-service-instance/get-started-create-service-instance-created.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="7b3af-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="7b3af-110">Log in to Azure</span></span>

<span data-ttu-id="7b3af-111">Log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="7b3af-111">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-new-service"></a><span data-ttu-id="7b3af-112">Create a new service</span><span class="sxs-lookup"><span data-stu-id="7b3af-112">Create a new service</span></span>

1. <span data-ttu-id="7b3af-113">In the [Azure portal](https://portal.azure.com/), select **Create a resource** > **Enterprise Integration** > **API management**.</span><span class="sxs-lookup"><span data-stu-id="7b3af-113">In the [Azure portal](https://portal.azure.com/), select **Create a resource** > **Enterprise Integration** > **API management**.</span></span>

    <span data-ttu-id="7b3af-114">Alternatively, choose **New**, type `API management` in the search box, and press Enter.</span><span class="sxs-lookup"><span data-stu-id="7b3af-114">Alternatively, choose **New**, type `API management` in the search box, and press Enter.</span></span> <span data-ttu-id="7b3af-115">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b3af-115">Click **Create**.</span></span>

2. <span data-ttu-id="7b3af-116">In the **API Management service** window, enter settings.</span><span class="sxs-lookup"><span data-stu-id="7b3af-116">In the **API Management service** window, enter settings.</span></span>

    ![new instance](./media/get-started-create-service-instance/get-started-create-service-instance-create-new.png)

    | <span data-ttu-id="7b3af-118">Setting</span><span class="sxs-lookup"><span data-stu-id="7b3af-118">Setting</span></span>      | <span data-ttu-id="7b3af-119">Suggested value</span><span class="sxs-lookup"><span data-stu-id="7b3af-119">Suggested value</span></span>  | <span data-ttu-id="7b3af-120">Description</span><span class="sxs-lookup"><span data-stu-id="7b3af-120">Description</span></span>              |
    | ------------ |  ------- | ---------------------------------|
    |<span data-ttu-id="7b3af-121">**Name**</span><span class="sxs-lookup"><span data-stu-id="7b3af-121">**Name**</span></span>|<span data-ttu-id="7b3af-122">A unique name for your API Management service</span><span class="sxs-lookup"><span data-stu-id="7b3af-122">A unique name for your API Management service</span></span>| <span data-ttu-id="7b3af-123">The name can't be changed later.</span><span class="sxs-lookup"><span data-stu-id="7b3af-123">The name can't be changed later.</span></span> <span data-ttu-id="7b3af-124">Service name is used to generate a default domain name in the form of *{name}.azure-api.net.*</span><span class="sxs-lookup"><span data-stu-id="7b3af-124">Service name is used to generate a default domain name in the form of *{name}.azure-api.net.*</span></span> <span data-ttu-id="7b3af-125">If you would like to use a custom domain name, see [Configure a custom domain](configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="7b3af-125">If you would like to use a custom domain name, see [Configure a custom domain](configure-custom-domain.md).</span></span> <br/> <span data-ttu-id="7b3af-126">Service name is used to refer to the service and the corresponding Azure resource.</span><span class="sxs-lookup"><span data-stu-id="7b3af-126">Service name is used to refer to the service and the corresponding Azure resource.</span></span>|
    |<span data-ttu-id="7b3af-127">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="7b3af-127">**Subscription**</span></span>|<span data-ttu-id="7b3af-128">Your subscription</span><span class="sxs-lookup"><span data-stu-id="7b3af-128">Your subscription</span></span> | <span data-ttu-id="7b3af-129">The subscription under which this new service instance will be created.</span><span class="sxs-lookup"><span data-stu-id="7b3af-129">The subscription under which this new service instance will be created.</span></span> <span data-ttu-id="7b3af-130">You can select the subscription among the different Azure subscriptions that you have access to.</span><span class="sxs-lookup"><span data-stu-id="7b3af-130">You can select the subscription among the different Azure subscriptions that you have access to.</span></span>|
    |<span data-ttu-id="7b3af-131">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="7b3af-131">**Resource Group**</span></span>|<span data-ttu-id="7b3af-132">*apimResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="7b3af-132">*apimResourceGroup*</span></span>|<span data-ttu-id="7b3af-133">You can select a new or existing resource.</span><span class="sxs-lookup"><span data-stu-id="7b3af-133">You can select a new or existing resource.</span></span> <span data-ttu-id="7b3af-134">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span><span class="sxs-lookup"><span data-stu-id="7b3af-134">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="7b3af-135">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="7b3af-135">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>|
    |<span data-ttu-id="7b3af-136">**Location**</span><span class="sxs-lookup"><span data-stu-id="7b3af-136">**Location**</span></span>|<span data-ttu-id="7b3af-137">*West USA*</span><span class="sxs-lookup"><span data-stu-id="7b3af-137">*West USA*</span></span>|<span data-ttu-id="7b3af-138">Select the geographic region near you.</span><span class="sxs-lookup"><span data-stu-id="7b3af-138">Select the geographic region near you.</span></span> <span data-ttu-id="7b3af-139">Only the available API Management service regions appear in the drop-down list box.</span><span class="sxs-lookup"><span data-stu-id="7b3af-139">Only the available API Management service regions appear in the drop-down list box.</span></span> |
    |<span data-ttu-id="7b3af-140">**Organization name**</span><span class="sxs-lookup"><span data-stu-id="7b3af-140">**Organization name**</span></span>|<span data-ttu-id="7b3af-141">The name of your organization</span><span class="sxs-lookup"><span data-stu-id="7b3af-141">The name of your organization</span></span>|<span data-ttu-id="7b3af-142">This name is used in a number of places, including the title of the developer portal and sender of notification emails.</span><span class="sxs-lookup"><span data-stu-id="7b3af-142">This name is used in a number of places, including the title of the developer portal and sender of notification emails.</span></span>|
    |<span data-ttu-id="7b3af-143">**Administrator email**</span><span class="sxs-lookup"><span data-stu-id="7b3af-143">**Administrator email**</span></span>|*admin@org.com*|<span data-ttu-id="7b3af-144">Set email address to which all the notifications from **API Management** will be sent.</span><span class="sxs-lookup"><span data-stu-id="7b3af-144">Set email address to which all the notifications from **API Management** will be sent.</span></span>|
    |<span data-ttu-id="7b3af-145">**Pricing tier**</span><span class="sxs-lookup"><span data-stu-id="7b3af-145">**Pricing tier**</span></span>|<span data-ttu-id="7b3af-146">*Developer*</span><span class="sxs-lookup"><span data-stu-id="7b3af-146">*Developer*</span></span>|<span data-ttu-id="7b3af-147">Set **Developer** tier to evaluate the service.</span><span class="sxs-lookup"><span data-stu-id="7b3af-147">Set **Developer** tier to evaluate the service.</span></span> <span data-ttu-id="7b3af-148">This tier is not for production use.</span><span class="sxs-lookup"><span data-stu-id="7b3af-148">This tier is not for production use.</span></span> <span data-ttu-id="7b3af-149">For more information about scaling the API Management tiers, see [upgrade and scale](upgrade-and-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7b3af-149">For more information about scaling the API Management tiers, see [upgrade and scale](upgrade-and-scale.md).</span></span>|
3. <span data-ttu-id="7b3af-150">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b3af-150">Choose **Create**.</span></span>

    > [!TIP]
    > <span data-ttu-id="7b3af-151">It usually takes between 20 and 30 minutes to create an API Management service.</span><span class="sxs-lookup"><span data-stu-id="7b3af-151">It usually takes between 20 and 30 minutes to create an API Management service.</span></span> <span data-ttu-id="7b3af-152">Selecting **Pin to dashboard** makes finding a newly created service easier.</span><span class="sxs-lookup"><span data-stu-id="7b3af-152">Selecting **Pin to dashboard** makes finding a newly created service easier.</span></span>

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7b3af-153">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7b3af-153">Clean up resources</span></span>

<span data-ttu-id="7b3af-154">When no longer needed, you can remove the resource group and all related resources by following these steps:</span><span class="sxs-lookup"><span data-stu-id="7b3af-154">When no longer needed, you can remove the resource group and all related resources by following these steps:</span></span>


1. <span data-ttu-id="7b3af-155">In the Azure portal, select</span><span class="sxs-lookup"><span data-stu-id="7b3af-155">In the Azure portal, select</span></span> ![arrow](./media/get-started-create-service-instance/arrow.png)<span data-ttu-id="7b3af-157">.</span><span class="sxs-lookup"><span data-stu-id="7b3af-157">.</span></span>
2. <span data-ttu-id="7b3af-158">Select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="7b3af-158">Select **Resource groups**.</span></span>
3. <span data-ttu-id="7b3af-159">Find your resource group.</span><span class="sxs-lookup"><span data-stu-id="7b3af-159">Find your resource group.</span></span>
4. <span data-ttu-id="7b3af-160">Click ".</span><span class="sxs-lookup"><span data-stu-id="7b3af-160">Click ".</span></span> <span data-ttu-id="7b3af-161">.</span><span class="sxs-lookup"><span data-stu-id="7b3af-161">.</span></span> <span data-ttu-id="7b3af-162">."</span><span class="sxs-lookup"><span data-stu-id="7b3af-162">."</span></span> <span data-ttu-id="7b3af-163">and delete your group.</span><span class="sxs-lookup"><span data-stu-id="7b3af-163">and delete your group.</span></span>

![cleanup](./media/get-started-create-service-instance/cleanup.png)

## <a name="next-steps"></a><span data-ttu-id="7b3af-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="7b3af-165">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7b3af-166">Import and publish your first API</span><span class="sxs-lookup"><span data-stu-id="7b3af-166">Import and publish your first API</span></span>](import-and-publish.md)
