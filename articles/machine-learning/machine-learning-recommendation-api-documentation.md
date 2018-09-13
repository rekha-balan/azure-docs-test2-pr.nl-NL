---
title: Machine Learning Recommendations API Documentation | Microsoft Docs
description: Azure Machine Learning Recommendations API documentation for a recommendations engine available in the Microsoft Azure Marketplace.
services: machine-learning
documentationcenter: ''
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: machine-learning-datamarket-deprecation
ms.openlocfilehash: 7f51e8f112dff71084280e1e132eb60d1bb2eeec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550056"
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="11474-103">Azure Machine Learning Recommendations API Documentation</span><span class="sxs-lookup"><span data-stu-id="11474-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="11474-104">You should start using the Recommendations API Cognitive Service instead of this version.</span><span class="sxs-lookup"><span data-stu-id="11474-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="11474-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span><span class="sxs-lookup"><span data-stu-id="11474-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="11474-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span><span class="sxs-lookup"><span data-stu-id="11474-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="11474-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="11474-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="11474-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span><span class="sxs-lookup"><span data-stu-id="11474-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="11474-109">1. General overview</span><span class="sxs-lookup"><span data-stu-id="11474-109">1. General overview</span></span>
<span data-ttu-id="11474-110">This document is an API reference.</span><span class="sxs-lookup"><span data-stu-id="11474-110">This document is an API reference.</span></span> <span data-ttu-id="11474-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span><span class="sxs-lookup"><span data-stu-id="11474-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="11474-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span><span class="sxs-lookup"><span data-stu-id="11474-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span></span>

* <span data-ttu-id="11474-113"><ins>Limitations</ins> - Recommendations API limitations.</span><span class="sxs-lookup"><span data-stu-id="11474-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="11474-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span><span class="sxs-lookup"><span data-stu-id="11474-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="11474-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span><span class="sxs-lookup"><span data-stu-id="11474-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="11474-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span><span class="sxs-lookup"><span data-stu-id="11474-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span></span>
* <span data-ttu-id="11474-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span><span class="sxs-lookup"><span data-stu-id="11474-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span></span>
* <span data-ttu-id="11474-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span></span> <span data-ttu-id="11474-119">A catalog contains metadata information on the items of the usage data.</span><span class="sxs-lookup"><span data-stu-id="11474-119">A catalog contains metadata information on the items of the usage data.</span></span>
* <span data-ttu-id="11474-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span><span class="sxs-lookup"><span data-stu-id="11474-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span></span>
* <span data-ttu-id="11474-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span><span class="sxs-lookup"><span data-stu-id="11474-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span></span> <span data-ttu-id="11474-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span><span class="sxs-lookup"><span data-stu-id="11474-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="11474-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span><span class="sxs-lookup"><span data-stu-id="11474-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span></span> <span data-ttu-id="11474-124">You can trigger a model build once you have valuable usage data.</span><span class="sxs-lookup"><span data-stu-id="11474-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="11474-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span><span class="sxs-lookup"><span data-stu-id="11474-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span></span>
* <span data-ttu-id="11474-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span><span class="sxs-lookup"><span data-stu-id="11474-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span></span>
* <span data-ttu-id="11474-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span><span class="sxs-lookup"><span data-stu-id="11474-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span></span> <span data-ttu-id="11474-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span><span class="sxs-lookup"><span data-stu-id="11474-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span></span> <span data-ttu-id="11474-129">An error notification will be raised.)</span><span class="sxs-lookup"><span data-stu-id="11474-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="11474-130">2. Limitations</span><span class="sxs-lookup"><span data-stu-id="11474-130">2. Limitations</span></span>
* <span data-ttu-id="11474-131">The maximum number of models per subscription is 10.</span><span class="sxs-lookup"><span data-stu-id="11474-131">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="11474-132">The maximum number of builds per model is 20.</span><span class="sxs-lookup"><span data-stu-id="11474-132">The maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="11474-133">The maximum number of items that a catalog can hold is 100,000.</span><span class="sxs-lookup"><span data-stu-id="11474-133">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="11474-134">The maximum number of usage points that are kept is ~5,000,000.</span><span class="sxs-lookup"><span data-stu-id="11474-134">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="11474-135">The oldest will be deleted if new ones will be uploaded or reported.</span><span class="sxs-lookup"><span data-stu-id="11474-135">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="11474-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span><span class="sxs-lookup"><span data-stu-id="11474-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="11474-137">The maximum number of items that can be asked for when getting recommendations is 150.</span><span class="sxs-lookup"><span data-stu-id="11474-137">The maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="11474-138">3. APIs - general information</span><span class="sxs-lookup"><span data-stu-id="11474-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="11474-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="11474-139">3.1.</span></span> <span data-ttu-id="11474-140">Authentication</span><span class="sxs-lookup"><span data-stu-id="11474-140">Authentication</span></span>
<span data-ttu-id="11474-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span><span class="sxs-lookup"><span data-stu-id="11474-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="11474-142">The marketplace supports either the Basic or OAuth authentication method.</span><span class="sxs-lookup"><span data-stu-id="11474-142">The marketplace supports either the Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="11474-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="11474-143">3.2.</span></span> <span data-ttu-id="11474-144">Service URI</span><span class="sxs-lookup"><span data-stu-id="11474-144">Service URI</span></span>
<span data-ttu-id="11474-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="11474-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="11474-146">The full service URI is expressed using elements of the OData specification.</span><span class="sxs-lookup"><span data-stu-id="11474-146">The full service URI is expressed using elements of the OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="11474-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="11474-147">3.3.</span></span> <span data-ttu-id="11474-148">API version</span><span class="sxs-lookup"><span data-stu-id="11474-148">API version</span></span>
<span data-ttu-id="11474-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span><span class="sxs-lookup"><span data-stu-id="11474-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="11474-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="11474-150">3.4.</span></span> <span data-ttu-id="11474-151">IDs are case sensitive</span><span class="sxs-lookup"><span data-stu-id="11474-151">IDs are case sensitive</span></span>
<span data-ttu-id="11474-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span><span class="sxs-lookup"><span data-stu-id="11474-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="11474-153">For instance, model IDs and catalog IDs are case sensitive.</span><span class="sxs-lookup"><span data-stu-id="11474-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="11474-154">4. Recommendations Quality and Cold Items</span><span class="sxs-lookup"><span data-stu-id="11474-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="11474-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="11474-155">4.1.</span></span> <span data-ttu-id="11474-156">Recommendation quality</span><span class="sxs-lookup"><span data-stu-id="11474-156">Recommendation quality</span></span>
<span data-ttu-id="11474-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span><span class="sxs-lookup"><span data-stu-id="11474-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span></span> <span data-ttu-id="11474-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span></span> <span data-ttu-id="11474-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span><span class="sxs-lookup"><span data-stu-id="11474-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="11474-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span><span class="sxs-lookup"><span data-stu-id="11474-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span></span> <span data-ttu-id="11474-161">This metadata is referred to as features.</span><span class="sxs-lookup"><span data-stu-id="11474-161">This metadata is referred to as features.</span></span> <span data-ttu-id="11474-162">Typical features are a book's author or a movie's actor.</span><span class="sxs-lookup"><span data-stu-id="11474-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="11474-163">Features are provided via the catalog in the form of key/value strings.</span><span class="sxs-lookup"><span data-stu-id="11474-163">Features are provided via the catalog in the form of key/value strings.</span></span> <span data-ttu-id="11474-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="11474-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="11474-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="11474-165">4.2.</span></span> <span data-ttu-id="11474-166">Rank build</span><span class="sxs-lookup"><span data-stu-id="11474-166">Rank build</span></span>
<span data-ttu-id="11474-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span><span class="sxs-lookup"><span data-stu-id="11474-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span></span> <span data-ttu-id="11474-168">For this purpose a new build was introduced - a rank build.</span><span class="sxs-lookup"><span data-stu-id="11474-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="11474-169">This build will rank the usefulness of features.</span><span class="sxs-lookup"><span data-stu-id="11474-169">This build will rank the usefulness of features.</span></span> <span data-ttu-id="11474-170">A meaningful feature is a feature with a rank score of 2 and up.</span><span class="sxs-lookup"><span data-stu-id="11474-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="11474-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span><span class="sxs-lookup"><span data-stu-id="11474-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span></span> <span data-ttu-id="11474-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span><span class="sxs-lookup"><span data-stu-id="11474-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span></span> <span data-ttu-id="11474-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span><span class="sxs-lookup"><span data-stu-id="11474-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="11474-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span><span class="sxs-lookup"><span data-stu-id="11474-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="11474-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="11474-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="11474-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="11474-176">4.3.</span></span> <span data-ttu-id="11474-177">Recommendation reasoning</span><span class="sxs-lookup"><span data-stu-id="11474-177">Recommendation reasoning</span></span>
<span data-ttu-id="11474-178">Recommendation reasoning is another aspect of feature usage.</span><span class="sxs-lookup"><span data-stu-id="11474-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="11474-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="11474-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span><span class="sxs-lookup"><span data-stu-id="11474-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span></span>
<span data-ttu-id="11474-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="11474-182">5. Model Basic</span><span class="sxs-lookup"><span data-stu-id="11474-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="11474-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="11474-183">5.1.</span></span> <span data-ttu-id="11474-184">Create Model</span><span class="sxs-lookup"><span data-stu-id="11474-184">Create Model</span></span>
<span data-ttu-id="11474-185">Creates a “create model” request.</span><span class="sxs-lookup"><span data-stu-id="11474-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="11474-186">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-186">HTTP Method</span></span> | <span data-ttu-id="11474-187">URI</span><span class="sxs-lookup"><span data-stu-id="11474-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-188">POST</span><span class="sxs-lookup"><span data-stu-id="11474-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-189">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-190">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-190">Parameter Name</span></span> | <span data-ttu-id="11474-191">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-192">modelName</span><span class="sxs-lookup"><span data-stu-id="11474-192">modelName</span></span> |<span data-ttu-id="11474-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span><span class="sxs-lookup"><span data-stu-id="11474-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="11474-194">Max length: 20</span><span class="sxs-lookup"><span data-stu-id="11474-194">Max length: 20</span></span> |
| <span data-ttu-id="11474-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-195">apiVersion</span></span> |<span data-ttu-id="11474-196">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-196">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-197">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-197">Request Body</span></span> |<span data-ttu-id="11474-198">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-198">NONE</span></span> |

<span data-ttu-id="11474-199">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-199">**Response**:</span></span>

<span data-ttu-id="11474-200">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="11474-201">`feed/entry/content/properties/id` - Contains the model ID.</span><span class="sxs-lookup"><span data-stu-id="11474-201">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="11474-202">**Note**: model ID is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="11474-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="11474-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="11474-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="11474-204">5.2.</span></span> <span data-ttu-id="11474-205">Get Model</span><span class="sxs-lookup"><span data-stu-id="11474-205">Get Model</span></span>
<span data-ttu-id="11474-206">Creates a “get model” request.</span><span class="sxs-lookup"><span data-stu-id="11474-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="11474-207">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-207">HTTP Method</span></span> | <span data-ttu-id="11474-208">URI</span><span class="sxs-lookup"><span data-stu-id="11474-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-209">GET</span><span class="sxs-lookup"><span data-stu-id="11474-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-210">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-211">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-211">Parameter Name</span></span> | <span data-ttu-id="11474-212">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-213">id</span><span class="sxs-lookup"><span data-stu-id="11474-213">id</span></span> |<span data-ttu-id="11474-214">Unique identifier of the model (case sensitive)</span><span class="sxs-lookup"><span data-stu-id="11474-214">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="11474-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-215">apiVersion</span></span> |<span data-ttu-id="11474-216">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-216">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-217">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-217">Request Body</span></span> |<span data-ttu-id="11474-218">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-218">NONE</span></span> |

<span data-ttu-id="11474-219">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-219">**Response**:</span></span>

<span data-ttu-id="11474-220">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-220">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-221">The model data can be found under the following elements:</span><span class="sxs-lookup"><span data-stu-id="11474-221">The model data can be found under the following elements:</span></span>

* <span data-ttu-id="11474-222">`feed/entry/content/properties/Id` - Model unique ID.</span><span class="sxs-lookup"><span data-stu-id="11474-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="11474-223">`feed/entry/content/properties/Name` - Model name.</span><span class="sxs-lookup"><span data-stu-id="11474-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="11474-224">`feed/entry/content/properties/Date` - Model creation date.</span><span class="sxs-lookup"><span data-stu-id="11474-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="11474-225">`feed/entry/content/properties/Status` - Model status.</span><span class="sxs-lookup"><span data-stu-id="11474-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="11474-226">One of the following:</span><span class="sxs-lookup"><span data-stu-id="11474-226">One of the following:</span></span>
  * <span data-ttu-id="11474-227">Created - Model is created and does not contain Catalog and Usage.</span><span class="sxs-lookup"><span data-stu-id="11474-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="11474-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span><span class="sxs-lookup"><span data-stu-id="11474-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="11474-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span><span class="sxs-lookup"><span data-stu-id="11474-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="11474-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span><span class="sxs-lookup"><span data-stu-id="11474-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="11474-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span><span class="sxs-lookup"><span data-stu-id="11474-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="11474-232">`feed/entry/content/properties/UserName` - Model internal user name.</span><span class="sxs-lookup"><span data-stu-id="11474-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="11474-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="11474-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="11474-234">5.3.</span></span>    <span data-ttu-id="11474-235">Get All Models</span><span class="sxs-lookup"><span data-stu-id="11474-235">Get All Models</span></span>
<span data-ttu-id="11474-236">Retrieves all models of the current user.</span><span class="sxs-lookup"><span data-stu-id="11474-236">Retrieves all models of the current user.</span></span>

| <span data-ttu-id="11474-237">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-237">HTTP Method</span></span> | <span data-ttu-id="11474-238">URI</span><span class="sxs-lookup"><span data-stu-id="11474-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-239">GET</span><span class="sxs-lookup"><span data-stu-id="11474-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="11474-240">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="11474-241">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-241">Parameter Name</span></span> | <span data-ttu-id="11474-242">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-243">apiVersion</span></span> |<span data-ttu-id="11474-244">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-244">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-245">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-245">Request Body</span></span> |<span data-ttu-id="11474-246">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-246">NONE</span></span> |

<span data-ttu-id="11474-247">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-247">**Response**:</span></span>

<span data-ttu-id="11474-248">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="11474-249">`feed/entry/content/properties/Id` - Model unique ID.</span><span class="sxs-lookup"><span data-stu-id="11474-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="11474-250">`feed/entry/content/properties/Name` - Model name.</span><span class="sxs-lookup"><span data-stu-id="11474-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="11474-251">`feed/entry/content/properties/Date` - Model creation date.</span><span class="sxs-lookup"><span data-stu-id="11474-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="11474-252">`feed/entry/content/properties/Status` - Model status.</span><span class="sxs-lookup"><span data-stu-id="11474-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="11474-253">One of the following:</span><span class="sxs-lookup"><span data-stu-id="11474-253">One of the following:</span></span>
  * <span data-ttu-id="11474-254">Created - Model is created and does not contain Catalog and Usage.</span><span class="sxs-lookup"><span data-stu-id="11474-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="11474-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span><span class="sxs-lookup"><span data-stu-id="11474-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="11474-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span><span class="sxs-lookup"><span data-stu-id="11474-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="11474-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span><span class="sxs-lookup"><span data-stu-id="11474-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="11474-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span><span class="sxs-lookup"><span data-stu-id="11474-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="11474-259">`feed/entry/content/properties/UserName` - Model internal user name.</span><span class="sxs-lookup"><span data-stu-id="11474-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="11474-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span><span class="sxs-lookup"><span data-stu-id="11474-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="11474-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span><span class="sxs-lookup"><span data-stu-id="11474-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="11474-262">`feed/entry/content/properties/Description` - Model description.</span><span class="sxs-lookup"><span data-stu-id="11474-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="11474-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span><span class="sxs-lookup"><span data-stu-id="11474-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="11474-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="11474-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="11474-265">5.4.</span></span>    <span data-ttu-id="11474-266">Update Model</span><span class="sxs-lookup"><span data-stu-id="11474-266">Update Model</span></span>
<span data-ttu-id="11474-267">You can update the model description or the active build ID.</span><span class="sxs-lookup"><span data-stu-id="11474-267">You can update the model description or the active build ID.</span></span><br>
<span data-ttu-id="11474-268"><ins>Active build ID</ins> - Every build for every model has a build ID.</span><span class="sxs-lookup"><span data-stu-id="11474-268"><ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="11474-269">The active build ID is the first successful build of every new model.</span><span class="sxs-lookup"><span data-stu-id="11474-269">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="11474-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span><span class="sxs-lookup"><span data-stu-id="11474-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="11474-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span><span class="sxs-lookup"><span data-stu-id="11474-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span><br>
<span data-ttu-id="11474-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span><span class="sxs-lookup"><span data-stu-id="11474-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="11474-273">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-273">HTTP Method</span></span> | <span data-ttu-id="11474-274">URI</span><span class="sxs-lookup"><span data-stu-id="11474-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-275">PUT</span><span class="sxs-lookup"><span data-stu-id="11474-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-276">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-277">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-277">Parameter Name</span></span> | <span data-ttu-id="11474-278">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-279">id</span><span class="sxs-lookup"><span data-stu-id="11474-279">id</span></span> |<span data-ttu-id="11474-280">Unique identifier of the model (case sensitive)</span><span class="sxs-lookup"><span data-stu-id="11474-280">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="11474-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-281">apiVersion</span></span> |<span data-ttu-id="11474-282">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-282">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-283">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="11474-284">Note that the XML tags Description and ActiveBuildId are optional.</span><span class="sxs-lookup"><span data-stu-id="11474-284">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="11474-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span><span class="sxs-lookup"><span data-stu-id="11474-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="11474-286">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-286">**Response**:</span></span>

