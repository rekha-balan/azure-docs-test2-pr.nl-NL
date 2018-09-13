---
title: 'Quick start: Azure Machine Learning Recommendations API (ver. 1)| Microsoft Docs'
description: Azure Machine Learning Recommendations - Quick Start Guide
services: machine-learning
documentationcenter: ''
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: machine-learning-datamarket-deprecation
ms.openlocfilehash: 21cf8b726ffd9b05f771c8ac6480140a6ed3199e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540696"
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="133e9-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span><span class="sxs-lookup"><span data-stu-id="133e9-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="133e9-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span><span class="sxs-lookup"><span data-stu-id="133e9-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="133e9-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span><span class="sxs-lookup"><span data-stu-id="133e9-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="133e9-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span><span class="sxs-lookup"><span data-stu-id="133e9-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="133e9-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="133e9-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="133e9-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span><span class="sxs-lookup"><span data-stu-id="133e9-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="133e9-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="133e9-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="133e9-111">General overview</span><span class="sxs-lookup"><span data-stu-id="133e9-111">General overview</span></span>
<span data-ttu-id="133e9-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span><span class="sxs-lookup"><span data-stu-id="133e9-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="133e9-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span><span class="sxs-lookup"><span data-stu-id="133e9-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="133e9-114">Import catalog data - A catalog contains metadata information on the items.</span><span class="sxs-lookup"><span data-stu-id="133e9-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="133e9-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span><span class="sxs-lookup"><span data-stu-id="133e9-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="133e9-116">By uploading a file that contains the usage data.</span><span class="sxs-lookup"><span data-stu-id="133e9-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="133e9-117">By sending data acquisition events.</span><span class="sxs-lookup"><span data-stu-id="133e9-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="133e9-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span><span class="sxs-lookup"><span data-stu-id="133e9-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="133e9-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span><span class="sxs-lookup"><span data-stu-id="133e9-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="133e9-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span><span class="sxs-lookup"><span data-stu-id="133e9-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="133e9-121">When triggering the build, you will get a build ID.</span><span class="sxs-lookup"><span data-stu-id="133e9-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="133e9-122">Use it to check when the build process has ended before starting to consume recommendations.</span><span class="sxs-lookup"><span data-stu-id="133e9-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="133e9-123">Consume recommendations - Get recommendations for a specific item or list of items.</span><span class="sxs-lookup"><span data-stu-id="133e9-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="133e9-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span><span class="sxs-lookup"><span data-stu-id="133e9-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="133e9-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="133e9-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="133e9-126">Limitations</span><span class="sxs-lookup"><span data-stu-id="133e9-126">Limitations</span></span>
* <span data-ttu-id="133e9-127">The maximum number of models per subscription is 10.</span><span class="sxs-lookup"><span data-stu-id="133e9-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="133e9-128">The maximum number of items that a catalog can hold is 100,000.</span><span class="sxs-lookup"><span data-stu-id="133e9-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="133e9-129">The maximum number of usage points that are kept is ~5,000,000.</span><span class="sxs-lookup"><span data-stu-id="133e9-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="133e9-130">The oldest will be deleted if new ones will be uploaded or reported.</span><span class="sxs-lookup"><span data-stu-id="133e9-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="133e9-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span><span class="sxs-lookup"><span data-stu-id="133e9-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="133e9-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span><span class="sxs-lookup"><span data-stu-id="133e9-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="133e9-133">A recommendation model build that is active can hold up to 20TPS.</span><span class="sxs-lookup"><span data-stu-id="133e9-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="133e9-134">Integration</span><span class="sxs-lookup"><span data-stu-id="133e9-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="133e9-135">Authentication</span><span class="sxs-lookup"><span data-stu-id="133e9-135">Authentication</span></span>
<span data-ttu-id="133e9-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span><span class="sxs-lookup"><span data-stu-id="133e9-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="133e9-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="133e9-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="133e9-138">Basic Authentication</span><span class="sxs-lookup"><span data-stu-id="133e9-138">Basic Authentication</span></span>
<span data-ttu-id="133e9-139">Add the Authorization header:</span><span class="sxs-lookup"><span data-stu-id="133e9-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="133e9-140">Convert to Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="133e9-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="133e9-141">Convert to Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="133e9-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="133e9-142">Service URI</span><span class="sxs-lookup"><span data-stu-id="133e9-142">Service URI</span></span>
<span data-ttu-id="133e9-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="133e9-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="133e9-144">The full service URI is expressed using elements of the OData specification.</span><span class="sxs-lookup"><span data-stu-id="133e9-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="133e9-145">API version</span><span class="sxs-lookup"><span data-stu-id="133e9-145">API version</span></span>
<span data-ttu-id="133e9-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span><span class="sxs-lookup"><span data-stu-id="133e9-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="133e9-147">IDs are case-sensitive</span><span class="sxs-lookup"><span data-stu-id="133e9-147">IDs are case-sensitive</span></span>
<span data-ttu-id="133e9-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span><span class="sxs-lookup"><span data-stu-id="133e9-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="133e9-149">For instance, model IDs and catalog IDs are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="133e9-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="133e9-150">Create a model</span><span class="sxs-lookup"><span data-stu-id="133e9-150">Create a model</span></span>
<span data-ttu-id="133e9-151">Creating a "create model" request:</span><span class="sxs-lookup"><span data-stu-id="133e9-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="133e9-152">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-152">HTTP Method</span></span> | <span data-ttu-id="133e9-153">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-154">POST</span><span class="sxs-lookup"><span data-stu-id="133e9-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-155">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-156">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-156">Parameter Name</span></span> | <span data-ttu-id="133e9-157">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-158">modelName</span><span class="sxs-lookup"><span data-stu-id="133e9-158">modelName</span></span> |<span data-ttu-id="133e9-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span><span class="sxs-lookup"><span data-stu-id="133e9-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="133e9-160">Max length: 20</span><span class="sxs-lookup"><span data-stu-id="133e9-160">Max length: 20</span></span> |
| <span data-ttu-id="133e9-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-161">apiVersion</span></span> |<span data-ttu-id="133e9-162">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-162">1.0</span></span> |
|  | |
| <span data-ttu-id="133e9-163">Request Body</span><span class="sxs-lookup"><span data-stu-id="133e9-163">Request Body</span></span> |<span data-ttu-id="133e9-164">NONE</span><span class="sxs-lookup"><span data-stu-id="133e9-164">NONE</span></span> |

