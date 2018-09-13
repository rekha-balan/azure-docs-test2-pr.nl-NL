---
title: Integrate an Azure storage account with Azure CDN | Microsoft Docs
description: Learn how to use the Azure Content Delivery Network (CDN) to deliver high-bandwidth content by caching blobs from Azure Storage.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 439219819ba5675c0a80f784b6e034e21e1030d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540822"
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="f5b0b-103">Integrate an Azure storage account with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f5b0b-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="f5b0b-104">CDN can be enabled to cache content from your Azure storage.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="f5b0b-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="f5b0b-106">Step 1: Create a storage account</span><span class="sxs-lookup"><span data-stu-id="f5b0b-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="f5b0b-107">Use the following procedure to create a new storage account for a Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="f5b0b-108">A storage account gives access to Azure storage services.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="f5b0b-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="f5b0b-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5b0b-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/storage-introduction.md).</span></span>

<span data-ttu-id="f5b0b-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f5b0b-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="f5b0b-113">For this tutorial, we'll be using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="f5b0b-114">**To create a storage account for an Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="f5b0b-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="f5b0b-115">Sign in to the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f5b0b-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f5b0b-116">In the upper left corner, select **New**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="f5b0b-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
   
   <span data-ttu-id="f5b0b-118">The **Create storage account** blade appears.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-118">The **Create storage account** blade appears.</span></span>
   
   ![Create Storage Account][create-new-storage-account]
