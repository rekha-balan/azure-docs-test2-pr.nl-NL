---
title: Azure Media Services v3 overview | Microsoft Docs
description: This article provides a high-level overview of Media Services and provides links to articles for more details.
services: media-services
documentationcenter: na
author: Juliako
manager: cfowler
editor: ''
tags: ''
keywords: azure media services, stream, broadcast, live, offline
ms.service: media-services
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: media
ms.date: 07/14/2018
ms.author: juliako
ms.custom: mvc
ms.openlocfilehash: 6c3fb7391c25628ba12526a04c022215bdbd9d40
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866368"
---
# <a name="what-is-azure-media-services-v3"></a><span data-ttu-id="36183-104">What is Azure Media Services v3?</span><span class="sxs-lookup"><span data-stu-id="36183-104">What is Azure Media Services v3?</span></span>

> [!div class="op_single_selector" title1="Select the version of Media Services that you are using:"]
> * [Version 2 - GA](../previous/media-services-overview.md)
> * [Version 3 - Preview](media-services-overview.md)

> [!NOTE]
> The latest version of Azure Media Services is in Preview and may be referred to as v3.

<span data-ttu-id="36183-108">Azure Media Services is a cloud-based platform that enables you to build solutions that achieve broadcast-quality video streaming, enhance accessibility and distribution, analyze content, and much more.</span><span class="sxs-lookup"><span data-stu-id="36183-108">Azure Media Services is a cloud-based platform that enables you to build solutions that achieve broadcast-quality video streaming, enhance accessibility and distribution, analyze content, and much more.</span></span> <span data-ttu-id="36183-109">Whether you are an application developer, a call center, a government agency, an entertainment company, Media Services helps you create applications that deliver media experiences of outstanding quality to large audiences on today’s most popular mobile devices and browsers.</span><span class="sxs-lookup"><span data-stu-id="36183-109">Whether you are an application developer, a call center, a government agency, an entertainment company, Media Services helps you create applications that deliver media experiences of outstanding quality to large audiences on today’s most popular mobile devices and browsers.</span></span> 

## <a name="what-can-i-do-with-media-services"></a><span data-ttu-id="36183-110">What can I do with Media Services?</span><span class="sxs-lookup"><span data-stu-id="36183-110">What can I do with Media Services?</span></span>

<span data-ttu-id="36183-111">Media Services enables you to build a variety of media workflows in the cloud, the following are some examples of what can be accomplished with Media Services.</span><span class="sxs-lookup"><span data-stu-id="36183-111">Media Services enables you to build a variety of media workflows in the cloud, the following are some examples of what can be accomplished with Media Services.</span></span>  

