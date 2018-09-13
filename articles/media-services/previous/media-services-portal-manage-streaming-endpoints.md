---
title: Manage streaming endpoints with the Azure portal | Microsoft Docs
description: This topic shows how to manage streaming endpoints with the Azure portal.
services: media-services
documentationcenter: ''
author: Juliako
writer: juliako
manager: cfowler
editor: ''
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2017
ms.author: juliako
ms.openlocfilehash: 542780766cfa90026d5ff492fcf7b579cb2d7029
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865728"
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="a7533-103">Manage streaming endpoints with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a7533-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="a7533-104">This article shows  how to use the Azure portal to manage streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="a7533-104">This article shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="a7533-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="a7533-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) article.</span></span> 

<span data-ttu-id="a7533-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) article.</span><span class="sxs-lookup"><span data-stu-id="a7533-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) article.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="a7533-107">Start managing streaming endpoints</span><span class="sxs-lookup"><span data-stu-id="a7533-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="a7533-108">To start managing streaming endpoints for your account, do the following.</span><span class="sxs-lookup"><span data-stu-id="a7533-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="a7533-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="a7533-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a7533-110">In the **Settings** blade, select **Streaming endpoints**.</span><span class="sxs-lookup"><span data-stu-id="a7533-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![Streaming endpoint](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="a7533-112">You are only billed when your Streaming Endpoint is in running state.</span><span class="sxs-lookup"><span data-stu-id="a7533-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="a7533-113">Add/delete a streaming endpoint</span><span class="sxs-lookup"><span data-stu-id="a7533-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="a7533-114">The default streaming endpoint cannot be deleted.</span><span class="sxs-lookup"><span data-stu-id="a7533-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="a7533-115">To add/delete streaming endpoint using the Azure portal, do the following:</span><span class="sxs-lookup"><span data-stu-id="a7533-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="a7533-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="a7533-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="a7533-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span><span class="sxs-lookup"><span data-stu-id="a7533-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="a7533-118">To delete a streaming endpoint, press **Delete** button.</span><span class="sxs-lookup"><span data-stu-id="a7533-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="a7533-119">Click the **Start** button to start the streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="a7533-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![Streaming endpoint](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a><span data-ttu-id="a7533-121">Configuring the Streaming Endpoint</span><span class="sxs-lookup"><span data-stu-id="a7533-121">Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="a7533-122">Streaming Endpoint enables you to configure the following properties:</span><span class="sxs-lookup"><span data-stu-id="a7533-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="a7533-123">Access control</span><span class="sxs-lookup"><span data-stu-id="a7533-123">Access control</span></span>
* <span data-ttu-id="a7533-124">Cache control</span><span class="sxs-lookup"><span data-stu-id="a7533-124">Cache control</span></span>
* <span data-ttu-id="a7533-125">Cross site access policies</span><span class="sxs-lookup"><span data-stu-id="a7533-125">Cross site access policies</span></span>

<span data-ttu-id="a7533-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="a7533-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

>[!NOTE]
><span data-ttu-id="a7533-127">When CDN is enabled, you cannot access IP access.</span><span class="sxs-lookup"><span data-stu-id="a7533-127">When CDN is enabled, you cannot access IP access.</span></span> <span data-ttu-id="a7533-128">IP access is only applicable when you don’t have CDN.</span><span class="sxs-lookup"><span data-stu-id="a7533-128">IP access is only applicable when you don’t have CDN.</span></span>

<span data-ttu-id="a7533-129">You can configure streaming endpoint by doing the following:</span><span class="sxs-lookup"><span data-stu-id="a7533-129">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="a7533-130">Select the streaming endpoint you want to configure.</span><span class="sxs-lookup"><span data-stu-id="a7533-130">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="a7533-131">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a7533-131">Click **Settings**.</span></span>

<span data-ttu-id="a7533-132">A brief description of the fields follows.</span><span class="sxs-lookup"><span data-stu-id="a7533-132">A brief description of the fields follows.</span></span>

![Streaming endpoint](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="a7533-134">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="a7533-134">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="a7533-135">If no value is set, the default is used.</span><span class="sxs-lookup"><span data-stu-id="a7533-135">If no value is set, the default is used.</span></span> <span data-ttu-id="a7533-136">The default values can also be defined directly in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="a7533-136">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="a7533-137">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span><span class="sxs-lookup"><span data-stu-id="a7533-137">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="a7533-138">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="a7533-138">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="a7533-139">If no IP addresses specified, any IP address would be able to connect.</span><span class="sxs-lookup"><span data-stu-id="a7533-139">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="a7533-140">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span><span class="sxs-lookup"><span data-stu-id="a7533-140">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="a7533-141">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span><span class="sxs-lookup"><span data-stu-id="a7533-141">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="a7533-142">Expiration is in UTC.</span><span class="sxs-lookup"><span data-stu-id="a7533-142">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="a7533-143">Scale your Premium streaming endpoint</span><span class="sxs-lookup"><span data-stu-id="a7533-143">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="a7533-144">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) article.</span><span class="sxs-lookup"><span data-stu-id="a7533-144">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) article.</span></span>

## <a id="enable_cdn"></a><span data-ttu-id="a7533-145">Enable Azure CDN integration</span><span class="sxs-lookup"><span data-stu-id="a7533-145">Enable Azure CDN integration</span></span>

<span data-ttu-id="a7533-146">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="a7533-146">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="a7533-147">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span><span class="sxs-lookup"><span data-stu-id="a7533-147">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="a7533-148">It could take up to two hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span><span class="sxs-lookup"><span data-stu-id="a7533-148">It could take up to two hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="a7533-149">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream is delivered from the CDN.</span><span class="sxs-lookup"><span data-stu-id="a7533-149">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream is delivered from the CDN.</span></span> <span data-ttu-id="a7533-150">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span><span class="sxs-lookup"><span data-stu-id="a7533-150">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="a7533-151">CDN integration is enabled in all the Azure data centers except China and Federal Government regions.</span><span class="sxs-lookup"><span data-stu-id="a7533-151">CDN integration is enabled in all the Azure data centers except China and Federal Government regions.</span></span>

<span data-ttu-id="a7533-152">Once it is enabled, the **Access Control**, \*\*Custom hostname, and **Akamai Signature authentication** configuration gets disabled.</span><span class="sxs-lookup"><span data-stu-id="a7533-152">Once it is enabled, the **Access Control**, \*\*Custom hostname, and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="a7533-153">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="a7533-153">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="a7533-154">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span><span class="sxs-lookup"><span data-stu-id="a7533-154">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="a7533-155">For more information about Azure CDN features, see the [CDN overview](../../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a7533-155">For more information about Azure CDN features, see the [CDN overview](../../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="a7533-156">Additional considerations</span><span class="sxs-lookup"><span data-stu-id="a7533-156">Additional considerations</span></span>

* <span data-ttu-id="a7533-157">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span><span class="sxs-lookup"><span data-stu-id="a7533-157">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="a7533-158">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span><span class="sxs-lookup"><span data-stu-id="a7533-158">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="a7533-159">Your streaming endpoint hostname remains the same after enabling CDN.</span><span class="sxs-lookup"><span data-stu-id="a7533-159">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="a7533-160">You don’t need to make any changes to your media services workflow after CDN is enabled.</span><span class="sxs-lookup"><span data-stu-id="a7533-160">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="a7533-161">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span><span class="sxs-lookup"><span data-stu-id="a7533-161">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="a7533-162">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span><span class="sxs-lookup"><span data-stu-id="a7533-162">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="a7533-163">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="a7533-163">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure classic portal.</span></span> <span data-ttu-id="a7533-164">However, you can enable other Azure CDN providers using REST APIs.</span><span class="sxs-lookup"><span data-stu-id="a7533-164">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="a7533-165">Configure CDN profile</span><span class="sxs-lookup"><span data-stu-id="a7533-165">Configure CDN profile</span></span>

<span data-ttu-id="a7533-166">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span><span class="sxs-lookup"><span data-stu-id="a7533-166">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![Streaming endpoint](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="a7533-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7533-168">Next steps</span></span>
<span data-ttu-id="a7533-169">Review Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="a7533-169">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7533-170">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="a7533-170">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

