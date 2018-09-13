---
title: Azure Media Services overview | Microsoft Docs
description: This topic gives an overview of Azure Media Services
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 10/24/2017
ms.author: juliako;anilmur
ms.openlocfilehash: d79a8937c0190246218153e42ead74ada619b121
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856415"
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="73e09-103">Azure Media Services overview</span><span class="sxs-lookup"><span data-stu-id="73e09-103">Azure Media Services overview</span></span> 

> [!div class="op_single_selector" title1="Select the version of Media Services that you are using:"]
> * [Version 2 - GA](media-services-overview.md)
> * [Version 3 - Preview](../latest/media-services-overview.md)

<span data-ttu-id="73e09-106">Microsoft Azure Media Services (AMS) is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span><span class="sxs-lookup"><span data-stu-id="73e09-106">Microsoft Azure Media Services (AMS) is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="73e09-107">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span><span class="sxs-lookup"><span data-stu-id="73e09-107">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="73e09-108">You can build end-to-end workflows using entirely Media Services.</span><span class="sxs-lookup"><span data-stu-id="73e09-108">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="73e09-109">You can also choose to use third-party components for some parts of your workflow.</span><span class="sxs-lookup"><span data-stu-id="73e09-109">You can also choose to use third-party components for some parts of your workflow.</span></span> <span data-ttu-id="73e09-110">For example, encode using a third-party encoder.</span><span class="sxs-lookup"><span data-stu-id="73e09-110">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="73e09-111">Then, upload, protect, package, deliver using Media Services.</span><span class="sxs-lookup"><span data-stu-id="73e09-111">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="73e09-112">You can choose to stream your content live or deliver content on-demand.</span><span class="sxs-lookup"><span data-stu-id="73e09-112">You can choose to stream your content live or deliver content on-demand.</span></span> <span data-ttu-id="73e09-113">The topic also links to other relevant topics.</span><span class="sxs-lookup"><span data-stu-id="73e09-113">The topic also links to other relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="73e09-114">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="73e09-114">Media Services learning paths</span></span>
<span data-ttu-id="73e09-115">You can view AMS learning paths here:</span><span class="sxs-lookup"><span data-stu-id="73e09-115">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="73e09-116">AMS Live Streaming Workflow</span><span class="sxs-lookup"><span data-stu-id="73e09-116">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="73e09-117">AMS on-Demand Streaming Workflow</span><span class="sxs-lookup"><span data-stu-id="73e09-117">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="73e09-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="73e09-118">Prerequisites</span></span>