<span data-ttu-id="11474-287">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="11474-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="11474-288">5.5.</span></span>    <span data-ttu-id="11474-289">Delete Model</span><span class="sxs-lookup"><span data-stu-id="11474-289">Delete Model</span></span>
<span data-ttu-id="11474-290">Deletes an existing model by ID.</span><span class="sxs-lookup"><span data-stu-id="11474-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="11474-291">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-291">HTTP Method</span></span> | <span data-ttu-id="11474-292">URI</span><span class="sxs-lookup"><span data-stu-id="11474-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-293">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-294">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-295">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-295">Parameter Name</span></span> | <span data-ttu-id="11474-296">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-297">id</span><span class="sxs-lookup"><span data-stu-id="11474-297">id</span></span> |<span data-ttu-id="11474-298">Unique identifier of the model (case sensitive)</span><span class="sxs-lookup"><span data-stu-id="11474-298">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="11474-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-299">apiVersion</span></span> |<span data-ttu-id="11474-300">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-300">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-301">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-301">Request Body</span></span> |<span data-ttu-id="11474-302">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-302">NONE</span></span> |

<span data-ttu-id="11474-303">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-303">**Response**:</span></span>

<span data-ttu-id="11474-304">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-304">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="11474-306">6. Model Advanced</span><span class="sxs-lookup"><span data-stu-id="11474-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="11474-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="11474-307">6.1.</span></span>    <span data-ttu-id="11474-308">Model Data Insight</span><span class="sxs-lookup"><span data-stu-id="11474-308">Model Data Insight</span></span>
<span data-ttu-id="11474-309">Returns statistical data on the usage data that this model was built with.</span><span class="sxs-lookup"><span data-stu-id="11474-309">Returns statistical data on the usage data that this model was built with.</span></span>

<span data-ttu-id="11474-310">Available only for Recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="11474-311">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-311">HTTP Method</span></span> | <span data-ttu-id="11474-312">URI</span><span class="sxs-lookup"><span data-stu-id="11474-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-313">GET</span><span class="sxs-lookup"><span data-stu-id="11474-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-314">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-315">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-315">Parameter Name</span></span> | <span data-ttu-id="11474-316">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-317">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-317">modelId</span></span> |<span data-ttu-id="11474-318">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-318">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-319">apiVersion</span></span> |<span data-ttu-id="11474-320">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-320">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-321">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-321">Request Body</span></span> |<span data-ttu-id="11474-322">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-322">NONE</span></span> |

<span data-ttu-id="11474-323">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-323">**Response**:</span></span>

<span data-ttu-id="11474-324">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-324">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-325">The data is returned as a collection of properties.</span><span class="sxs-lookup"><span data-stu-id="11474-325">The data is returned as a collection of properties.</span></span>

* <span data-ttu-id="11474-326">`feed/entry/id/content/properties/key` - Holds the property name.</span><span class="sxs-lookup"><span data-stu-id="11474-326">`feed/entry/id/content/properties/key` - Holds the property name.</span></span>
* <span data-ttu-id="11474-327">`feed/entry/id/content/properties/value` - Holds the property value.</span><span class="sxs-lookup"><span data-stu-id="11474-327">`feed/entry/id/content/properties/value` - Holds the property value.</span></span>

<span data-ttu-id="11474-328">The table below depicts the value that each key represents.</span><span class="sxs-lookup"><span data-stu-id="11474-328">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="11474-329">Key</span><span class="sxs-lookup"><span data-stu-id="11474-329">Key</span></span> | <span data-ttu-id="11474-330">Description</span><span class="sxs-lookup"><span data-stu-id="11474-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="11474-331">AvgItemLength</span></span> |<span data-ttu-id="11474-332">Average number of distinct users per item.</span><span class="sxs-lookup"><span data-stu-id="11474-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="11474-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="11474-333">AvgUserLength</span></span> |<span data-ttu-id="11474-334">Average number of distinct items per user.</span><span class="sxs-lookup"><span data-stu-id="11474-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="11474-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="11474-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="11474-336">Number of items after pruning items that cannot be modelled.</span><span class="sxs-lookup"><span data-stu-id="11474-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="11474-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="11474-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="11474-338">Number of usage points after pruning users and items that can't be modelled.</span><span class="sxs-lookup"><span data-stu-id="11474-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="11474-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="11474-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="11474-340">Number of usage points after pruning users and items that can't be modelled.</span><span class="sxs-lookup"><span data-stu-id="11474-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="11474-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="11474-341">MaxItemLength</span></span> |<span data-ttu-id="11474-342">Number of distinct users for the most popular item.</span><span class="sxs-lookup"><span data-stu-id="11474-342">Number of distinct users for the most popular item.</span></span> |
| <span data-ttu-id="11474-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="11474-343">MaxUserLength</span></span> |<span data-ttu-id="11474-344">Maximal number of distinct items for a user.</span><span class="sxs-lookup"><span data-stu-id="11474-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="11474-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="11474-345">MinItemLength</span></span> |<span data-ttu-id="11474-346">Maximal number of distinct users for an item.</span><span class="sxs-lookup"><span data-stu-id="11474-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="11474-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="11474-347">MinUserLength</span></span> |<span data-ttu-id="11474-348">Minimal number of distinct items for a user.</span><span class="sxs-lookup"><span data-stu-id="11474-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="11474-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="11474-349">RawNumberOfItems</span></span> |<span data-ttu-id="11474-350">Number of items in the usage files.</span><span class="sxs-lookup"><span data-stu-id="11474-350">Number of items in the usage files.</span></span> |
| <span data-ttu-id="11474-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="11474-351">RawNumberOfUsers</span></span> |<span data-ttu-id="11474-352">Number of usage points before any pruning.</span><span class="sxs-lookup"><span data-stu-id="11474-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="11474-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="11474-353">RawNumberOfRecords</span></span> |<span data-ttu-id="11474-354">Number of usage points before any pruning.</span><span class="sxs-lookup"><span data-stu-id="11474-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="11474-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="11474-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="11474-356">N/A</span><span class="sxs-lookup"><span data-stu-id="11474-356">N/A</span></span> |
| <span data-ttu-id="11474-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="11474-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="11474-358">N/A</span><span class="sxs-lookup"><span data-stu-id="11474-358">N/A</span></span> |
| <span data-ttu-id="11474-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="11474-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="11474-360">N/A</span><span class="sxs-lookup"><span data-stu-id="11474-360">N/A</span></span> |

<span data-ttu-id="11474-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="11474-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="11474-362">6.2.</span></span>    <span data-ttu-id="11474-363">Model Insight</span><span class="sxs-lookup"><span data-stu-id="11474-363">Model Insight</span></span>
<span data-ttu-id="11474-364">Returns model insight on the active build or (if given) on a specific build.</span><span class="sxs-lookup"><span data-stu-id="11474-364">Returns model insight on the active build or (if given) on a specific build.</span></span>

<span data-ttu-id="11474-365">Available only for Recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="11474-366">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-366">HTTP Method</span></span> | <span data-ttu-id="11474-367">URI</span><span class="sxs-lookup"><span data-stu-id="11474-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-368">GET</span><span class="sxs-lookup"><span data-stu-id="11474-368">GET</span></span> |<span data-ttu-id="11474-369">With active build ID:</span><span class="sxs-lookup"><span data-stu-id="11474-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-370">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-371">With specific build ID:</span><span class="sxs-lookup"><span data-stu-id="11474-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-372">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-372">Parameter Name</span></span> | <span data-ttu-id="11474-373">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-374">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-374">modelId</span></span> |<span data-ttu-id="11474-375">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-375">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-376">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-376">buildId</span></span> |<span data-ttu-id="11474-377">Optional - number that identifies a successful build.</span><span class="sxs-lookup"><span data-stu-id="11474-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="11474-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-378">apiVersion</span></span> |<span data-ttu-id="11474-379">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-379">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-380">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-380">Request Body</span></span> |<span data-ttu-id="11474-381">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-381">NONE</span></span> |

<span data-ttu-id="11474-382">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-382">**Response**:</span></span>

<span data-ttu-id="11474-383">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-383">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-384">The data is returned as a collection of properties.</span><span class="sxs-lookup"><span data-stu-id="11474-384">The data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="11474-385">The table below depicts the value that each key represents.</span><span class="sxs-lookup"><span data-stu-id="11474-385">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="11474-386">Key</span><span class="sxs-lookup"><span data-stu-id="11474-386">Key</span></span> | <span data-ttu-id="11474-387">Description</span><span class="sxs-lookup"><span data-stu-id="11474-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="11474-388">CatalogCoverage</span></span> |<span data-ttu-id="11474-389">What part of the catalog can be modelled with usage patterns.</span><span class="sxs-lookup"><span data-stu-id="11474-389">What part of the catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="11474-390">The rest of the items will need content-based features.</span><span class="sxs-lookup"><span data-stu-id="11474-390">The rest of the items will need content-based features.</span></span> |
| <span data-ttu-id="11474-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="11474-391">Mpr</span></span> |<span data-ttu-id="11474-392">Mean percentile ranking of the model.</span><span class="sxs-lookup"><span data-stu-id="11474-392">Mean percentile ranking of the model.</span></span> <span data-ttu-id="11474-393">Lower is better.</span><span class="sxs-lookup"><span data-stu-id="11474-393">Lower is better.</span></span> |
| <span data-ttu-id="11474-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="11474-394">NumberOfDimensions</span></span> |<span data-ttu-id="11474-395">Number of dimensions used by the matrix factorization algorithm.</span><span class="sxs-lookup"><span data-stu-id="11474-395">Number of dimensions used by the matrix factorization algorithm.</span></span> |

<span data-ttu-id="11474-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="11474-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="11474-397">6.3.</span></span>    <span data-ttu-id="11474-398">Get Model Sample</span><span class="sxs-lookup"><span data-stu-id="11474-398">Get Model Sample</span></span>
<span data-ttu-id="11474-399">Gets a sample of the recommendation model.</span><span class="sxs-lookup"><span data-stu-id="11474-399">Gets a sample of the recommendation model.</span></span>

| <span data-ttu-id="11474-400">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-400">HTTP Method</span></span> | <span data-ttu-id="11474-401">URI</span><span class="sxs-lookup"><span data-stu-id="11474-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-402">GET</span><span class="sxs-lookup"><span data-stu-id="11474-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-403">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-404">With specific build ID:</span><span class="sxs-lookup"><span data-stu-id="11474-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-405">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-406">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-406">Parameter Name</span></span> | <span data-ttu-id="11474-407">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-408">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-408">modelId</span></span> |<span data-ttu-id="11474-409">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-409">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-410">apiVersion</span></span> |<span data-ttu-id="11474-411">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-411">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-412">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-412">Request Body</span></span> |<span data-ttu-id="11474-413">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-413">NONE</span></span> |

<span data-ttu-id="11474-414">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-414">**Response**:</span></span>

<span data-ttu-id="11474-415">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-415">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-416">OData XML</span></span>

<span data-ttu-id="11474-417">Response is returned in raw text format:</span><span class="sxs-lookup"><span data-stu-id="11474-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If the Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of the Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on the Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in the Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, The Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On the Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, The Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories to Tell in the Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, The Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic the Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in the Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, The Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, The X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell the President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In the Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, The Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of the Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, The Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in the Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (The Official Guide to the X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, The Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, The Truth Is Out There (The Official Guide to the X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, The Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of the Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where the Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, The God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (The Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in the Time of Cholera (Penguin Great Books of the 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, The Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories To Tell In The Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from the Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="11474-418">7. Model Business Rules</span><span class="sxs-lookup"><span data-stu-id="11474-418">7. Model Business Rules</span></span>
<span data-ttu-id="11474-419">These are the types of rules supported:</span><span class="sxs-lookup"><span data-stu-id="11474-419">These are the types of rules supported:</span></span>

* <span data-ttu-id="11474-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span><span class="sxs-lookup"><span data-stu-id="11474-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span></span> 
* <span data-ttu-id="11474-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span><span class="sxs-lookup"><span data-stu-id="11474-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span></span>

<span data-ttu-id="11474-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span><span class="sxs-lookup"><span data-stu-id="11474-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="11474-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span><span class="sxs-lookup"><span data-stu-id="11474-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span></span>
* <span data-ttu-id="11474-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span><span class="sxs-lookup"><span data-stu-id="11474-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="11474-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span><span class="sxs-lookup"><span data-stu-id="11474-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span></span>
* <span data-ttu-id="11474-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span><span class="sxs-lookup"><span data-stu-id="11474-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="11474-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="11474-427">7.1.</span></span>    <span data-ttu-id="11474-428">Get Model Rules</span><span class="sxs-lookup"><span data-stu-id="11474-428">Get Model Rules</span></span>
| <span data-ttu-id="11474-429">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-429">HTTP Method</span></span> | <span data-ttu-id="11474-430">URI</span><span class="sxs-lookup"><span data-stu-id="11474-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-431">GET</span><span class="sxs-lookup"><span data-stu-id="11474-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="11474-432">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-433">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-433">Parameter Name</span></span> | <span data-ttu-id="11474-434">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-435">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-435">modelId</span></span> |<span data-ttu-id="11474-436">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-436">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-437">apiVersion</span></span> |<span data-ttu-id="11474-438">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-438">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-439">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-439">Request Body</span></span> |<span data-ttu-id="11474-440">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-440">NONE</span></span> |

<span data-ttu-id="11474-441">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-441">**Response**:</span></span>

<span data-ttu-id="11474-442">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="11474-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span><span class="sxs-lookup"><span data-stu-id="11474-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="11474-444">`feed/entry/content/properties/Type` - Type of the rule.</span><span class="sxs-lookup"><span data-stu-id="11474-444">`feed/entry/content/properties/Type` - Type of the rule.</span></span>
* <span data-ttu-id="11474-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span><span class="sxs-lookup"><span data-stu-id="11474-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="11474-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="11474-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="11474-447">7.2.</span></span>    <span data-ttu-id="11474-448">Add Rule</span><span class="sxs-lookup"><span data-stu-id="11474-448">Add Rule</span></span>
| <span data-ttu-id="11474-449">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-449">HTTP Method</span></span> | <span data-ttu-id="11474-450">URI</span><span class="sxs-lookup"><span data-stu-id="11474-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-451">POST</span><span class="sxs-lookup"><span data-stu-id="11474-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="11474-452">HEADER</span><span class="sxs-lookup"><span data-stu-id="11474-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="11474-453">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-453">Parameter Name</span></span> | <span data-ttu-id="11474-454">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-455">apiVersion</span></span> |<span data-ttu-id="11474-456">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-456">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-457">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-457">Request Body</span></span> | |

<span data-ttu-id="11474-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span><span class="sxs-lookup"><span data-stu-id="11474-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span></span><br>
<span data-ttu-id="11474-459"><ins>To add a BlockList rule:</ins></span><span class="sxs-lookup"><span data-stu-id="11474-459"><ins>To add a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="11474-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span><span class="sxs-lookup"><span data-stu-id="11474-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="11474-461"><ins> To add an Upsale rule:</ins></span><span class="sxs-lookup"><span data-stu-id="11474-461"><ins> To add an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<span data-ttu-id="11474-462"><ins>To add a WhiteList rule:</ins></span><span class="sxs-lookup"><span data-stu-id="11474-462"><ins>To add a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="11474-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span><span class="sxs-lookup"><span data-stu-id="11474-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="11474-464"><ins> To add a PerSeedBlockList rule:</ins></span><span class="sxs-lookup"><span data-stu-id="11474-464"><ins> To add a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="11474-465">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-465">**Response**:</span></span>

<span data-ttu-id="11474-466">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-466">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-467">The API returns the newly created rule with its details.</span><span class="sxs-lookup"><span data-stu-id="11474-467">The API returns the newly created rule with its details.</span></span> <span data-ttu-id="11474-468">The rules property can be retrieved from the following paths:</span><span class="sxs-lookup"><span data-stu-id="11474-468">The rules property can be retrieved from the following paths:</span></span>

* <span data-ttu-id="11474-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span><span class="sxs-lookup"><span data-stu-id="11474-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="11474-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span><span class="sxs-lookup"><span data-stu-id="11474-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="11474-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span><span class="sxs-lookup"><span data-stu-id="11474-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="11474-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="11474-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="11474-473">7.3.</span></span>    <span data-ttu-id="11474-474">Delete Rule</span><span class="sxs-lookup"><span data-stu-id="11474-474">Delete Rule</span></span>
| <span data-ttu-id="11474-475">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-475">HTTP Method</span></span> | <span data-ttu-id="11474-476">URI</span><span class="sxs-lookup"><span data-stu-id="11474-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-477">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-478">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-479">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-479">Parameter Name</span></span> | <span data-ttu-id="11474-480">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-481">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-481">modelId</span></span> |<span data-ttu-id="11474-482">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-482">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-483">filterId</span><span class="sxs-lookup"><span data-stu-id="11474-483">filterId</span></span> |<span data-ttu-id="11474-484">Unique identifier of the filter</span><span class="sxs-lookup"><span data-stu-id="11474-484">Unique identifier of the filter</span></span> |
| <span data-ttu-id="11474-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-485">apiVersion</span></span> |<span data-ttu-id="11474-486">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-486">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-487">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-487">Request Body</span></span> |<span data-ttu-id="11474-488">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-488">NONE</span></span> |

