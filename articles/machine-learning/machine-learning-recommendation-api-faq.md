---
title: Set up and use the Machine Learning Recommendations API | Microsoft Docs
description: Microsoft RECOMMENDATIONS API built with Azure Machine Learning FAQ
services: machine-learning
documentationcenter: ''
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: machine-learning-datamarket-deprecation
ms.openlocfilehash: cd9d1ddba3eb9da25ad74ca3567e69d6d720b595
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550302"
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="df9be-103">Setting up and using Machine Learning Recommendations API FAQ</span><span class="sxs-lookup"><span data-stu-id="df9be-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="df9be-104">**What is RECOMMENDATIONS?**</span><span class="sxs-lookup"><span data-stu-id="df9be-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="df9be-105">You should start using the Recommendations API Cognitive Service instead of this version.</span><span class="sxs-lookup"><span data-stu-id="df9be-105">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="df9be-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span><span class="sxs-lookup"><span data-stu-id="df9be-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="df9be-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span><span class="sxs-lookup"><span data-stu-id="df9be-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="df9be-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="df9be-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="df9be-109">For organizations and businesses that rely on recommendations to cross-sell and up-sell products and services to their customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span><span class="sxs-lookup"><span data-stu-id="df9be-109">For organizations and businesses that rely on recommendations to cross-sell and up-sell products and services to their customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="df9be-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span><span class="sxs-lookup"><span data-stu-id="df9be-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="df9be-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span><span class="sxs-lookup"><span data-stu-id="df9be-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="df9be-112">**What can I do with RECOMMENDATIONS?**</span><span class="sxs-lookup"><span data-stu-id="df9be-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="df9be-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span><span class="sxs-lookup"><span data-stu-id="df9be-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="df9be-114">For example: A customer of an online retailer clicks a product.</span><span class="sxs-lookup"><span data-stu-id="df9be-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="df9be-115">The online retailer sends that product as input to RECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown to the customer.</span><span class="sxs-lookup"><span data-stu-id="df9be-115">The online retailer sends that product as input to RECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown to the customer.</span></span> <span data-ttu-id="df9be-116">You may want to use RECOMMENDATIONS to optimize your online store or even to inform your inside sales department or call center.</span><span class="sxs-lookup"><span data-stu-id="df9be-116">You may want to use RECOMMENDATIONS to optimize your online store or even to inform your inside sales department or call center.</span></span>

<span data-ttu-id="df9be-117">**Are there any usage limitations?**</span><span class="sxs-lookup"><span data-stu-id="df9be-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="df9be-118">Recommendations has the following usage limitations:</span><span class="sxs-lookup"><span data-stu-id="df9be-118">Recommendations has the following usage limitations:</span></span>

* <span data-ttu-id="df9be-119">Maximum number of models per subscription: 10</span><span class="sxs-lookup"><span data-stu-id="df9be-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="df9be-120">Maximum number of items that a catalog can hold: 100,000</span><span class="sxs-lookup"><span data-stu-id="df9be-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="df9be-121">The maximum number of usage points that are kept is ~5,000,000.</span><span class="sxs-lookup"><span data-stu-id="df9be-121">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="df9be-122">The oldest will be deleted if new ones will be uploaded or reported.</span><span class="sxs-lookup"><span data-stu-id="df9be-122">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="df9be-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span><span class="sxs-lookup"><span data-stu-id="df9be-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="df9be-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span><span class="sxs-lookup"><span data-stu-id="df9be-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="df9be-125">A Recommendations model build that is active can hold up to 20 TPS.</span><span class="sxs-lookup"><span data-stu-id="df9be-125">A Recommendations model build that is active can hold up to 20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="df9be-126">Purchase and Billing</span><span class="sxs-lookup"><span data-stu-id="df9be-126">Purchase and Billing</span></span>
<span data-ttu-id="df9be-127">**How much does Recommendations cost during the launch period?**</span><span class="sxs-lookup"><span data-stu-id="df9be-127">**How much does Recommendations cost during the launch period?**</span></span>

