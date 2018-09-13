---
title: Create, link, delete, or move an integration account in Azure logic apps | Microsoft Docs
description: How to create an integration account, and link it to your logic apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mandia
ms.openlocfilehash: 75eb0f5846cf1b3247a83c012a7965d42037c58b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556642"
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="dcaeb-103">What is an integration account?</span><span class="sxs-lookup"><span data-stu-id="dcaeb-103">What is an integration account?</span></span>

<span data-ttu-id="dcaeb-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="dcaeb-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="dcaeb-106">Create an integration account</span><span class="sxs-lookup"><span data-stu-id="dcaeb-106">Create an integration account</span></span>

1.  <span data-ttu-id="dcaeb-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="dcaeb-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="dcaeb-108">From the left menu, select **More services**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-108">From the left menu, select **More services**.</span></span>

    ![Select "More services"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="dcaeb-110">In the search box, type "integration" for your filter.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="dcaeb-111">In the results list, select **Integration Accounts**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-111">In the results list, select **Integration Accounts**.</span></span>

    ![Filter on "integration", select "Integration Accounts"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="dcaeb-113">At the top of the page, choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-113">At the top of the page, choose **Add**.</span></span>

    ![Choose Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="dcaeb-115">Name your integration account and select the Azure subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="dcaeb-116">You can either create a new **Resource group** or select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="dcaeb-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="dcaeb-118">When you're ready, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-118">When you're ready, choose **Create**.</span></span>

    ![Provide details for your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="dcaeb-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="dcaeb-121">Refresh the page.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-121">Refresh the page.</span></span> <span data-ttu-id="dcaeb-122">You see your new integration account listed.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-122">You see your new integration account listed.</span></span>

    ![Your new integration account appears](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="dcaeb-124">Next, link the integration account that you created to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="dcaeb-125">Link an integration account to a logic app</span><span class="sxs-lookup"><span data-stu-id="dcaeb-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="dcaeb-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dcaeb-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dcaeb-127">Prerequisites</span></span>

* <span data-ttu-id="dcaeb-128">An integration account</span><span class="sxs-lookup"><span data-stu-id="dcaeb-128">An integration account</span></span>
* <span data-ttu-id="dcaeb-129">A logic app</span><span class="sxs-lookup"><span data-stu-id="dcaeb-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="dcaeb-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="dcaeb-131">In the Azure portal, select your logic app, and check your logic app's location.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Select your logic app, check location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="dcaeb-133">Under **Settings**, select **Integration Account**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Select "Integration Account"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="dcaeb-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="dcaeb-136">To finish linking, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-136">To finish linking, choose **Save**.</span></span>

    ![Select your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="dcaeb-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Your logic app is linked to your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="dcaeb-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="dcaeb-141">Some common B2B connectors include XML validation and flat file encode/decode.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="dcaeb-142">Delete your integration account</span><span class="sxs-lookup"><span data-stu-id="dcaeb-142">Delete your integration account</span></span>

1. <span data-ttu-id="dcaeb-143">Select **More services**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-143">Select **More services**.</span></span>

    ![Select "More services"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="dcaeb-145">In the search box, type "integration" for your filter.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="dcaeb-146">In the results list, select **Integration Accounts**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-146">In the results list, select **Integration Accounts**.</span></span>

    ![Filter on "integration", select "Integration Accounts"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="dcaeb-148">Select the integration account that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-148">Select the integration account that you want to delete.</span></span>

    ![Select integration account to delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="dcaeb-150">On the menu, choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-150">On the menu, choose **Delete**.</span></span>

    ![Choose "Delete"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="dcaeb-152">Confirm your choice to delete the integration account.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="dcaeb-153">Move your integration account</span><span class="sxs-lookup"><span data-stu-id="dcaeb-153">Move your integration account</span></span>

<span data-ttu-id="dcaeb-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcaeb-155">You must update all scripts to use the new resource IDs after you move an integration account.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="dcaeb-156">Select **More services**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-156">Select **More services**.</span></span>

    ![Select "More services"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="dcaeb-158">In the search box, type "integration" for your filter.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="dcaeb-159">In the results list, select **Integration Accounts**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-159">In the results list, select **Integration Accounts**.</span></span>

    ![Filter on "integration", select "Integration Accounts"](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="dcaeb-161">Select the integration account that you want to move.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="dcaeb-162">Under **Settings**, choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-162">Under **Settings**, choose **Properties**.</span></span>

    ![Select integration account to move.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="dcaeb-165">Change the resource group or Azure subscription that's associated with your integration account.</span><span class="sxs-lookup"><span data-stu-id="dcaeb-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Choose Change resource group or Change subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="dcaeb-167">Next Steps</span><span class="sxs-lookup"><span data-stu-id="dcaeb-167">Next Steps</span></span>
* [<span data-ttu-id="dcaeb-168">Learn more about agreements</span><span class="sxs-lookup"><span data-stu-id="dcaeb-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  


