<span data-ttu-id="11474-489">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-489">**Response**:</span></span>

<span data-ttu-id="11474-490">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="11474-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="11474-491">7.4.</span></span>    <span data-ttu-id="11474-492">Delete All Rules</span><span class="sxs-lookup"><span data-stu-id="11474-492">Delete All Rules</span></span>
| <span data-ttu-id="11474-493">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-493">HTTP Method</span></span> | <span data-ttu-id="11474-494">URI</span><span class="sxs-lookup"><span data-stu-id="11474-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-495">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-496">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-497">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-497">Parameter Name</span></span> | <span data-ttu-id="11474-498">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-499">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-499">modelId</span></span> |<span data-ttu-id="11474-500">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-500">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-501">apiVersion</span></span> |<span data-ttu-id="11474-502">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-502">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-503">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-503">Request Body</span></span> |<span data-ttu-id="11474-504">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-504">NONE</span></span> |

<span data-ttu-id="11474-505">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-505">**Response**:</span></span>

<span data-ttu-id="11474-506">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="11474-507">8. Catalog</span><span class="sxs-lookup"><span data-stu-id="11474-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="11474-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="11474-508">8.1.</span></span>    <span data-ttu-id="11474-509">Import Catalog Data</span><span class="sxs-lookup"><span data-stu-id="11474-509">Import Catalog Data</span></span>
<span data-ttu-id="11474-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span><span class="sxs-lookup"><span data-stu-id="11474-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="11474-511">Existing items will remain with the original values.</span><span class="sxs-lookup"><span data-stu-id="11474-511">Existing items will remain with the original values.</span></span> <span data-ttu-id="11474-512">You cannot update catalog data by using this method.</span><span class="sxs-lookup"><span data-stu-id="11474-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="11474-513">The catalog data should follow the following format:</span><span class="sxs-lookup"><span data-stu-id="11474-513">The catalog data should follow the following format:</span></span>

* <span data-ttu-id="11474-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="11474-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="11474-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="11474-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="11474-516">Note: The maximum file size is 200MB.</span><span class="sxs-lookup"><span data-stu-id="11474-516">Note: The maximum file size is 200MB.</span></span>

<span data-ttu-id="11474-517">\*\* Format details \*\*</span><span class="sxs-lookup"><span data-stu-id="11474-517">\*\* Format details \*\*</span></span>

| <span data-ttu-id="11474-518">Name</span><span class="sxs-lookup"><span data-stu-id="11474-518">Name</span></span> | <span data-ttu-id="11474-519">Mandatory</span><span class="sxs-lookup"><span data-stu-id="11474-519">Mandatory</span></span> | <span data-ttu-id="11474-520">Type</span><span class="sxs-lookup"><span data-stu-id="11474-520">Type</span></span> | <span data-ttu-id="11474-521">Description</span><span class="sxs-lookup"><span data-stu-id="11474-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="11474-522">Item Id</span><span class="sxs-lookup"><span data-stu-id="11474-522">Item Id</span></span> |<span data-ttu-id="11474-523">Yes</span><span class="sxs-lookup"><span data-stu-id="11474-523">Yes</span></span> |<span data-ttu-id="11474-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="11474-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="11474-525">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="11474-525">Max length: 50</span></span> |<span data-ttu-id="11474-526">Unique identifier of an item.</span><span class="sxs-lookup"><span data-stu-id="11474-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="11474-527">Item Name</span><span class="sxs-lookup"><span data-stu-id="11474-527">Item Name</span></span> |<span data-ttu-id="11474-528">Yes</span><span class="sxs-lookup"><span data-stu-id="11474-528">Yes</span></span> |<span data-ttu-id="11474-529">Any alphanumeric characters</span><span class="sxs-lookup"><span data-stu-id="11474-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="11474-530">Max length: 255</span><span class="sxs-lookup"><span data-stu-id="11474-530">Max length: 255</span></span> |<span data-ttu-id="11474-531">Item name.</span><span class="sxs-lookup"><span data-stu-id="11474-531">Item name.</span></span> |
| <span data-ttu-id="11474-532">Item Category</span><span class="sxs-lookup"><span data-stu-id="11474-532">Item Category</span></span> |<span data-ttu-id="11474-533">Yes</span><span class="sxs-lookup"><span data-stu-id="11474-533">Yes</span></span> |<span data-ttu-id="11474-534">Any alphanumeric characters</span><span class="sxs-lookup"><span data-stu-id="11474-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="11474-535">Max length: 255</span><span class="sxs-lookup"><span data-stu-id="11474-535">Max length: 255</span></span> |<span data-ttu-id="11474-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span><span class="sxs-lookup"><span data-stu-id="11474-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="11474-537">Description</span><span class="sxs-lookup"><span data-stu-id="11474-537">Description</span></span> |<span data-ttu-id="11474-538">No, unless features are present (but can be empty)</span><span class="sxs-lookup"><span data-stu-id="11474-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="11474-539">Any alphanumeric characters</span><span class="sxs-lookup"><span data-stu-id="11474-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="11474-540">Max length: 4000</span><span class="sxs-lookup"><span data-stu-id="11474-540">Max length: 4000</span></span> |<span data-ttu-id="11474-541">Description of this item.</span><span class="sxs-lookup"><span data-stu-id="11474-541">Description of this item.</span></span> |
| <span data-ttu-id="11474-542">Features list</span><span class="sxs-lookup"><span data-stu-id="11474-542">Features list</span></span> |<span data-ttu-id="11474-543">No</span><span class="sxs-lookup"><span data-stu-id="11474-543">No</span></span> |<span data-ttu-id="11474-544">Any alphanumeric characters</span><span class="sxs-lookup"><span data-stu-id="11474-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="11474-545">Max length: 4000; Max number of features:20</span><span class="sxs-lookup"><span data-stu-id="11474-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="11474-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span><span class="sxs-lookup"><span data-stu-id="11474-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="11474-547">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-547">HTTP Method</span></span> | <span data-ttu-id="11474-548">URI</span><span class="sxs-lookup"><span data-stu-id="11474-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-549">POST</span><span class="sxs-lookup"><span data-stu-id="11474-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-550">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="11474-551">HEADER</span><span class="sxs-lookup"><span data-stu-id="11474-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="11474-552">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-552">Parameter Name</span></span> | <span data-ttu-id="11474-553">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-554">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-554">modelId</span></span> |<span data-ttu-id="11474-555">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-555">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-556">filename</span><span class="sxs-lookup"><span data-stu-id="11474-556">filename</span></span> |<span data-ttu-id="11474-557">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-557">Textual identifier of the catalog.</span></span><br><span data-ttu-id="11474-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span><span class="sxs-lookup"><span data-stu-id="11474-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="11474-559">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="11474-559">Max length: 50</span></span> |
| <span data-ttu-id="11474-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-560">apiVersion</span></span> |<span data-ttu-id="11474-561">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-561">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-562">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-562">Request Body</span></span> |<span data-ttu-id="11474-563">Example (with features):</span><span class="sxs-lookup"><span data-stu-id="11474-563">Example (with features):</span></span><br/><span data-ttu-id="11474-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span><span class="sxs-lookup"><span data-stu-id="11474-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="11474-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span><span class="sxs-lookup"><span data-stu-id="11474-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="11474-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="11474-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="11474-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span><span class="sxs-lookup"><span data-stu-id="11474-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="11474-568">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-568">**Response**:</span></span>

<span data-ttu-id="11474-569">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-569">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-570">The API returns a report of the import.</span><span class="sxs-lookup"><span data-stu-id="11474-570">The API returns a report of the import.</span></span>

* <span data-ttu-id="11474-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span><span class="sxs-lookup"><span data-stu-id="11474-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="11474-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span><span class="sxs-lookup"><span data-stu-id="11474-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="11474-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="11474-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="11474-574">8.2.</span></span>    <span data-ttu-id="11474-575">Get Catalog</span><span class="sxs-lookup"><span data-stu-id="11474-575">Get Catalog</span></span>
<span data-ttu-id="11474-576">Retrieves all catalog items.</span><span class="sxs-lookup"><span data-stu-id="11474-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="11474-577">The catalog will be retrieved one page at a time.</span><span class="sxs-lookup"><span data-stu-id="11474-577">The catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="11474-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span><span class="sxs-lookup"><span data-stu-id="11474-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="11474-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span><span class="sxs-lookup"><span data-stu-id="11474-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="11474-580">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-580">HTTP Method</span></span> | <span data-ttu-id="11474-581">URI</span><span class="sxs-lookup"><span data-stu-id="11474-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-582">GET</span><span class="sxs-lookup"><span data-stu-id="11474-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-583">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-584">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-584">Parameter Name</span></span> | <span data-ttu-id="11474-585">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-586">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-586">modelId</span></span> |<span data-ttu-id="11474-587">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-587">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-588">apiVersion</span></span> |<span data-ttu-id="11474-589">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-589">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-590">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-590">Request Body</span></span> |<span data-ttu-id="11474-591">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-591">NONE</span></span> |

<span data-ttu-id="11474-592">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-592">**Response**:</span></span>

<span data-ttu-id="11474-593">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-593">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-594">The response includes one entry per catalog item.</span><span class="sxs-lookup"><span data-stu-id="11474-594">The response includes one entry per catalog item.</span></span> <span data-ttu-id="11474-595">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-595">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span><span class="sxs-lookup"><span data-stu-id="11474-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span></span>
* <span data-ttu-id="11474-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span><span class="sxs-lookup"><span data-stu-id="11474-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="11474-598">`feed/entry/content/properties/Name` - Catalog item name.</span><span class="sxs-lookup"><span data-stu-id="11474-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="11474-599">`feed/entry/content/properties/Category` - Catalog item category.</span><span class="sxs-lookup"><span data-stu-id="11474-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="11474-600">`feed/entry/content/properties/Description` - Catalog item description.</span><span class="sxs-lookup"><span data-stu-id="11474-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="11474-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span><span class="sxs-lookup"><span data-stu-id="11474-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="11474-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">The Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="11474-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="11474-603">8.3.</span></span>    <span data-ttu-id="11474-604">Get Catalog Items by Token</span><span class="sxs-lookup"><span data-stu-id="11474-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="11474-605">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-605">HTTP Method</span></span> | <span data-ttu-id="11474-606">URI</span><span class="sxs-lookup"><span data-stu-id="11474-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-607">GET</span><span class="sxs-lookup"><span data-stu-id="11474-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-608">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-609">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-609">Parameter Name</span></span> | <span data-ttu-id="11474-610">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-611">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-611">modelId</span></span> |<span data-ttu-id="11474-612">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-612">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-613">token</span><span class="sxs-lookup"><span data-stu-id="11474-613">token</span></span> |<span data-ttu-id="11474-614">Token of the catalog item’s name.</span><span class="sxs-lookup"><span data-stu-id="11474-614">Token of the catalog item’s name.</span></span> <span data-ttu-id="11474-615">Should contain at least 3 characters.</span><span class="sxs-lookup"><span data-stu-id="11474-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="11474-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-616">apiVersion</span></span> |<span data-ttu-id="11474-617">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-617">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-618">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-618">Request Body</span></span> |<span data-ttu-id="11474-619">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-619">NONE</span></span> |

<span data-ttu-id="11474-620">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-620">**Response**:</span></span>

<span data-ttu-id="11474-621">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-621">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-622">The response includes one entry per catalog item.</span><span class="sxs-lookup"><span data-stu-id="11474-622">The response includes one entry per catalog item.</span></span> <span data-ttu-id="11474-623">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-623">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span><span class="sxs-lookup"><span data-stu-id="11474-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="11474-625">`feed/entry/content/properties/Name` - Catalog item name.</span><span class="sxs-lookup"><span data-stu-id="11474-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="11474-626">`feed/entry/content/properties/Rating` -  (for future use)</span><span class="sxs-lookup"><span data-stu-id="11474-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="11474-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span><span class="sxs-lookup"><span data-stu-id="11474-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="11474-628">`feed/entry/content/properties/Metadata` -  (for future use)</span><span class="sxs-lookup"><span data-stu-id="11474-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="11474-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span><span class="sxs-lookup"><span data-stu-id="11474-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="11474-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="11474-631">9. Usage data</span><span class="sxs-lookup"><span data-stu-id="11474-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="11474-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="11474-632">9.1.</span></span>    <span data-ttu-id="11474-633">Import Usage Data</span><span class="sxs-lookup"><span data-stu-id="11474-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="11474-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="11474-634">9.1.1.</span></span> <span data-ttu-id="11474-635">Uploading File</span><span class="sxs-lookup"><span data-stu-id="11474-635">Uploading File</span></span>
<span data-ttu-id="11474-636">This section shows how to upload usage data by using a file.</span><span class="sxs-lookup"><span data-stu-id="11474-636">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="11474-637">You can call this API several times with usage data.</span><span class="sxs-lookup"><span data-stu-id="11474-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="11474-638">All usage data will be saved for all calls.</span><span class="sxs-lookup"><span data-stu-id="11474-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="11474-639">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-639">HTTP Method</span></span> | <span data-ttu-id="11474-640">URI</span><span class="sxs-lookup"><span data-stu-id="11474-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-641">POST</span><span class="sxs-lookup"><span data-stu-id="11474-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-642">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-643">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-643">Parameter Name</span></span> | <span data-ttu-id="11474-644">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-645">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-645">modelId</span></span> |<span data-ttu-id="11474-646">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-646">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-647">filename</span><span class="sxs-lookup"><span data-stu-id="11474-647">filename</span></span> |<span data-ttu-id="11474-648">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-648">Textual identifier of the catalog.</span></span><br><span data-ttu-id="11474-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span><span class="sxs-lookup"><span data-stu-id="11474-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="11474-650">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="11474-650">Max length: 50</span></span> |
| <span data-ttu-id="11474-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-651">apiVersion</span></span> |<span data-ttu-id="11474-652">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-652">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-653">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-653">Request Body</span></span> |<span data-ttu-id="11474-654">Usage data.</span><span class="sxs-lookup"><span data-stu-id="11474-654">Usage data.</span></span> <span data-ttu-id="11474-655">Format:</span><span class="sxs-lookup"><span data-stu-id="11474-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="11474-656">Name</span><span class="sxs-lookup"><span data-stu-id="11474-656">Name</span></span></th><th><span data-ttu-id="11474-657">Mandatory</span><span class="sxs-lookup"><span data-stu-id="11474-657">Mandatory</span></span></th><th><span data-ttu-id="11474-658">Type</span><span class="sxs-lookup"><span data-stu-id="11474-658">Type</span></span></th><th><span data-ttu-id="11474-659">Description</span><span class="sxs-lookup"><span data-stu-id="11474-659">Description</span></span></th></tr><tr><td><span data-ttu-id="11474-660">User Id</span><span class="sxs-lookup"><span data-stu-id="11474-660">User Id</span></span></td><td><span data-ttu-id="11474-661">Yes</span><span class="sxs-lookup"><span data-stu-id="11474-661">Yes</span></span></td><td><span data-ttu-id="11474-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="11474-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="11474-663">Max length: 255</span><span class="sxs-lookup"><span data-stu-id="11474-663">Max length: 255</span></span> </td><td><span data-ttu-id="11474-664">Unique identifier of a user.</span><span class="sxs-lookup"><span data-stu-id="11474-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="11474-665">Item Id</span><span class="sxs-lookup"><span data-stu-id="11474-665">Item Id</span></span></td><td><span data-ttu-id="11474-666">Yes</span><span class="sxs-lookup"><span data-stu-id="11474-666">Yes</span></span></td><td><span data-ttu-id="11474-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="11474-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="11474-668">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="11474-668">Max length: 50</span></span></td><td><span data-ttu-id="11474-669">Unique identifier of an item.</span><span class="sxs-lookup"><span data-stu-id="11474-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="11474-670">Time</span><span class="sxs-lookup"><span data-stu-id="11474-670">Time</span></span></td><td><span data-ttu-id="11474-671">No</span><span class="sxs-lookup"><span data-stu-id="11474-671">No</span></span></td><td><span data-ttu-id="11474-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="11474-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="11474-673">Time of data.</span><span class="sxs-lookup"><span data-stu-id="11474-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="11474-674">Event</span><span class="sxs-lookup"><span data-stu-id="11474-674">Event</span></span></td><td><span data-ttu-id="11474-675">No; if supplied then must also put date</span><span class="sxs-lookup"><span data-stu-id="11474-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="11474-676">One of the following:</span><span class="sxs-lookup"><span data-stu-id="11474-676">One of the following:</span></span><br><span data-ttu-id="11474-677">• Click</span><span class="sxs-lookup"><span data-stu-id="11474-677">• Click</span></span><br><span data-ttu-id="11474-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="11474-678">• RecommendationClick</span></span><br><span data-ttu-id="11474-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="11474-679">•    AddShopCart</span></span><br><span data-ttu-id="11474-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="11474-680">• RemoveShopCart</span></span><br><span data-ttu-id="11474-681">• Purchase</span><span class="sxs-lookup"><span data-stu-id="11474-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="11474-682">Maximum file size: 200MB</span><span class="sxs-lookup"><span data-stu-id="11474-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="11474-683">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="11474-684">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-684">**Response**:</span></span>