* <span data-ttu-id="36183-112">Deliver videos in various formats so they can be played on a wide variety of browsers and devices.</span><span class="sxs-lookup"><span data-stu-id="36183-112">Deliver videos in various formats so they can be played on a wide variety of browsers and devices.</span></span> <span data-ttu-id="36183-113">For both on-demand and live streaming delivery to various clients (mobile devices, TV, PC, etc.) the video and audio content needs to be encoded and packaged appropriately.</span><span class="sxs-lookup"><span data-stu-id="36183-113">For both on-demand and live streaming delivery to various clients (mobile devices, TV, PC, etc.) the video and audio content needs to be encoded and packaged appropriately.</span></span> <span data-ttu-id="36183-114">To see how to deliver and stream such content, see [Quickstart: Encode and stream files](stream-files-dotnet-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="36183-114">To see how to deliver and stream such content, see [Quickstart: Encode and stream files](stream-files-dotnet-quickstart.md).</span></span>
* <span data-ttu-id="36183-115">Stream live sporting events to a large online audience, such as soccer, baseball, college and high school sports, and more.</span><span class="sxs-lookup"><span data-stu-id="36183-115">Stream live sporting events to a large online audience, such as soccer, baseball, college and high school sports, and more.</span></span> 
* <span data-ttu-id="36183-116">Broadcast public meetings and events such as town halls, city council meetings, and legislative bodies.</span><span class="sxs-lookup"><span data-stu-id="36183-116">Broadcast public meetings and events such as town halls, city council meetings, and legislative bodies.</span></span>
* <span data-ttu-id="36183-117">Analyze recorded videos or audio content.</span><span class="sxs-lookup"><span data-stu-id="36183-117">Analyze recorded videos or audio content.</span></span> <span data-ttu-id="36183-118">For example, to achieve higher customer satisfaction, organizations can extract speech-to-text and build search indexes and dashboards.</span><span class="sxs-lookup"><span data-stu-id="36183-118">For example, to achieve higher customer satisfaction, organizations can extract speech-to-text and build search indexes and dashboards.</span></span> <span data-ttu-id="36183-119">Then, they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span><span class="sxs-lookup"><span data-stu-id="36183-119">Then, they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span> 
* <span data-ttu-id="36183-120">Create a subscription video service and stream DRM protected content when a customer (for example, a movie studio) needs to restrict the access and use of proprietary copyrighted work.</span><span class="sxs-lookup"><span data-stu-id="36183-120">Create a subscription video service and stream DRM protected content when a customer (for example, a movie studio) needs to restrict the access and use of proprietary copyrighted work.</span></span>
* <span data-ttu-id="36183-121">Deliver offline content for playback on airplanes, trains, and automobiles.</span><span class="sxs-lookup"><span data-stu-id="36183-121">Deliver offline content for playback on airplanes, trains, and automobiles.</span></span> <span data-ttu-id="36183-122">A customer might need to download content onto their phone or tablet for playback when they anticipate to be disconnected from the network.</span><span class="sxs-lookup"><span data-stu-id="36183-122">A customer might need to download content onto their phone or tablet for playback when they anticipate to be disconnected from the network.</span></span>
* <span data-ttu-id="36183-123">Add subtitles and captions to videos to cater to a broader audience (for example, people with hearing disabilities or people who want to read along in a different language).</span><span class="sxs-lookup"><span data-stu-id="36183-123">Add subtitles and captions to videos to cater to a broader audience (for example, people with hearing disabilities or people who want to read along in a different language).</span></span> 
* <span data-ttu-id="36183-124">Implement an educational e-learning video platform with Azure Media Services and [Azure Cognitive Services APIs](https://docs.microsoft.com/azure/#pivot=products&panel=ai) for speech-to-text captioning, translating to multi-languages, etc.</span><span class="sxs-lookup"><span data-stu-id="36183-124">Implement an educational e-learning video platform with Azure Media Services and [Azure Cognitive Services APIs](https://docs.microsoft.com/azure/#pivot=products&panel=ai) for speech-to-text captioning, translating to multi-languages, etc.</span></span>
* <span data-ttu-id="36183-125">Enable Azure CDN to achieve large scaling to better handle instantaneous high loads (for example, the start of a product launch event.)</span><span class="sxs-lookup"><span data-stu-id="36183-125">Enable Azure CDN to achieve large scaling to better handle instantaneous high loads (for example, the start of a product launch event.)</span></span> 

## <a name="v3-capabilities"></a><span data-ttu-id="36183-126">v3 capabilities</span><span class="sxs-lookup"><span data-stu-id="36183-126">v3 capabilities</span></span>

<span data-ttu-id="36183-127">v3 is based on a unified API surface, which exposes both management and operations functionality built on Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36183-127">v3 is based on a unified API surface, which exposes both management and operations functionality built on Azure Resource Manager.</span></span> 

<span data-ttu-id="36183-128">This version provides the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="36183-128">This version provides the following capabilities:</span></span>  

* <span data-ttu-id="36183-129">**Transforms** that help you define simple workflows of media processing or analytics tasks.</span><span class="sxs-lookup"><span data-stu-id="36183-129">**Transforms** that help you define simple workflows of media processing or analytics tasks.</span></span> <span data-ttu-id="36183-130">Transform is a recipe for processing your video and audio files.</span><span class="sxs-lookup"><span data-stu-id="36183-130">Transform is a recipe for processing your video and audio files.</span></span> <span data-ttu-id="36183-131">You can then apply it repeatedly to process all the files in your content library, by submitting jobs to the Transform.</span><span class="sxs-lookup"><span data-stu-id="36183-131">You can then apply it repeatedly to process all the files in your content library, by submitting jobs to the Transform.</span></span>
* <span data-ttu-id="36183-132">**Jobs** to process (encode or analyze) your videos.</span><span class="sxs-lookup"><span data-stu-id="36183-132">**Jobs** to process (encode or analyze) your videos.</span></span> <span data-ttu-id="36183-133">An input content can be specified on a job using HTTP(s) URLs, SAS URLs, or paths to files located in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="36183-133">An input content can be specified on a job using HTTP(s) URLs, SAS URLs, or paths to files located in Azure Blob storage.</span></span> 
* <span data-ttu-id="36183-134">**Notifications** that monitor job progress or states, or Live Channel start/stop and error events.</span><span class="sxs-lookup"><span data-stu-id="36183-134">**Notifications** that monitor job progress or states, or Live Channel start/stop and error events.</span></span> <span data-ttu-id="36183-135">Notifications are integrated with the Azure Event Grid notification system.</span><span class="sxs-lookup"><span data-stu-id="36183-135">Notifications are integrated with the Azure Event Grid notification system.</span></span> <span data-ttu-id="36183-136">You can easily subscribe to events on several resources in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="36183-136">You can easily subscribe to events on several resources in Azure Media Services.</span></span> 
* <span data-ttu-id="36183-137">**Azure Resource Management** templates can be used to create and deploy Transforms, Streaming Endpoints, Channels, and more.</span><span class="sxs-lookup"><span data-stu-id="36183-137">**Azure Resource Management** templates can be used to create and deploy Transforms, Streaming Endpoints, Channels, and more.</span></span>
* <span data-ttu-id="36183-138">**Role-based access control** can be set at the resource level, allowing you to lock down access to specific resources like Transforms, Channels, and more.</span><span class="sxs-lookup"><span data-stu-id="36183-138">**Role-based access control** can be set at the resource level, allowing you to lock down access to specific resources like Transforms, Channels, and more.</span></span>
* <span data-ttu-id="36183-139">**Client SDKs** in multiple languages: .NET, .NET core, Python, Go, Java, and Node.js.</span><span class="sxs-lookup"><span data-stu-id="36183-139">**Client SDKs** in multiple languages: .NET, .NET core, Python, Go, Java, and Node.js.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="36183-140">Naming conventions</span><span class="sxs-lookup"><span data-stu-id="36183-140">Naming conventions</span></span>

<span data-ttu-id="36183-141">Azure Media Services v3 resource names (for example, Assets, Jobs, Transforms) are subject to Azure Resource Manager naming constraints.</span><span class="sxs-lookup"><span data-stu-id="36183-141">Azure Media Services v3 resource names (for example, Assets, Jobs, Transforms) are subject to Azure Resource Manager naming constraints.</span></span> <span data-ttu-id="36183-142">In accordance with Azure Resource Manager, the resource names are always unique.</span><span class="sxs-lookup"><span data-stu-id="36183-142">In accordance with Azure Resource Manager, the resource names are always unique.</span></span> <span data-ttu-id="36183-143">Thus, you can use any unique identifier strings (for example, GUIDs) for your resource names.</span><span class="sxs-lookup"><span data-stu-id="36183-143">Thus, you can use any unique identifier strings (for example, GUIDs) for your resource names.</span></span> 

<span data-ttu-id="36183-144">Media Services resource names cannot include: '<', '>', '%', '&', ':', '&#92;', '?', '/', '\*', '+', '.', the single quote character, or any control characters.</span><span class="sxs-lookup"><span data-stu-id="36183-144">Media Services resource names cannot include: '<', '>', '%', '&', ':', '&#92;', '?', '/', '\*', '+', '.', the single quote character, or any control characters.</span></span> <span data-ttu-id="36183-145">All other characters are allowed.</span><span class="sxs-lookup"><span data-stu-id="36183-145">All other characters are allowed.</span></span> <span data-ttu-id="36183-146">The max length of a resource name is 260 characters.</span><span class="sxs-lookup"><span data-stu-id="36183-146">The max length of a resource name is 260 characters.</span></span> 

<span data-ttu-id="36183-147">For more information about Azure Resource Manager naming, see: [Naming requirements](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/resource-api-reference.md#arguments-for-crud-on-resource) and [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="36183-147">For more information about Azure Resource Manager naming, see: [Naming requirements](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/resource-api-reference.md#arguments-for-crud-on-resource) and [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span>

## <a name="media-services-v3-api-design-principles"></a><span data-ttu-id="36183-148">Media Services v3 API design principles</span><span class="sxs-lookup"><span data-stu-id="36183-148">Media Services v3 API design principles</span></span>

<span data-ttu-id="36183-149">One of the key design principles of the v3 API is to make the API more secure.</span><span class="sxs-lookup"><span data-stu-id="36183-149">One of the key design principles of the v3 API is to make the API more secure.</span></span> <span data-ttu-id="36183-150">v3 APIs do not return secrets or credentials on a **Get** or **List** operation.</span><span class="sxs-lookup"><span data-stu-id="36183-150">v3 APIs do not return secrets or credentials on a **Get** or **List** operation.</span></span> <span data-ttu-id="36183-151">The keys are always null, empty, or sanitized from the response.</span><span class="sxs-lookup"><span data-stu-id="36183-151">The keys are always null, empty, or sanitized from the response.</span></span> <span data-ttu-id="36183-152">You need to call a separate action method to get secrets or credentials.</span><span class="sxs-lookup"><span data-stu-id="36183-152">You need to call a separate action method to get secrets or credentials.</span></span> <span data-ttu-id="36183-153">Separate actions enable you to set different RBAC security permissions in case some APIs do retrieve/display  secrets while other APIs do not.</span><span class="sxs-lookup"><span data-stu-id="36183-153">Separate actions enable you to set different RBAC security permissions in case some APIs do retrieve/display  secrets while other APIs do not.</span></span> <span data-ttu-id="36183-154">For information on how to manager access using RBAC, see [Use RBAC to manage access](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-rest).</span><span class="sxs-lookup"><span data-stu-id="36183-154">For information on how to manager access using RBAC, see [Use RBAC to manage access](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-rest).</span></span>

<span data-ttu-id="36183-155">Examples of this include</span><span class="sxs-lookup"><span data-stu-id="36183-155">Examples of this include</span></span> 

* <span data-ttu-id="36183-156">not returning ContentKey values in the Get of the StreamingLocator,</span><span class="sxs-lookup"><span data-stu-id="36183-156">not returning ContentKey values in the Get of the StreamingLocator,</span></span> 
* <span data-ttu-id="36183-157">not returning the restriction keys in the get of the ContentKeyPolicy,</span><span class="sxs-lookup"><span data-stu-id="36183-157">not returning the restriction keys in the get of the ContentKeyPolicy,</span></span> 
* <span data-ttu-id="36183-158">not returning the query string part of the URL (to remove the signature) of Jobs' HTTP Input URLs.</span><span class="sxs-lookup"><span data-stu-id="36183-158">not returning the query string part of the URL (to remove the signature) of Jobs' HTTP Input URLs.</span></span>

<span data-ttu-id="36183-159">The following .NET example shows how to get a signing key from the existing policy.</span><span class="sxs-lookup"><span data-stu-id="36183-159">The following .NET example shows how to get a signing key from the existing policy.</span></span> <span data-ttu-id="36183-160">You need to use **GetPolicyPropertiesWithSecretsAsync** to get to the key.</span><span class="sxs-lookup"><span data-stu-id="36183-160">You need to use **GetPolicyPropertiesWithSecretsAsync** to get to the key.</span></span>

```csharp
private static async Task<ContentKeyPolicy> GetOrCreateContentKeyPolicyAsync(
    IAzureMediaServicesClient client,
    string resourceGroupName,
    string accountName,
    string contentKeyPolicyName)
{
    ContentKeyPolicy policy = await client.ContentKeyPolicies.GetAsync(resourceGroupName, accountName, contentKeyPolicyName);

    if (policy == null)
    {
        // Configure and create a new policy.
        
        . . . 
        policy = await client.ContentKeyPolicies.CreateOrUpdateAsync(resourceGroupName, accountName, contentKeyPolicyName, options);
    }
    else
    {
        var policyProperties = await client.ContentKeyPolicies.GetPolicyPropertiesWithSecretsAsync(resourceGroupName, accountName, contentKeyPolicyName);
        var restriction = policyProperties.Options[0].Restriction as ContentKeyPolicyTokenRestriction;
        if (restriction != null)
        {
            var signingKey = restriction.PrimaryVerificationKey as ContentKeyPolicySymmetricTokenKey;
            if (signingKey != null)
            {
                TokenSigningKey = signingKey.KeyValue;
            }
        }
    }

    return policy;
}
```

## <a name="how-can-i-get-started-with-v3"></a><span data-ttu-id="36183-161">How can I get started with v3?</span><span class="sxs-lookup"><span data-stu-id="36183-161">How can I get started with v3?</span></span>

<span data-ttu-id="36183-162">As a developer, you can use Media Services [REST API](https://go.microsoft.com/fwlink/p/?linkid=873030) or client libraries that allow you to interact with the REST API, to easily create, manage, and maintain custom media workflows.</span><span class="sxs-lookup"><span data-stu-id="36183-162">As a developer, you can use Media Services [REST API](https://go.microsoft.com/fwlink/p/?linkid=873030) or client libraries that allow you to interact with the REST API, to easily create, manage, and maintain custom media workflows.</span></span>  

<span data-ttu-id="36183-163">Media Services provides [Swagger files](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/mediaservices/resource-manager/Microsoft.Media) that you can use to generate SDKs for your preferred language/technology.</span><span class="sxs-lookup"><span data-stu-id="36183-163">Media Services provides [Swagger files](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/mediaservices/resource-manager/Microsoft.Media) that you can use to generate SDKs for your preferred language/technology.</span></span>  

<span data-ttu-id="36183-164">Microsoft generates and supports the following client libraries:</span><span class="sxs-lookup"><span data-stu-id="36183-164">Microsoft generates and supports the following client libraries:</span></span> 

|<span data-ttu-id="36183-165">API references</span><span class="sxs-lookup"><span data-stu-id="36183-165">API references</span></span>|<span data-ttu-id="36183-166">SDKs/Tools</span><span class="sxs-lookup"><span data-stu-id="36183-166">SDKs/Tools</span></span>|<span data-ttu-id="36183-167">Examples</span><span class="sxs-lookup"><span data-stu-id="36183-167">Examples</span></span>|
|---|---|---|---|
|[<span data-ttu-id="36183-168">REST ref</span><span class="sxs-lookup"><span data-stu-id="36183-168">REST ref</span></span>](https://aka.ms/ams-v3-rest-ref)|[<span data-ttu-id="36183-169">REST SDK</span><span class="sxs-lookup"><span data-stu-id="36183-169">REST SDK</span></span>](https://aka.ms/ams-v3-rest-sdk)|[<span data-ttu-id="36183-170">REST Postman examples</span><span class="sxs-lookup"><span data-stu-id="36183-170">REST Postman examples</span></span>](https://github.com/Azure-Samples/media-services-v3-rest-postman)<br/>[<span data-ttu-id="36183-171">Azure Resource Manager based REST API</span><span class="sxs-lookup"><span data-stu-id="36183-171">Azure Resource Manager based REST API</span></span>](https://github.com/Azure-Samples/media-services-v3-arm-templates)|
|[<span data-ttu-id="36183-172">Azure CLI ref</span><span class="sxs-lookup"><span data-stu-id="36183-172">Azure CLI ref</span></span>](https://aka.ms/ams-v3-cli-ref)|[<span data-ttu-id="36183-173">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="36183-173">Azure CLI</span></span>](https://aka.ms/ams-v3-cli)|[<span data-ttu-id="36183-174">Azure CLI examples</span><span class="sxs-lookup"><span data-stu-id="36183-174">Azure CLI examples</span></span>](https://github.com/Azure/azure-docs-cli-python-samples/tree/master/media-services)||
|[<span data-ttu-id="36183-175">.NET ref</span><span class="sxs-lookup"><span data-stu-id="36183-175">.NET ref</span></span>](https://aka.ms/ams-v3-dotnet-ref)|[<span data-ttu-id="36183-176">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="36183-176">.NET SDK</span></span>](https://aka.ms/ams-v3-dotnet-sdk)|[<span data-ttu-id="36183-177">.NET examples</span><span class="sxs-lookup"><span data-stu-id="36183-177">.NET examples</span></span>](https://github.com/Azure-Samples/media-services-v3-dotnet-tutorials)||
||<span data-ttu-id="36183-178">[.NET Core SDK](https://aka.ms/ams-v3-dotnet-sdk) (Choose the **.NET CLI** tab)</span><span class="sxs-lookup"><span data-stu-id="36183-178">[.NET Core SDK](https://aka.ms/ams-v3-dotnet-sdk) (Choose the **.NET CLI** tab)</span></span>|[<span data-ttu-id="36183-179">.NET Core examples</span><span class="sxs-lookup"><span data-stu-id="36183-179">.NET Core examples</span></span>](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials)||
|[<span data-ttu-id="36183-180">Java ref</span><span class="sxs-lookup"><span data-stu-id="36183-180">Java ref</span></span>](https://aka.ms/ams-v3-java-ref)|[<span data-ttu-id="36183-181">Java SDK</span><span class="sxs-lookup"><span data-stu-id="36183-181">Java SDK</span></span>](https://aka.ms/ams-v3-java-sdk)||
|[<span data-ttu-id="36183-182">Node.js ref</span><span class="sxs-lookup"><span data-stu-id="36183-182">Node.js ref</span></span>](https://aka.ms/ams-v3-nodejs-ref)|[<span data-ttu-id="36183-183">Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="36183-183">Node.js SDK</span></span>](https://aka.ms/ams-v3-nodejs-sdk)|[<span data-ttu-id="36183-184">Node.js samples</span><span class="sxs-lookup"><span data-stu-id="36183-184">Node.js samples</span></span>](https://github.com/Azure-Samples/media-services-v3-node-tutorials)||
|[<span data-ttu-id="36183-185">Python ref</span><span class="sxs-lookup"><span data-stu-id="36183-185">Python ref</span></span>](https://aka.ms/ams-v3-python-ref)|[<span data-ttu-id="36183-186">Python SDK</span><span class="sxs-lookup"><span data-stu-id="36183-186">Python SDK</span></span>](https://aka.ms/ams-v3-python-sdk)||
|[<span data-ttu-id="36183-187">Go ref</span><span class="sxs-lookup"><span data-stu-id="36183-187">Go ref</span></span>](https://aka.ms/ams-v3-go-ref)|[<span data-ttu-id="36183-188">Go SDK</span><span class="sxs-lookup"><span data-stu-id="36183-188">Go SDK</span></span>](https://aka.ms/ams-v3-go-sdk)||

## <a name="next-steps"></a><span data-ttu-id="36183-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="36183-189">Next steps</span></span>

<span data-ttu-id="36183-190">To see how easy it is to start encoding and streaming video files, check out [Stream files](stream-files-dotnet-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="36183-190">To see how easy it is to start encoding and streaming video files, check out [Stream files](stream-files-dotnet-quickstart.md).</span></span> 