<span data-ttu-id="73e09-119">To start using Azure Media Services, you should have the following:</span><span class="sxs-lookup"><span data-stu-id="73e09-119">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="73e09-120">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="73e09-120">An Azure account.</span></span> <span data-ttu-id="73e09-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="73e09-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="73e09-122">For details, see [Azure Free Trial](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="73e09-122">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="73e09-123">An Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="73e09-123">An Azure Media Services account.</span></span> <span data-ttu-id="73e09-124">For more information, see [Create Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="73e09-124">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="73e09-125">(Optional) Set up development environment.</span><span class="sxs-lookup"><span data-stu-id="73e09-125">(Optional) Set up development environment.</span></span> <span data-ttu-id="73e09-126">Choose .NET or REST API for your development environment.</span><span class="sxs-lookup"><span data-stu-id="73e09-126">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="73e09-127">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="73e09-127">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="73e09-128">Also, learn how to [connect  programmatically to AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="73e09-128">Also, learn how to [connect  programmatically to AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="73e09-129">A standard or premium streaming endpoint in started state.</span><span class="sxs-lookup"><span data-stu-id="73e09-129">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="73e09-130">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="73e09-130">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="73e09-131">SDKs and tools</span><span class="sxs-lookup"><span data-stu-id="73e09-131">SDKs and tools</span></span>

<span data-ttu-id="73e09-132">To build Media Services solutions, you can use:</span><span class="sxs-lookup"><span data-stu-id="73e09-132">To build Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="73e09-133">Media Services REST API</span><span class="sxs-lookup"><span data-stu-id="73e09-133">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="73e09-134">One of the available client SDKs:</span><span class="sxs-lookup"><span data-stu-id="73e09-134">One of the available client SDKs:</span></span>
    * <span data-ttu-id="73e09-135">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="73e09-135">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="73e09-136">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="73e09-136">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="73e09-137">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="73e09-137">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="73e09-138">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="73e09-138">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="73e09-139">It is maintained by a community and currently does not have a 100% coverage of the AMS APIs).</span><span class="sxs-lookup"><span data-stu-id="73e09-139">It is maintained by a community and currently does not have a 100% coverage of the AMS APIs).</span></span>
* <span data-ttu-id="73e09-140">Existing tools:</span><span class="sxs-lookup"><span data-stu-id="73e09-140">Existing tools:</span></span>
    * [<span data-ttu-id="73e09-141">Azure portal</span><span class="sxs-lookup"><span data-stu-id="73e09-141">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="73e09-142">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span><span class="sxs-lookup"><span data-stu-id="73e09-142">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

> [!NOTE]
> To get the latest version of Java SDK and get started developing with Java, see [Get started with the Java client SDK for Media Services](https://docs.microsoft.com/azure/media-services/media-services-java-how-to-use). <br/>
> To download the latest PHP SDK for Media Services, look for version 0.5.7 of the Microsoft/WindowAzure package in the [Packagist repository](https://packagist.org/packages/microsoft/windowsazure#v0.5.7).  

## <a name="code-samples"></a><span data-ttu-id="73e09-145">Code samples</span><span class="sxs-lookup"><span data-stu-id="73e09-145">Code samples</span></span>

<span data-ttu-id="73e09-146">Find multiple code samples in the **Azure Code Samples** gallery: [Azure Media Services code samples](https://azure.microsoft.com/resources/samples/?service=media-services&sort=0).</span><span class="sxs-lookup"><span data-stu-id="73e09-146">Find multiple code samples in the **Azure Code Samples** gallery: [Azure Media Services code samples](https://azure.microsoft.com/resources/samples/?service=media-services&sort=0).</span></span>

## <a name="concepts"></a><span data-ttu-id="73e09-147">Concepts</span><span class="sxs-lookup"><span data-stu-id="73e09-147">Concepts</span></span>

<span data-ttu-id="73e09-148">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="73e09-148">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="73e09-149">Supported scenarios and availability of Media Services across data centers</span><span class="sxs-lookup"><span data-stu-id="73e09-149">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="73e09-150">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="73e09-150">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="73e09-151">Service Level Agreement (SLA)</span><span class="sxs-lookup"><span data-stu-id="73e09-151">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="73e09-152">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span><span class="sxs-lookup"><span data-stu-id="73e09-152">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="73e09-153">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span><span class="sxs-lookup"><span data-stu-id="73e09-153">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="73e09-154">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of the time.</span><span class="sxs-lookup"><span data-stu-id="73e09-154">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of the time.</span></span>
* <span data-ttu-id="73e09-155">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of the time.</span><span class="sxs-lookup"><span data-stu-id="73e09-155">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of the time.</span></span>
* <span data-ttu-id="73e09-156">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of the time.</span><span class="sxs-lookup"><span data-stu-id="73e09-156">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of the time.</span></span>

<span data-ttu-id="73e09-157">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="73e09-157">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="73e09-158">For information about availability in datacenters, see the [Availability](scenarios-and-availability.md#availability) section.</span><span class="sxs-lookup"><span data-stu-id="73e09-158">For information about availability in datacenters, see the [Availability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="73e09-159">Support</span><span class="sxs-lookup"><span data-stu-id="73e09-159">Support</span></span>

<span data-ttu-id="73e09-160">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span><span class="sxs-lookup"><span data-stu-id="73e09-160">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="73e09-161">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="73e09-161">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