<span data-ttu-id="133e9-165">**Response**:</span><span class="sxs-lookup"><span data-stu-id="133e9-165">**Response**:</span></span>

<span data-ttu-id="133e9-166">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="133e9-167">`feed/entry/content/properties/id` - Contains the model ID.</span><span class="sxs-lookup"><span data-stu-id="133e9-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="133e9-168">Note that the model ID is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="133e9-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="133e9-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="133e9-170">Import catalog data</span><span class="sxs-lookup"><span data-stu-id="133e9-170">Import catalog data</span></span>
<span data-ttu-id="133e9-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span><span class="sxs-lookup"><span data-stu-id="133e9-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="133e9-172">Existing items will remain with the original values.</span><span class="sxs-lookup"><span data-stu-id="133e9-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="133e9-173">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-173">HTTP Method</span></span> | <span data-ttu-id="133e9-174">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-175">POST</span><span class="sxs-lookup"><span data-stu-id="133e9-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-176">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-177">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-177">Parameter Name</span></span> | <span data-ttu-id="133e9-178">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-179">modelId</span><span class="sxs-lookup"><span data-stu-id="133e9-179">modelId</span></span> |<span data-ttu-id="133e9-180">Unique identifier of the model (case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="133e9-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="133e9-181">filename</span><span class="sxs-lookup"><span data-stu-id="133e9-181">filename</span></span> |<span data-ttu-id="133e9-182">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="133e9-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="133e9-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span><span class="sxs-lookup"><span data-stu-id="133e9-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="133e9-184">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="133e9-184">Max length: 50</span></span> |
| <span data-ttu-id="133e9-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-185">apiVersion</span></span> |<span data-ttu-id="133e9-186">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-186">1.0</span></span> |
|  | |
| <span data-ttu-id="133e9-187">Request Body</span><span class="sxs-lookup"><span data-stu-id="133e9-187">Request Body</span></span> |<span data-ttu-id="133e9-188">Catalog data.</span><span class="sxs-lookup"><span data-stu-id="133e9-188">Catalog data.</span></span> <span data-ttu-id="133e9-189">Format:</span><span class="sxs-lookup"><span data-stu-id="133e9-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="133e9-190">Name</span><span class="sxs-lookup"><span data-stu-id="133e9-190">Name</span></span></th><th><span data-ttu-id="133e9-191">Mandatory</span><span class="sxs-lookup"><span data-stu-id="133e9-191">Mandatory</span></span></th><th><span data-ttu-id="133e9-192">Type</span><span class="sxs-lookup"><span data-stu-id="133e9-192">Type</span></span></th><th><span data-ttu-id="133e9-193">Description</span><span class="sxs-lookup"><span data-stu-id="133e9-193">Description</span></span></th></tr><tr><td><span data-ttu-id="133e9-194">Item Id</span><span class="sxs-lookup"><span data-stu-id="133e9-194">Item Id</span></span></td><td><span data-ttu-id="133e9-195">Yes</span><span class="sxs-lookup"><span data-stu-id="133e9-195">Yes</span></span></td><td><span data-ttu-id="133e9-196">Alphanumeric, max length 50</span><span class="sxs-lookup"><span data-stu-id="133e9-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="133e9-197">Unique identifier of an item</span><span class="sxs-lookup"><span data-stu-id="133e9-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="133e9-198">Item Name</span><span class="sxs-lookup"><span data-stu-id="133e9-198">Item Name</span></span></td><td><span data-ttu-id="133e9-199">Yes</span><span class="sxs-lookup"><span data-stu-id="133e9-199">Yes</span></span></td><td><span data-ttu-id="133e9-200">Alphanumeric, max length 255</span><span class="sxs-lookup"><span data-stu-id="133e9-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="133e9-201">Item name</span><span class="sxs-lookup"><span data-stu-id="133e9-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="133e9-202">Item Category</span><span class="sxs-lookup"><span data-stu-id="133e9-202">Item Category</span></span></td><td><span data-ttu-id="133e9-203">Yes</span><span class="sxs-lookup"><span data-stu-id="133e9-203">Yes</span></span></td><td><span data-ttu-id="133e9-204">Alphanumeric, max length 255</span><span class="sxs-lookup"><span data-stu-id="133e9-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="133e9-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span><span class="sxs-lookup"><span data-stu-id="133e9-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="133e9-206">Description</span><span class="sxs-lookup"><span data-stu-id="133e9-206">Description</span></span></td><td><span data-ttu-id="133e9-207">No</span><span class="sxs-lookup"><span data-stu-id="133e9-207">No</span></span></td><td><span data-ttu-id="133e9-208">Alphanumeric, max length 4000</span><span class="sxs-lookup"><span data-stu-id="133e9-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="133e9-209">Description of this item</span><span class="sxs-lookup"><span data-stu-id="133e9-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="133e9-210">Maximum file size is 200MB.</span><span class="sxs-lookup"><span data-stu-id="133e9-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="133e9-211">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="133e9-212">**Response**:</span><span class="sxs-lookup"><span data-stu-id="133e9-212">**Response**:</span></span>

<span data-ttu-id="133e9-213">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="133e9-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span><span class="sxs-lookup"><span data-stu-id="133e9-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="133e9-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span><span class="sxs-lookup"><span data-stu-id="133e9-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="133e9-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="133e9-217">Import usage data</span><span class="sxs-lookup"><span data-stu-id="133e9-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="133e9-218">Uploading a file</span><span class="sxs-lookup"><span data-stu-id="133e9-218">Uploading a file</span></span>
<span data-ttu-id="133e9-219">This section shows how to upload usage data by using a file.</span><span class="sxs-lookup"><span data-stu-id="133e9-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="133e9-220">You can call this API several times with usage data.</span><span class="sxs-lookup"><span data-stu-id="133e9-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="133e9-221">All usage data will be saved for all calls.</span><span class="sxs-lookup"><span data-stu-id="133e9-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="133e9-222">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-222">HTTP Method</span></span> | <span data-ttu-id="133e9-223">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-224">POST</span><span class="sxs-lookup"><span data-stu-id="133e9-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-225">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-226">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-226">Parameter Name</span></span> | <span data-ttu-id="133e9-227">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-228">modelId</span><span class="sxs-lookup"><span data-stu-id="133e9-228">modelId</span></span> |<span data-ttu-id="133e9-229">Unique identifier of the model (case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="133e9-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="133e9-230">filename</span><span class="sxs-lookup"><span data-stu-id="133e9-230">filename</span></span> |<span data-ttu-id="133e9-231">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="133e9-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="133e9-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span><span class="sxs-lookup"><span data-stu-id="133e9-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="133e9-233">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="133e9-233">Max length: 50</span></span> |
| <span data-ttu-id="133e9-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-234">apiVersion</span></span> |<span data-ttu-id="133e9-235">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-235">1.0</span></span> |
|  | |
| <span data-ttu-id="133e9-236">Request Body</span><span class="sxs-lookup"><span data-stu-id="133e9-236">Request Body</span></span> |<span data-ttu-id="133e9-237">Usage data.</span><span class="sxs-lookup"><span data-stu-id="133e9-237">Usage data.</span></span> <span data-ttu-id="133e9-238">Format:</span><span class="sxs-lookup"><span data-stu-id="133e9-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="133e9-239">Name</span><span class="sxs-lookup"><span data-stu-id="133e9-239">Name</span></span></th><th><span data-ttu-id="133e9-240">Mandatory</span><span class="sxs-lookup"><span data-stu-id="133e9-240">Mandatory</span></span></th><th><span data-ttu-id="133e9-241">Type</span><span class="sxs-lookup"><span data-stu-id="133e9-241">Type</span></span></th><th><span data-ttu-id="133e9-242">Description</span><span class="sxs-lookup"><span data-stu-id="133e9-242">Description</span></span></th></tr><tr><td><span data-ttu-id="133e9-243">User Id</span><span class="sxs-lookup"><span data-stu-id="133e9-243">User Id</span></span></td><td><span data-ttu-id="133e9-244">Yes</span><span class="sxs-lookup"><span data-stu-id="133e9-244">Yes</span></span></td><td><span data-ttu-id="133e9-245">Alphanumeric</span><span class="sxs-lookup"><span data-stu-id="133e9-245">Alphanumeric</span></span></td><td><span data-ttu-id="133e9-246">Unique identifier of a user</span><span class="sxs-lookup"><span data-stu-id="133e9-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="133e9-247">Item Id</span><span class="sxs-lookup"><span data-stu-id="133e9-247">Item Id</span></span></td><td><span data-ttu-id="133e9-248">Yes</span><span class="sxs-lookup"><span data-stu-id="133e9-248">Yes</span></span></td><td><span data-ttu-id="133e9-249">Alphanumeric, max length 50</span><span class="sxs-lookup"><span data-stu-id="133e9-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="133e9-250">Unique identifier of an item</span><span class="sxs-lookup"><span data-stu-id="133e9-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="133e9-251">Time</span><span class="sxs-lookup"><span data-stu-id="133e9-251">Time</span></span></td><td><span data-ttu-id="133e9-252">No</span><span class="sxs-lookup"><span data-stu-id="133e9-252">No</span></span></td><td><span data-ttu-id="133e9-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="133e9-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="133e9-254">Time of data</span><span class="sxs-lookup"><span data-stu-id="133e9-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="133e9-255">Event</span><span class="sxs-lookup"><span data-stu-id="133e9-255">Event</span></span></td><td><span data-ttu-id="133e9-256">No, if supplied then must also put date</span><span class="sxs-lookup"><span data-stu-id="133e9-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="133e9-257">One of the following:</span><span class="sxs-lookup"><span data-stu-id="133e9-257">One of the following:</span></span><br><span data-ttu-id="133e9-258">• Click</span><span class="sxs-lookup"><span data-stu-id="133e9-258">• Click</span></span><br><span data-ttu-id="133e9-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="133e9-259">• RecommendationClick</span></span><br><span data-ttu-id="133e9-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="133e9-260">•    AddShopCart</span></span><br><span data-ttu-id="133e9-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="133e9-261">• RemoveShopCart</span></span><br><span data-ttu-id="133e9-262">• Purchase</span><span class="sxs-lookup"><span data-stu-id="133e9-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="133e9-263">Maximum file size is 200MB.</span><span class="sxs-lookup"><span data-stu-id="133e9-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="133e9-264">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="133e9-265">**Response**:</span><span class="sxs-lookup"><span data-stu-id="133e9-265">**Response**:</span></span>

<span data-ttu-id="133e9-266">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="133e9-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span><span class="sxs-lookup"><span data-stu-id="133e9-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="133e9-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span><span class="sxs-lookup"><span data-stu-id="133e9-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="133e9-269">`Feed\entry\content\properties\FileId` - File identifier.</span><span class="sxs-lookup"><span data-stu-id="133e9-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="133e9-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="133e9-271">Using data acquisition</span><span class="sxs-lookup"><span data-stu-id="133e9-271">Using data acquisition</span></span>
<span data-ttu-id="133e9-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span><span class="sxs-lookup"><span data-stu-id="133e9-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="133e9-273">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-273">HTTP Method</span></span> | <span data-ttu-id="133e9-274">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-275">POST</span><span class="sxs-lookup"><span data-stu-id="133e9-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-276">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-276">Parameter Name</span></span> | <span data-ttu-id="133e9-277">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-278">apiVersion</span></span> |<span data-ttu-id="133e9-279">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-279">1.0</span></span> |
|  | |
| <span data-ttu-id="133e9-280">Request body</span><span class="sxs-lookup"><span data-stu-id="133e9-280">Request body</span></span> |<span data-ttu-id="133e9-281">Event data entry for each event you want to send.</span><span class="sxs-lookup"><span data-stu-id="133e9-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="133e9-282">You should send for the same user or browser session the same ID in the SessionId field.</span><span class="sxs-lookup"><span data-stu-id="133e9-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="133e9-283">(See sample of event body below.)</span><span class="sxs-lookup"><span data-stu-id="133e9-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="133e9-284">Example for event 'Click':</span><span class="sxs-lookup"><span data-stu-id="133e9-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="133e9-285">Example for event 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="133e9-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="133e9-286">Example for event 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="133e9-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="133e9-287">Example for event 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="133e9-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="133e9-288">Example for event 'Purchase':</span><span class="sxs-lookup"><span data-stu-id="133e9-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="133e9-289">Example sending 2 events, 'Click' and 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="133e9-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="133e9-290">**Response**: HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="133e9-291">Build a recommendation model</span><span class="sxs-lookup"><span data-stu-id="133e9-291">Build a recommendation model</span></span>
| <span data-ttu-id="133e9-292">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-292">HTTP Method</span></span> | <span data-ttu-id="133e9-293">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-294">POST</span><span class="sxs-lookup"><span data-stu-id="133e9-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-295">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-296">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-296">Parameter Name</span></span> | <span data-ttu-id="133e9-297">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-298">modelId</span><span class="sxs-lookup"><span data-stu-id="133e9-298">modelId</span></span> |<span data-ttu-id="133e9-299">Unique identifier of the model (case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="133e9-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="133e9-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="133e9-300">userDescription</span></span> |<span data-ttu-id="133e9-301">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="133e9-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="133e9-302">Note that if you use spaces you must encode it with %20 instead.</span><span class="sxs-lookup"><span data-stu-id="133e9-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="133e9-303">See example above.</span><span class="sxs-lookup"><span data-stu-id="133e9-303">See example above.</span></span><br><span data-ttu-id="133e9-304">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="133e9-304">Max length: 50</span></span> |
| <span data-ttu-id="133e9-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-305">apiVersion</span></span> |<span data-ttu-id="133e9-306">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-306">1.0</span></span> |
|  | |
| <span data-ttu-id="133e9-307">Request Body</span><span class="sxs-lookup"><span data-stu-id="133e9-307">Request Body</span></span> |<span data-ttu-id="133e9-308">NONE</span><span class="sxs-lookup"><span data-stu-id="133e9-308">NONE</span></span> |

<span data-ttu-id="133e9-309">**Response**:</span><span class="sxs-lookup"><span data-stu-id="133e9-309">**Response**:</span></span>

<span data-ttu-id="133e9-310">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-310">HTTP Status code: 200</span></span>

<span data-ttu-id="133e9-311">This is an asynchronous API.</span><span class="sxs-lookup"><span data-stu-id="133e9-311">This is an asynchronous API.</span></span> <span data-ttu-id="133e9-312">You will get a build ID as a response.</span><span class="sxs-lookup"><span data-stu-id="133e9-312">You will get a build ID as a response.</span></span> <span data-ttu-id="133e9-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span><span class="sxs-lookup"><span data-stu-id="133e9-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="133e9-314">Note that a build can take from minutes to hours depending on the size of the data.</span><span class="sxs-lookup"><span data-stu-id="133e9-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="133e9-315">You cannot consume recommendations till the build ends.</span><span class="sxs-lookup"><span data-stu-id="133e9-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="133e9-316">Valid build status:</span><span class="sxs-lookup"><span data-stu-id="133e9-316">Valid build status:</span></span>

* <span data-ttu-id="133e9-317">Create – Model was created.</span><span class="sxs-lookup"><span data-stu-id="133e9-317">Create – Model was created.</span></span>
* <span data-ttu-id="133e9-318">Queued – Model build was triggered and it is queued.</span><span class="sxs-lookup"><span data-stu-id="133e9-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="133e9-319">Building – Model is being built.</span><span class="sxs-lookup"><span data-stu-id="133e9-319">Building – Model is being built.</span></span>
* <span data-ttu-id="133e9-320">Success – Build ended successfully.</span><span class="sxs-lookup"><span data-stu-id="133e9-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="133e9-321">Error – Build ended with a failure.</span><span class="sxs-lookup"><span data-stu-id="133e9-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="133e9-322">Canceled – Build was canceled.</span><span class="sxs-lookup"><span data-stu-id="133e9-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="133e9-323">Canceling – Build is being canceled.</span><span class="sxs-lookup"><span data-stu-id="133e9-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="133e9-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="133e9-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="133e9-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="133e9-326">Get build status of a model</span><span class="sxs-lookup"><span data-stu-id="133e9-326">Get build status of a model</span></span>
| <span data-ttu-id="133e9-327">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-327">HTTP Method</span></span> | <span data-ttu-id="133e9-328">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-329">GET</span><span class="sxs-lookup"><span data-stu-id="133e9-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-330">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-331">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-331">Parameter Name</span></span> | <span data-ttu-id="133e9-332">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-333">modelId</span><span class="sxs-lookup"><span data-stu-id="133e9-333">modelId</span></span> |<span data-ttu-id="133e9-334">Unique identifier of the model  (case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="133e9-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="133e9-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="133e9-335">onlyLastBuild</span></span> |<span data-ttu-id="133e9-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span><span class="sxs-lookup"><span data-stu-id="133e9-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="133e9-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-337">apiVersion</span></span> |<span data-ttu-id="133e9-338">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-338">1.0</span></span> |

<span data-ttu-id="133e9-339">**Response**:</span><span class="sxs-lookup"><span data-stu-id="133e9-339">**Response**:</span></span>

<span data-ttu-id="133e9-340">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-340">HTTP Status code: 200</span></span>

<span data-ttu-id="133e9-341">The response includes one entry per build.</span><span class="sxs-lookup"><span data-stu-id="133e9-341">The response includes one entry per build.</span></span> <span data-ttu-id="133e9-342">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="133e9-342">Each entry has the following data:</span></span>

* <span data-ttu-id="133e9-343">`feed/entry/content/properties/UserName` – Name of the user.</span><span class="sxs-lookup"><span data-stu-id="133e9-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="133e9-344">`feed/entry/content/properties/ModelName` – Name of the model.</span><span class="sxs-lookup"><span data-stu-id="133e9-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="133e9-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span><span class="sxs-lookup"><span data-stu-id="133e9-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="133e9-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="133e9-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="133e9-347">active build).</span><span class="sxs-lookup"><span data-stu-id="133e9-347">active build).</span></span>
* <span data-ttu-id="133e9-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span><span class="sxs-lookup"><span data-stu-id="133e9-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="133e9-349">`feed/entry/content/properties/BuildType` - Type of the build.</span><span class="sxs-lookup"><span data-stu-id="133e9-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="133e9-350">`feed/entry/content/properties/Status` – Build status.</span><span class="sxs-lookup"><span data-stu-id="133e9-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="133e9-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span><span class="sxs-lookup"><span data-stu-id="133e9-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="133e9-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span><span class="sxs-lookup"><span data-stu-id="133e9-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="133e9-353">`feed/entry/content/properties/Progress` – Build progress (%).</span><span class="sxs-lookup"><span data-stu-id="133e9-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="133e9-354">`feed/entry/content/properties/StartTime` – Build start time.</span><span class="sxs-lookup"><span data-stu-id="133e9-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="133e9-355">`feed/entry/content/properties/EndTime` – Build end time.</span><span class="sxs-lookup"><span data-stu-id="133e9-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="133e9-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span><span class="sxs-lookup"><span data-stu-id="133e9-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="133e9-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span><span class="sxs-lookup"><span data-stu-id="133e9-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="133e9-358">Valid build status:</span><span class="sxs-lookup"><span data-stu-id="133e9-358">Valid build status:</span></span>

