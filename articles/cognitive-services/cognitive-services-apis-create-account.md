---
title: Create a Cognitive Services APIs account in the Azure portal | Microsoft Docs
description: How to create a Microsoft Cognitive Services APIs account in the Azure portal.
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: garye;gibattag
ms.openlocfilehash: 1f5f891404546bd87940adb9ecbdc2d319e34f3d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661290"
---
# <a name="create-a-cognitive-services-apis-account-in-the-azure-portal"></a><span data-ttu-id="7e626-103">Create a Cognitive Services APIs account in the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7e626-103">Create a Cognitive Services APIs account in the Azure Portal</span></span>

<span data-ttu-id="7e626-104">To use Microsoft Cognitive Service APIs, you first need to create an account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7e626-104">To use Microsoft Cognitive Service APIs, you first need to create an account in the Azure portal.</span></span>

1. <span data-ttu-id="7e626-105">Sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7e626-105">Sign in to the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="7e626-106">Click **+ NEW**.</span><span class="sxs-lookup"><span data-stu-id="7e626-106">Click **+ NEW**.</span></span>

3. <span data-ttu-id="7e626-107">Select **Intelligence + Analytics** and then **Cognitive Services APIs (preview)**.</span><span class="sxs-lookup"><span data-stu-id="7e626-107">Select **Intelligence + Analytics** and then **Cognitive Services APIs (preview)**.</span></span>

    ![Select Cognitive Services APIs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/select-cognitive-services-apis.png)

