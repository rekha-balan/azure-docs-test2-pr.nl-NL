---
title: Get started with delivering content on demand using REST | Microsoft Docs
description: This tutorial walks you through the steps of implementing an on demand content delivery application with Azure Media Services using REST API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2018
ms.author: juliako
ms.openlocfilehash: 015b8570e9cbb06a33107de7a8cb9ae00d60cacb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867317"
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="a317a-103">Get started with delivering content on demand using REST</span><span class="sxs-lookup"><span data-stu-id="a317a-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="a317a-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span><span class="sxs-lookup"><span data-stu-id="a317a-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="a317a-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span><span class="sxs-lookup"><span data-stu-id="a317a-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="a317a-106">At the completion of the tutorial, you are able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span><span class="sxs-lookup"><span data-stu-id="a317a-106">At the completion of the tutorial, you are able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="a317a-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span><span class="sxs-lookup"><span data-stu-id="a317a-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="a317a-108">Click the image to view it full size.</span><span class="sxs-lookup"><span data-stu-id="a317a-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="a317a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a317a-109">Prerequisites</span></span>
<span data-ttu-id="a317a-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span><span class="sxs-lookup"><span data-stu-id="a317a-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="a317a-111">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="a317a-111">An Azure account.</span></span> <span data-ttu-id="a317a-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a317a-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a317a-113">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="a317a-113">A Media Services account.</span></span> <span data-ttu-id="a317a-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a317a-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="a317a-115">Understanding of how to develop with Media Services REST API.</span><span class="sxs-lookup"><span data-stu-id="a317a-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="a317a-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a317a-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="a317a-117">An application of your choice that can send HTTP requests and responses.</span><span class="sxs-lookup"><span data-stu-id="a317a-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="a317a-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="a317a-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="a317a-119">The following tasks are shown in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a317a-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="a317a-120">Start streaming endpoint (using the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="a317a-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="a317a-121">Connect to the Media Services account with REST API.</span><span class="sxs-lookup"><span data-stu-id="a317a-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="a317a-122">Create a new asset and upload a video file with REST API.</span><span class="sxs-lookup"><span data-stu-id="a317a-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="a317a-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span><span class="sxs-lookup"><span data-stu-id="a317a-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="a317a-124">Publish the asset and get streaming and progressive download URLs with REST API.</span><span class="sxs-lookup"><span data-stu-id="a317a-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="a317a-125">Play your content.</span><span class="sxs-lookup"><span data-stu-id="a317a-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="a317a-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a317a-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a317a-127">Use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span><span class="sxs-lookup"><span data-stu-id="a317a-127">Use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a317a-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.</span><span class="sxs-lookup"><span data-stu-id="a317a-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.</span></span>

<span data-ttu-id="a317a-129">For details about AMS REST entities used in this article, see [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="a317a-129">For details about AMS REST entities used in this article, see [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="a317a-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a317a-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="a317a-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="a317a-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a317a-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a317a-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="a317a-133">Start streaming endpoints using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a317a-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="a317a-134">When working with Azure Media Services, one of the most common scenarios is delivering video via adaptive bitrate streaming.</span><span class="sxs-lookup"><span data-stu-id="a317a-134">When working with Azure Media Services, one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="a317a-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span><span class="sxs-lookup"><span data-stu-id="a317a-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a317a-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="a317a-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a317a-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="a317a-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="a317a-138">To start the streaming endpoint, do the following:</span><span class="sxs-lookup"><span data-stu-id="a317a-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="a317a-139">Log in at the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a317a-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a317a-140">In the Settings window, click Streaming endpoints.</span><span class="sxs-lookup"><span data-stu-id="a317a-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="a317a-141">Click the default streaming endpoint.</span><span class="sxs-lookup"><span data-stu-id="a317a-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="a317a-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span><span class="sxs-lookup"><span data-stu-id="a317a-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="a317a-143">Click the Start icon.</span><span class="sxs-lookup"><span data-stu-id="a317a-143">Click the Start icon.</span></span>
5. <span data-ttu-id="a317a-144">Click the Save button to save your changes.</span><span class="sxs-lookup"><span data-stu-id="a317a-144">Click the Save button to save your changes.</span></span>

## <a id="connect"></a><span data-ttu-id="a317a-145">Connect to the Media Services account with REST API</span><span class="sxs-lookup"><span data-stu-id="a317a-145">Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="a317a-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a317a-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

## <a id="upload"></a><span data-ttu-id="a317a-147">Create a new asset and upload a video file with REST API</span><span class="sxs-lookup"><span data-stu-id="a317a-147">Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="a317a-148">In Media Services, you upload your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-148">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="a317a-149">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="a317a-149">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="a317a-150">One of the values that you have to provide when creating an asset is asset creation options.</span><span class="sxs-lookup"><span data-stu-id="a317a-150">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="a317a-151">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span><span class="sxs-lookup"><span data-stu-id="a317a-151">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="a317a-152">A valid value is one of the values from the list below, not a combination of values from this list:</span><span class="sxs-lookup"><span data-stu-id="a317a-152">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="a317a-153">**None** = **0** - No encryption is used.</span><span class="sxs-lookup"><span data-stu-id="a317a-153">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="a317a-154">When using this option your content is not protected in transit or at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="a317a-154">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="a317a-155">If you plan to deliver an MP4 using progressive download, use this option.</span><span class="sxs-lookup"><span data-stu-id="a317a-155">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="a317a-156">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="a317a-156">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="a317a-157">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-157">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="a317a-158">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span><span class="sxs-lookup"><span data-stu-id="a317a-158">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="a317a-159">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="a317a-159">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="a317a-160">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span><span class="sxs-lookup"><span data-stu-id="a317a-160">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="a317a-161">The files must have been encoded and encrypted by Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="a317a-161">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="a317a-162">Create an asset</span><span class="sxs-lookup"><span data-stu-id="a317a-162">Create an asset</span></span>
<span data-ttu-id="a317a-163">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span><span class="sxs-lookup"><span data-stu-id="a317a-163">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="a317a-164">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span><span class="sxs-lookup"><span data-stu-id="a317a-164">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="a317a-165">The following example shows how to create an asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-165">The following example shows how to create an asset.</span></span>

<span data-ttu-id="a317a-166">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-166">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="a317a-167">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-167">**HTTP Response**</span></span>

<span data-ttu-id="a317a-168">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-168">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="a317a-169">Create an AssetFile</span><span class="sxs-lookup"><span data-stu-id="a317a-169">Create an AssetFile</span></span>
<span data-ttu-id="a317a-170">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span><span class="sxs-lookup"><span data-stu-id="a317a-170">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="a317a-171">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="a317a-171">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="a317a-172">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span><span class="sxs-lookup"><span data-stu-id="a317a-172">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="a317a-173">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span><span class="sxs-lookup"><span data-stu-id="a317a-173">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="a317a-174">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-174">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="a317a-175">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-175">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="a317a-176">Creating the AccessPolicy with write permission</span><span class="sxs-lookup"><span data-stu-id="a317a-176">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="a317a-177">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-177">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="a317a-178">To do that, POST an HTTP request to the AccessPolicies entity set.</span><span class="sxs-lookup"><span data-stu-id="a317a-178">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="a317a-179">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span><span class="sxs-lookup"><span data-stu-id="a317a-179">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="a317a-180">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="a317a-180">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="a317a-181">The following example shows how to create an AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="a317a-181">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="a317a-182">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-182">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="a317a-183">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-183">**HTTP Response**</span></span>

<span data-ttu-id="a317a-184">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-184">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-the-upload-url"></a><span data-ttu-id="a317a-185">Get the Upload URL</span><span class="sxs-lookup"><span data-stu-id="a317a-185">Get the Upload URL</span></span>

<span data-ttu-id="a317a-186">To receive the actual upload URL, create a SAS Locator.</span><span class="sxs-lookup"><span data-stu-id="a317a-186">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="a317a-187">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-187">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="a317a-188">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span><span class="sxs-lookup"><span data-stu-id="a317a-188">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="a317a-189">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span><span class="sxs-lookup"><span data-stu-id="a317a-189">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="a317a-190">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="a317a-190">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="a317a-191">A SAS URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="a317a-191">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="a317a-192">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="a317a-192">Some considerations apply:</span></span>

* <span data-ttu-id="a317a-193">You cannot have more than five unique Locators associated with a given Asset at one time.</span><span class="sxs-lookup"><span data-stu-id="a317a-193">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> 
* <span data-ttu-id="a317a-194">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span><span class="sxs-lookup"><span data-stu-id="a317a-194">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="a317a-195">This is because there may be clock skew between your client machine and Media Services.</span><span class="sxs-lookup"><span data-stu-id="a317a-195">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="a317a-196">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="a317a-196">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="a317a-197">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span><span class="sxs-lookup"><span data-stu-id="a317a-197">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="a317a-198">This issue applies to both [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) and Origin Locators.</span><span class="sxs-lookup"><span data-stu-id="a317a-198">This issue applies to both [SAS URL](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1) and Origin Locators.</span></span>

<span data-ttu-id="a317a-199">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span><span class="sxs-lookup"><span data-stu-id="a317a-199">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="a317a-200">The **Path** property returned contains the URL that you must use to upload your file.</span><span class="sxs-lookup"><span data-stu-id="a317a-200">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="a317a-201">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-201">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="a317a-202">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-202">**HTTP Response**</span></span>

<span data-ttu-id="a317a-203">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-203">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="a317a-204">Upload a file into a blob storage container</span><span class="sxs-lookup"><span data-stu-id="a317a-204">Upload a file into a blob storage container</span></span>
<span data-ttu-id="a317a-205">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span><span class="sxs-lookup"><span data-stu-id="a317a-205">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="a317a-206">You must upload the files as block blobs.</span><span class="sxs-lookup"><span data-stu-id="a317a-206">You must upload the files as block blobs.</span></span> <span data-ttu-id="a317a-207">Page blobs are not supported by Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="a317a-207">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="a317a-208">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a317a-208">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="a317a-209">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="a317a-209">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="a317a-210">.</span><span class="sxs-lookup"><span data-stu-id="a317a-210">.</span></span> <span data-ttu-id="a317a-211">.</span><span class="sxs-lookup"><span data-stu-id="a317a-211">.</span></span> <span data-ttu-id="a317a-212">.</span><span class="sxs-lookup"><span data-stu-id="a317a-212">.</span></span>
>
>

<span data-ttu-id="a317a-213">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="a317a-213">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="a317a-214">Update the AssetFile</span><span class="sxs-lookup"><span data-stu-id="a317a-214">Update the AssetFile</span></span>
<span data-ttu-id="a317a-215">Now that you've uploaded your file, update the FileAsset size (and other) information.</span><span class="sxs-lookup"><span data-stu-id="a317a-215">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="a317a-216">For example:</span><span class="sxs-lookup"><span data-stu-id="a317a-216">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="a317a-217">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-217">**HTTP Response**</span></span>

<span data-ttu-id="a317a-218">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-218">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="a317a-219">Delete the Locator and AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="a317a-219">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="a317a-220">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-220">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a317a-221">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-221">**HTTP Response**</span></span>

<span data-ttu-id="a317a-222">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-222">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="a317a-223">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-223">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="a317a-224">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-224">**HTTP Response**</span></span>

<span data-ttu-id="a317a-225">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-225">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a><span data-ttu-id="a317a-226">Encode the source file into a set of adaptive bitrate MP4 files</span><span class="sxs-lookup"><span data-stu-id="a317a-226">Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="a317a-227">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span><span class="sxs-lookup"><span data-stu-id="a317a-227">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="a317a-228">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span><span class="sxs-lookup"><span data-stu-id="a317a-228">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="a317a-229">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](https://docs.microsoft.com/rest/api/media/operations/job), [Task](https://docs.microsoft.com/rest/api/media/operations/task) descriptions).</span><span class="sxs-lookup"><span data-stu-id="a317a-229">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](https://docs.microsoft.com/rest/api/media/operations/job), [Task](https://docs.microsoft.com/rest/api/media/operations/task) descriptions).</span></span>

<span data-ttu-id="a317a-230">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span><span class="sxs-lookup"><span data-stu-id="a317a-230">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="a317a-231">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a317a-231">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="a317a-232">The following section shows how to create a job that contains one encoding task.</span><span class="sxs-lookup"><span data-stu-id="a317a-232">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="a317a-233">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="a317a-233">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="a317a-234">The section also shows how to monitor the job processing progress.</span><span class="sxs-lookup"><span data-stu-id="a317a-234">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="a317a-235">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span><span class="sxs-lookup"><span data-stu-id="a317a-235">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="a317a-236">Get a media processor</span><span class="sxs-lookup"><span data-stu-id="a317a-236">Get a media processor</span></span>
<span data-ttu-id="a317a-237">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span><span class="sxs-lookup"><span data-stu-id="a317a-237">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="a317a-238">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="a317a-238">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="a317a-239">The following code requests the encoder's id.</span><span class="sxs-lookup"><span data-stu-id="a317a-239">The following code requests the encoder's id.</span></span>

<span data-ttu-id="a317a-240">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-240">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a317a-241">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-241">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="a317a-242">Create a job</span><span class="sxs-lookup"><span data-stu-id="a317a-242">Create a job</span></span>
<span data-ttu-id="a317a-243">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span><span class="sxs-lookup"><span data-stu-id="a317a-243">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="a317a-244">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span><span class="sxs-lookup"><span data-stu-id="a317a-244">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="a317a-245">The Media Services SDK uses batch processing.</span><span class="sxs-lookup"><span data-stu-id="a317a-245">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="a317a-246">However, for the readability of the code examples in this article, tasks are defined inline.</span><span class="sxs-lookup"><span data-stu-id="a317a-246">However, for the readability of the code examples in this article, tasks are defined inline.</span></span> <span data-ttu-id="a317a-247">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="a317a-247">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="a317a-248">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span><span class="sxs-lookup"><span data-stu-id="a317a-248">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="a317a-249">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span><span class="sxs-lookup"><span data-stu-id="a317a-249">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="a317a-250">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-250">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="a317a-251">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-251">**HTTP Response**</span></span>

<span data-ttu-id="a317a-252">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-252">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="a317a-253">There are a few important things to note in any Job request:</span><span class="sxs-lookup"><span data-stu-id="a317a-253">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="a317a-254">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span><span class="sxs-lookup"><span data-stu-id="a317a-254">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="a317a-255">The Task article contains the XML Schema Definition for the XML.</span><span class="sxs-lookup"><span data-stu-id="a317a-255">The Task article contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="a317a-256">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="a317a-256">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="a317a-257">A task can have multiple output assets.</span><span class="sxs-lookup"><span data-stu-id="a317a-257">A task can have multiple output assets.</span></span> <span data-ttu-id="a317a-258">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span><span class="sxs-lookup"><span data-stu-id="a317a-258">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="a317a-259">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span><span class="sxs-lookup"><span data-stu-id="a317a-259">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="a317a-260">Tasks must not form a cycle.</span><span class="sxs-lookup"><span data-stu-id="a317a-260">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="a317a-261">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-261">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="a317a-262">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span><span class="sxs-lookup"><span data-stu-id="a317a-262">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="a317a-263">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span><span class="sxs-lookup"><span data-stu-id="a317a-263">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="a317a-264">InputMediaAssets maps to one or more Assets you have created in Media Services.</span><span class="sxs-lookup"><span data-stu-id="a317a-264">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="a317a-265">OutputMediaAssets are created by the system.</span><span class="sxs-lookup"><span data-stu-id="a317a-265">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="a317a-266">They do not reference an existing asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-266">They do not reference an existing asset.</span></span>
* <span data-ttu-id="a317a-267">OutputMediaAssets can be named using the assetName attribute.</span><span class="sxs-lookup"><span data-stu-id="a317a-267">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="a317a-268">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span><span class="sxs-lookup"><span data-stu-id="a317a-268">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="a317a-269">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span><span class="sxs-lookup"><span data-stu-id="a317a-269">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="a317a-270">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span><span class="sxs-lookup"><span data-stu-id="a317a-270">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="a317a-271">The following example shows how to set the assetName attribute:</span><span class="sxs-lookup"><span data-stu-id="a317a-271">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="a317a-272">To enable task chaining:</span><span class="sxs-lookup"><span data-stu-id="a317a-272">To enable task chaining:</span></span>

  * <span data-ttu-id="a317a-273">A job must have at least two tasks</span><span class="sxs-lookup"><span data-stu-id="a317a-273">A job must have at least two tasks</span></span>
  * <span data-ttu-id="a317a-274">There must be at least one task whose input is output of another task in the job.</span><span class="sxs-lookup"><span data-stu-id="a317a-274">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="a317a-275">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="a317a-275">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="a317a-276">Monitor Processing Progress</span><span class="sxs-lookup"><span data-stu-id="a317a-276">Monitor Processing Progress</span></span>
<span data-ttu-id="a317a-277">You can retrieve the Job status by using the State property, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a317a-277">You can retrieve the Job status by using the State property, as shown in the following example:</span></span>

<span data-ttu-id="a317a-278">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-278">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN>
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="a317a-279">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-279">**HTTP Response**</span></span>

<span data-ttu-id="a317a-280">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-280">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="a317a-281">Cancel a job</span><span class="sxs-lookup"><span data-stu-id="a317a-281">Cancel a job</span></span>
<span data-ttu-id="a317a-282">Media Services allows you to cancel running jobs through the CancelJob function.</span><span class="sxs-lookup"><span data-stu-id="a317a-282">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="a317a-283">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span><span class="sxs-lookup"><span data-stu-id="a317a-283">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="a317a-284">The following example shows how to call CancelJob.</span><span class="sxs-lookup"><span data-stu-id="a317a-284">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="a317a-285">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-285">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer <ENCODED JWT TOKEN>
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="a317a-286">If successful, a 204 response code is returned with no message body.</span><span class="sxs-lookup"><span data-stu-id="a317a-286">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="a317a-287">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span><span class="sxs-lookup"><span data-stu-id="a317a-287">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="a317a-288">Get the output asset</span><span class="sxs-lookup"><span data-stu-id="a317a-288">Get the output asset</span></span>
<span data-ttu-id="a317a-289">The following code shows how to request the output asset Id.</span><span class="sxs-lookup"><span data-stu-id="a317a-289">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="a317a-290">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a317a-290">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <ENCODED JWT TOKEN>
    x-ms-version: 2.17
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="a317a-291">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a317a-291">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }

## <a id="publish_get_urls"></a><span data-ttu-id="a317a-292">Publish the asset and get streaming and progressive download URLs with REST API</span><span class="sxs-lookup"><span data-stu-id="a317a-292">Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="a317a-293">To stream or download an asset, you first need to "publish" it by creating a locator.</span><span class="sxs-lookup"><span data-stu-id="a317a-293">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="a317a-294">Locators provide access to files contained in the asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-294">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="a317a-295">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span><span class="sxs-lookup"><span data-stu-id="a317a-295">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> 

<span data-ttu-id="a317a-296">Once you create the locators, you can build the URLs that are used to stream or download your files.</span><span class="sxs-lookup"><span data-stu-id="a317a-296">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="a317a-297">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span><span class="sxs-lookup"><span data-stu-id="a317a-297">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a317a-298">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="a317a-298">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="a317a-299">A streaming URL for Smooth Streaming has the following format:</span><span class="sxs-lookup"><span data-stu-id="a317a-299">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="a317a-300">A streaming URL for HLS has the following format:</span><span class="sxs-lookup"><span data-stu-id="a317a-300">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="a317a-301">A streaming URL for MPEG DASH has the following format:</span><span class="sxs-lookup"><span data-stu-id="a317a-301">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="a317a-302">A SAS URL used to download files has the following format:</span><span class="sxs-lookup"><span data-stu-id="a317a-302">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="a317a-303">This section shows how to perform the following tasks necessary to "publish" your assets.</span><span class="sxs-lookup"><span data-stu-id="a317a-303">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="a317a-304">Creating the AccessPolicy with read permission</span><span class="sxs-lookup"><span data-stu-id="a317a-304">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="a317a-305">Creating a SAS URL for downloading content</span><span class="sxs-lookup"><span data-stu-id="a317a-305">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="a317a-306">Creating an origin URL for streaming content</span><span class="sxs-lookup"><span data-stu-id="a317a-306">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="a317a-307">Creating the AccessPolicy with read permission</span><span class="sxs-lookup"><span data-stu-id="a317a-307">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="a317a-308">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span><span class="sxs-lookup"><span data-stu-id="a317a-308">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="a317a-309">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="a317a-309">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="a317a-310">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-310">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN>
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="a317a-311">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span><span class="sxs-lookup"><span data-stu-id="a317a-311">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="a317a-312">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span><span class="sxs-lookup"><span data-stu-id="a317a-312">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="a317a-313">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span><span class="sxs-lookup"><span data-stu-id="a317a-313">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="a317a-314">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span><span class="sxs-lookup"><span data-stu-id="a317a-314">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="a317a-315">This action is necessary because there may be clock skew between the client and Media Services.</span><span class="sxs-lookup"><span data-stu-id="a317a-315">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="a317a-316">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="a317a-316">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="a317a-317">Creating a SAS URL for downloading content</span><span class="sxs-lookup"><span data-stu-id="a317a-317">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="a317a-318">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span><span class="sxs-lookup"><span data-stu-id="a317a-318">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="a317a-319">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span><span class="sxs-lookup"><span data-stu-id="a317a-319">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN>
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="a317a-320">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-320">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }

<span data-ttu-id="a317a-321">The returned **Path** property contains the SAS URL.</span><span class="sxs-lookup"><span data-stu-id="a317a-321">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="a317a-322">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span><span class="sxs-lookup"><span data-stu-id="a317a-322">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="a317a-323">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span><span class="sxs-lookup"><span data-stu-id="a317a-323">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="a317a-324">Also, SAS URL Locators cannot be updated after they have been created.</span><span class="sxs-lookup"><span data-stu-id="a317a-324">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="a317a-325">For example, you cannot reuse the same Locator with an updated StartTime value.</span><span class="sxs-lookup"><span data-stu-id="a317a-325">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="a317a-326">This is because of the way SAS URLs are created.</span><span class="sxs-lookup"><span data-stu-id="a317a-326">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="a317a-327">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span><span class="sxs-lookup"><span data-stu-id="a317a-327">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="a317a-328">Download files</span><span class="sxs-lookup"><span data-stu-id="a317a-328">Download files</span></span>
<span data-ttu-id="a317a-329">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span><span class="sxs-lookup"><span data-stu-id="a317a-329">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="a317a-330">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a317a-330">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="a317a-331">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="a317a-331">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="a317a-332">.</span><span class="sxs-lookup"><span data-stu-id="a317a-332">.</span></span> <span data-ttu-id="a317a-333">.</span><span class="sxs-lookup"><span data-stu-id="a317a-333">.</span></span> <span data-ttu-id="a317a-334">.</span><span class="sxs-lookup"><span data-stu-id="a317a-334">.</span></span>
>
>

<span data-ttu-id="a317a-335">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="a317a-335">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="a317a-336">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span><span class="sxs-lookup"><span data-stu-id="a317a-336">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="a317a-337">For example:</span><span class="sxs-lookup"><span data-stu-id="a317a-337">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="a317a-338">Creating a streaming URL for streaming content</span><span class="sxs-lookup"><span data-stu-id="a317a-338">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="a317a-339">The following code shows how to create a streaming URL Locator:</span><span class="sxs-lookup"><span data-stu-id="a317a-339">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.17
    Authorization: Bearer <ENCODED JWT TOKEN>
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="a317a-340">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a317a-340">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="a317a-341">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span><span class="sxs-lookup"><span data-stu-id="a317a-341">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="a317a-342">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span><span class="sxs-lookup"><span data-stu-id="a317a-342">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="a317a-343">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span><span class="sxs-lookup"><span data-stu-id="a317a-343">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a><span data-ttu-id="a317a-344">Play your content</span><span class="sxs-lookup"><span data-stu-id="a317a-344">Play your content</span></span>
<span data-ttu-id="a317a-345">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="a317a-345">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="a317a-346">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="a317a-346">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="a317a-347">Next Steps: Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="a317a-347">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a317a-348">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="a317a-348">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
