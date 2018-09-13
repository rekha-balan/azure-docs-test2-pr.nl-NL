---
title: Manage expiration of Azure Blob storage in Azure Content Delivery Network | Microsoft Docs
description: Learn about the options for controlling time-to-live for blobs in Azure CDN caching.
services: cdn
documentationcenter: ''
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 02/1/2018
ms.author: mazha
ms.openlocfilehash: a0f89a272fa300f6acced2de02ba5465ab282079
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825994"
---
# <a name="manage-expiration-of-azure-blob-storage-in-azure-cdn"></a><span data-ttu-id="644ad-103">Manage expiration of Azure Blob storage in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="644ad-103">Manage expiration of Azure Blob storage in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [Azure web content](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure Blob storage](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="644ad-106">The [Blob storage service](../storage/common/storage-introduction.md#blob-storage) in Azure Storage is one of several Azure-based origins integrated with Azure Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="644ad-106">The [Blob storage service](../storage/common/storage-introduction.md#blob-storage) in Azure Storage is one of several Azure-based origins integrated with Azure Content Delivery Network (CDN).</span></span> <span data-ttu-id="644ad-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span><span class="sxs-lookup"><span data-stu-id="644ad-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span> <span data-ttu-id="644ad-108">The TTL is determined by the `Cache-Control` header in the HTTP response from the origin server.</span><span class="sxs-lookup"><span data-stu-id="644ad-108">The TTL is determined by the `Cache-Control` header in the HTTP response from the origin server.</span></span> <span data-ttu-id="644ad-109">This article describes several ways that you can set the `Cache-Control` header on a blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="644ad-109">This article describes several ways that you can set the `Cache-Control` header on a blob in Azure Storage.</span></span>