<span data-ttu-id="11474-685">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="11474-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span><span class="sxs-lookup"><span data-stu-id="11474-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="11474-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span><span class="sxs-lookup"><span data-stu-id="11474-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="11474-688">`Feed\entry\content\properties\FileId` - File identifier.</span><span class="sxs-lookup"><span data-stu-id="11474-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="11474-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="11474-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="11474-690">9.1.2.</span></span> <span data-ttu-id="11474-691">Using Data Acquisition</span><span class="sxs-lookup"><span data-stu-id="11474-691">Using Data Acquisition</span></span>
<span data-ttu-id="11474-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span><span class="sxs-lookup"><span data-stu-id="11474-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="11474-693">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-693">HTTP Method</span></span> | <span data-ttu-id="11474-694">URI</span><span class="sxs-lookup"><span data-stu-id="11474-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-695">POST</span><span class="sxs-lookup"><span data-stu-id="11474-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="11474-696">HEADER</span><span class="sxs-lookup"><span data-stu-id="11474-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="11474-697">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-697">Parameter Name</span></span> | <span data-ttu-id="11474-698">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-699">apiVersion</span></span> |<span data-ttu-id="11474-700">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-700">1.0</span></span> |
| <span data-ttu-id="11474-701">Request body</span><span class="sxs-lookup"><span data-stu-id="11474-701">Request body</span></span> |<span data-ttu-id="11474-702">Event data entry for each event you want to send.</span><span class="sxs-lookup"><span data-stu-id="11474-702">Event data entry for each event you want to send.</span></span> <span data-ttu-id="11474-703">You should send for the same user or browser session the same ID in the SessionId field.</span><span class="sxs-lookup"><span data-stu-id="11474-703">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="11474-704">(See sample of event body below.)</span><span class="sxs-lookup"><span data-stu-id="11474-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="11474-705">Example for event 'Click':</span><span class="sxs-lookup"><span data-stu-id="11474-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="11474-706">Example for event 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="11474-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="11474-707">Example for event 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="11474-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="11474-708">Example for event 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="11474-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="11474-709">Example for event 'Purchase':</span><span class="sxs-lookup"><span data-stu-id="11474-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="11474-710">Example sending 2 events, 'Click' and 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="11474-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="11474-711">**Response**: HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="11474-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="11474-712">9.2.</span></span>    <span data-ttu-id="11474-713">List Model Usage Files</span><span class="sxs-lookup"><span data-stu-id="11474-713">List Model Usage Files</span></span>
<span data-ttu-id="11474-714">Retrieves metadata of all model usage files.</span><span class="sxs-lookup"><span data-stu-id="11474-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="11474-715">The usage files will be retrieved one page at a time.</span><span class="sxs-lookup"><span data-stu-id="11474-715">The usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="11474-716">Each page containes 100 items.</span><span class="sxs-lookup"><span data-stu-id="11474-716">Each page containes 100 items.</span></span> <span data-ttu-id="11474-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span><span class="sxs-lookup"><span data-stu-id="11474-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="11474-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span><span class="sxs-lookup"><span data-stu-id="11474-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="11474-719">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-719">HTTP Method</span></span> | <span data-ttu-id="11474-720">URI</span><span class="sxs-lookup"><span data-stu-id="11474-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-721">GET</span><span class="sxs-lookup"><span data-stu-id="11474-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-722">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-723">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-723">Parameter Name</span></span> | <span data-ttu-id="11474-724">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="11474-725">forModelId</span></span> |<span data-ttu-id="11474-726">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-726">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-727">apiVersion</span></span> |<span data-ttu-id="11474-728">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-728">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-729">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-729">Request Body</span></span> |<span data-ttu-id="11474-730">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-730">NONE</span></span> |

<span data-ttu-id="11474-731">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-731">**Response**:</span></span>

<span data-ttu-id="11474-732">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-732">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-733">The response includes one entry per usage file.</span><span class="sxs-lookup"><span data-stu-id="11474-733">The response includes one entry per usage file.</span></span> <span data-ttu-id="11474-734">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-734">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-735">`feed\entry\content\properties\Id` - Usage file ID.</span><span class="sxs-lookup"><span data-stu-id="11474-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="11474-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span><span class="sxs-lookup"><span data-stu-id="11474-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="11474-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span><span class="sxs-lookup"><span data-stu-id="11474-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span></span>
* <span data-ttu-id="11474-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span><span class="sxs-lookup"><span data-stu-id="11474-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span></span>

<span data-ttu-id="11474-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="11474-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="11474-740">9.3.</span></span>    <span data-ttu-id="11474-741">Get Usage Statistics</span><span class="sxs-lookup"><span data-stu-id="11474-741">Get Usage Statistics</span></span>
<span data-ttu-id="11474-742">Gets usage statistics.</span><span class="sxs-lookup"><span data-stu-id="11474-742">Gets usage statistics.</span></span>

| <span data-ttu-id="11474-743">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-743">HTTP Method</span></span> | <span data-ttu-id="11474-744">URI</span><span class="sxs-lookup"><span data-stu-id="11474-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-745">GET</span><span class="sxs-lookup"><span data-stu-id="11474-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-746">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-747">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-747">Parameter Name</span></span> | <span data-ttu-id="11474-748">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-749">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-749">modelId</span></span> |<span data-ttu-id="11474-750">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-750">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-751">startDate</span><span class="sxs-lookup"><span data-stu-id="11474-751">startDate</span></span> |<span data-ttu-id="11474-752">Start date.</span><span class="sxs-lookup"><span data-stu-id="11474-752">Start date.</span></span> <span data-ttu-id="11474-753">Format: yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="11474-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="11474-754">endDate</span><span class="sxs-lookup"><span data-stu-id="11474-754">endDate</span></span> |<span data-ttu-id="11474-755">End date.</span><span class="sxs-lookup"><span data-stu-id="11474-755">End date.</span></span> <span data-ttu-id="11474-756">Format: yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="11474-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="11474-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="11474-757">eventTypes</span></span> |<span data-ttu-id="11474-758">Comma-separated string of event types or null to get all events</span><span class="sxs-lookup"><span data-stu-id="11474-758">Comma-separated string of event types or null to get all events</span></span> |
| <span data-ttu-id="11474-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-759">apiVersion</span></span> |<span data-ttu-id="11474-760">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-760">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-761">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-761">Request Body</span></span> |<span data-ttu-id="11474-762">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-762">NONE</span></span> |

<span data-ttu-id="11474-763">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-763">**Response**:</span></span>

<span data-ttu-id="11474-764">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-764">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-765">A collection of key/value elements.</span><span class="sxs-lookup"><span data-stu-id="11474-765">A collection of key/value elements.</span></span> <span data-ttu-id="11474-766">Each one contains the sum of events for a specific event type grouped by hour.</span><span class="sxs-lookup"><span data-stu-id="11474-766">Each one contains the sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="11474-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span><span class="sxs-lookup"><span data-stu-id="11474-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span></span>
* <span data-ttu-id="11474-768">`feed\entry[i]\content\properties\Value` - Total event count.</span><span class="sxs-lookup"><span data-stu-id="11474-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="11474-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="11474-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="11474-770">9.4.</span></span>    <span data-ttu-id="11474-771">Get Usage File Sample</span><span class="sxs-lookup"><span data-stu-id="11474-771">Get Usage File Sample</span></span>
<span data-ttu-id="11474-772">Retrieves the first 2KB of usage file content.</span><span class="sxs-lookup"><span data-stu-id="11474-772">Retrieves the first 2KB of usage file content.</span></span>

| <span data-ttu-id="11474-773">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-773">HTTP Method</span></span> | <span data-ttu-id="11474-774">URI</span><span class="sxs-lookup"><span data-stu-id="11474-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-775">GET</span><span class="sxs-lookup"><span data-stu-id="11474-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-776">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-777">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-777">Parameter Name</span></span> | <span data-ttu-id="11474-778">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-779">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-779">modelId</span></span> |<span data-ttu-id="11474-780">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-780">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-781">fileId</span><span class="sxs-lookup"><span data-stu-id="11474-781">fileId</span></span> |<span data-ttu-id="11474-782">Unique identifier of the model usage file</span><span class="sxs-lookup"><span data-stu-id="11474-782">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="11474-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-783">apiVersion</span></span> |<span data-ttu-id="11474-784">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-784">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-785">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-785">Request Body</span></span> |<span data-ttu-id="11474-786">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-786">NONE</span></span> |

<span data-ttu-id="11474-787">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-787">**Response**:</span></span>

<span data-ttu-id="11474-788">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-788">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-789">Response is returned in raw text format:</span><span class="sxs-lookup"><span data-stu-id="11474-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="11474-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="11474-790">9.5.</span></span>    <span data-ttu-id="11474-791">Get Model Usage File</span><span class="sxs-lookup"><span data-stu-id="11474-791">Get Model Usage File</span></span>
<span data-ttu-id="11474-792">Retrieves the full content of the usage file.</span><span class="sxs-lookup"><span data-stu-id="11474-792">Retrieves the full content of the usage file.</span></span>

| <span data-ttu-id="11474-793">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-793">HTTP Method</span></span> | <span data-ttu-id="11474-794">URI</span><span class="sxs-lookup"><span data-stu-id="11474-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-795">GET</span><span class="sxs-lookup"><span data-stu-id="11474-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-796">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-797">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-797">Parameter Name</span></span> | <span data-ttu-id="11474-798">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-799">mid</span><span class="sxs-lookup"><span data-stu-id="11474-799">mid</span></span> |<span data-ttu-id="11474-800">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-800">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-801">fid</span><span class="sxs-lookup"><span data-stu-id="11474-801">fid</span></span> |<span data-ttu-id="11474-802">Unique identifier of the model usage file</span><span class="sxs-lookup"><span data-stu-id="11474-802">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="11474-803">download</span><span class="sxs-lookup"><span data-stu-id="11474-803">download</span></span> |<span data-ttu-id="11474-804">1</span><span class="sxs-lookup"><span data-stu-id="11474-804">1</span></span> |
| <span data-ttu-id="11474-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-805">apiVersion</span></span> |<span data-ttu-id="11474-806">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-806">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-807">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-807">Request Body</span></span> |<span data-ttu-id="11474-808">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-808">NONE</span></span> |

<span data-ttu-id="11474-809">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-809">**Response**:</span></span>

<span data-ttu-id="11474-810">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-810">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-811">Response is returned in raw text format:</span><span class="sxs-lookup"><span data-stu-id="11474-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="11474-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="11474-812">9.6.</span></span>    <span data-ttu-id="11474-813">Delete Usage File</span><span class="sxs-lookup"><span data-stu-id="11474-813">Delete Usage File</span></span>
<span data-ttu-id="11474-814">Deletes the specified model usage file.</span><span class="sxs-lookup"><span data-stu-id="11474-814">Deletes the specified model usage file.</span></span>

| <span data-ttu-id="11474-815">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-815">HTTP Method</span></span> | <span data-ttu-id="11474-816">URI</span><span class="sxs-lookup"><span data-stu-id="11474-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-817">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-818">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-819">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-819">Parameter Name</span></span> | <span data-ttu-id="11474-820">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-821">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-821">modelId</span></span> |<span data-ttu-id="11474-822">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-822">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-823">fileId</span><span class="sxs-lookup"><span data-stu-id="11474-823">fileId</span></span> |<span data-ttu-id="11474-824">Unique identifier of the file to be deleted</span><span class="sxs-lookup"><span data-stu-id="11474-824">Unique identifier of the file to be deleted</span></span> |
| <span data-ttu-id="11474-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-825">apiVersion</span></span> |<span data-ttu-id="11474-826">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-826">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-827">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-827">Request Body</span></span> |<span data-ttu-id="11474-828">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-828">NONE</span></span> |

<span data-ttu-id="11474-829">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-829">**Response**:</span></span>

<span data-ttu-id="11474-830">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="11474-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="11474-831">9.7.</span></span>    <span data-ttu-id="11474-832">Delete All Usage Files</span><span class="sxs-lookup"><span data-stu-id="11474-832">Delete All Usage Files</span></span>
<span data-ttu-id="11474-833">Deletes all model usage files.</span><span class="sxs-lookup"><span data-stu-id="11474-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="11474-834">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-834">HTTP Method</span></span> | <span data-ttu-id="11474-835">URI</span><span class="sxs-lookup"><span data-stu-id="11474-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-836">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-837">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-838">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-838">Parameter Name</span></span> | <span data-ttu-id="11474-839">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-840">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-840">modelId</span></span> |<span data-ttu-id="11474-841">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-841">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-842">apiVersion</span></span> |<span data-ttu-id="11474-843">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-843">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-844">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-844">Request Body</span></span> |<span data-ttu-id="11474-845">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-845">NONE</span></span> |

<span data-ttu-id="11474-846">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-846">**Response**:</span></span>

<span data-ttu-id="11474-847">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="11474-848">10. Features</span><span class="sxs-lookup"><span data-stu-id="11474-848">10. Features</span></span>
<span data-ttu-id="11474-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span><span class="sxs-lookup"><span data-stu-id="11474-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="11474-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span><span class="sxs-lookup"><span data-stu-id="11474-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="11474-851">Feature rank can change according to the pattern of usage data and type of items.</span><span class="sxs-lookup"><span data-stu-id="11474-851">Feature rank can change according to the pattern of usage data and type of items.</span></span> <span data-ttu-id="11474-852">But for consistent usage/items, the rank should have only small fluctuations.</span><span class="sxs-lookup"><span data-stu-id="11474-852">But for consistent usage/items, the rank should have only small fluctuations.</span></span>
<span data-ttu-id="11474-853">The rank of features is a non-negative number.</span><span class="sxs-lookup"><span data-stu-id="11474-853">The rank of features is a non-negative number.</span></span> <span data-ttu-id="11474-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span><span class="sxs-lookup"><span data-stu-id="11474-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span></span> <span data-ttu-id="11474-855">The date at which the rank was attributed is called the score freshness.</span><span class="sxs-lookup"><span data-stu-id="11474-855">The date at which the rank was attributed is called the score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="11474-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="11474-856">10.1.</span></span> <span data-ttu-id="11474-857">Get Features Info (For Last Rank Build)</span><span class="sxs-lookup"><span data-stu-id="11474-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="11474-858">Retrieves the feature information, including ranking, for the last successful rank build.</span><span class="sxs-lookup"><span data-stu-id="11474-858">Retrieves the feature information, including ranking, for the last successful rank build.</span></span>

| <span data-ttu-id="11474-859">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-859">HTTP Method</span></span> | <span data-ttu-id="11474-860">URI</span><span class="sxs-lookup"><span data-stu-id="11474-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-861">GET</span><span class="sxs-lookup"><span data-stu-id="11474-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-862">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-863">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-863">Parameter Name</span></span> | <span data-ttu-id="11474-864">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-865">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-865">modelId</span></span> |<span data-ttu-id="11474-866">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-866">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="11474-867">samplingSize</span></span> |<span data-ttu-id="11474-868">Number of values to include for each feature according to the data present in the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-868">Number of values to include for each feature according to the data present in the catalog.</span></span> <br/><span data-ttu-id="11474-869">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="11474-869">Possible values are:</span></span><br> <span data-ttu-id="11474-870">-1 - All samples.</span><span class="sxs-lookup"><span data-stu-id="11474-870">-1 - All samples.</span></span> <br><span data-ttu-id="11474-871">0 - No sampling.</span><span class="sxs-lookup"><span data-stu-id="11474-871">0 - No sampling.</span></span> <br><span data-ttu-id="11474-872">N - Return N samples for each feature name.</span><span class="sxs-lookup"><span data-stu-id="11474-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="11474-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-873">apiVersion</span></span> |<span data-ttu-id="11474-874">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-874">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-875">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-875">Request Body</span></span> |<span data-ttu-id="11474-876">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-876">NONE</span></span> |

<span data-ttu-id="11474-877">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-877">**Response**:</span></span>

<span data-ttu-id="11474-878">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-878">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-879">The response contains a list of feature info entries.</span><span class="sxs-lookup"><span data-stu-id="11474-879">The response contains a list of feature info entries.</span></span> <span data-ttu-id="11474-880">Each entry contains:</span><span class="sxs-lookup"><span data-stu-id="11474-880">Each entry contains:</span></span>

* <span data-ttu-id="11474-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span><span class="sxs-lookup"><span data-stu-id="11474-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="11474-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="11474-883">score freshness feature.</span><span class="sxs-lookup"><span data-stu-id="11474-883">score freshness feature.</span></span> <span data-ttu-id="11474-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span><span class="sxs-lookup"><span data-stu-id="11474-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="11474-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span><span class="sxs-lookup"><span data-stu-id="11474-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="11474-886">A rank of 2.0 and up is considered a good feature.</span><span class="sxs-lookup"><span data-stu-id="11474-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="11474-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span><span class="sxs-lookup"><span data-stu-id="11474-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="11474-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get the features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="11474-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="11474-889">10.2.</span></span> <span data-ttu-id="11474-890">Get Features Info (For Specific Rank Build)</span><span class="sxs-lookup"><span data-stu-id="11474-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="11474-891">Retrieves the feature information, including the ranking for a specific rank build.</span><span class="sxs-lookup"><span data-stu-id="11474-891">Retrieves the feature information, including the ranking for a specific rank build.</span></span>