3. <span data-ttu-id="f5b0b-120">In the **Name** field, type a subdomain name.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="f5b0b-121">This entry can contain 3-24 lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="f5b0b-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="f5b0b-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span><span class="sxs-lookup"><span data-stu-id="f5b0b-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="f5b0b-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="f5b0b-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="f5b0b-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="f5b0b-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="f5b0b-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="f5b0b-128">Select the **Subscription** that the storage account will be used with.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="f5b0b-129">Select or create a **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="f5b0b-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="f5b0b-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="f5b0b-131">Select a location for your storage account.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="f5b0b-132">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-132">Click **Create**.</span></span> <span data-ttu-id="f5b0b-133">The process of creating the storage account might take several minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-create-a-new-cdn-profile"></a><span data-ttu-id="f5b0b-134">Step 2: Create a new CDN profile</span><span class="sxs-lookup"><span data-stu-id="f5b0b-134">Step 2: Create a new CDN profile</span></span>
<span data-ttu-id="f5b0b-135">A CDN profile is a collection of CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-135">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="f5b0b-136">Each profile contains one or more CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-136">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="f5b0b-137">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-137">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="f5b0b-138">If you already have a CDN profile that you want to use for this tutorial, proceed to [Step 3](#step-3-create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f5b0b-138">If you already have a CDN profile that you want to use for this tutorial, proceed to [Step 3](#step-3-create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="step-3-create-a-new-cdn-endpoint"></a><span data-ttu-id="f5b0b-139">Step 3: Create a new CDN endpoint</span><span class="sxs-lookup"><span data-stu-id="f5b0b-139">Step 3: Create a new CDN endpoint</span></span>
<span data-ttu-id="f5b0b-140">**To create a new CDN endpoint for your storage account**</span><span class="sxs-lookup"><span data-stu-id="f5b0b-140">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="f5b0b-141">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-141">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="f5b0b-142">You may have pinned it to the dashboard in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-142">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="f5b0b-143">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-143">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="f5b0b-144">The CDN profile blade appears.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-144">The CDN profile blade appears.</span></span>
   
    ![CDN profile][cdn-profile-settings]
2. <span data-ttu-id="f5b0b-146">Click the **Add Endpoint** button.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-146">Click the **Add Endpoint** button.</span></span>
   
    ![Add endpoint button][cdn-new-endpoint-button]
   
    <span data-ttu-id="f5b0b-148">The **Add an endpoint** blade appears.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-148">The **Add an endpoint** blade appears.</span></span>
   
    ![Add endpoint blade][cdn-add-endpoint]
3. <span data-ttu-id="f5b0b-150">Enter a **Name** for this CDN endpoint.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-150">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="f5b0b-151">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-151">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="f5b0b-152">In the **Origin type** dropdown, select *Storage*.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-152">In the **Origin type** dropdown, select *Storage*.</span></span>  
5. <span data-ttu-id="f5b0b-153">In the **Origin hostname** dropdown, select your storage account.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-153">In the **Origin hostname** dropdown, select your storage account.</span></span>
6. <span data-ttu-id="f5b0b-154">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-154">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="f5b0b-155">You must specify at least one protocol (HTTP or HTTPS).</span><span class="sxs-lookup"><span data-stu-id="f5b0b-155">You must specify at least one protocol (HTTP or HTTPS).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f5b0b-156">This configuration enables all of your publicly visible containers in your storage account for caching in the CDN.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-156">This configuration enables all of your publicly visible containers in your storage account for caching in the CDN.</span></span>  <span data-ttu-id="f5b0b-157">If you want to limit the scope to a single container, use **Origin path**.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-157">If you want to limit the scope to a single container, use **Origin path**.</span></span>  <span data-ttu-id="f5b0b-158">Note the container must have its visibility set to public.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-158">Note the container must have its visibility set to public.</span></span>
   > 
   > 
7. <span data-ttu-id="f5b0b-159">Click the **Add** button to create the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-159">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="f5b0b-160">Once the endpoint is created, it appears in a list of endpoints for the profile.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-160">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="f5b0b-161">The list view shows the URL to use to access cached content, as well as the origin domain.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-161">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![CDN endpoint][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="f5b0b-163">The endpoint will not immediately be available for use.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-163">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="f5b0b-164">It can take up to 90 minutes for the registration to propagate through the CDN network.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-164">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="f5b0b-165">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-165">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="f5b0b-166">Step 4: Access CDN content</span><span class="sxs-lookup"><span data-stu-id="f5b0b-166">Step 4: Access CDN content</span></span>
<span data-ttu-id="f5b0b-167">To access cached content on the CDN, use the CDN URL provided in the portal.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-167">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="f5b0b-168">The address for a cached blob will be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f5b0b-168">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="f5b0b-169">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="f5b0b-169">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="f5b0b-170">Once you enable CDN access to a storage account or hosted service, all publicly available objects are eligible for CDN edge caching.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-170">Once you enable CDN access to a storage account or hosted service, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="f5b0b-171">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-171">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="f5b0b-172">Step 5: Remove content from the CDN</span><span class="sxs-lookup"><span data-stu-id="f5b0b-172">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="f5b0b-173">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5b0b-173">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="f5b0b-174">You can make the container private instead of public.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-174">You can make the container private instead of public.</span></span> <span data-ttu-id="f5b0b-175">See [Manage anonymous read access to containers and blobs](../storage/storage-manage-access-to-resources.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-175">See [Manage anonymous read access to containers and blobs](../storage/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="f5b0b-176">You can disable or delete the CDN endpoint using the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-176">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="f5b0b-177">You can modify your hosted service to no longer respond to requests for the object.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-177">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="f5b0b-178">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-178">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="f5b0b-179">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-179">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="f5b0b-180">If it is not, then the object will no longer be cached.</span><span class="sxs-lookup"><span data-stu-id="f5b0b-180">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5b0b-181">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f5b0b-181">Additional resources</span></span>
* [<span data-ttu-id="f5b0b-182">How to Map CDN Content to a Custom Domain</span><span class="sxs-lookup"><span data-stu-id="f5b0b-182">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)

[create-new-storage-account]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png

[cdn-profile-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-a-storage-account-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-a-storage-account-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-a-storage-account-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-create-a-storage-account-with-cdn/cdn-endpoint-success.png