<span data-ttu-id="df9be-128">Recommendations is a subscription-based service.</span><span class="sxs-lookup"><span data-stu-id="df9be-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="df9be-129">Charging is based on volume of transactions per month.</span><span class="sxs-lookup"><span data-stu-id="df9be-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="df9be-130">You can check the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span><span class="sxs-lookup"><span data-stu-id="df9be-130">You can check the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="df9be-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span><span class="sxs-lookup"><span data-stu-id="df9be-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="df9be-132">Not at the moment.</span><span class="sxs-lookup"><span data-stu-id="df9be-132">Not at the moment.</span></span>

<span data-ttu-id="df9be-133">**Does Recommendations have a free trial?**</span><span class="sxs-lookup"><span data-stu-id="df9be-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="df9be-134">There is a free trail which is restricted to 10,000 transactions per month.</span><span class="sxs-lookup"><span data-stu-id="df9be-134">There is a free trail which is restricted to 10,000 transactions per month.</span></span>

<span data-ttu-id="df9be-135">**When will I be billed for Recommendations?**</span><span class="sxs-lookup"><span data-stu-id="df9be-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="df9be-136">A paid subscription is any subscription for which there is a monthly fee.</span><span class="sxs-lookup"><span data-stu-id="df9be-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="df9be-137">When you purchase a paid subscription, you are immediately charged for the first month's use.</span><span class="sxs-lookup"><span data-stu-id="df9be-137">When you purchase a paid subscription, you are immediately charged for the first month's use.</span></span> <span data-ttu-id="df9be-138">You are charged the amount that is associated with the offer on the subscription page (plus applicable taxes).</span><span class="sxs-lookup"><span data-stu-id="df9be-138">You are charged the amount that is associated with the offer on the subscription page (plus applicable taxes).</span></span> <span data-ttu-id="df9be-139">This monthly charge is made each month on the same calendar date as your original purchase until you cancel the subscription.</span><span class="sxs-lookup"><span data-stu-id="df9be-139">This monthly charge is made each month on the same calendar date as your original purchase until you cancel the subscription.</span></span> 

<span data-ttu-id="df9be-140">**How do I upgrade to a higher tier service?**</span><span class="sxs-lookup"><span data-stu-id="df9be-140">**How do I upgrade to a higher tier service?**</span></span>

