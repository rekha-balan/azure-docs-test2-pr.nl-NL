---
title: Get started with Azure Search in NodeJS | Microsoft Docs
description: Walk through building a search application on a hosted cloud search service on Azure using NodeJS as your programming language.
services: search
documentationcenter: ''
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 24ae297a8ea2a7f36a46cef9faac0d3619178055
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551547"
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="61c32-103">Get started with Azure Search in NodeJS</span><span class="sxs-lookup"><span data-stu-id="61c32-103">Get started with Azure Search in NodeJS</span></span>
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="61c32-106">Learn how to build a custom NodeJS search application that uses Azure Search for its search experience.</span><span class="sxs-lookup"><span data-stu-id="61c32-106">Learn how to build a custom NodeJS search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="61c32-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span><span class="sxs-lookup"><span data-stu-id="61c32-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="61c32-108">We used [NodeJS](https://nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span><span class="sxs-lookup"><span data-stu-id="61c32-108">We used [NodeJS](https://nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="61c32-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61c32-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="61c32-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="61c32-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="61c32-111">About the data</span><span class="sxs-lookup"><span data-stu-id="61c32-111">About the data</span></span>
<span data-ttu-id="61c32-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span><span class="sxs-lookup"><span data-stu-id="61c32-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="61c32-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span><span class="sxs-lookup"><span data-stu-id="61c32-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="61c32-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="61c32-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="61c32-115">Credentials and connection  information to the online data source is provided in the program code.</span><span class="sxs-lookup"><span data-stu-id="61c32-115">Credentials and connection  information to the online data source is provided in the program code.</span></span> <span data-ttu-id="61c32-116">No further configuration is necessary.</span><span class="sxs-lookup"><span data-stu-id="61c32-116">No further configuration is necessary.</span></span>

> [!NOTE]
> We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier. If you use the standard tier, this limit does not apply. For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="61c32-120">Find the service name and api-key of your Azure Search service</span><span class="sxs-lookup"><span data-stu-id="61c32-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="61c32-121">After you create the service, return to the portal to get the URL or `api-key`.</span><span class="sxs-lookup"><span data-stu-id="61c32-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="61c32-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span><span class="sxs-lookup"><span data-stu-id="61c32-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="61c32-123">Sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61c32-123">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61c32-124">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span><span class="sxs-lookup"><span data-stu-id="61c32-124">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="61c32-125">Select the service you want to use.</span><span class="sxs-lookup"><span data-stu-id="61c32-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="61c32-126">On the service dashboard, you'll see tiles for essential information, as well as the key icon for accessing the admin keys.</span><span class="sxs-lookup"><span data-stu-id="61c32-126">On the service dashboard, you'll see tiles for essential information, as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="61c32-127">Copy the service URL, an admin key, and a query key.</span><span class="sxs-lookup"><span data-stu-id="61c32-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="61c32-128">You'll need all three later, when you add them to the config.js file.</span><span class="sxs-lookup"><span data-stu-id="61c32-128">You'll need all three later, when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="61c32-129">Download the sample files</span><span class="sxs-lookup"><span data-stu-id="61c32-129">Download the sample files</span></span>
<span data-ttu-id="61c32-130">Use either one of the following approaches to download the sample.</span><span class="sxs-lookup"><span data-stu-id="61c32-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="61c32-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodeJSIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="61c32-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodeJSIndexerDemo).</span></span>
2. <span data-ttu-id="61c32-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span><span class="sxs-lookup"><span data-stu-id="61c32-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="61c32-133">All subsequent file modifications and run statements will be made against files in this folder.</span><span class="sxs-lookup"><span data-stu-id="61c32-133">All subsequent file modifications and run statements will be made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="61c32-134">Update the config.js.</span><span class="sxs-lookup"><span data-stu-id="61c32-134">Update the config.js.</span></span> <span data-ttu-id="61c32-135">with your Search service URL and api-key</span><span class="sxs-lookup"><span data-stu-id="61c32-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="61c32-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span><span class="sxs-lookup"><span data-stu-id="61c32-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="61c32-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span><span class="sxs-lookup"><span data-stu-id="61c32-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="61c32-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span><span class="sxs-lookup"><span data-stu-id="61c32-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="61c32-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span><span class="sxs-lookup"><span data-stu-id="61c32-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="61c32-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span><span class="sxs-lookup"><span data-stu-id="61c32-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="61c32-141">Host a runtime environment for the sample</span><span class="sxs-lookup"><span data-stu-id="61c32-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="61c32-142">The sample requires an HTTP server, which you can install globally using npm.</span><span class="sxs-lookup"><span data-stu-id="61c32-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="61c32-143">Use a PowerShell window for the following commands.</span><span class="sxs-lookup"><span data-stu-id="61c32-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="61c32-144">Navigate to the folder that contains the **package.json** file.</span><span class="sxs-lookup"><span data-stu-id="61c32-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="61c32-145">Type `npm install`.</span><span class="sxs-lookup"><span data-stu-id="61c32-145">Type `npm install`.</span></span>
3. <span data-ttu-id="61c32-146">Type `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="61c32-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="61c32-147">Build the index and run the application</span><span class="sxs-lookup"><span data-stu-id="61c32-147">Build the index and run the application</span></span>
1. <span data-ttu-id="61c32-148">Type `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="61c32-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="61c32-149">Type `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="61c32-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="61c32-150">Type `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="61c32-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="61c32-151">Direct your browser at `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="61c32-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="61c32-152">Search on USGS data</span><span class="sxs-lookup"><span data-stu-id="61c32-152">Search on USGS data</span></span>
<span data-ttu-id="61c32-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="61c32-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="61c32-154">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span><span class="sxs-lookup"><span data-stu-id="61c32-154">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="61c32-155">Entering a search term will give the search engine something to go on.</span><span class="sxs-lookup"><span data-stu-id="61c32-155">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="61c32-156">Try entering a regional name.</span><span class="sxs-lookup"><span data-stu-id="61c32-156">Try entering a regional name.</span></span> <span data-ttu-id="61c32-157">"Roger Williams" was the first governor of Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="61c32-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="61c32-158">Numerous parks, buildings, and schools are named after him.</span><span class="sxs-lookup"><span data-stu-id="61c32-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="61c32-159">You could also try any of these terms:</span><span class="sxs-lookup"><span data-stu-id="61c32-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="61c32-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="61c32-160">Pawtucket</span></span>
* <span data-ttu-id="61c32-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="61c32-161">Pembroke</span></span>
* <span data-ttu-id="61c32-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="61c32-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="61c32-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="61c32-163">Next steps</span></span>
<span data-ttu-id="61c32-164">This is the first Azure Search tutorial based on NodeJS and the USGS dataset.</span><span class="sxs-lookup"><span data-stu-id="61c32-164">This is the first Azure Search tutorial based on NodeJS and the USGS dataset.</span></span> <span data-ttu-id="61c32-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span><span class="sxs-lookup"><span data-stu-id="61c32-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="61c32-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span><span class="sxs-lookup"><span data-stu-id="61c32-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="61c32-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span><span class="sxs-lookup"><span data-stu-id="61c32-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="61c32-168">New to Azure Search?</span><span class="sxs-lookup"><span data-stu-id="61c32-168">New to Azure Search?</span></span> <span data-ttu-id="61c32-169">We recommend trying other tutorials to develop an understanding of what you can create.</span><span class="sxs-lookup"><span data-stu-id="61c32-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="61c32-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span><span class="sxs-lookup"><span data-stu-id="61c32-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="61c32-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span><span class="sxs-lookup"><span data-stu-id="61c32-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-nodejs/create-search-portal-1.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-nodejs/create-search-portal-2.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-nodejs/create-search-portal-3.PNG
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-nodejs/AzSearch-NodeJS-configjs.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/search/media/search-get-started-nodejs/rogerwilliamsschool.png