* <span data-ttu-id="133e9-359">Created – Build request entry was created.</span><span class="sxs-lookup"><span data-stu-id="133e9-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="133e9-360">Queued – Build request was triggered and it is queued.</span><span class="sxs-lookup"><span data-stu-id="133e9-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="133e9-361">Building – Build is in process.</span><span class="sxs-lookup"><span data-stu-id="133e9-361">Building – Build is in process.</span></span>
* <span data-ttu-id="133e9-362">Success – Build ended successfully.</span><span class="sxs-lookup"><span data-stu-id="133e9-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="133e9-363">Error – Build ended with a failure.</span><span class="sxs-lookup"><span data-stu-id="133e9-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="133e9-364">Canceled – Build was canceled.</span><span class="sxs-lookup"><span data-stu-id="133e9-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="133e9-365">Canceling – Build is being canceled.</span><span class="sxs-lookup"><span data-stu-id="133e9-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="133e9-366">Valid values for build type:</span><span class="sxs-lookup"><span data-stu-id="133e9-366">Valid values for build type:</span></span>

* <span data-ttu-id="133e9-367">Rank - Rank build.</span><span class="sxs-lookup"><span data-stu-id="133e9-367">Rank - Rank build.</span></span> <span data-ttu-id="133e9-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span><span class="sxs-lookup"><span data-stu-id="133e9-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="133e9-369">Recommendation - Recommendation build.</span><span class="sxs-lookup"><span data-stu-id="133e9-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="133e9-370">Fbt - Frequently bought together build.</span><span class="sxs-lookup"><span data-stu-id="133e9-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="133e9-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="133e9-372">Get recommendations</span><span class="sxs-lookup"><span data-stu-id="133e9-372">Get recommendations</span></span>
| <span data-ttu-id="133e9-373">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-373">HTTP Method</span></span> | <span data-ttu-id="133e9-374">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-375">GET</span><span class="sxs-lookup"><span data-stu-id="133e9-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-376">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-377">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-377">Parameter Name</span></span> | <span data-ttu-id="133e9-378">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-379">modelId</span><span class="sxs-lookup"><span data-stu-id="133e9-379">modelId</span></span> |<span data-ttu-id="133e9-380">Unique identifier of the model (case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="133e9-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="133e9-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="133e9-381">itemIds</span></span> |<span data-ttu-id="133e9-382">Comma-separated list of the items to recommend for.</span><span class="sxs-lookup"><span data-stu-id="133e9-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="133e9-383">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="133e9-383">Max length: 1024</span></span> |
| <span data-ttu-id="133e9-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="133e9-384">numberOfResults</span></span> |<span data-ttu-id="133e9-385">Number of required results</span><span class="sxs-lookup"><span data-stu-id="133e9-385">Number of required results</span></span> |
| <span data-ttu-id="133e9-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="133e9-386">includeMetatadata</span></span> |<span data-ttu-id="133e9-387">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="133e9-387">Future use, always false</span></span> |
| <span data-ttu-id="133e9-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-388">apiVersion</span></span> |<span data-ttu-id="133e9-389">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-389">1.0</span></span> |