4. <span data-ttu-id="7e626-109">On the **Create** page, provide the following information:</span><span class="sxs-lookup"><span data-stu-id="7e626-109">On the **Create** page, provide the following information:</span></span>

    -   <span data-ttu-id="7e626-110">**Account Name:** Name of the account.</span><span class="sxs-lookup"><span data-stu-id="7e626-110">**Account Name:** Name of the account.</span></span> <span data-ttu-id="7e626-111">We recommend using a descriptive name, for example *AFaceAPIAccount*.</span><span class="sxs-lookup"><span data-stu-id="7e626-111">We recommend using a descriptive name, for example *AFaceAPIAccount*.</span></span>

    -   <span data-ttu-id="7e626-112">**Subscription:** Select one of the available Azure subscriptions in which you have at least Contributor permissions.</span><span class="sxs-lookup"><span data-stu-id="7e626-112">**Subscription:** Select one of the available Azure subscriptions in which you have at least Contributor permissions.</span></span>

    -   <span data-ttu-id="7e626-113">**API Type:** Choose the Cognitive Services API you want to use.</span><span class="sxs-lookup"><span data-stu-id="7e626-113">**API Type:** Choose the Cognitive Services API you want to use.</span></span> <span data-ttu-id="7e626-114">For more information about the various Cognitive Services APIs available, please refer to the [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/) site.</span><span class="sxs-lookup"><span data-stu-id="7e626-114">For more information about the various Cognitive Services APIs available, please refer to the [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/) site.</span></span>

    ![Select API type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/list-of-apis.png)

    -   <span data-ttu-id="7e626-116">**Pricing tier:** The cost of your Cognitive Services account depends on the actual usage and the options you choose.</span><span class="sxs-lookup"><span data-stu-id="7e626-116">**Pricing tier:** The cost of your Cognitive Services account depends on the actual usage and the options you choose.</span></span> <span data-ttu-id="7e626-117">For more information about pricing for each API, please refer to the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="7e626-117">For more information about pricing for each API, please refer to the [pricing pages](https://azure.microsoft.com/pricing/details/cognitive-services/).</span></span>

    -   <span data-ttu-id="7e626-118">**Resource Group:** A resource group is a collection of resources that share the same lifecycle, permissions, and policies.</span><span class="sxs-lookup"><span data-stu-id="7e626-118">**Resource Group:** A resource group is a collection of resources that share the same lifecycle, permissions, and policies.</span></span> <span data-ttu-id="7e626-119">To learn more about Resource Groups, see [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="7e626-119">To learn more about Resource Groups, see [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    -   <span data-ttu-id="7e626-120">**Resource Group Location:** This is required only if the API selected is global (not bound to a location).</span><span class="sxs-lookup"><span data-stu-id="7e626-120">**Resource Group Location:** This is required only if the API selected is global (not bound to a location).</span></span> <span data-ttu-id="7e626-121">If the API is global and not bound to a location, however, you must specify a location for the resource group where the metadata associated with the Cognitive Services API account will reside.</span><span class="sxs-lookup"><span data-stu-id="7e626-121">If the API is global and not bound to a location, however, you must specify a location for the resource group where the metadata associated with the Cognitive Services API account will reside.</span></span> <span data-ttu-id="7e626-122">This location will have no impact on the runtime availability of your account.</span><span class="sxs-lookup"><span data-stu-id="7e626-122">This location will have no impact on the runtime availability of your account.</span></span> <span data-ttu-id="7e626-123">To learn more about resource group, please refer to [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="7e626-123">To learn more about resource group, please refer to [Manage Azure resources through portal](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    -   <span data-ttu-id="7e626-124">**API Setting:** By default, account creation is disabled until your [Azure Account Administrator](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles) explicitly enables it.</span><span class="sxs-lookup"><span data-stu-id="7e626-124">**API Setting:** By default, account creation is disabled until your [Azure Account Administrator](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles) explicitly enables it.</span></span>

        <span data-ttu-id="7e626-125">This setting change will apply only to the currently selected API type and location or Resource group location on the panel to the left.</span><span class="sxs-lookup"><span data-stu-id="7e626-125">This setting change will apply only to the currently selected API type and location or Resource group location on the panel to the left.</span></span>

        ![Create Cognitive Services APIs account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/create-account.png)

        > [!NOTE]
        > <span data-ttu-id="7e626-127">If you receive a notification that the update setting failed, you are not logged in as an [Account Administrator](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#types-of-azure-admin-accounts).</span><span class="sxs-lookup"><span data-stu-id="7e626-127">If you receive a notification that the update setting failed, you are not logged in as an [Account Administrator](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#types-of-azure-admin-accounts).</span></span> <span data-ttu-id="7e626-128">The Account Administrator must follow the previous steps to enable creation.</span><span class="sxs-lookup"><span data-stu-id="7e626-128">The Account Administrator must follow the previous steps to enable creation.</span></span>
        >
        > ![Update setting failed message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/updatefailed.png)
        
        <span data-ttu-id="7e626-130">In some cases, the Account Administrator may not have access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="7e626-130">In some cases, the Account Administrator may not have access to the subscription.</span></span> <span data-ttu-id="7e626-131">If so, have the Service Administrator follow the steps in the [Add or change Azure administrator roles that manage the subscription or service](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator) document.</span><span class="sxs-lookup"><span data-stu-id="7e626-131">If so, have the Service Administrator follow the steps in the [Add or change Azure administrator roles that manage the subscription or service](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator) document.</span></span>
        
        <span data-ttu-id="7e626-132">To find the Account Administrator or Service Administrator for your subscription, select your subscription in the [Azure portal](https://portal.azure.com), and then select __Properties__.</span><span class="sxs-lookup"><span data-stu-id="7e626-132">To find the Account Administrator or Service Administrator for your subscription, select your subscription in the [Azure portal](https://portal.azure.com), and then select __Properties__.</span></span> <span data-ttu-id="7e626-133">The __Account Admin__ and __Service Admin__ information is displayed at the bottom of the properties blade.</span><span class="sxs-lookup"><span data-stu-id="7e626-133">The __Account Admin__ and __Service Admin__ information is displayed at the bottom of the properties blade.</span></span>
        
        ![Subscription properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/subscription-properties.png)
    
    <span data-ttu-id="7e626-135">Microsoft may use data you send to the Cognitive Services to improve Microsoft products and services.</span><span class="sxs-lookup"><span data-stu-id="7e626-135">Microsoft may use data you send to the Cognitive Services to improve Microsoft products and services.</span></span> <span data-ttu-id="7e626-136">For more information, please refer to the [Microsoft Cognitive Services section](http://www.microsoft.com/Licensing/product-licensing/products.aspx) in the Online Services Terms.</span><span class="sxs-lookup"><span data-stu-id="7e626-136">For more information, please refer to the [Microsoft Cognitive Services section](http://www.microsoft.com/Licensing/product-licensing/products.aspx) in the Online Services Terms.</span></span>

5. <span data-ttu-id="7e626-137">To pin the account to the Azure portal dashboard, click **Pin to Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="7e626-137">To pin the account to the Azure portal dashboard, click **Pin to Dashboard**.</span></span>

6. <span data-ttu-id="7e626-138">Click **Create** to create the account.</span><span class="sxs-lookup"><span data-stu-id="7e626-138">Click **Create** to create the account.</span></span>

<span data-ttu-id="7e626-139">After the Cognitive Services account is successfully deployed, click the tile in the dashboard to view the account information.</span><span class="sxs-lookup"><span data-stu-id="7e626-139">After the Cognitive Services account is successfully deployed, click the tile in the dashboard to view the account information.</span></span>

<span data-ttu-id="7e626-140">You can use the **Endpoint URL** in the **Overview** section and keys in the **Keys** section to start making API calls in your applications.</span><span class="sxs-lookup"><span data-stu-id="7e626-140">You can use the **Endpoint URL** in the **Overview** section and keys in the **Keys** section to start making API calls in your applications.</span></span>

![Display account information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/display-account.png)

![Display account keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/media/cognitive-services-apis-create-account/account-keys.png)

### <a name="next-steps"></a><span data-ttu-id="7e626-143">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7e626-143">Next Steps</span></span>

- <span data-ttu-id="7e626-144">For more information about all the Microsoft Cognitive Services available, see [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="7e626-144">For more information about all the Microsoft Cognitive Services available, see [Cognitive Services](https://azure.microsoft.com/services/cognitive-services/).</span></span>

- <span data-ttu-id="7e626-145">For quick start guides to using some example Cognitive Services APIs, see:</span><span class="sxs-lookup"><span data-stu-id="7e626-145">For quick start guides to using some example Cognitive Services APIs, see:</span></span>
    - [<span data-ttu-id="7e626-146">Getting started with the Text Analytics APIs to detect sentiment, key phrases, topics and language</span><span class="sxs-lookup"><span data-stu-id="7e626-146">Getting started with the Text Analytics APIs to detect sentiment, key phrases, topics and language</span></span>](cognitive-services-text-analytics-quick-start.md)
    - [<span data-ttu-id="7e626-147">Quick start guide for the Cognitive Services Recommendations API</span><span class="sxs-lookup"><span data-stu-id="7e626-147">Quick start guide for the Cognitive Services Recommendations API</span></span>](cognitive-services-recommendations-quick-start.md)