<span data-ttu-id="644ad-110">You can also control cache settings from the Azure portal by setting [CDN caching rules](#setting-cache-control-headers-by-using-caching-rules).</span><span class="sxs-lookup"><span data-stu-id="644ad-110">You can also control cache settings from the Azure portal by setting [CDN caching rules](#setting-cache-control-headers-by-using-caching-rules).</span></span> <span data-ttu-id="644ad-111">If you create a caching rule and set its caching behavior to **Override** or **Bypass cache**, the origin-provided caching settings discussed in this article are ignored.</span><span class="sxs-lookup"><span data-stu-id="644ad-111">If you create a caching rule and set its caching behavior to **Override** or **Bypass cache**, the origin-provided caching settings discussed in this article are ignored.</span></span> <span data-ttu-id="644ad-112">For information about general caching concepts, see [How caching works](cdn-how-caching-works.md).</span><span class="sxs-lookup"><span data-stu-id="644ad-112">For information about general caching concepts, see [How caching works](cdn-how-caching-works.md).</span></span>

> [!TIP]
> You can choose to set no TTL on a blob. In this case, Azure CDN automatically applies a default TTL of seven days, unless you have set up caching rules in the Azure portal. This default TTL applies only to general web delivery optimizations. For large file optimizations, the default TTL is one day, and for media streaming optimizations, the default TTL is one year.
> 
> For more information about how Azure CDN works to speed up access to blobs and other files, see [Overview of the Azure Content Delivery Network](cdn-overview.md).
> 
> For more information about Azure Blob storage, see [Introduction to Blob storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).
 

## <a name="setting-cache-control-headers-by-using-cdn-caching-rules"></a><span data-ttu-id="644ad-119">Setting Cache-Control headers by using CDN caching rules</span><span class="sxs-lookup"><span data-stu-id="644ad-119">Setting Cache-Control headers by using CDN caching rules</span></span>
<span data-ttu-id="644ad-120">The preferred method for setting a blob's `Cache-Control` header is to use caching rules in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="644ad-120">The preferred method for setting a blob's `Cache-Control` header is to use caching rules in the Azure portal.</span></span> <span data-ttu-id="644ad-121">For more information about CDN caching rules, see [Control Azure CDN caching behavior with caching rules](cdn-caching-rules.md).</span><span class="sxs-lookup"><span data-stu-id="644ad-121">For more information about CDN caching rules, see [Control Azure CDN caching behavior with caching rules](cdn-caching-rules.md).</span></span>

> [!NOTE] 
> Caching rules are available only for **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles. For **Azure CDN Premium from Verizon** profiles, you must use the [Azure CDN rules engine](cdn-rules-engine.md) in the **Manage** portal for similar functionality.

<span data-ttu-id="644ad-124">**To navigate to the CDN caching rules page**:</span><span class="sxs-lookup"><span data-stu-id="644ad-124">**To navigate to the CDN caching rules page**:</span></span>

1. <span data-ttu-id="644ad-125">In the Azure portal, select a CDN profile, then select the endpoint for the blob.</span><span class="sxs-lookup"><span data-stu-id="644ad-125">In the Azure portal, select a CDN profile, then select the endpoint for the blob.</span></span>

2. <span data-ttu-id="644ad-126">In the left pane under Settings, select **Caching rules**.</span><span class="sxs-lookup"><span data-stu-id="644ad-126">In the left pane under Settings, select **Caching rules**.</span></span>

   ![CDN caching rules button](./media/cdn-manage-expiration-of-blob-content/cdn-caching-rules-btn.png)

   <span data-ttu-id="644ad-128">The **Caching rules** page appears.</span><span class="sxs-lookup"><span data-stu-id="644ad-128">The **Caching rules** page appears.</span></span>

   ![CDN caching page](./media/cdn-manage-expiration-of-blob-content/cdn-caching-page.png)


<span data-ttu-id="644ad-130">**To set a Blob storage service's Cache-Control headers by using global caching rules:**</span><span class="sxs-lookup"><span data-stu-id="644ad-130">**To set a Blob storage service's Cache-Control headers by using global caching rules:**</span></span>

1. <span data-ttu-id="644ad-131">Under **Global caching rules**, set **Query string caching behavior** to **Ignore query strings** and set **Caching behavior** to **Override**.</span><span class="sxs-lookup"><span data-stu-id="644ad-131">Under **Global caching rules**, set **Query string caching behavior** to **Ignore query strings** and set **Caching behavior** to **Override**.</span></span>
      
2. <span data-ttu-id="644ad-132">For **Cache expiration duration**, enter 3600 in the **Seconds** box or 1 in the **Hours** box.</span><span class="sxs-lookup"><span data-stu-id="644ad-132">For **Cache expiration duration**, enter 3600 in the **Seconds** box or 1 in the **Hours** box.</span></span> 

   ![CDN global caching rules example](./media/cdn-manage-expiration-of-blob-content/cdn-global-caching-rules-example.png)

   <span data-ttu-id="644ad-134">This global caching rule sets a cache duration of one hour and affects all requests to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="644ad-134">This global caching rule sets a cache duration of one hour and affects all requests to the endpoint.</span></span> <span data-ttu-id="644ad-135">It overrides any `Cache-Control` or `Expires` HTTP headers that are sent by the origin server specified by the endpoint.</span><span class="sxs-lookup"><span data-stu-id="644ad-135">It overrides any `Cache-Control` or `Expires` HTTP headers that are sent by the origin server specified by the endpoint.</span></span>   

3. <span data-ttu-id="644ad-136">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="644ad-136">Select **Save**.</span></span>
 
<span data-ttu-id="644ad-137">**To set a blob file's Cache-Control headers by using custom caching rules:**</span><span class="sxs-lookup"><span data-stu-id="644ad-137">**To set a blob file's Cache-Control headers by using custom caching rules:**</span></span>

1. <span data-ttu-id="644ad-138">Under **Custom caching rules**, create two match conditions:</span><span class="sxs-lookup"><span data-stu-id="644ad-138">Under **Custom caching rules**, create two match conditions:</span></span>

     <span data-ttu-id="644ad-139">A.</span><span class="sxs-lookup"><span data-stu-id="644ad-139">A.</span></span> <span data-ttu-id="644ad-140">For the first match condition, set **Match condition** to **Path** and enter `/blobcontainer1/*` for **Match value**.</span><span class="sxs-lookup"><span data-stu-id="644ad-140">For the first match condition, set **Match condition** to **Path** and enter `/blobcontainer1/*` for **Match value**.</span></span> <span data-ttu-id="644ad-141">Set **Caching behavior** to **Override** and enter 4 in the **Hours** box.</span><span class="sxs-lookup"><span data-stu-id="644ad-141">Set **Caching behavior** to **Override** and enter 4 in the **Hours** box.</span></span>

    <span data-ttu-id="644ad-142">B.</span><span class="sxs-lookup"><span data-stu-id="644ad-142">B.</span></span> <span data-ttu-id="644ad-143">For the second match condition, set **Match condition** to **Path** and enter `/blobcontainer1/blob1.txt` for **Match value**.</span><span class="sxs-lookup"><span data-stu-id="644ad-143">For the second match condition, set **Match condition** to **Path** and enter `/blobcontainer1/blob1.txt` for **Match value**.</span></span> <span data-ttu-id="644ad-144">Set **Caching behavior** to **Override** and enter 2 in the **Hours** box.</span><span class="sxs-lookup"><span data-stu-id="644ad-144">Set **Caching behavior** to **Override** and enter 2 in the **Hours** box.</span></span>

    ![CDN custom caching rules example](./media/cdn-manage-expiration-of-blob-content/cdn-custom-caching-rules-example.png)

    <span data-ttu-id="644ad-146">The first custom caching rule sets a cache duration of four hours for any blob files in the `/blobcontainer1` folder on the origin server specified by your endpoint.</span><span class="sxs-lookup"><span data-stu-id="644ad-146">The first custom caching rule sets a cache duration of four hours for any blob files in the `/blobcontainer1` folder on the origin server specified by your endpoint.</span></span> <span data-ttu-id="644ad-147">The second rule overrides the first rule for the `blob1.txt` blob file only and sets a cache duration of two hours for it.</span><span class="sxs-lookup"><span data-stu-id="644ad-147">The second rule overrides the first rule for the `blob1.txt` blob file only and sets a cache duration of two hours for it.</span></span>

2. <span data-ttu-id="644ad-148">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="644ad-148">Select **Save**.</span></span>


## <a name="setting-cache-control-headers-by-using-azure-powershell"></a><span data-ttu-id="644ad-149">Setting Cache-Control headers by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="644ad-149">Setting Cache-Control headers by using Azure PowerShell</span></span>
<span data-ttu-id="644ad-150">[Azure PowerShell](/powershell/azure/overview) is one of the quickest and most powerful ways to administer your Azure services.</span><span class="sxs-lookup"><span data-stu-id="644ad-150">[Azure PowerShell](/powershell/azure/overview) is one of the quickest and most powerful ways to administer your Azure services.</span></span> <span data-ttu-id="644ad-151">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span><span class="sxs-lookup"><span data-stu-id="644ad-151">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

<span data-ttu-id="644ad-152">For example:</span><span class="sxs-lookup"><span data-stu-id="644ad-152">For example:</span></span>

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).
> 
>

