---
title: Testing your Data Service offer for the Marketplace | Microsoft Docs
description: Understand how to test your Data Service offer for the Azure Marketplace.
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: c2e0e8eb270ab53f137e6c95b9f4e6bdb2964481
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553568"
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="f9bb7-103">Testing your Data Service offer in Staging</span><span class="sxs-lookup"><span data-stu-id="f9bb7-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f9bb7-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span><span class="sxs-lookup"><span data-stu-id="f9bb7-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="f9bb7-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="f9bb7-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="f9bb7-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="f9bb7-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="f9bb7-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-107">After completing the first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in the Azure Marketplace.</span></span> <span data-ttu-id="f9bb7-108">This topic will walk you through the first, intermediate, step called “Staging”</span><span class="sxs-lookup"><span data-stu-id="f9bb7-108">This topic will walk you through the first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="f9bb7-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="f9bb7-110">The offer will appear in staging just as it would to a customer who has deployed it.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-110">The offer will appear in staging just as it would to a customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-to-staging"></a><span data-ttu-id="f9bb7-111">Step 1.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-111">Step 1.</span></span> <span data-ttu-id="f9bb7-112">Pushing your offer to staging</span><span class="sxs-lookup"><span data-stu-id="f9bb7-112">Pushing your offer to staging</span></span>
<span data-ttu-id="f9bb7-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-113">Pushing your offer to staging allows you to test the offer before it becomes available to future subscribers.</span></span>  <span data-ttu-id="f9bb7-114">You can see how your offer will appear and function for those subscribing to your data.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-114">You can see how your offer will appear and function for those subscribing to your data.</span></span>  

  ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="f9bb7-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="f9bb7-116">Login into the [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="f9bb7-117">Select **Data Services** in the left navigation window</span><span class="sxs-lookup"><span data-stu-id="f9bb7-117">Select **Data Services** in the left navigation window</span></span>
3. <span data-ttu-id="f9bb7-118">Select your offer you want to push to staging.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-118">Select your offer you want to push to staging.</span></span> <span data-ttu-id="f9bb7-119">You will see the above screen.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-119">You will see the above screen.</span></span>
4. <span data-ttu-id="f9bb7-120">Click **Push To Staging** button.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-120">Click **Push To Staging** button.</span></span>  
5. <span data-ttu-id="f9bb7-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-121">If there are issues with the offer that needed to be completed prior to pushing to staging, you will see a list displayed.</span></span>  <span data-ttu-id="f9bb7-122">Correct these items by clicking on each item in the list.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-122">Correct these items by clicking on each item in the list.</span></span> <span data-ttu-id="f9bb7-123">When all corrections made, click **Push to Staging** button again.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-123">When all corrections made, click **Push to Staging** button again.</span></span>

<span data-ttu-id="f9bb7-124">If there are no issues with your offer you will see the popup window below.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-124">If there are no issues with your offer you will see the popup window below.</span></span>  

<span data-ttu-id="f9bb7-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-125">If you’re not planning/not approved to surface your offer in Azure Portal (currently has limited capacity), then just close the pop-up window.</span></span>

<span data-ttu-id="f9bb7-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-126">To test your Data Service in Azure Portal (in addition to the DataMarket portal), you will need an Azure Subscription ID to test with.</span></span>  <span data-ttu-id="f9bb7-127">This Subscription ID will identify the account that will be allowed to test your offer.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-127">This Subscription ID will identify the account that will be allowed to test your offer.</span></span>  