<span data-ttu-id="df9be-141">You can buy or update your subscription from the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="df9be-141">You can buy or update your subscription from the [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="df9be-142">When you upgrade a subscription:</span><span class="sxs-lookup"><span data-stu-id="df9be-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="df9be-143">Transactions that are remaining on your old subscription are not added to your new subscription.</span><span class="sxs-lookup"><span data-stu-id="df9be-143">Transactions that are remaining on your old subscription are not added to your new subscription.</span></span> 
* <span data-ttu-id="df9be-144">You pay full price for the new subscription, even though you have unused transactions on your old subscription.</span><span class="sxs-lookup"><span data-stu-id="df9be-144">You pay full price for the new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="df9be-145">Process to upgrade a subscription:</span><span class="sxs-lookup"><span data-stu-id="df9be-145">Process to upgrade a subscription:</span></span>

* <span data-ttu-id="df9be-146">Nevigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="df9be-146">Nevigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="df9be-147">Sign in to the Marketplace if you aren't already Signed in.</span><span class="sxs-lookup"><span data-stu-id="df9be-147">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="df9be-148">In the right pane, all the available plans are listed.</span><span class="sxs-lookup"><span data-stu-id="df9be-148">In the right pane, all the available plans are listed.</span></span> <span data-ttu-id="df9be-149">Click the radio button for the plan you want to upgrade to.</span><span class="sxs-lookup"><span data-stu-id="df9be-149">Click the radio button for the plan you want to upgrade to.</span></span>
* <span data-ttu-id="df9be-150">If you want to upgrade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="df9be-150">If you want to upgrade, click **OK**.</span></span> <span data-ttu-id="df9be-151">If you do not want to upgrade, click **Cancel**.</span><span class="sxs-lookup"><span data-stu-id="df9be-151">If you do not want to upgrade, click **Cancel**.</span></span>

<span data-ttu-id="df9be-152">**Important** Carefully read the dialog box before you upgrade because there are billing and use implications.</span><span class="sxs-lookup"><span data-stu-id="df9be-152">**Important** Carefully read the dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="df9be-153">**When will my subscription to Recommendations end?**</span><span class="sxs-lookup"><span data-stu-id="df9be-153">**When will my subscription to Recommendations end?**</span></span>

<span data-ttu-id="df9be-154">Your subscription will end when you cancel it.</span><span class="sxs-lookup"><span data-stu-id="df9be-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="df9be-155">If you would like to cancel your subscriptions, see the following instructions.</span><span class="sxs-lookup"><span data-stu-id="df9be-155">If you would like to cancel your subscriptions, see the following instructions.</span></span>

<span data-ttu-id="df9be-156">**How do I cancel my Recommendations subscription?**</span><span class="sxs-lookup"><span data-stu-id="df9be-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="df9be-157">To cancel your subscription, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="df9be-157">To cancel your subscription, use the following steps.</span></span> <span data-ttu-id="df9be-158">If your current subscription is a paid subscription, your subscription continues in effect until the end of the current billing period.</span><span class="sxs-lookup"><span data-stu-id="df9be-158">If your current subscription is a paid subscription, your subscription continues in effect until the end of the current billing period.</span></span> <span data-ttu-id="df9be-159">If you need the cancellation to be effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="df9be-159">If you need the cancellation to be effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="df9be-160">**Note** No refund is given if you cancel before the end of a billing period or for unused transactions in a billing period.</span><span class="sxs-lookup"><span data-stu-id="df9be-160">**Note** No refund is given if you cancel before the end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="df9be-161">Navigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="df9be-161">Navigate to the [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="df9be-162">Sign in to the Marketplace if you aren't already Signed in.</span><span class="sxs-lookup"><span data-stu-id="df9be-162">Sign in to the Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="df9be-163">Click **Cancel** to the right of the dataset name and status.</span><span class="sxs-lookup"><span data-stu-id="df9be-163">Click **Cancel** to the right of the dataset name and status.</span></span> <span data-ttu-id="df9be-164">You can use this subscription until the end of the current billing period or your transaction limit is reached (whichever occurs first).</span><span class="sxs-lookup"><span data-stu-id="df9be-164">You can use this subscription until the end of the current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="df9be-165">If you would like to cancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="df9be-165">If you would like to cancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="df9be-166">Getting started with Recommendations</span><span class="sxs-lookup"><span data-stu-id="df9be-166">Getting started with Recommendations</span></span>
<span data-ttu-id="df9be-167">**Is Recommendations for me?**</span><span class="sxs-lookup"><span data-stu-id="df9be-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="df9be-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations to cross-sell and up-sell products or services to their customers.</span><span class="sxs-lookup"><span data-stu-id="df9be-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations to cross-sell and up-sell products or services to their customers.</span></span> <span data-ttu-id="df9be-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span><span class="sxs-lookup"><span data-stu-id="df9be-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="df9be-170">Experimenting with Recommendations is designed to be fairly simple.</span><span class="sxs-lookup"><span data-stu-id="df9be-170">Experimenting with Recommendations is designed to be fairly simple.</span></span> <span data-ttu-id="df9be-171">The current API-based version requires basic programming skills.</span><span class="sxs-lookup"><span data-stu-id="df9be-171">The current API-based version requires basic programming skills.</span></span> <span data-ttu-id="df9be-172">If you need assistance, contact the vendor who developed your website.</span><span class="sxs-lookup"><span data-stu-id="df9be-172">If you need assistance, contact the vendor who developed your website.</span></span> <span data-ttu-id="df9be-173">If you have an internal IT department or an in-house developer, they should be able to get Recommendations to work for you.</span><span class="sxs-lookup"><span data-stu-id="df9be-173">If you have an internal IT department or an in-house developer, they should be able to get Recommendations to work for you.</span></span> 

<span data-ttu-id="df9be-174">**What are the prerequisites for setting up Recommendations?**</span><span class="sxs-lookup"><span data-stu-id="df9be-174">**What are the prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="df9be-175">Recommendations requires that you have a log of user choices as it relates to your catalog.</span><span class="sxs-lookup"><span data-stu-id="df9be-175">Recommendations requires that you have a log of user choices as it relates to your catalog.</span></span> <span data-ttu-id="df9be-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span><span class="sxs-lookup"><span data-stu-id="df9be-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="df9be-177">Recommendations also requires a catalog of your products or services.</span><span class="sxs-lookup"><span data-stu-id="df9be-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="df9be-178">If you don't have the catalog, Recommendations can use the actual customer usage data and distill a catalog.</span><span class="sxs-lookup"><span data-stu-id="df9be-178">If you don't have the catalog, Recommendations can use the actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="df9be-179">An implied catalog will not include items that were not reported as part of user transactions.</span><span class="sxs-lookup"><span data-stu-id="df9be-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="df9be-180">**How do I set up Recommendations for the first time?**</span><span class="sxs-lookup"><span data-stu-id="df9be-180">**How do I set up Recommendations for the first time?**</span></span>

<span data-ttu-id="df9be-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) to Recommendations, you should use the API documentation in the [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) to set up the service.</span><span class="sxs-lookup"><span data-stu-id="df9be-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) to Recommendations, you should use the API documentation in the [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) to set up the service.</span></span>