<span data-ttu-id="133e9-390">**Response:**</span><span class="sxs-lookup"><span data-stu-id="133e9-390">**Response:**</span></span>

<span data-ttu-id="133e9-391">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-391">HTTP Status code: 200</span></span>

<span data-ttu-id="133e9-392">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="133e9-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="133e9-393">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="133e9-393">Each entry has the following data:</span></span>

* <span data-ttu-id="133e9-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="133e9-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="133e9-395">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="133e9-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="133e9-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="133e9-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="133e9-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="133e9-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="133e9-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-398">OData XML</span></span>

<span data-ttu-id="133e9-399">The example response below includes 10 recommended items:</span><span class="sxs-lookup"><span data-stu-id="133e9-399">The example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="133e9-400">Update model</span><span class="sxs-lookup"><span data-stu-id="133e9-400">Update model</span></span>
<span data-ttu-id="133e9-401">You can update the model description or the active build ID.</span><span class="sxs-lookup"><span data-stu-id="133e9-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="133e9-402">*Active build ID* - Every build for every model has a build ID.</span><span class="sxs-lookup"><span data-stu-id="133e9-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="133e9-403">The active build ID is the first successful build of every new model.</span><span class="sxs-lookup"><span data-stu-id="133e9-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="133e9-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span><span class="sxs-lookup"><span data-stu-id="133e9-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="133e9-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span><span class="sxs-lookup"><span data-stu-id="133e9-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="133e9-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span><span class="sxs-lookup"><span data-stu-id="133e9-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="133e9-407">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="133e9-407">HTTP Method</span></span> | <span data-ttu-id="133e9-408">URI</span><span class="sxs-lookup"><span data-stu-id="133e9-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-409">PUT</span><span class="sxs-lookup"><span data-stu-id="133e9-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="133e9-410">Example:</span><span class="sxs-lookup"><span data-stu-id="133e9-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="133e9-411">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="133e9-411">Parameter Name</span></span> | <span data-ttu-id="133e9-412">Valid Values</span><span class="sxs-lookup"><span data-stu-id="133e9-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="133e9-413">id</span><span class="sxs-lookup"><span data-stu-id="133e9-413">id</span></span> |<span data-ttu-id="133e9-414">Unique identifier of the model (case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="133e9-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="133e9-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="133e9-415">apiVersion</span></span> |<span data-ttu-id="133e9-416">1.0</span><span class="sxs-lookup"><span data-stu-id="133e9-416">1.0</span></span> |
|  | |
| <span data-ttu-id="133e9-417">Request Body</span><span class="sxs-lookup"><span data-stu-id="133e9-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="133e9-418">Note that the XML tags Description and ActiveBuildId are optional.</span><span class="sxs-lookup"><span data-stu-id="133e9-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="133e9-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span><span class="sxs-lookup"><span data-stu-id="133e9-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="133e9-420">**Response**:</span><span class="sxs-lookup"><span data-stu-id="133e9-420">**Response**:</span></span>

<span data-ttu-id="133e9-421">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="133e9-421">HTTP Status code: 200</span></span>

<span data-ttu-id="133e9-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="133e9-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="133e9-423">Legal</span><span class="sxs-lookup"><span data-stu-id="133e9-423">Legal</span></span>
<span data-ttu-id="133e9-424">This document is provided "as-is".</span><span class="sxs-lookup"><span data-stu-id="133e9-424">This document is provided "as-is".</span></span> <span data-ttu-id="133e9-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span><span class="sxs-lookup"><span data-stu-id="133e9-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="133e9-426">Some examples depicted herein are provided for illustration only and are fictitious.</span><span class="sxs-lookup"><span data-stu-id="133e9-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="133e9-427">No real association or connection is intended or should be inferred.</span><span class="sxs-lookup"><span data-stu-id="133e9-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="133e9-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span><span class="sxs-lookup"><span data-stu-id="133e9-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="133e9-429">You may copy and use this document for your internal, reference purposes.</span><span class="sxs-lookup"><span data-stu-id="133e9-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="133e9-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="133e9-430">© 2014 Microsoft.</span></span> <span data-ttu-id="133e9-431">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="133e9-431">All rights reserved.</span></span> 