<span data-ttu-id="f9bb7-128">Cut and paste your Subscription ID and click the checkmark to continue.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-128">Cut and paste your Subscription ID and click the checkmark to continue.</span></span>

  ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="f9bb7-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f9bb7-130">These Azure subscriptions IDs are only required for testing and staging in the [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="f9bb7-131">They are not required to test in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-131">They are not required to test in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="f9bb7-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-132">The next screen that appears shows that publishing is taking place by displaying the “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="f9bb7-133">Pushing to staging takes between 10 to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-133">Pushing to staging takes between 10 to 15 minutes.</span></span>  <span data-ttu-id="f9bb7-134">If it takes longer, first refresh your browser (press F5 in IE).</span><span class="sxs-lookup"><span data-stu-id="f9bb7-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="f9bb7-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-135">In the rare cases where your offer is still pushing to staging after an hour, click the contact us link to let us know that there is an issue.</span></span>

  ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="f9bb7-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-137">When the Push to Staging completes the “In progress” icon will stop moving and the status will be updated to “Staged”.</span></span>  <span data-ttu-id="f9bb7-138">You are now ready to test your offer.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-138">You are now ready to test your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="f9bb7-139">Step 2.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-139">Step 2.</span></span> <span data-ttu-id="f9bb7-140">Test your staged offer in DataMarket</span><span class="sxs-lookup"><span data-stu-id="f9bb7-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="f9bb7-141">Click the link following the text **“See Your service offer at…”**</span><span class="sxs-lookup"><span data-stu-id="f9bb7-141">Click the link following the text **“See Your service offer at…”**</span></span> <span data-ttu-id="f9bb7-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-142">to display the screen that the subscriber will see when your offer goes to production and will appear in DataMarket.</span></span>

  ![drawing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="f9bb7-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-144">Test or verify each of the 12 items marked above to ensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="f9bb7-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-145">This is a good time to ensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="f9bb7-146">Offer logo</span><span class="sxs-lookup"><span data-stu-id="f9bb7-146">Offer logo</span></span>
2. <span data-ttu-id="f9bb7-147">Offer name</span><span class="sxs-lookup"><span data-stu-id="f9bb7-147">Offer name</span></span>
3. <span data-ttu-id="f9bb7-148">Publisher name/link to your company's website</span><span class="sxs-lookup"><span data-stu-id="f9bb7-148">Publisher name/link to your company's website</span></span>
4. <span data-ttu-id="f9bb7-149">Search categories for your offer</span><span class="sxs-lookup"><span data-stu-id="f9bb7-149">Search categories for your offer</span></span>
5. <span data-ttu-id="f9bb7-150">Your offer's support link to assist subscribers</span><span class="sxs-lookup"><span data-stu-id="f9bb7-150">Your offer's support link to assist subscribers</span></span>
6. <span data-ttu-id="f9bb7-151">Contextual description for your offer</span><span class="sxs-lookup"><span data-stu-id="f9bb7-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="f9bb7-152">Offer plan depicting billing details</span><span class="sxs-lookup"><span data-stu-id="f9bb7-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="f9bb7-153">Link to implementation code</span><span class="sxs-lookup"><span data-stu-id="f9bb7-153">Link to implementation code</span></span>
9. <span data-ttu-id="f9bb7-154">Sample images that illustrate use of offer data</span><span class="sxs-lookup"><span data-stu-id="f9bb7-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="f9bb7-155">Input/Output metadata for each service within the offer</span><span class="sxs-lookup"><span data-stu-id="f9bb7-155">Input/Output metadata for each service within the offer</span></span>
11. <span data-ttu-id="f9bb7-156">Offer's Terms of Use</span><span class="sxs-lookup"><span data-stu-id="f9bb7-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="f9bb7-157">Preview of the offer's data</span><span class="sxs-lookup"><span data-stu-id="f9bb7-157">Preview of the offer's data</span></span>

<span data-ttu-id="f9bb7-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-158">Finally, check the service will work through the Datamarket by clicking the link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="f9bb7-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-159">A new window will open in the tool we call “Service Explorer” so you can preview the results of a query against your service.</span></span>  <span data-ttu-id="f9bb7-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-160">In this window, you can enter the parameters needed and see the results displayed from a query against your service.</span></span>   <span data-ttu-id="f9bb7-161">Also, displayed is the URL for your Query.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-161">Also, displayed is the URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="f9bb7-162">Be sure to review the textual description of the service displayed at the top.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-162">Be sure to review the textual description of the service displayed at the top.</span></span>  <span data-ttu-id="f9bb7-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-163">And if your offer consists of more than one service call, click the tabs at the bottom to switch to the next service to review and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="f9bb7-164">Next step</span><span class="sxs-lookup"><span data-stu-id="f9bb7-164">Next step</span></span>
<span data-ttu-id="f9bb7-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="f9bb7-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="f9bb7-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-166">If you are satisfied and ready to publish your offer please read the [Request Approval to Push To Production](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9bb7-167">See Also</span><span class="sxs-lookup"><span data-stu-id="f9bb7-167">See Also</span></span>
* [<span data-ttu-id="f9bb7-168">Getting Started: How to publish an offer to the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f9bb7-168">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)