## <a name="setting-cache-control-headers-by-using-net"></a><span data-ttu-id="644ad-154">Setting Cache-Control headers by using .NET</span><span class="sxs-lookup"><span data-stu-id="644ad-154">Setting Cache-Control headers by using .NET</span></span>
<span data-ttu-id="644ad-155">To specify a blob's `Cache-Control` header by using .NET code, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span><span class="sxs-lookup"><span data-stu-id="644ad-155">To specify a blob's `Cache-Control` header by using .NET code, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

<span data-ttu-id="644ad-156">For example:</span><span class="sxs-lookup"><span data-stu-id="644ad-156">For example:</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer <container name> = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob <blob name> = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> There are more .NET code samples available in [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 

## <a name="setting-cache-control-headers-by-using-other-methods"></a><span data-ttu-id="644ad-158">Setting Cache-Control headers by using other methods</span><span class="sxs-lookup"><span data-stu-id="644ad-158">Setting Cache-Control headers by using other methods</span></span>

### <a name="azure-storage-explorer"></a><span data-ttu-id="644ad-159">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="644ad-159">Azure Storage Explorer</span></span>
<span data-ttu-id="644ad-160">With [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/), you can view and edit your blob storage resources, including properties such as the *CacheControl* property.</span><span class="sxs-lookup"><span data-stu-id="644ad-160">With [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/), you can view and edit your blob storage resources, including properties such as the *CacheControl* property.</span></span> 

<span data-ttu-id="644ad-161">To update the *CacheControl* property of a blob with Azure Storage Explorer:</span><span class="sxs-lookup"><span data-stu-id="644ad-161">To update the *CacheControl* property of a blob with Azure Storage Explorer:</span></span>
   1. <span data-ttu-id="644ad-162">Select a blob, then select **Properties** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="644ad-162">Select a blob, then select **Properties** from the context menu.</span></span> 
   2. <span data-ttu-id="644ad-163">Scroll down to the *CacheControl* property.</span><span class="sxs-lookup"><span data-stu-id="644ad-163">Scroll down to the *CacheControl* property.</span></span>
   3. <span data-ttu-id="644ad-164">Enter a value, then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="644ad-164">Enter a value, then select **Save**.</span></span>


![Azure Storage Explorer properties](./media/cdn-manage-expiration-of-blob-content/cdn-storage-explorer-properties.png)

### <a name="azure-command-line-interface"></a><span data-ttu-id="644ad-166">Azure Command-Line Interface</span><span class="sxs-lookup"><span data-stu-id="644ad-166">Azure Command-Line Interface</span></span>
<span data-ttu-id="644ad-167">With the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) (CLI), you can manage Azure blob resources from the command line.</span><span class="sxs-lookup"><span data-stu-id="644ad-167">With the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure?view=azure-cli-latest) (CLI), you can manage Azure blob resources from the command line.</span></span> <span data-ttu-id="644ad-168">To set the cache-control header when you upload a blob with the Azure CLI, set the *cacheControl* property by using the `-p` switch.</span><span class="sxs-lookup"><span data-stu-id="644ad-168">To set the cache-control header when you upload a blob with the Azure CLI, set the *cacheControl* property by using the `-p` switch.</span></span> <span data-ttu-id="644ad-169">The following example shows how to set the TTL to one hour (3600 seconds):</span><span class="sxs-lookup"><span data-stu-id="644ad-169">The following example shows how to set the TTL to one hour (3600 seconds):</span></span>
  