| <span data-ttu-id="11474-892">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-892">HTTP Method</span></span> | <span data-ttu-id="11474-893">URI</span><span class="sxs-lookup"><span data-stu-id="11474-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-894">GET</span><span class="sxs-lookup"><span data-stu-id="11474-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-895">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-896">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-896">Parameter Name</span></span> | <span data-ttu-id="11474-897">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-898">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-898">modelId</span></span> |<span data-ttu-id="11474-899">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-899">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="11474-900">samplingSize</span></span> |<span data-ttu-id="11474-901">Number of values to include for each feature according to the data present in the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-901">Number of values to include for each feature according to the data present in the catalog.</span></span><br/> <span data-ttu-id="11474-902">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="11474-902">Possible values are:</span></span><br> <span data-ttu-id="11474-903">-1 - All samples.</span><span class="sxs-lookup"><span data-stu-id="11474-903">-1 - All samples.</span></span> <br><span data-ttu-id="11474-904">0 - No sampling.</span><span class="sxs-lookup"><span data-stu-id="11474-904">0 - No sampling.</span></span> <br><span data-ttu-id="11474-905">N - Return N samples for each feature name.</span><span class="sxs-lookup"><span data-stu-id="11474-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="11474-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="11474-906">rankBuildId</span></span> |<span data-ttu-id="11474-907">Unique identifier of the rank build or -1 for the last rank build</span><span class="sxs-lookup"><span data-stu-id="11474-907">Unique identifier of the rank build or -1 for the last rank build</span></span> |
| <span data-ttu-id="11474-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-908">apiVersion</span></span> |<span data-ttu-id="11474-909">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-909">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-910">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-910">Request Body</span></span> |<span data-ttu-id="11474-911">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-911">NONE</span></span> |

<span data-ttu-id="11474-912">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-912">**Response**:</span></span>

<span data-ttu-id="11474-913">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-913">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-914">The response contains a list of feature info entries.</span><span class="sxs-lookup"><span data-stu-id="11474-914">The response contains a list of feature info entries.</span></span> <span data-ttu-id="11474-915">Each entry contains:</span><span class="sxs-lookup"><span data-stu-id="11474-915">Each entry contains:</span></span>

* <span data-ttu-id="11474-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span><span class="sxs-lookup"><span data-stu-id="11474-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="11474-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="11474-918">score freshness feature.</span><span class="sxs-lookup"><span data-stu-id="11474-918">score freshness feature.</span></span> <span data-ttu-id="11474-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span><span class="sxs-lookup"><span data-stu-id="11474-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="11474-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span><span class="sxs-lookup"><span data-stu-id="11474-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="11474-921">A rank of 2.0 and up is considered a good feature.</span><span class="sxs-lookup"><span data-stu-id="11474-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="11474-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span><span class="sxs-lookup"><span data-stu-id="11474-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="11474-923">OData</span><span class="sxs-lookup"><span data-stu-id="11474-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get the features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="11474-924">11. Build</span><span class="sxs-lookup"><span data-stu-id="11474-924">11. Build</span></span>
  <span data-ttu-id="11474-925">This section explains the different APIs related to builds.</span><span class="sxs-lookup"><span data-stu-id="11474-925">This section explains the different APIs related to builds.</span></span> <span data-ttu-id="11474-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span><span class="sxs-lookup"><span data-stu-id="11474-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="11474-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span><span class="sxs-lookup"><span data-stu-id="11474-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span></span> <span data-ttu-id="11474-928">Predictions (for this type of build) come in two flavors:</span><span class="sxs-lookup"><span data-stu-id="11474-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="11474-929">I2I - a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-929">I2I - a.k.a.</span></span> <span data-ttu-id="11474-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span><span class="sxs-lookup"><span data-stu-id="11474-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span></span>
* <span data-ttu-id="11474-931">U2I - a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-931">U2I - a.k.a.</span></span> <span data-ttu-id="11474-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span><span class="sxs-lookup"><span data-stu-id="11474-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span></span> <span data-ttu-id="11474-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span><span class="sxs-lookup"><span data-stu-id="11474-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span></span>

<span data-ttu-id="11474-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span><span class="sxs-lookup"><span data-stu-id="11474-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span></span> <span data-ttu-id="11474-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span><span class="sxs-lookup"><span data-stu-id="11474-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span></span>

* <span data-ttu-id="11474-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span><span class="sxs-lookup"><span data-stu-id="11474-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span></span>
* <span data-ttu-id="11474-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="11474-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="11474-938">Configure a recommendation build with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="11474-938">Configure a recommendation build with the following parameters:</span></span>
  * <span data-ttu-id="11474-939">`useFeatureInModel` - Set to True.</span><span class="sxs-lookup"><span data-stu-id="11474-939">`useFeatureInModel` - Set to True.</span></span>
  * <span data-ttu-id="11474-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span><span class="sxs-lookup"><span data-stu-id="11474-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span></span>
  * <span data-ttu-id="11474-941">`AllowColdItemPlacement` - Set to True.</span><span class="sxs-lookup"><span data-stu-id="11474-941">`AllowColdItemPlacement` - Set to True.</span></span>
  * <span data-ttu-id="11474-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span><span class="sxs-lookup"><span data-stu-id="11474-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="11474-943">Trigger the recommendation build with the configured parameters.</span><span class="sxs-lookup"><span data-stu-id="11474-943">Trigger the recommendation build with the configured parameters.</span></span>

<span data-ttu-id="11474-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span><span class="sxs-lookup"><span data-stu-id="11474-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span></span>

<span data-ttu-id="11474-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span><span class="sxs-lookup"><span data-stu-id="11474-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span></span> <span data-ttu-id="11474-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span><span class="sxs-lookup"><span data-stu-id="11474-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span></span>

<span data-ttu-id="11474-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span><span class="sxs-lookup"><span data-stu-id="11474-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="11474-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span><span class="sxs-lookup"><span data-stu-id="11474-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="11474-949">If no event type is provided all events will be considered as purchase.</span><span class="sxs-lookup"><span data-stu-id="11474-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="11474-950">11.1 Build parameters</span><span class="sxs-lookup"><span data-stu-id="11474-950">11.1 Build parameters</span></span>
<span data-ttu-id="11474-951">Each build type can be configured via a set of parameters (depicted below).</span><span class="sxs-lookup"><span data-stu-id="11474-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="11474-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span><span class="sxs-lookup"><span data-stu-id="11474-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="11474-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="11474-953">11.1.1.</span></span> <span data-ttu-id="11474-954">Usage condenser</span><span class="sxs-lookup"><span data-stu-id="11474-954">Usage condenser</span></span>
<span data-ttu-id="11474-955">Users or items with few usage points might contain more noise than information.</span><span class="sxs-lookup"><span data-stu-id="11474-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="11474-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span><span class="sxs-lookup"><span data-stu-id="11474-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span></span> <span data-ttu-id="11474-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span><span class="sxs-lookup"><span data-stu-id="11474-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="11474-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span><span class="sxs-lookup"><span data-stu-id="11474-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="11474-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="11474-959">11.1.2.</span></span> <span data-ttu-id="11474-960">Rank build parameters</span><span class="sxs-lookup"><span data-stu-id="11474-960">Rank build parameters</span></span>
<span data-ttu-id="11474-961">The table below depicts the build parameters for a rank build.</span><span class="sxs-lookup"><span data-stu-id="11474-961">The table below depicts the build parameters for a rank build.</span></span>

| <span data-ttu-id="11474-962">Key</span><span class="sxs-lookup"><span data-stu-id="11474-962">Key</span></span> | <span data-ttu-id="11474-963">Description</span><span class="sxs-lookup"><span data-stu-id="11474-963">Description</span></span> | <span data-ttu-id="11474-964">Type</span><span class="sxs-lookup"><span data-stu-id="11474-964">Type</span></span> | <span data-ttu-id="11474-965">Valid Value</span><span class="sxs-lookup"><span data-stu-id="11474-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="11474-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="11474-966">NumberOfModelIterations</span></span> |<span data-ttu-id="11474-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span><span class="sxs-lookup"><span data-stu-id="11474-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="11474-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span><span class="sxs-lookup"><span data-stu-id="11474-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="11474-969">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-969">Integer</span></span> |<span data-ttu-id="11474-970">10-50</span><span class="sxs-lookup"><span data-stu-id="11474-970">10-50</span></span> |
| <span data-ttu-id="11474-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="11474-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="11474-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span><span class="sxs-lookup"><span data-stu-id="11474-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="11474-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span><span class="sxs-lookup"><span data-stu-id="11474-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="11474-974">However, too many dimensions will prevent the model from finding correlations between items.</span><span class="sxs-lookup"><span data-stu-id="11474-974">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="11474-975">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-975">Integer</span></span> |<span data-ttu-id="11474-976">10-40</span><span class="sxs-lookup"><span data-stu-id="11474-976">10-40</span></span> |
| <span data-ttu-id="11474-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="11474-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="11474-978">Defines the item lower bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-978">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="11474-979">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-979">See usage condenser above.</span></span> |<span data-ttu-id="11474-980">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-980">Integer</span></span> |<span data-ttu-id="11474-981">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="11474-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="11474-983">Defines the item upper bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-983">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="11474-984">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-984">See usage condenser above.</span></span> |<span data-ttu-id="11474-985">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-985">Integer</span></span> |<span data-ttu-id="11474-986">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="11474-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="11474-988">Defines the user lower bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-988">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="11474-989">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-989">See usage condenser above.</span></span> |<span data-ttu-id="11474-990">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-990">Integer</span></span> |<span data-ttu-id="11474-991">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="11474-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="11474-993">Defines the user upper bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-993">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="11474-994">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-994">See usage condenser above.</span></span> |<span data-ttu-id="11474-995">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-995">Integer</span></span> |<span data-ttu-id="11474-996">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="11474-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="11474-997">11.1.3.</span></span> <span data-ttu-id="11474-998">Recommendation build parameters</span><span class="sxs-lookup"><span data-stu-id="11474-998">Recommendation build parameters</span></span>
<span data-ttu-id="11474-999">The table below depicts the build parameters for recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-999">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="11474-1000">Key</span><span class="sxs-lookup"><span data-stu-id="11474-1000">Key</span></span> | <span data-ttu-id="11474-1001">Description</span><span class="sxs-lookup"><span data-stu-id="11474-1001">Description</span></span> | <span data-ttu-id="11474-1002">Type</span><span class="sxs-lookup"><span data-stu-id="11474-1002">Type</span></span> | <span data-ttu-id="11474-1003">Valid Value</span><span class="sxs-lookup"><span data-stu-id="11474-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="11474-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="11474-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="11474-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span><span class="sxs-lookup"><span data-stu-id="11474-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="11474-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span><span class="sxs-lookup"><span data-stu-id="11474-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="11474-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1007">Integer</span></span> |<span data-ttu-id="11474-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="11474-1008">10-50</span></span> |
| <span data-ttu-id="11474-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="11474-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="11474-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span><span class="sxs-lookup"><span data-stu-id="11474-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="11474-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span><span class="sxs-lookup"><span data-stu-id="11474-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="11474-1012">However, too many dimensions will prevent the model from finding correlations between items.</span><span class="sxs-lookup"><span data-stu-id="11474-1012">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="11474-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1013">Integer</span></span> |<span data-ttu-id="11474-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="11474-1014">10-40</span></span> |
| <span data-ttu-id="11474-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="11474-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="11474-1016">Defines the item lower bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1016">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="11474-1017">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1017">See usage condenser above.</span></span> |<span data-ttu-id="11474-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1018">Integer</span></span> |<span data-ttu-id="11474-1019">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="11474-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="11474-1021">Defines the item upper bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1021">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="11474-1022">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1022">See usage condenser above.</span></span> |<span data-ttu-id="11474-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1023">Integer</span></span> |<span data-ttu-id="11474-1024">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="11474-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="11474-1026">Defines the user lower bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1026">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="11474-1027">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1027">See usage condenser above.</span></span> |<span data-ttu-id="11474-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1028">Integer</span></span> |<span data-ttu-id="11474-1029">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="11474-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="11474-1031">Defines the user upper bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1031">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="11474-1032">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1032">See usage condenser above.</span></span> |<span data-ttu-id="11474-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1033">Integer</span></span> |<span data-ttu-id="11474-1034">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1035">Description</span><span class="sxs-lookup"><span data-stu-id="11474-1035">Description</span></span> |<span data-ttu-id="11474-1036">Build description.</span><span class="sxs-lookup"><span data-stu-id="11474-1036">Build description.</span></span> |<span data-ttu-id="11474-1037">String</span><span class="sxs-lookup"><span data-stu-id="11474-1037">String</span></span> |<span data-ttu-id="11474-1038">Any text, maximum 512 chars</span><span class="sxs-lookup"><span data-stu-id="11474-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="11474-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="11474-1039">EnableModelingInsights</span></span> |<span data-ttu-id="11474-1040">Allows you to compute metrics on the recommendation model.</span><span class="sxs-lookup"><span data-stu-id="11474-1040">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="11474-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1041">Boolean</span></span> |<span data-ttu-id="11474-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1042">True/False</span></span> |
| <span data-ttu-id="11474-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="11474-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="11474-1044">Indicates if features can be used in order to enhance the recommendation model.</span><span class="sxs-lookup"><span data-stu-id="11474-1044">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="11474-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1045">Boolean</span></span> |<span data-ttu-id="11474-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1046">True/False</span></span> |
| <span data-ttu-id="11474-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="11474-1047">ModelingFeatureList</span></span> |<span data-ttu-id="11474-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span><span class="sxs-lookup"><span data-stu-id="11474-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="11474-1049">String</span><span class="sxs-lookup"><span data-stu-id="11474-1049">String</span></span> |<span data-ttu-id="11474-1050">Feature names, up to 512 chars</span><span class="sxs-lookup"><span data-stu-id="11474-1050">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="11474-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="11474-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="11474-1052">Indicates if the recommendation should also push cold items via feature similarity.</span><span class="sxs-lookup"><span data-stu-id="11474-1052">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="11474-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1053">Boolean</span></span> |<span data-ttu-id="11474-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1054">True/False</span></span> |
| <span data-ttu-id="11474-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="11474-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="11474-1056">Indicates if features can be used in reasoning.</span><span class="sxs-lookup"><span data-stu-id="11474-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="11474-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1057">Boolean</span></span> |<span data-ttu-id="11474-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1058">True/False</span></span> |
| <span data-ttu-id="11474-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="11474-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="11474-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="11474-1061">String</span><span class="sxs-lookup"><span data-stu-id="11474-1061">String</span></span> |<span data-ttu-id="11474-1062">Feature names, up to 512 chars</span><span class="sxs-lookup"><span data-stu-id="11474-1062">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="11474-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="11474-1063">EnableU2I</span></span> |<span data-ttu-id="11474-1064">Allow the personalized recommendation a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-1064">Allow the personalized recommendation a.k.a.</span></span> <span data-ttu-id="11474-1065">U2I (user to item recommendations).</span><span class="sxs-lookup"><span data-stu-id="11474-1065">U2I (user to item recommendations).</span></span> |<span data-ttu-id="11474-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1066">Boolean</span></span> |<span data-ttu-id="11474-1067">True/False (default true)</span><span class="sxs-lookup"><span data-stu-id="11474-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="11474-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="11474-1068">11.1.4.</span></span> <span data-ttu-id="11474-1069">FBT build parameters</span><span class="sxs-lookup"><span data-stu-id="11474-1069">FBT build parameters</span></span>
<span data-ttu-id="11474-1070">The table below depicts the build parameters for recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-1070">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="11474-1071">Key</span><span class="sxs-lookup"><span data-stu-id="11474-1071">Key</span></span> | <span data-ttu-id="11474-1072">Description</span><span class="sxs-lookup"><span data-stu-id="11474-1072">Description</span></span> | <span data-ttu-id="11474-1073">Type</span><span class="sxs-lookup"><span data-stu-id="11474-1073">Type</span></span> | <span data-ttu-id="11474-1074">Valid Value (Default)</span><span class="sxs-lookup"><span data-stu-id="11474-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="11474-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="11474-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="11474-1076">How conservative the model is.</span><span class="sxs-lookup"><span data-stu-id="11474-1076">How conservative the model is.</span></span> <span data-ttu-id="11474-1077">Number of co-occurrences of items to be considered for modeling.</span><span class="sxs-lookup"><span data-stu-id="11474-1077">Number of co-occurrences of items to be considered for modeling.</span></span> |<span data-ttu-id="11474-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1078">Integer</span></span> |<span data-ttu-id="11474-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="11474-1079">3-50 (6)</span></span> |
| <span data-ttu-id="11474-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="11474-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="11474-1081">Bounds the number of items in a frequent set.</span><span class="sxs-lookup"><span data-stu-id="11474-1081">Bounds the number of items in a frequent set.</span></span> |<span data-ttu-id="11474-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1082">Integer</span></span> |<span data-ttu-id="11474-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="11474-1083">2-3 (2)</span></span> |
| <span data-ttu-id="11474-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="11474-1084">FbtMinimalScore</span></span> |<span data-ttu-id="11474-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span><span class="sxs-lookup"><span data-stu-id="11474-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span></span> <span data-ttu-id="11474-1086">The higher the better.</span><span class="sxs-lookup"><span data-stu-id="11474-1086">The higher the better.</span></span> |<span data-ttu-id="11474-1087">Double</span><span class="sxs-lookup"><span data-stu-id="11474-1087">Double</span></span> |<span data-ttu-id="11474-1088">0 and above (0)</span><span class="sxs-lookup"><span data-stu-id="11474-1088">0 and above (0)</span></span> |
| <span data-ttu-id="11474-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="11474-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="11474-1090">Defines the similarity function to be used by the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1090">Defines the similarity function to be used by the build.</span></span> <span data-ttu-id="11474-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span><span class="sxs-lookup"><span data-stu-id="11474-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span></span> |<span data-ttu-id="11474-1092">String</span><span class="sxs-lookup"><span data-stu-id="11474-1092">String</span></span> |<span data-ttu-id="11474-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="11474-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="11474-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="11474-1094">11.2.</span></span> <span data-ttu-id="11474-1095">Trigger a Recommendation Build</span><span class="sxs-lookup"><span data-stu-id="11474-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="11474-1096">By default this API will trigger a recommendation model build.</span><span class="sxs-lookup"><span data-stu-id="11474-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="11474-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span><span class="sxs-lookup"><span data-stu-id="11474-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="11474-1098">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1098">HTTP Method</span></span> | <span data-ttu-id="11474-1099">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1100">POST</span><span class="sxs-lookup"><span data-stu-id="11474-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1101">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="11474-1102">HEADER</span><span class="sxs-lookup"><span data-stu-id="11474-1102">HEADER</span></span> |<span data-ttu-id="11474-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span><span class="sxs-lookup"><span data-stu-id="11474-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="11474-1104">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1104">Parameter Name</span></span> | <span data-ttu-id="11474-1105">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1106">modelId</span></span> |<span data-ttu-id="11474-1107">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1107">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="11474-1108">userDescription</span></span> |<span data-ttu-id="11474-1109">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-1109">Textual identifier of the catalog.</span></span> <span data-ttu-id="11474-1110">Note that if you use spaces you must encode it with %20 instead.</span><span class="sxs-lookup"><span data-stu-id="11474-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="11474-1111">See example above.</span><span class="sxs-lookup"><span data-stu-id="11474-1111">See example above.</span></span><br><span data-ttu-id="11474-1112">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="11474-1112">Max length: 50</span></span> |
| <span data-ttu-id="11474-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1113">apiVersion</span></span> |<span data-ttu-id="11474-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-1115">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-1115">Request Body</span></span> |<span data-ttu-id="11474-1116">If left empty then the build will be executed with the default build parameters.</span><span class="sxs-lookup"><span data-stu-id="11474-1116">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="11474-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span><span class="sxs-lookup"><span data-stu-id="11474-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span></span> <span data-ttu-id="11474-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="11474-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="11474-1119">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-1119">**Response**:</span></span>

