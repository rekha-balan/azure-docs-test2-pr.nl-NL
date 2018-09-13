---
title: (deprecated) FAQ - Publish and use Machine Learning apps in Azure Marketplace | Microsoft Docs
description: (deprecated) Frequently asked questions about publishing Machine Learning apps in the Azure Marketplace
services: machine-learning
documentationcenter: ''
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 15e9b635974285813fc6c795f7c4e35ebd0631c5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670650"
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="64f49-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span><span class="sxs-lookup"><span data-stu-id="64f49-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="64f49-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span><span class="sxs-lookup"><span data-stu-id="64f49-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="64f49-105">As a result, this article is being deprecated.</span><span class="sxs-lookup"><span data-stu-id="64f49-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="64f49-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span><span class="sxs-lookup"><span data-stu-id="64f49-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="64f49-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="64f49-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="64f49-108">Questions about consuming from Marketplace</span><span class="sxs-lookup"><span data-stu-id="64f49-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="64f49-109">**1. Why do I get the following error message after I enter input for the web service:**</span><span class="sxs-lookup"><span data-stu-id="64f49-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="64f49-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span><span class="sxs-lookup"><span data-stu-id="64f49-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="64f49-111">Your input parameter(s) may not conform to the required format for the specific web service.</span><span class="sxs-lookup"><span data-stu-id="64f49-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="64f49-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span><span class="sxs-lookup"><span data-stu-id="64f49-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="64f49-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span><span class="sxs-lookup"><span data-stu-id="64f49-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="64f49-114">You should use your Marketplace account as the username and the primary account key as the password.</span><span class="sxs-lookup"><span data-stu-id="64f49-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="64f49-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span><span class="sxs-lookup"><span data-stu-id="64f49-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="64f49-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span><span class="sxs-lookup"><span data-stu-id="64f49-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="64f49-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span><span class="sxs-lookup"><span data-stu-id="64f49-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="64f49-118">**An unexpected error occurred while processing your request. Please try again.**</span><span class="sxs-lookup"><span data-stu-id="64f49-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="64f49-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span><span class="sxs-lookup"><span data-stu-id="64f49-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="64f49-120">The services can be called with a longer input length by using HTTP POST methods.</span><span class="sxs-lookup"><span data-stu-id="64f49-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="64f49-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="64f49-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="64f49-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span><span class="sxs-lookup"><span data-stu-id="64f49-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="64f49-123">This is a known issue with the Azure Classic Portal Marketplace.</span><span class="sxs-lookup"><span data-stu-id="64f49-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="64f49-124">The team is working to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="64f49-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="64f49-125">Questions about publishing from Azure Machine Learning on Marketplace</span><span class="sxs-lookup"><span data-stu-id="64f49-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="64f49-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span><span class="sxs-lookup"><span data-stu-id="64f49-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="64f49-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span><span class="sxs-lookup"><span data-stu-id="64f49-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="64f49-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span><span class="sxs-lookup"><span data-stu-id="64f49-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="64f49-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span><span class="sxs-lookup"><span data-stu-id="64f49-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="64f49-130">The team is working to resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="64f49-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="64f49-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="64f49-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="64f49-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="64f49-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="64f49-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span><span class="sxs-lookup"><span data-stu-id="64f49-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="64f49-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span><span class="sxs-lookup"><span data-stu-id="64f49-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="64f49-135">The support links are global per publisher, not per offer.</span><span class="sxs-lookup"><span data-stu-id="64f49-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="64f49-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="64f49-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="64f49-137">The batch input mode is currently not supported in Marketplace web services.</span><span class="sxs-lookup"><span data-stu-id="64f49-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="64f49-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span><span class="sxs-lookup"><span data-stu-id="64f49-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="64f49-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span><span class="sxs-lookup"><span data-stu-id="64f49-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