```azurecli
azure storage blob upload -c <connectionstring> -p cacheControl="max-age=3600" .\<blob name> <container name> <blob name>
```

### <a name="azure-storage-services-rest-api"></a><span data-ttu-id="644ad-170">Azure storage services REST API</span><span class="sxs-lookup"><span data-stu-id="644ad-170">Azure storage services REST API</span></span>
<span data-ttu-id="644ad-171">You can use the [Azure storage services REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx) to explicitly set the *x-ms-blob-cache-control* property by using the following operations on a request:</span><span class="sxs-lookup"><span data-stu-id="644ad-171">You can use the [Azure storage services REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx) to explicitly set the *x-ms-blob-cache-control* property by using the following operations on a request:</span></span>
  
   - [<span data-ttu-id="644ad-172">Put Blob</span><span class="sxs-lookup"><span data-stu-id="644ad-172">Put Blob</span></span>](https://msdn.microsoft.com/library/azure/dd179451.aspx)
   - [<span data-ttu-id="644ad-173">Put Block List</span><span class="sxs-lookup"><span data-stu-id="644ad-173">Put Block List</span></span>](https://msdn.microsoft.com/library/azure/dd179467.aspx)
   - [<span data-ttu-id="644ad-174">Set Blob Properties</span><span class="sxs-lookup"><span data-stu-id="644ad-174">Set Blob Properties</span></span>](https://msdn.microsoft.com/library/azure/ee691966.aspx)

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="644ad-175">Testing the Cache-Control header</span><span class="sxs-lookup"><span data-stu-id="644ad-175">Testing the Cache-Control header</span></span>
<span data-ttu-id="644ad-176">You can easily verify the TTL settings of your blobs.</span><span class="sxs-lookup"><span data-stu-id="644ad-176">You can easily verify the TTL settings of your blobs.</span></span> <span data-ttu-id="644ad-177">With your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob includes the `Cache-Control` response header.</span><span class="sxs-lookup"><span data-stu-id="644ad-177">With your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob includes the `Cache-Control` response header.</span></span> <span data-ttu-id="644ad-178">You can also use a tool such as [Wget](https://www.gnu.org/software/wget/), [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span><span class="sxs-lookup"><span data-stu-id="644ad-178">You can also use a tool such as [Wget](https://www.gnu.org/software/wget/), [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="644ad-179">Next Steps</span><span class="sxs-lookup"><span data-stu-id="644ad-179">Next Steps</span></span>
* [<span data-ttu-id="644ad-180">Learn how to manage expiration of Cloud Service content in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="644ad-180">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
* [<span data-ttu-id="644ad-181">Learn about caching concepts</span><span class="sxs-lookup"><span data-stu-id="644ad-181">Learn about caching concepts</span></span>](cdn-how-caching-works.md)

