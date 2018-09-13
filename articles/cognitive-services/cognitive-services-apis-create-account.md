---
title: Create a Cognitive Services APIs account in the Azure portal | Microsoft Docs
description: How to create a Microsoft Cognitive Services APIs account in the Azure portal.
services: cognitive-services
documentationcenter: ''
author: garyericson
manager: cgronlun
editor: ''
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: cognitive-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2018
ms.author: garye
ms.reviewer: gibattag
ms.openlocfilehash: f7c60c9a53dce433598ce98f8048608bedeb8e6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828906"
---
# <a name="create-a-cognitive-services-apis-account-in-the-azure-portal"></a><span data-ttu-id="e96dc-103">Create a Cognitive Services APIs account in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e96dc-103">Create a Cognitive Services APIs account in the Azure portal</span></span>

<span data-ttu-id="e96dc-104">To use Microsoft Cognitive Service APIs, you first need to create an account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e96dc-104">To use Microsoft Cognitive Service APIs, you first need to create an account in the Azure portal.</span></span>

1. <span data-ttu-id="e96dc-105">Sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e96dc-105">Sign in to the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="e96dc-106">Click **+ Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="e96dc-106">Click **+ Create a resource**.</span></span>

3. <span data-ttu-id="e96dc-107">Under Azure Marketplace, select **AI + Cognitive Services** and discover the list of available APIs.</span><span class="sxs-lookup"><span data-stu-id="e96dc-107">Under Azure Marketplace, select **AI + Cognitive Services** and discover the list of available APIs.</span></span> <span data-ttu-id="e96dc-108">Click on **See all** to see the entire list of Cognitive Services APIs.</span><span class="sxs-lookup"><span data-stu-id="e96dc-108">Click on **See all** to see the entire list of Cognitive Services APIs.</span></span> <span data-ttu-id="e96dc-109">Click on the API of your choice to proceed.</span><span class="sxs-lookup"><span data-stu-id="e96dc-109">Click on the API of your choice to proceed.</span></span>

    ![Select Cognitive Services APIs](media/cognitive-services-apis-create-account/select-cognitive-services-apis.png)

