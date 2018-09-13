---
title: (deprecated) Publish machine learning web service to Azure Marketplace | Microsoft Docs
description: (deprecated) How to publish your Azure Machine Learning Web Service to the Azure Marketplace
services: machine-learning
documentationcenter: ''
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: deprecated
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 4db4a52e467323aa8417db5df784d1316019d541
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554574"
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a><span data-ttu-id="2f6ec-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2f6ec-103">(deprecated) Publish Azure Machine Learning Web Service to the Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="2f6ec-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="2f6ec-105">As a result, this article is being deprecated.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="2f6ec-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="2f6ec-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="2f6ec-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="2f6ec-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-108">The Azure Marketplace provides the ability to publish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="2f6ec-109">This article provides an overview of that process with links to guidelines to get you started.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-109">This article provides an overview of that process with links to guidelines to get you started.</span></span> <span data-ttu-id="2f6ec-110">By using this process, you can make your web services available for other developers to consume in their applications.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-110">By using this process, you can make your web services available for other developers to consume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a><span data-ttu-id="2f6ec-111">Overview of the publishing process</span><span class="sxs-lookup"><span data-stu-id="2f6ec-111">Overview of the publishing process</span></span>
<span data-ttu-id="2f6ec-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="2f6ec-112">The following are the steps for publishing an Azure Machine Learning web service to Azure Marketplace:</span></span>

1. <span data-ttu-id="2f6ec-113">Create and publish a Machine Learning Request-Response service (RRS)</span><span class="sxs-lookup"><span data-stu-id="2f6ec-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="2f6ec-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-114">Deploy the service to production, and obtain the API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="2f6ec-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="2f6ec-115">Use the URL of the published web service to publish to [Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="2f6ec-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-116">Once submitted, your offer is reviewed and needs to be approved before your customers can start purchasing it.</span></span> <span data-ttu-id="2f6ec-117">The publishing process can take a few business days.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-117">The publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="2f6ec-118">Walk through</span><span class="sxs-lookup"><span data-stu-id="2f6ec-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="2f6ec-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span><span class="sxs-lookup"><span data-stu-id="2f6ec-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="2f6ec-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="2f6ec-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a><span data-ttu-id="2f6ec-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span><span class="sxs-lookup"><span data-stu-id="2f6ec-121">Step 2: Deploy the service to production, and obtain the API Key and OData endpoint information</span></span>
1. <span data-ttu-id="2f6ec-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-122">From the [Azure Classic Portal](http://manage.windowsazure.com), select the **MACHINE LEARNING** option from the left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="2f6ec-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-123">Click on the **WEB SERVICES** tab, and select the web service you would like to publish to the marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="2f6ec-125">Select the endpoint you would like to have the marketplace consume.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-125">Select the endpoint you would like to have the marketplace consume.</span></span> <span data-ttu-id="2f6ec-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-126">If you have not created any additional endpoints, you can select the **Default** endpoint.</span></span>
4. <span data-ttu-id="2f6ec-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-127">Once you have clicked on the endpoint, you will be able to see the **API KEY**.</span></span> <span data-ttu-id="2f6ec-128">You will need this piece of information later on in Step 3, so make a copy of it.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="2f6ec-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-130">Click on the **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services to the marketplace.</span></span> <span data-ttu-id="2f6ec-131">That will take you to the API help page for the Request/Response method.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-131">That will take you to the API help page for the Request/Response method.</span></span>
6. <span data-ttu-id="2f6ec-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-132">Copy the **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="2f6ec-134">deploy the service into production.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-134">deploy the service into production.</span></span>

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a><span data-ttu-id="2f6ec-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="2f6ec-135">Step 3: Use the URL of the published web service to publish to Azure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="2f6ec-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="2f6ec-136">Navigate to [Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="2f6ec-137">Click on the **Publish** link at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-137">Click on the **Publish** link at the top of the page.</span></span> <span data-ttu-id="2f6ec-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="2f6ec-138">This will take you to the [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="2f6ec-139">Click on the **publishers** section to register as a publisher.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-139">Click on the **publishers** section to register as a publisher.</span></span>
4. <span data-ttu-id="2f6ec-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="2f6ec-142">Under **Plans** provide information on your offering, including a pricing plan.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="2f6ec-143">Decide if you will offer a free or paid service.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="2f6ec-144">To get paid, provide payment information such as your bank and tax information.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-144">To get paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="2f6ec-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-145">Under **Marketing** provide information about your offer, such as the title and description for your offer.</span></span>
7. <span data-ttu-id="2f6ec-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-146">Under **Pricing** you can set the price for your plans for specific countries, or let the system "autoprice" your offer.</span></span>
8. <span data-ttu-id="2f6ec-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-147">On the **Data Service** tab, click **Web Service** as the **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="2f6ec-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-149">Get the web service URL and API key from the Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="2f6ec-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-150">In the Marketplace Data Service setup dialog box, paste the OData endpoint address into the **Service URL** text box.</span></span>
11. <span data-ttu-id="2f6ec-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-151">For **Authentication**, choose **Header** as the **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="2f6ec-152">Enter "Authorization" for the **Header Name**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-152">Enter "Authorization" for the **Header Name**.</span></span>
    * <span data-ttu-id="2f6ec-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-153">For the **Header Value**, enter "Bearer" (without the quotation marks), click the **Space** bar, and then paste the API key.</span></span>
    * <span data-ttu-id="2f6ec-154">Select the **This Service is OData** check box.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-154">Select the **This Service is OData** check box.</span></span>
    * <span data-ttu-id="2f6ec-155">Click **Test Connection** to test the connection.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-155">Click **Test Connection** to test the connection.</span></span>
12. <span data-ttu-id="2f6ec-156">Under **Categories**, ensure **Machine Learning** is selected.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="2f6ec-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-157">When you are done entering all the metadata about your offer, click on **Publish**, and then **Push to Staging**.</span></span> <span data-ttu-id="2f6ec-158">At this point, you will be notified of any remaining issues that you need to fix.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-158">At this point, you will be notified of any remaining issues that you need to fix.</span></span>
14. <span data-ttu-id="2f6ec-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-159">After you have ensured completion of all the outstanding issues, click on **Request approval to push to Production**.</span></span> <span data-ttu-id="2f6ec-160">The publishing process can take a few business days.</span><span class="sxs-lookup"><span data-stu-id="2f6ec-160">The publishing process can take a few business days.</span></span> 

[image1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-publish-web-service-to-azure-marketplace/odata.png