<span data-ttu-id="11474-1120">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1121">This is an asynchronous API.</span><span class="sxs-lookup"><span data-stu-id="11474-1121">This is an asynchronous API.</span></span> <span data-ttu-id="11474-1122">You will get a build ID as a response.</span><span class="sxs-lookup"><span data-stu-id="11474-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="11474-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span><span class="sxs-lookup"><span data-stu-id="11474-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="11474-1124">Note that a build can take from minutes to hours depending on the size of the data.</span><span class="sxs-lookup"><span data-stu-id="11474-1124">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="11474-1125">You cannot consume recommendations till the build ends.</span><span class="sxs-lookup"><span data-stu-id="11474-1125">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="11474-1126">Valid build status:</span><span class="sxs-lookup"><span data-stu-id="11474-1126">Valid build status:</span></span>

* <span data-ttu-id="11474-1127">Create - Build request was created.</span><span class="sxs-lookup"><span data-stu-id="11474-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="11474-1128">Queued - Build request was sent and it is queued.</span><span class="sxs-lookup"><span data-stu-id="11474-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="11474-1129">Building - Build is in progress.</span><span class="sxs-lookup"><span data-stu-id="11474-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="11474-1130">Success - Build ended successfully.</span><span class="sxs-lookup"><span data-stu-id="11474-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="11474-1131">Error - Build ended with a failure.</span><span class="sxs-lookup"><span data-stu-id="11474-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="11474-1132">Cancelled - Build was cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="11474-1133">Cancelling - A cancel request for the build was sent.</span><span class="sxs-lookup"><span data-stu-id="11474-1133">Cancelling - A cancel request for the build was sent.</span></span>

<span data-ttu-id="11474-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="11474-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="11474-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="11474-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="11474-1136">11.3.</span></span> <span data-ttu-id="11474-1137">Trigger Build (Recommendation, Rank or FBT)</span><span class="sxs-lookup"><span data-stu-id="11474-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="11474-1138">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1138">HTTP Method</span></span> | <span data-ttu-id="11474-1139">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1140">POST</span><span class="sxs-lookup"><span data-stu-id="11474-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1141">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="11474-1142">HEADER</span><span class="sxs-lookup"><span data-stu-id="11474-1142">HEADER</span></span> |<span data-ttu-id="11474-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span><span class="sxs-lookup"><span data-stu-id="11474-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="11474-1144">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1144">Parameter Name</span></span> | <span data-ttu-id="11474-1145">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1146">modelId</span></span> |<span data-ttu-id="11474-1147">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1147">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="11474-1148">userDescription</span></span> |<span data-ttu-id="11474-1149">Textual identifier of the catalog.</span><span class="sxs-lookup"><span data-stu-id="11474-1149">Textual identifier of the catalog.</span></span> <span data-ttu-id="11474-1150">Note that if you use spaces you must encode it with %20 instead.</span><span class="sxs-lookup"><span data-stu-id="11474-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="11474-1151">See example above.</span><span class="sxs-lookup"><span data-stu-id="11474-1151">See example above.</span></span><br><span data-ttu-id="11474-1152">Max length: 50</span><span class="sxs-lookup"><span data-stu-id="11474-1152">Max length: 50</span></span> |
| <span data-ttu-id="11474-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="11474-1153">buildType</span></span> |<span data-ttu-id="11474-1154">Type of the build to invoke:</span><span class="sxs-lookup"><span data-stu-id="11474-1154">Type of the build to invoke:</span></span> <br/> <span data-ttu-id="11474-1155">- 'Recommendation' for recommendation build</span><span class="sxs-lookup"><span data-stu-id="11474-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="11474-1156">- 'Ranking' for rank build</span><span class="sxs-lookup"><span data-stu-id="11474-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="11474-1157">- 'Fbt' for FBT build</span><span class="sxs-lookup"><span data-stu-id="11474-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="11474-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1158">apiVersion</span></span> |<span data-ttu-id="11474-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-1160">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-1160">Request Body</span></span> |<span data-ttu-id="11474-1161">If left empty then the build will be executed with the default build parameters.</span><span class="sxs-lookup"><span data-stu-id="11474-1161">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="11474-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span><span class="sxs-lookup"><span data-stu-id="11474-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span></span> <span data-ttu-id="11474-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="11474-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="11474-1164">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-1164">**Response**:</span></span>

<span data-ttu-id="11474-1165">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1166">This is an asynchronous API.</span><span class="sxs-lookup"><span data-stu-id="11474-1166">This is an asynchronous API.</span></span> <span data-ttu-id="11474-1167">You will get a build ID as a response.</span><span class="sxs-lookup"><span data-stu-id="11474-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="11474-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span><span class="sxs-lookup"><span data-stu-id="11474-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="11474-1169">Note that a build can take from minutes to hours depending on the size of the data.</span><span class="sxs-lookup"><span data-stu-id="11474-1169">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="11474-1170">You cannot consume recommendations till the build ends.</span><span class="sxs-lookup"><span data-stu-id="11474-1170">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="11474-1171">Valid build status:</span><span class="sxs-lookup"><span data-stu-id="11474-1171">Valid build status:</span></span>

* <span data-ttu-id="11474-1172">Create - Model was created.</span><span class="sxs-lookup"><span data-stu-id="11474-1172">Create - Model was created.</span></span>
* <span data-ttu-id="11474-1173">Queued - Model build was triggered and it is queued.</span><span class="sxs-lookup"><span data-stu-id="11474-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="11474-1174">Building - Model is being built.</span><span class="sxs-lookup"><span data-stu-id="11474-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="11474-1175">Success - Build ended successfully.</span><span class="sxs-lookup"><span data-stu-id="11474-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="11474-1176">Error - Build ended with a failure.</span><span class="sxs-lookup"><span data-stu-id="11474-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="11474-1177">Cancelled - Build was cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="11474-1178">Cancelling - Build is being cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="11474-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="11474-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="11474-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="11474-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="11474-1181">11.4.</span></span> <span data-ttu-id="11474-1182">Get Builds Status of a Model</span><span class="sxs-lookup"><span data-stu-id="11474-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="11474-1183">Retrieves builds and their status for a specified model.</span><span class="sxs-lookup"><span data-stu-id="11474-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="11474-1184">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1184">HTTP Method</span></span> | <span data-ttu-id="11474-1185">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1186">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1187">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1188">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1188">Parameter Name</span></span> | <span data-ttu-id="11474-1189">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1190">modelId</span></span> |<span data-ttu-id="11474-1191">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1191">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="11474-1192">onlyLastBuild</span></span> |<span data-ttu-id="11474-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span><span class="sxs-lookup"><span data-stu-id="11474-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span></span> |
| <span data-ttu-id="11474-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1194">apiVersion</span></span> |<span data-ttu-id="11474-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1195">1.0</span></span> |

<span data-ttu-id="11474-1196">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-1196">**Response**:</span></span>

<span data-ttu-id="11474-1197">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1198">The response includes one entry per build.</span><span class="sxs-lookup"><span data-stu-id="11474-1198">The response includes one entry per build.</span></span> <span data-ttu-id="11474-1199">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1199">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1200">`feed/entry/content/properties/UserName` - Name of the user.</span><span class="sxs-lookup"><span data-stu-id="11474-1200">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="11474-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span><span class="sxs-lookup"><span data-stu-id="11474-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="11474-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span><span class="sxs-lookup"><span data-stu-id="11474-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="11474-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="11474-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="11474-1204">active build).</span><span class="sxs-lookup"><span data-stu-id="11474-1204">active build).</span></span>
* <span data-ttu-id="11474-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span><span class="sxs-lookup"><span data-stu-id="11474-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="11474-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="11474-1207">`feed/entry/content/properties/Status` - Build status.</span><span class="sxs-lookup"><span data-stu-id="11474-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="11474-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span><span class="sxs-lookup"><span data-stu-id="11474-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="11474-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span><span class="sxs-lookup"><span data-stu-id="11474-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="11474-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span><span class="sxs-lookup"><span data-stu-id="11474-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="11474-1211">`feed/entry/content/properties/StartTime` - Build start time.</span><span class="sxs-lookup"><span data-stu-id="11474-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="11474-1212">`feed/entry/content/properties/EndTime` - Build end time.</span><span class="sxs-lookup"><span data-stu-id="11474-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="11474-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span><span class="sxs-lookup"><span data-stu-id="11474-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="11474-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span><span class="sxs-lookup"><span data-stu-id="11474-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="11474-1215">Valid build status:</span><span class="sxs-lookup"><span data-stu-id="11474-1215">Valid build status:</span></span>

* <span data-ttu-id="11474-1216">Created - Build request entry was created.</span><span class="sxs-lookup"><span data-stu-id="11474-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="11474-1217">Queued - Build request was triggered and it is queued.</span><span class="sxs-lookup"><span data-stu-id="11474-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="11474-1218">Building - Build is in process.</span><span class="sxs-lookup"><span data-stu-id="11474-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="11474-1219">Success - Build ended successfully.</span><span class="sxs-lookup"><span data-stu-id="11474-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="11474-1220">Error - Build ended with a failure.</span><span class="sxs-lookup"><span data-stu-id="11474-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="11474-1221">Cancelled - Build was cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="11474-1222">Cancelling - Build is being cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="11474-1223">Valid values for build type:</span><span class="sxs-lookup"><span data-stu-id="11474-1223">Valid values for build type:</span></span>

* <span data-ttu-id="11474-1224">Rank - Rank build.</span><span class="sxs-lookup"><span data-stu-id="11474-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="11474-1225">Recommendation - Recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="11474-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="11474-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="11474-1227">11.5.</span></span> <span data-ttu-id="11474-1228">Get Builds Status</span><span class="sxs-lookup"><span data-stu-id="11474-1228">Get Builds Status</span></span>
<span data-ttu-id="11474-1229">Retrieves build statuses of all models of a user.</span><span class="sxs-lookup"><span data-stu-id="11474-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="11474-1230">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1230">HTTP Method</span></span> | <span data-ttu-id="11474-1231">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1232">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1233">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1234">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1234">Parameter Name</span></span> | <span data-ttu-id="11474-1235">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="11474-1236">onlyLastBuild</span></span> |<span data-ttu-id="11474-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span><span class="sxs-lookup"><span data-stu-id="11474-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="11474-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1238">apiVersion</span></span> |<span data-ttu-id="11474-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1239">1.0</span></span> |

<span data-ttu-id="11474-1240">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-1240">**Response**:</span></span>

<span data-ttu-id="11474-1241">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1242">The response includes one entry per build.</span><span class="sxs-lookup"><span data-stu-id="11474-1242">The response includes one entry per build.</span></span> <span data-ttu-id="11474-1243">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1243">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1244">`feed/entry/content/properties/UserName` - Name of the user.</span><span class="sxs-lookup"><span data-stu-id="11474-1244">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="11474-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span><span class="sxs-lookup"><span data-stu-id="11474-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="11474-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span><span class="sxs-lookup"><span data-stu-id="11474-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="11474-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span><span class="sxs-lookup"><span data-stu-id="11474-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span></span>
* <span data-ttu-id="11474-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span><span class="sxs-lookup"><span data-stu-id="11474-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="11474-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="11474-1250">`feed/entry/content/properties/Status` - Build status.</span><span class="sxs-lookup"><span data-stu-id="11474-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="11474-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span><span class="sxs-lookup"><span data-stu-id="11474-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="11474-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span><span class="sxs-lookup"><span data-stu-id="11474-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="11474-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span><span class="sxs-lookup"><span data-stu-id="11474-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="11474-1254">`feed/entry/content/properties/StartTime` - Build start time.</span><span class="sxs-lookup"><span data-stu-id="11474-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="11474-1255">`feed/entry/content/properties/EndTime` - Build end time.</span><span class="sxs-lookup"><span data-stu-id="11474-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="11474-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span><span class="sxs-lookup"><span data-stu-id="11474-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="11474-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span><span class="sxs-lookup"><span data-stu-id="11474-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="11474-1258">Valid build status:</span><span class="sxs-lookup"><span data-stu-id="11474-1258">Valid build status:</span></span>

* <span data-ttu-id="11474-1259">Created - Build request entry was created.</span><span class="sxs-lookup"><span data-stu-id="11474-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="11474-1260">Queued - Build request was triggered and it is queued.</span><span class="sxs-lookup"><span data-stu-id="11474-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="11474-1261">Building - Build is in process.</span><span class="sxs-lookup"><span data-stu-id="11474-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="11474-1262">Success - Build ended successfully.</span><span class="sxs-lookup"><span data-stu-id="11474-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="11474-1263">Error - Build ended with a failure.</span><span class="sxs-lookup"><span data-stu-id="11474-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="11474-1264">Cancelled - Build was cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="11474-1265">Cancelling - Build is being cancelled.</span><span class="sxs-lookup"><span data-stu-id="11474-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="11474-1266">Valid values for build type:</span><span class="sxs-lookup"><span data-stu-id="11474-1266">Valid values for build type:</span></span>

* <span data-ttu-id="11474-1267">Rank - Rank build.</span><span class="sxs-lookup"><span data-stu-id="11474-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="11474-1268">Recommendation - Recommendation build.</span><span class="sxs-lookup"><span data-stu-id="11474-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="11474-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="11474-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="11474-1270">11.6.</span></span> <span data-ttu-id="11474-1271">Delete Build</span><span class="sxs-lookup"><span data-stu-id="11474-1271">Delete Build</span></span>
<span data-ttu-id="11474-1272">Deletes a build.</span><span class="sxs-lookup"><span data-stu-id="11474-1272">Deletes a build.</span></span>

<span data-ttu-id="11474-1273">NOTE:</span><span class="sxs-lookup"><span data-stu-id="11474-1273">NOTE:</span></span> <br><span data-ttu-id="11474-1274">You cannot delete an active build.</span><span class="sxs-lookup"><span data-stu-id="11474-1274">You cannot delete an active build.</span></span> <span data-ttu-id="11474-1275">The model should be updated to a different active build before you delete it.</span><span class="sxs-lookup"><span data-stu-id="11474-1275">The model should be updated to a different active build before you delete it.</span></span><br><span data-ttu-id="11474-1276">You cannot delete an in-progress build.</span><span class="sxs-lookup"><span data-stu-id="11474-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="11474-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span><span class="sxs-lookup"><span data-stu-id="11474-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="11474-1278">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1278">HTTP Method</span></span> | <span data-ttu-id="11474-1279">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1280">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1281">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1282">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1282">Parameter Name</span></span> | <span data-ttu-id="11474-1283">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1284">buildId</span></span> |<span data-ttu-id="11474-1285">Unique identifier of the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1285">Unique identifier of the build.</span></span> |
| <span data-ttu-id="11474-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1286">apiVersion</span></span> |<span data-ttu-id="11474-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1287">1.0</span></span> |

<span data-ttu-id="11474-1288">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1288">**Response:**</span></span>