4. <span data-ttu-id="e96dc-111">On the **Create** page, provide the following information:</span><span class="sxs-lookup"><span data-stu-id="e96dc-111">On the **Create** page, provide the following information:</span></span>

   - <span data-ttu-id="e96dc-112">**Account Name:** Name of the account.</span><span class="sxs-lookup"><span data-stu-id="e96dc-112">**Account Name:** Name of the account.</span></span> <span data-ttu-id="e96dc-113">We recommend using a descriptive name, for example *AFaceAPIAccount*.</span><span class="sxs-lookup"><span data-stu-id="e96dc-113">We recommend using a descriptive name, for example *AFaceAPIAccount*.</span></span>

   - <span data-ttu-id="e96dc-114">**Subscription:** Select one of the available Azure subscriptions in which you have at least Contributor permissions.</span><span class="sxs-lookup"><span data-stu-id="e96dc-114">**Subscription:** Select one of the available Azure subscriptions in which you have at least Contributor permissions.</span></span>

   - <span data-ttu-id="e96dc-115">**API Type:** Choose the Cognitive Services API you want to use.</span><span class="sxs-lookup"><span data-stu-id="e96dc-115">**API Type:** Choose the Cognitive Services API you want to use.</span></span> <span data-ttu-id="e96dc-116">For more information about the various Cognitive Services APIs available, visit the [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/) site.</span><span class="sxs-lookup"><span data-stu-id="e96dc-116">For more information about the various Cognitive Services APIs available, visit the [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/) site.</span></span>

   - <span data-ttu-id="e96dc-117">**Pricing tier:** The cost of your Cognitive Services account depends on the actual usage and the options you choose.</span><span class="sxs-lookup"><span data-stu-id="e96dc-117">**Pricing tier:** The cost of your Cognitive Services account depends on the actual usage and the options you choose.</span></span> <span data-ttu-id="e96dc-118">For more information about pricing for each API, refer to the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="e96dc-118">For more information about pricing for each API, refer to the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/).</span></span>

   - <span data-ttu-id="e96dc-119">**Resource Group:** A resource group is a collection of resources that share the same lifecycle, permissions, and policies.</span><span class="sxs-lookup"><span data-stu-id="e96dc-119">**Resource Group:** A resource group is a collection of resources that share the same lifecycle, permissions, and policies.</span></span> <span data-ttu-id="e96dc-120">To learn more about Resource Groups, see [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="e96dc-120">To learn more about Resource Groups, see [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

   - <span data-ttu-id="e96dc-121">**Resource Group Location:** This is required only if the API selected is global (not bound to a location).</span><span class="sxs-lookup"><span data-stu-id="e96dc-121">**Resource Group Location:** This is required only if the API selected is global (not bound to a location).</span></span> <span data-ttu-id="e96dc-122">If the API is global and not bound to a location, however, you must specify a location for the resource group where the metadata associated with the Cognitive Services API account resides.</span><span class="sxs-lookup"><span data-stu-id="e96dc-122">If the API is global and not bound to a location, however, you must specify a location for the resource group where the metadata associated with the Cognitive Services API account resides.</span></span> <span data-ttu-id="e96dc-123">This location has no impact on the runtime availability of your account.</span><span class="sxs-lookup"><span data-stu-id="e96dc-123">This location has no impact on the runtime availability of your account.</span></span> <span data-ttu-id="e96dc-124">To learn more about resource group, see [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="e96dc-124">To learn more about resource group, see [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

   - <span data-ttu-id="e96dc-125">**Explicit acknowledgment of Online Service Terms:** In order to create an account, subscription Owners or Contributors (as defined by [Azure Role-Based Access Control](https://docs.microsoft.com/azure/role-based-access-control/overview)) need to explicitly acknowledge the terms that apply to Cognitive Services in [Online Service Terms](https://www.microsoft.com/en-us/Licensing/product-licensing/products.aspx).</span><span class="sxs-lookup"><span data-stu-id="e96dc-125">**Explicit acknowledgment of Online Service Terms:** In order to create an account, subscription Owners or Contributors (as defined by [Azure Role-Based Access Control](https://docs.microsoft.com/azure/role-based-access-control/overview)) need to explicitly acknowledge the terms that apply to Cognitive Services in [Online Service Terms](https://www.microsoft.com/en-us/Licensing/product-licensing/products.aspx).</span></span> 

     <span data-ttu-id="e96dc-126">The subscription Owner can disable the creation of Cognitive Services account for a specific resource group or subscription through [Azure policies](../azure-policy/azure-policy-introduction.md) by following the article [Using Azure portal to assign and manage resource policies](../azure-policy/assign-policy-definition.md) and assigning a “Not allowed resource types” policy definition and specifying **Microsoft.CognitiveServices/accounts** as the target resource type.</span><span class="sxs-lookup"><span data-stu-id="e96dc-126">The subscription Owner can disable the creation of Cognitive Services account for a specific resource group or subscription through [Azure policies](../azure-policy/azure-policy-introduction.md) by following the article [Using Azure portal to assign and manage resource policies](../azure-policy/assign-policy-definition.md) and assigning a “Not allowed resource types” policy definition and specifying **Microsoft.CognitiveServices/accounts** as the target resource type.</span></span>

     <span data-ttu-id="e96dc-127">If account creation was disabled, the following error would be displayed at the time of account creation:</span><span class="sxs-lookup"><span data-stu-id="e96dc-127">If account creation was disabled, the following error would be displayed at the time of account creation:</span></span>

     ![Account creation error](media/cognitive-services-apis-create-account/error-message.png)

5. <span data-ttu-id="e96dc-129">To pin the account to the Azure portal dashboard, click **Pin to Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="e96dc-129">To pin the account to the Azure portal dashboard, click **Pin to Dashboard**.</span></span>

6. <span data-ttu-id="e96dc-130">Click **Create** to create the account.</span><span class="sxs-lookup"><span data-stu-id="e96dc-130">Click **Create** to create the account.</span></span>

<span data-ttu-id="e96dc-131">After the Cognitive Services account is successfully deployed, click the tile in the dashboard to view the account information.</span><span class="sxs-lookup"><span data-stu-id="e96dc-131">After the Cognitive Services account is successfully deployed, click the tile in the dashboard to view the account information.</span></span>

<span data-ttu-id="e96dc-132">You can use the **Endpoint URL** in the **Overview** section and keys in the **Keys** section to start making API calls in your applications.</span><span class="sxs-lookup"><span data-stu-id="e96dc-132">You can use the **Endpoint URL** in the **Overview** section and keys in the **Keys** section to start making API calls in your applications.</span></span>

![Display account information](media/cognitive-services-apis-create-account/display-account.png)

![Display account keys](media/cognitive-services-apis-create-account/account-keys.png)

### <a name="next-steps"></a><span data-ttu-id="e96dc-135">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e96dc-135">Next Steps</span></span>

<span data-ttu-id="e96dc-136">For more information about all the Microsoft Cognitive Services available, see [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="e96dc-136">For more information about all the Microsoft Cognitive Services available, see [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/).</span></span>

<span data-ttu-id="e96dc-137">For quickstart guides to using some example Cognitive Services APIs:</span><span class="sxs-lookup"><span data-stu-id="e96dc-137">For quickstart guides to using some example Cognitive Services APIs:</span></span>

 - [<span data-ttu-id="e96dc-138">Computer Vision C# quickstarts</span><span class="sxs-lookup"><span data-stu-id="e96dc-138">Computer Vision C# quickstarts</span></span>](computer-vision/quickstarts/csharp.md)
 - [<span data-ttu-id="e96dc-139">Text Analytics with Python</span><span class="sxs-lookup"><span data-stu-id="e96dc-139">Text Analytics with Python</span></span>](text-analytics/quickstarts/python.md)
 - [<span data-ttu-id="e96dc-140">Face API with JavaScript</span><span class="sxs-lookup"><span data-stu-id="e96dc-140">Face API with JavaScript</span></span>](face/quickstarts/javascript.md)