<span data-ttu-id="df9be-182">**Where can I find API documentation?**</span><span class="sxs-lookup"><span data-stu-id="df9be-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="df9be-183">The API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="df9be-183">The API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="df9be-184">**What options do I have to upload catalog and usage data to Recommendations?**</span><span class="sxs-lookup"><span data-stu-id="df9be-184">**What options do I have to upload catalog and usage data to Recommendations?**</span></span>

<span data-ttu-id="df9be-185">You have two options for uploading your catalog and usage data: You can export the data from your CRM system or other logs and upload it to Recommendations, or you can add tags to your website that will track user activities.</span><span class="sxs-lookup"><span data-stu-id="df9be-185">You have two options for uploading your catalog and usage data: You can export the data from your CRM system or other logs and upload it to Recommendations, or you can add tags to your website that will track user activities.</span></span> <span data-ttu-id="df9be-186">If you use the latter method, the data will be stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="df9be-186">If you use the latter method, the data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="df9be-187">Maintenance and support</span><span class="sxs-lookup"><span data-stu-id="df9be-187">Maintenance and support</span></span>
<span data-ttu-id="df9be-188">**How large can my data set be?**</span><span class="sxs-lookup"><span data-stu-id="df9be-188">**How large can my data set be?**</span></span>

<span data-ttu-id="df9be-189">Each data set can contain up to 100,000 catalog items and up to 2048 MB of usage data.</span><span class="sxs-lookup"><span data-stu-id="df9be-189">Each data set can contain up to 100,000 catalog items and up to 2048 MB of usage data.</span></span>
<span data-ttu-id="df9be-190">In addition, a subscription can contain up to 10 data sets (models).</span><span class="sxs-lookup"><span data-stu-id="df9be-190">In addition, a subscription can contain up to 10 data sets (models).</span></span>

<span data-ttu-id="df9be-191">**Where can I get technical support for Recommendations?**</span><span class="sxs-lookup"><span data-stu-id="df9be-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="df9be-192">Technical support is available on the [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span><span class="sxs-lookup"><span data-stu-id="df9be-192">Technical support is available on the [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="df9be-193">**Where can I find the terms of use?**</span><span class="sxs-lookup"><span data-stu-id="df9be-193">**Where can I find the terms of use?**</span></span>

<span data-ttu-id="df9be-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="df9be-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