<span data-ttu-id="11474-1289">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="11474-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="11474-1290">11.7.</span></span> <span data-ttu-id="11474-1291">Cancel Build</span><span class="sxs-lookup"><span data-stu-id="11474-1291">Cancel Build</span></span>
<span data-ttu-id="11474-1292">Cancels a build that is in building status.</span><span class="sxs-lookup"><span data-stu-id="11474-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="11474-1293">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1293">HTTP Method</span></span> | <span data-ttu-id="11474-1294">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="11474-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1296">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1297">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1297">Parameter Name</span></span> | <span data-ttu-id="11474-1298">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1299">buildId</span></span> |<span data-ttu-id="11474-1300">Unique identifier of the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1300">Unique identifier of the build.</span></span> |
| <span data-ttu-id="11474-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1301">apiVersion</span></span> |<span data-ttu-id="11474-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1302">1.0</span></span> |

<span data-ttu-id="11474-1303">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1303">**Response:**</span></span>

<span data-ttu-id="11474-1304">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="11474-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="11474-1305">11.8.</span></span> <span data-ttu-id="11474-1306">Get Build Parameters</span><span class="sxs-lookup"><span data-stu-id="11474-1306">Get Build Parameters</span></span>
<span data-ttu-id="11474-1307">Retrieves build parameters.</span><span class="sxs-lookup"><span data-stu-id="11474-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="11474-1308">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1308">HTTP Method</span></span> | <span data-ttu-id="11474-1309">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1310">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1311">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1312">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1312">Parameter Name</span></span> | <span data-ttu-id="11474-1313">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1314">buildId</span></span> |<span data-ttu-id="11474-1315">Unique identifier of the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1315">Unique identifier of the build.</span></span> |
| <span data-ttu-id="11474-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1316">apiVersion</span></span> |<span data-ttu-id="11474-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1317">1.0</span></span> |

<span data-ttu-id="11474-1318">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1318">**Response:**</span></span>

<span data-ttu-id="11474-1319">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1320">This API returns a collection of key/value elements.</span><span class="sxs-lookup"><span data-stu-id="11474-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="11474-1321">Each element represents a parameter and its value:</span><span class="sxs-lookup"><span data-stu-id="11474-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="11474-1322">`feed/entry/content/properties/Key` - Build parameter name.</span><span class="sxs-lookup"><span data-stu-id="11474-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="11474-1323">`feed/entry/content/properties/Value` - Build parameter value.</span><span class="sxs-lookup"><span data-stu-id="11474-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="11474-1324">The table below depicts the value that each key represents.</span><span class="sxs-lookup"><span data-stu-id="11474-1324">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="11474-1325">Key</span><span class="sxs-lookup"><span data-stu-id="11474-1325">Key</span></span> | <span data-ttu-id="11474-1326">Description</span><span class="sxs-lookup"><span data-stu-id="11474-1326">Description</span></span> | <span data-ttu-id="11474-1327">Type</span><span class="sxs-lookup"><span data-stu-id="11474-1327">Type</span></span> | <span data-ttu-id="11474-1328">Valid Value</span><span class="sxs-lookup"><span data-stu-id="11474-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="11474-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="11474-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="11474-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span><span class="sxs-lookup"><span data-stu-id="11474-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="11474-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span><span class="sxs-lookup"><span data-stu-id="11474-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="11474-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1332">Integer</span></span> |<span data-ttu-id="11474-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="11474-1333">10-50</span></span> |
| <span data-ttu-id="11474-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="11474-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="11474-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span><span class="sxs-lookup"><span data-stu-id="11474-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="11474-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span><span class="sxs-lookup"><span data-stu-id="11474-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="11474-1337">However, too many dimensions will prevent the model from finding correlations between items.</span><span class="sxs-lookup"><span data-stu-id="11474-1337">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="11474-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1338">Integer</span></span> |<span data-ttu-id="11474-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="11474-1339">10-40</span></span> |
| <span data-ttu-id="11474-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="11474-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="11474-1341">Defines the item lower bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1341">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="11474-1342">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1342">See usage condenser above.</span></span> |<span data-ttu-id="11474-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1343">Integer</span></span> |<span data-ttu-id="11474-1344">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="11474-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="11474-1346">Defines the item upper bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1346">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="11474-1347">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1347">See usage condenser above.</span></span> |<span data-ttu-id="11474-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1348">Integer</span></span> |<span data-ttu-id="11474-1349">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="11474-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="11474-1351">Defines the user lower bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1351">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="11474-1352">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1352">See usage condenser above.</span></span> |<span data-ttu-id="11474-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1353">Integer</span></span> |<span data-ttu-id="11474-1354">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="11474-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="11474-1356">Defines the user upper bound for the condenser.</span><span class="sxs-lookup"><span data-stu-id="11474-1356">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="11474-1357">See usage condenser above.</span><span class="sxs-lookup"><span data-stu-id="11474-1357">See usage condenser above.</span></span> |<span data-ttu-id="11474-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="11474-1358">Integer</span></span> |<span data-ttu-id="11474-1359">2 or more (0 disable condenser)</span><span class="sxs-lookup"><span data-stu-id="11474-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="11474-1360">Description</span><span class="sxs-lookup"><span data-stu-id="11474-1360">Description</span></span> |<span data-ttu-id="11474-1361">Build description.</span><span class="sxs-lookup"><span data-stu-id="11474-1361">Build description.</span></span> |<span data-ttu-id="11474-1362">String</span><span class="sxs-lookup"><span data-stu-id="11474-1362">String</span></span> |<span data-ttu-id="11474-1363">Any text, maximum 512 chars</span><span class="sxs-lookup"><span data-stu-id="11474-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="11474-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="11474-1364">EnableModelingInsights</span></span> |<span data-ttu-id="11474-1365">Allows you to compute metrics on the recommendation model.</span><span class="sxs-lookup"><span data-stu-id="11474-1365">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="11474-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1366">Boolean</span></span> |<span data-ttu-id="11474-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1367">True/False</span></span> |
| <span data-ttu-id="11474-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="11474-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="11474-1369">Indicates if features can be used in order to enhance the recommendation model.</span><span class="sxs-lookup"><span data-stu-id="11474-1369">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="11474-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1370">Boolean</span></span> |<span data-ttu-id="11474-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1371">True/False</span></span> |
| <span data-ttu-id="11474-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="11474-1372">ModelingFeatureList</span></span> |<span data-ttu-id="11474-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span><span class="sxs-lookup"><span data-stu-id="11474-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="11474-1374">String</span><span class="sxs-lookup"><span data-stu-id="11474-1374">String</span></span> |<span data-ttu-id="11474-1375">Feature names, up to 512 chars</span><span class="sxs-lookup"><span data-stu-id="11474-1375">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="11474-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="11474-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="11474-1377">Indicates if the recommendation should also push cold items via feature similarity.</span><span class="sxs-lookup"><span data-stu-id="11474-1377">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="11474-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1378">Boolean</span></span> |<span data-ttu-id="11474-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1379">True/False</span></span> |
| <span data-ttu-id="11474-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="11474-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="11474-1381">Indicates if features can be used in reasoning.</span><span class="sxs-lookup"><span data-stu-id="11474-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="11474-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="11474-1382">Boolean</span></span> |<span data-ttu-id="11474-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="11474-1383">True/False</span></span> |
| <span data-ttu-id="11474-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="11474-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="11474-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="11474-1386">String</span><span class="sxs-lookup"><span data-stu-id="11474-1386">String</span></span> |<span data-ttu-id="11474-1387">Feature names, up to 512 chars</span><span class="sxs-lookup"><span data-stu-id="11474-1387">Feature names, up to 512 chars</span></span> |

<span data-ttu-id="11474-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="11474-1389">12. Recommendation</span><span class="sxs-lookup"><span data-stu-id="11474-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="11474-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="11474-1390">12.1.</span></span> <span data-ttu-id="11474-1391">Get Item Recommendations (for active build)</span><span class="sxs-lookup"><span data-stu-id="11474-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="11474-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span><span class="sxs-lookup"><span data-stu-id="11474-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="11474-1393">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1393">HTTP Method</span></span> | <span data-ttu-id="11474-1394">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1395">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1396">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1397">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1397">Parameter Name</span></span> | <span data-ttu-id="11474-1398">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1399">modelId</span></span> |<span data-ttu-id="11474-1400">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1400">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="11474-1401">itemIds</span></span> |<span data-ttu-id="11474-1402">Comma-separated list of the items to recommend for.</span><span class="sxs-lookup"><span data-stu-id="11474-1402">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="11474-1403">If the active build is of type FBT then you can send only one item.</span><span class="sxs-lookup"><span data-stu-id="11474-1403">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="11474-1404">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="11474-1404">Max length: 1024</span></span> |
| <span data-ttu-id="11474-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1405">numberOfResults</span></span> |<span data-ttu-id="11474-1406">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1406">Number of required results</span></span> <br> <span data-ttu-id="11474-1407">Max: 150</span><span class="sxs-lookup"><span data-stu-id="11474-1407">Max: 150</span></span> |
| <span data-ttu-id="11474-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1408">includeMetatadata</span></span> |<span data-ttu-id="11474-1409">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1409">Future use, always false</span></span> |
| <span data-ttu-id="11474-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1410">apiVersion</span></span> |<span data-ttu-id="11474-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1411">1.0</span></span> |

<span data-ttu-id="11474-1412">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1412">**Response:**</span></span>

<span data-ttu-id="11474-1413">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1414">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1414">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1415">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1415">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1417">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1417">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1420">The example response below includes 10 recommended items.</span><span class="sxs-lookup"><span data-stu-id="11474-1420">The example response below includes 10 recommended items.</span></span>

<span data-ttu-id="11474-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="11474-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="11474-1422">12.2.</span></span> <span data-ttu-id="11474-1423">Get Item Recommendations (of a specific build)</span><span class="sxs-lookup"><span data-stu-id="11474-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="11474-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span><span class="sxs-lookup"><span data-stu-id="11474-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="11474-1425">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1425">HTTP Method</span></span> | <span data-ttu-id="11474-1426">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1427">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1428">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1429">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1429">Parameter Name</span></span> | <span data-ttu-id="11474-1430">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1431">modelId</span></span> |<span data-ttu-id="11474-1432">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1432">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="11474-1433">itemIds</span></span> |<span data-ttu-id="11474-1434">Comma-separated list of the items to recommend for.</span><span class="sxs-lookup"><span data-stu-id="11474-1434">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="11474-1435">If the active build is of type FBT then you can send only one item.</span><span class="sxs-lookup"><span data-stu-id="11474-1435">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="11474-1436">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="11474-1436">Max length: 1024</span></span> |
| <span data-ttu-id="11474-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1437">numberOfResults</span></span> |<span data-ttu-id="11474-1438">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1438">Number of required results</span></span> <br> <span data-ttu-id="11474-1439">Max: 150</span><span class="sxs-lookup"><span data-stu-id="11474-1439">Max: 150</span></span> |
| <span data-ttu-id="11474-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1440">includeMetatadata</span></span> |<span data-ttu-id="11474-1441">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1441">Future use, always false</span></span> |
| <span data-ttu-id="11474-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1442">buildId</span></span> |<span data-ttu-id="11474-1443">the build id to use for this recommendation request</span><span class="sxs-lookup"><span data-stu-id="11474-1443">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="11474-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1444">apiVersion</span></span> |<span data-ttu-id="11474-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1445">1.0</span></span> |

<span data-ttu-id="11474-1446">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1446">**Response:**</span></span>

<span data-ttu-id="11474-1447">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1448">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1448">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1449">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1449">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1451">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1451">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1454">See a response example in 12.1</span><span class="sxs-lookup"><span data-stu-id="11474-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="11474-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="11474-1455">12.3.</span></span> <span data-ttu-id="11474-1456">Get FBT Recommendations (for active build)</span><span class="sxs-lookup"><span data-stu-id="11474-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="11474-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span><span class="sxs-lookup"><span data-stu-id="11474-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="11474-1458">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1458">HTTP Method</span></span> | <span data-ttu-id="11474-1459">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1460">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1461">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1462">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1462">Parameter Name</span></span> | <span data-ttu-id="11474-1463">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1464">modelId</span></span> |<span data-ttu-id="11474-1465">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1465">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="11474-1466">itemId</span></span> |<span data-ttu-id="11474-1467">Item to recommend for.</span><span class="sxs-lookup"><span data-stu-id="11474-1467">Item to recommend for.</span></span> <br><span data-ttu-id="11474-1468">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="11474-1468">Max length: 1024</span></span> |
| <span data-ttu-id="11474-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1469">numberOfResults</span></span> |<span data-ttu-id="11474-1470">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1470">Number of required results</span></span> <br><span data-ttu-id="11474-1471">Max: 150</span><span class="sxs-lookup"><span data-stu-id="11474-1471">Max: 150</span></span> |
| <span data-ttu-id="11474-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="11474-1472">minimalScore</span></span> |<span data-ttu-id="11474-1473">Minimal score that a frequent set should have in order to be included in the returned results</span><span class="sxs-lookup"><span data-stu-id="11474-1473">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="11474-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1474">includeMetatadata</span></span> |<span data-ttu-id="11474-1475">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1475">Future use, always false</span></span> |
| <span data-ttu-id="11474-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1476">apiVersion</span></span> |<span data-ttu-id="11474-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1477">1.0</span></span> |

<span data-ttu-id="11474-1478">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1478">**Response:**</span></span>

<span data-ttu-id="11474-1479">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span><span class="sxs-lookup"><span data-stu-id="11474-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="11474-1481">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1481">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="11474-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span><span class="sxs-lookup"><span data-stu-id="11474-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="11474-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span><span class="sxs-lookup"><span data-stu-id="11474-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="11474-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1488">The example response below includes 3 recommended item sets.</span><span class="sxs-lookup"><span data-stu-id="11474-1488">The example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="11474-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="11474-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="11474-1490">12.4.</span></span> <span data-ttu-id="11474-1491">Get FBT Recommendations (of a specific build)</span><span class="sxs-lookup"><span data-stu-id="11474-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="11474-1492">Get recommendations of a specific build of type "Fbt".</span><span class="sxs-lookup"><span data-stu-id="11474-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="11474-1493">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1493">HTTP Method</span></span> | <span data-ttu-id="11474-1494">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1495">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1496">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1497">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1497">Parameter Name</span></span> | <span data-ttu-id="11474-1498">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1499">modelId</span></span> |<span data-ttu-id="11474-1500">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1500">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="11474-1501">itemId</span></span> |<span data-ttu-id="11474-1502">Item to recommend for.</span><span class="sxs-lookup"><span data-stu-id="11474-1502">Item to recommend for.</span></span> <br><span data-ttu-id="11474-1503">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="11474-1503">Max length: 1024</span></span> |
| <span data-ttu-id="11474-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1504">numberOfResults</span></span> |<span data-ttu-id="11474-1505">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1505">Number of required results</span></span> <br><span data-ttu-id="11474-1506">Max: 150</span><span class="sxs-lookup"><span data-stu-id="11474-1506">Max: 150</span></span> |
| <span data-ttu-id="11474-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="11474-1507">minimalScore</span></span> |<span data-ttu-id="11474-1508">Minimal score that a frequent set should have in order to be included in the returned results</span><span class="sxs-lookup"><span data-stu-id="11474-1508">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="11474-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1509">includeMetatadata</span></span> |<span data-ttu-id="11474-1510">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1510">Future use, always false</span></span> |
| <span data-ttu-id="11474-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1511">buildId</span></span> |<span data-ttu-id="11474-1512">the build id to use for this recommendation request</span><span class="sxs-lookup"><span data-stu-id="11474-1512">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="11474-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1513">apiVersion</span></span> |<span data-ttu-id="11474-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1514">1.0</span></span> |

<span data-ttu-id="11474-1515">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1515">**Response:**</span></span>

<span data-ttu-id="11474-1516">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span><span class="sxs-lookup"><span data-stu-id="11474-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="11474-1518">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1518">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="11474-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span><span class="sxs-lookup"><span data-stu-id="11474-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="11474-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span><span class="sxs-lookup"><span data-stu-id="11474-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="11474-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1525">See a response example in 12.3</span><span class="sxs-lookup"><span data-stu-id="11474-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="11474-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="11474-1526">12.5.</span></span> <span data-ttu-id="11474-1527">Get User Recommendations (for active build)</span><span class="sxs-lookup"><span data-stu-id="11474-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="11474-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span><span class="sxs-lookup"><span data-stu-id="11474-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="11474-1529">The API will return a list of predicted item according to the usage history of the user.</span><span class="sxs-lookup"><span data-stu-id="11474-1529">The API will return a list of predicted item according to the usage history of the user.</span></span>

<span data-ttu-id="11474-1530">Notes:</span><span class="sxs-lookup"><span data-stu-id="11474-1530">Notes:</span></span> 

1. <span data-ttu-id="11474-1531">There is no user recommendation for FBT build.</span><span class="sxs-lookup"><span data-stu-id="11474-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="11474-1532">If the active build is FBT this method will returns an error.</span><span class="sxs-lookup"><span data-stu-id="11474-1532">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="11474-1533">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1533">HTTP Method</span></span> | <span data-ttu-id="11474-1534">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1535">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1536">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1537">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1537">Parameter Name</span></span> | <span data-ttu-id="11474-1538">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1539">modelId</span></span> |<span data-ttu-id="11474-1540">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1540">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1541">userId</span><span class="sxs-lookup"><span data-stu-id="11474-1541">userId</span></span> |<span data-ttu-id="11474-1542">Unique identifier of the user</span><span class="sxs-lookup"><span data-stu-id="11474-1542">Unique identifier of the user</span></span> |
| <span data-ttu-id="11474-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1543">numberOfResults</span></span> |<span data-ttu-id="11474-1544">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1544">Number of required results</span></span> |
| <span data-ttu-id="11474-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1545">includeMetatadata</span></span> |<span data-ttu-id="11474-1546">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1546">Future use, always false</span></span> |
| <span data-ttu-id="11474-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1547">apiVersion</span></span> |<span data-ttu-id="11474-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1548">1.0</span></span> |

<span data-ttu-id="11474-1549">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1549">**Response:**</span></span>

<span data-ttu-id="11474-1550">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1551">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1551">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1552">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1552">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1554">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1554">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1557">See a response example in 12.1</span><span class="sxs-lookup"><span data-stu-id="11474-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="11474-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="11474-1558">12.6.</span></span> <span data-ttu-id="11474-1559">Get User Recommendations with item list (for active build)</span><span class="sxs-lookup"><span data-stu-id="11474-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="11474-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span><span class="sxs-lookup"><span data-stu-id="11474-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="11474-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span><span class="sxs-lookup"><span data-stu-id="11474-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span></span>

<span data-ttu-id="11474-1562">Notes:</span><span class="sxs-lookup"><span data-stu-id="11474-1562">Notes:</span></span> 

1. <span data-ttu-id="11474-1563">There is no user recommendation for FBT build.</span><span class="sxs-lookup"><span data-stu-id="11474-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="11474-1564">If the active build is FBT this method will returns an error.</span><span class="sxs-lookup"><span data-stu-id="11474-1564">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="11474-1565">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1565">HTTP Method</span></span> | <span data-ttu-id="11474-1566">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1567">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1568">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1569">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1569">Parameter Name</span></span> | <span data-ttu-id="11474-1570">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1571">modelId</span></span> |<span data-ttu-id="11474-1572">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1572">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1573">userId</span><span class="sxs-lookup"><span data-stu-id="11474-1573">userId</span></span> |<span data-ttu-id="11474-1574">Unique identifier of the user</span><span class="sxs-lookup"><span data-stu-id="11474-1574">Unique identifier of the user</span></span> |
| <span data-ttu-id="11474-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="11474-1575">itemsIds</span></span> |<span data-ttu-id="11474-1576">Comma-separated list of the items to recommend for.</span><span class="sxs-lookup"><span data-stu-id="11474-1576">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="11474-1577">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="11474-1577">Max length: 1024</span></span> |
| <span data-ttu-id="11474-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1578">numberOfResults</span></span> |<span data-ttu-id="11474-1579">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1579">Number of required results</span></span> |
| <span data-ttu-id="11474-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1580">includeMetatadata</span></span> |<span data-ttu-id="11474-1581">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1581">Future use, always false</span></span> |
| <span data-ttu-id="11474-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1582">apiVersion</span></span> |<span data-ttu-id="11474-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1583">1.0</span></span> |

<span data-ttu-id="11474-1584">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1584">**Response:**</span></span>

<span data-ttu-id="11474-1585">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1586">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1586">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1587">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1587">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1589">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1589">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1592">See a response example in 12.1</span><span class="sxs-lookup"><span data-stu-id="11474-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="11474-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="11474-1593">12.7.</span></span> <span data-ttu-id="11474-1594">Get User Recommendations  (of a specific build)</span><span class="sxs-lookup"><span data-stu-id="11474-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="11474-1595">Get user recommendations of a specific build of type "Recommendation".</span><span class="sxs-lookup"><span data-stu-id="11474-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="11474-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span><span class="sxs-lookup"><span data-stu-id="11474-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span></span>

<span data-ttu-id="11474-1597">Note: There is no user recommendation for FBT build.</span><span class="sxs-lookup"><span data-stu-id="11474-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="11474-1598">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1598">HTTP Method</span></span> | <span data-ttu-id="11474-1599">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1600">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1601">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1602">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1602">Parameter Name</span></span> | <span data-ttu-id="11474-1603">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1604">modelId</span></span> |<span data-ttu-id="11474-1605">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1605">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1606">userId</span><span class="sxs-lookup"><span data-stu-id="11474-1606">userId</span></span> |<span data-ttu-id="11474-1607">Unique identifier of the user</span><span class="sxs-lookup"><span data-stu-id="11474-1607">Unique identifier of the user</span></span> |
| <span data-ttu-id="11474-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1608">numberOfResults</span></span> |<span data-ttu-id="11474-1609">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1609">Number of required results</span></span> |
| <span data-ttu-id="11474-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1610">includeMetatadata</span></span> |<span data-ttu-id="11474-1611">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1611">Future use, always false</span></span> |
| <span data-ttu-id="11474-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1612">buildId</span></span> |<span data-ttu-id="11474-1613">the build id to use for this recommendation request</span><span class="sxs-lookup"><span data-stu-id="11474-1613">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="11474-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1614">apiVersion</span></span> |<span data-ttu-id="11474-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1615">1.0</span></span> |

<span data-ttu-id="11474-1616">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1616">**Response:**</span></span>

<span data-ttu-id="11474-1617">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1618">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1618">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1619">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1619">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1621">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1621">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1624">See a response example in 12.1</span><span class="sxs-lookup"><span data-stu-id="11474-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="11474-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="11474-1625">12.8.</span></span> <span data-ttu-id="11474-1626">Get User Recommendations with item list (of a specific build)</span><span class="sxs-lookup"><span data-stu-id="11474-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="11474-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span><span class="sxs-lookup"><span data-stu-id="11474-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span></span>

<span data-ttu-id="11474-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span><span class="sxs-lookup"><span data-stu-id="11474-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span></span>

<span data-ttu-id="11474-1629">Note: Tthere is no user recommendation for FBT build.</span><span class="sxs-lookup"><span data-stu-id="11474-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="11474-1630">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1630">HTTP Method</span></span> | <span data-ttu-id="11474-1631">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1632">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1633">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1634">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1634">Parameter Name</span></span> | <span data-ttu-id="11474-1635">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1636">modelId</span></span> |<span data-ttu-id="11474-1637">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1637">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1638">userId</span><span class="sxs-lookup"><span data-stu-id="11474-1638">userId</span></span> |<span data-ttu-id="11474-1639">Unique identifier of the user</span><span class="sxs-lookup"><span data-stu-id="11474-1639">Unique identifier of the user</span></span> |
| <span data-ttu-id="11474-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="11474-1640">itemIds</span></span> |<span data-ttu-id="11474-1641">Comma-separated list of the items to recommend for.</span><span class="sxs-lookup"><span data-stu-id="11474-1641">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="11474-1642">Max length: 1024</span><span class="sxs-lookup"><span data-stu-id="11474-1642">Max length: 1024</span></span> |
| <span data-ttu-id="11474-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="11474-1643">numberOfResults</span></span> |<span data-ttu-id="11474-1644">Number of required results</span><span class="sxs-lookup"><span data-stu-id="11474-1644">Number of required results</span></span> |
| <span data-ttu-id="11474-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="11474-1645">includeMetatadata</span></span> |<span data-ttu-id="11474-1646">Future use, always false</span><span class="sxs-lookup"><span data-stu-id="11474-1646">Future use, always false</span></span> |
| <span data-ttu-id="11474-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1647">buildId</span></span> |<span data-ttu-id="11474-1648">the build id to use for this recommendation request</span><span class="sxs-lookup"><span data-stu-id="11474-1648">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="11474-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1649">apiVersion</span></span> |<span data-ttu-id="11474-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1650">1.0</span></span> |

<span data-ttu-id="11474-1651">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1651">**Response:**</span></span>

<span data-ttu-id="11474-1652">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1653">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1653">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1654">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1654">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1656">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1656">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span><span class="sxs-lookup"><span data-stu-id="11474-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="11474-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span><span class="sxs-lookup"><span data-stu-id="11474-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="11474-1659">See a response example in 12.1</span><span class="sxs-lookup"><span data-stu-id="11474-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="11474-1660">13. User Usage History</span><span class="sxs-lookup"><span data-stu-id="11474-1660">13. User Usage History</span></span>
<span data-ttu-id="11474-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span><span class="sxs-lookup"><span data-stu-id="11474-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span></span>
<span data-ttu-id="11474-1662">This API allow to retrieve the user history</span><span class="sxs-lookup"><span data-stu-id="11474-1662">This API allow to retrieve the user history</span></span>

<span data-ttu-id="11474-1663">Note: the user history is currently available only for recommendation builds.</span><span class="sxs-lookup"><span data-stu-id="11474-1663">Note: the user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="11474-1664">13.1 Retrieve user history</span><span class="sxs-lookup"><span data-stu-id="11474-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="11474-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span><span class="sxs-lookup"><span data-stu-id="11474-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span></span>

| <span data-ttu-id="11474-1666">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1666">HTTP Method</span></span> | <span data-ttu-id="11474-1667">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1668">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1668">GET</span></span> |<span data-ttu-id="11474-1669">Get the user history for the active build.</span><span class="sxs-lookup"><span data-stu-id="11474-1669">Get the user history for the active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="11474-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="11474-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="11474-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="11474-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="11474-1672">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1672">Parameter Name</span></span> | <span data-ttu-id="11474-1673">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1674">modelId</span></span> |<span data-ttu-id="11474-1675">the unique identifier of the model.</span><span class="sxs-lookup"><span data-stu-id="11474-1675">the unique identifier of the model.</span></span> |
| <span data-ttu-id="11474-1676">userId</span><span class="sxs-lookup"><span data-stu-id="11474-1676">userId</span></span> |<span data-ttu-id="11474-1677">the unique identifier of the user.</span><span class="sxs-lookup"><span data-stu-id="11474-1677">the unique identifier of the user.</span></span> |
| <span data-ttu-id="11474-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="11474-1678">buildId</span></span> |<span data-ttu-id="11474-1679">optional parameter, allow to indicate from which build the user history should be fetch</span><span class="sxs-lookup"><span data-stu-id="11474-1679">optional parameter, allow to indicate from which build the user history should be fetch</span></span> |
| <span data-ttu-id="11474-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1680">apiVersion</span></span> |<span data-ttu-id="11474-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1681">1.0</span></span> |

<span data-ttu-id="11474-1682">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1682">**Response:**</span></span>

<span data-ttu-id="11474-1683">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1684">The response includes one entry per recommended item.</span><span class="sxs-lookup"><span data-stu-id="11474-1684">The response includes one entry per recommended item.</span></span> <span data-ttu-id="11474-1685">Each entry has the following data:</span><span class="sxs-lookup"><span data-stu-id="11474-1685">Each entry has the following data:</span></span>

* <span data-ttu-id="11474-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span><span class="sxs-lookup"><span data-stu-id="11474-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="11474-1687">`Feed\entry\content\properties\Name` - Name of the item.</span><span class="sxs-lookup"><span data-stu-id="11474-1687">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="11474-1688">`Feed\entry\content\properties\Rating` - N/A.</span><span class="sxs-lookup"><span data-stu-id="11474-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="11474-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span><span class="sxs-lookup"><span data-stu-id="11474-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="11474-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="11474-1691">14. Notifications</span><span class="sxs-lookup"><span data-stu-id="11474-1691">14. Notifications</span></span>
<span data-ttu-id="11474-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span><span class="sxs-lookup"><span data-stu-id="11474-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span></span> <span data-ttu-id="11474-1693">There are 3 types of notifications:</span><span class="sxs-lookup"><span data-stu-id="11474-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="11474-1694">Build failure - This notification is triggered for every build failure.</span><span class="sxs-lookup"><span data-stu-id="11474-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="11474-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span><span class="sxs-lookup"><span data-stu-id="11474-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span></span>
3. <span data-ttu-id="11474-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span><span class="sxs-lookup"><span data-stu-id="11474-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="11474-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="11474-1697">14.1.</span></span> <span data-ttu-id="11474-1698">Get Notifications</span><span class="sxs-lookup"><span data-stu-id="11474-1698">Get Notifications</span></span>
<span data-ttu-id="11474-1699">Retrieves all the notifications for all models or for a single model.</span><span class="sxs-lookup"><span data-stu-id="11474-1699">Retrieves all the notifications for all models or for a single model.</span></span>

| <span data-ttu-id="11474-1700">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1700">HTTP Method</span></span> | <span data-ttu-id="11474-1701">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1702">GET</span><span class="sxs-lookup"><span data-stu-id="11474-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1703">Getting all notifications for all models:</span><span class="sxs-lookup"><span data-stu-id="11474-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1704">Example for getting notifications for a specific model:</span><span class="sxs-lookup"><span data-stu-id="11474-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="11474-1705">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1705">Parameter Name</span></span> | <span data-ttu-id="11474-1706">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1707">modelId</span></span> |<span data-ttu-id="11474-1708">Optional parameter.</span><span class="sxs-lookup"><span data-stu-id="11474-1708">Optional parameter.</span></span> <span data-ttu-id="11474-1709">When omitted, you will get all notifications for all models.</span><span class="sxs-lookup"><span data-stu-id="11474-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="11474-1710">Valid value: unique identifier of the model.</span><span class="sxs-lookup"><span data-stu-id="11474-1710">Valid value: unique identifier of the model.</span></span> |
| <span data-ttu-id="11474-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1711">apiVersion</span></span> |<span data-ttu-id="11474-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-1713">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-1713">Request Body</span></span> |<span data-ttu-id="11474-1714">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-1714">NONE</span></span> |

<span data-ttu-id="11474-1715">**Response:**</span><span class="sxs-lookup"><span data-stu-id="11474-1715">**Response:**</span></span>

<span data-ttu-id="11474-1716">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="11474-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="11474-1717">OData XML</span></span>

    The response includes one entry per notification. Each entry has the following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="11474-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="11474-1718">14.2.</span></span> <span data-ttu-id="11474-1719">Delete Model Notifications</span><span class="sxs-lookup"><span data-stu-id="11474-1719">Delete Model Notifications</span></span>
<span data-ttu-id="11474-1720">Deletes all read notifications for a model.</span><span class="sxs-lookup"><span data-stu-id="11474-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="11474-1721">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1721">HTTP Method</span></span> | <span data-ttu-id="11474-1722">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1723">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="11474-1724">Example:</span><span class="sxs-lookup"><span data-stu-id="11474-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1725">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1725">Parameter Name</span></span> | <span data-ttu-id="11474-1726">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="11474-1727">modelId</span></span> |<span data-ttu-id="11474-1728">Unique identifier of the model</span><span class="sxs-lookup"><span data-stu-id="11474-1728">Unique identifier of the model</span></span> |
| <span data-ttu-id="11474-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1729">apiVersion</span></span> |<span data-ttu-id="11474-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-1731">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-1731">Request Body</span></span> |<span data-ttu-id="11474-1732">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-1732">NONE</span></span> |

<span data-ttu-id="11474-1733">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-1733">**Response**:</span></span>

<span data-ttu-id="11474-1734">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="11474-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="11474-1735">14.3.</span></span> <span data-ttu-id="11474-1736">Delete User Notifications</span><span class="sxs-lookup"><span data-stu-id="11474-1736">Delete User Notifications</span></span>
<span data-ttu-id="11474-1737">Deletes all notifications for all models.</span><span class="sxs-lookup"><span data-stu-id="11474-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="11474-1738">HTTP Method</span><span class="sxs-lookup"><span data-stu-id="11474-1738">HTTP Method</span></span> | <span data-ttu-id="11474-1739">URI</span><span class="sxs-lookup"><span data-stu-id="11474-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1740">DELETE</span><span class="sxs-lookup"><span data-stu-id="11474-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="11474-1741">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="11474-1741">Parameter Name</span></span> | <span data-ttu-id="11474-1742">Valid Values</span><span class="sxs-lookup"><span data-stu-id="11474-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="11474-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="11474-1743">apiVersion</span></span> |<span data-ttu-id="11474-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="11474-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="11474-1745">Request Body</span><span class="sxs-lookup"><span data-stu-id="11474-1745">Request Body</span></span> |<span data-ttu-id="11474-1746">NONE</span><span class="sxs-lookup"><span data-stu-id="11474-1746">NONE</span></span> |

<span data-ttu-id="11474-1747">**Response**:</span><span class="sxs-lookup"><span data-stu-id="11474-1747">**Response**:</span></span>

<span data-ttu-id="11474-1748">HTTP Status code: 200</span><span class="sxs-lookup"><span data-stu-id="11474-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="11474-1749">15. Legal</span><span class="sxs-lookup"><span data-stu-id="11474-1749">15. Legal</span></span>
<span data-ttu-id="11474-1750">This document is provided “as-is”.</span><span class="sxs-lookup"><span data-stu-id="11474-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="11474-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span><span class="sxs-lookup"><span data-stu-id="11474-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="11474-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span><span class="sxs-lookup"><span data-stu-id="11474-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="11474-1753">No real association or connection is intended or should be inferred.</span><span class="sxs-lookup"><span data-stu-id="11474-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="11474-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span><span class="sxs-lookup"><span data-stu-id="11474-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="11474-1755">You may copy and use this document for your internal, reference purposes.</span><span class="sxs-lookup"><span data-stu-id="11474-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="11474-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="11474-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="11474-1757">All rights reserved.</span><span class="sxs-lookup"><span data-stu-id="11474-1757">All rights reserved.</span></span>

