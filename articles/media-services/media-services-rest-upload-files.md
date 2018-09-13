---
title: Upload files into a Media Services account using REST  | Microsoft Docs
description: Learn how to get media content into Media Services by creating and uploading assets.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: juliako
ms.openlocfilehash: c0ea95ed12a704116e8cdff257dacd7768b45708
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553280"
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="1ad50-103">Upload files into a Media Services account using REST</span><span class="sxs-lookup"><span data-stu-id="1ad50-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="1ad50-107">In Media Services, you upload your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="1ad50-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="1ad50-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="1ad50-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> The following considerations apply:
> 
> * Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed. The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]". Also, there can only be one '.' for the file name extension.
> * The length of the name should not be greater than 260 characters.
> * There is a limit to the maximum file size supported for processing in Media Services. Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.
> 

<span data-ttu-id="1ad50-116">The basic workflow for uploading Assets is divided into the following sections:</span><span class="sxs-lookup"><span data-stu-id="1ad50-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="1ad50-117">Create an Asset</span><span class="sxs-lookup"><span data-stu-id="1ad50-117">Create an Asset</span></span>
* <span data-ttu-id="1ad50-118">Encrypt an Asset (Optional)</span><span class="sxs-lookup"><span data-stu-id="1ad50-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="1ad50-119">Upload a file to blob storage</span><span class="sxs-lookup"><span data-stu-id="1ad50-119">Upload a file to blob storage</span></span>

<span data-ttu-id="1ad50-120">AMS also enables you to upload assets in bulk.</span><span class="sxs-lookup"><span data-stu-id="1ad50-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="1ad50-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span><span class="sxs-lookup"><span data-stu-id="1ad50-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="1ad50-122">Upload assets</span><span class="sxs-lookup"><span data-stu-id="1ad50-122">Upload assets</span></span>
### <a name="create-an-asset"></a><span data-ttu-id="1ad50-123">Create an asset</span><span class="sxs-lookup"><span data-stu-id="1ad50-123">Create an asset</span></span>
> [!NOTE]
> When working with the Media Services REST API, the following considerations apply:
> 
> When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests. For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).
> 
> After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI. You must make subsequent calls to the new URI as described in [Connecting to Media Services using REST API](media-services-rest-connect-programmatically.md). 
> 
> 

<span data-ttu-id="1ad50-129">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span><span class="sxs-lookup"><span data-stu-id="1ad50-129">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="1ad50-130">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span><span class="sxs-lookup"><span data-stu-id="1ad50-130">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="1ad50-131">One of the properties that you can specify when creating an asset is **Options**.</span><span class="sxs-lookup"><span data-stu-id="1ad50-131">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="1ad50-132">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span><span class="sxs-lookup"><span data-stu-id="1ad50-132">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="1ad50-133">A valid value is one of the values from the list below, not a combination of values.</span><span class="sxs-lookup"><span data-stu-id="1ad50-133">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="1ad50-134">**None** = **0**: No encryption will be used.</span><span class="sxs-lookup"><span data-stu-id="1ad50-134">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="1ad50-135">This is the default value.</span><span class="sxs-lookup"><span data-stu-id="1ad50-135">This is the default value.</span></span> <span data-ttu-id="1ad50-136">Note that when using this option your content is not protected in transit or at rest in storage.</span><span class="sxs-lookup"><span data-stu-id="1ad50-136">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="1ad50-137">If you plan to deliver an MP4 using progressive download, use this option.</span><span class="sxs-lookup"><span data-stu-id="1ad50-137">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="1ad50-138">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span><span class="sxs-lookup"><span data-stu-id="1ad50-138">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="1ad50-139">If your asset is storage encrypted, you must configure asset delivery policy.</span><span class="sxs-lookup"><span data-stu-id="1ad50-139">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="1ad50-140">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="1ad50-140">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="1ad50-141">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span><span class="sxs-lookup"><span data-stu-id="1ad50-141">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="1ad50-142">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span><span class="sxs-lookup"><span data-stu-id="1ad50-142">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="1ad50-143">Note that the files must have been encoded and encrypted by Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="1ad50-143">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md). Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption. Do it by using the **MERGE** HTTP request. 
> 
> 

<span data-ttu-id="1ad50-147">The following example shows how to create an asset.</span><span class="sxs-lookup"><span data-stu-id="1ad50-147">The following example shows how to create an asset.</span></span>

<span data-ttu-id="1ad50-148">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-148">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}


<span data-ttu-id="1ad50-149">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-149">**HTTP Response**</span></span>

<span data-ttu-id="1ad50-150">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="1ad50-150">If successful, the following is returned:</span></span>

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="1ad50-151">Create an AssetFile</span><span class="sxs-lookup"><span data-stu-id="1ad50-151">Create an AssetFile</span></span>
<span data-ttu-id="1ad50-152">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span><span class="sxs-lookup"><span data-stu-id="1ad50-152">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="1ad50-153">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span><span class="sxs-lookup"><span data-stu-id="1ad50-153">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="1ad50-154">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span><span class="sxs-lookup"><span data-stu-id="1ad50-154">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="1ad50-155">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span><span class="sxs-lookup"><span data-stu-id="1ad50-155">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="1ad50-156">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span><span class="sxs-lookup"><span data-stu-id="1ad50-156">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="1ad50-157">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span><span class="sxs-lookup"><span data-stu-id="1ad50-157">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="1ad50-158">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-158">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="1ad50-159">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-159">**HTTP Response**</span></span>

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


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="1ad50-160">Creating the AccessPolicy with write permission.</span><span class="sxs-lookup"><span data-stu-id="1ad50-160">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
>There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy). You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies). For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.

<span data-ttu-id="1ad50-164">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span><span class="sxs-lookup"><span data-stu-id="1ad50-164">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="1ad50-165">To do that, POST an HTTP request to the AccessPolicies entity set.</span><span class="sxs-lookup"><span data-stu-id="1ad50-165">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="1ad50-166">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span><span class="sxs-lookup"><span data-stu-id="1ad50-166">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="1ad50-167">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="1ad50-167">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="1ad50-168">The following example shows how to create an AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="1ad50-168">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="1ad50-169">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-169">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="1ad50-170">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-170">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="1ad50-171">Get the Upload URL</span><span class="sxs-lookup"><span data-stu-id="1ad50-171">Get the Upload URL</span></span>
<span data-ttu-id="1ad50-172">To receive the actual upload URL, create a SAS Locator.</span><span class="sxs-lookup"><span data-stu-id="1ad50-172">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="1ad50-173">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span><span class="sxs-lookup"><span data-stu-id="1ad50-173">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="1ad50-174">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span><span class="sxs-lookup"><span data-stu-id="1ad50-174">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="1ad50-175">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span><span class="sxs-lookup"><span data-stu-id="1ad50-175">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="1ad50-176">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="1ad50-176">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="1ad50-177">A SAS URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="1ad50-177">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="1ad50-178">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="1ad50-178">Some considerations apply:</span></span>

* <span data-ttu-id="1ad50-179">You cannot have more than five unique Locators associated with a given Asset at one time.</span><span class="sxs-lookup"><span data-stu-id="1ad50-179">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="1ad50-180">For more information, see Locator.</span><span class="sxs-lookup"><span data-stu-id="1ad50-180">For more information, see Locator.</span></span>
* <span data-ttu-id="1ad50-181">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span><span class="sxs-lookup"><span data-stu-id="1ad50-181">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="1ad50-182">This is because there may be clock skew between your client machine and Media Services.</span><span class="sxs-lookup"><span data-stu-id="1ad50-182">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="1ad50-183">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="1ad50-183">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="1ad50-184">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span><span class="sxs-lookup"><span data-stu-id="1ad50-184">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="1ad50-185">This issue applies to both SAS URL and Origin Locators.</span><span class="sxs-lookup"><span data-stu-id="1ad50-185">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="1ad50-186">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span><span class="sxs-lookup"><span data-stu-id="1ad50-186">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="1ad50-187">The **Path** property returned contains the URL that you must use to upload your file.</span><span class="sxs-lookup"><span data-stu-id="1ad50-187">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="1ad50-188">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-188">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="1ad50-189">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-189">**HTTP Response**</span></span>

<span data-ttu-id="1ad50-190">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="1ad50-190">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="1ad50-191">Upload a file into a blob storage container</span><span class="sxs-lookup"><span data-stu-id="1ad50-191">Upload a file into a blob storage container</span></span>
<span data-ttu-id="1ad50-192">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span><span class="sxs-lookup"><span data-stu-id="1ad50-192">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="1ad50-193">You must upload the files as block blobs.</span><span class="sxs-lookup"><span data-stu-id="1ad50-193">You must upload the files as block blobs.</span></span> <span data-ttu-id="1ad50-194">Page blobs are not supported by Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1ad50-194">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section. For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

<span data-ttu-id="1ad50-200">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="1ad50-200">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="1ad50-201">Update the AssetFile</span><span class="sxs-lookup"><span data-stu-id="1ad50-201">Update the AssetFile</span></span>
<span data-ttu-id="1ad50-202">Now that you've uploaded your file, update the FileAsset size (and other) information.</span><span class="sxs-lookup"><span data-stu-id="1ad50-202">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="1ad50-203">For example:</span><span class="sxs-lookup"><span data-stu-id="1ad50-203">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="1ad50-204">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-204">**HTTP Response**</span></span>

<span data-ttu-id="1ad50-205">If successful, the following is returned: HTTP/1.1 204 No Content</span><span class="sxs-lookup"><span data-stu-id="1ad50-205">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="1ad50-206">Delete the Locator and AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="1ad50-206">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="1ad50-207">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-207">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="1ad50-208">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-208">**HTTP Response**</span></span>

<span data-ttu-id="1ad50-209">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="1ad50-209">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="1ad50-210">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-210">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="1ad50-211">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-211">**HTTP Response**</span></span>

<span data-ttu-id="1ad50-212">If successful, the following is returned:</span><span class="sxs-lookup"><span data-stu-id="1ad50-212">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a><span data-ttu-id="1ad50-213">Upload assets in bulk</span><span class="sxs-lookup"><span data-stu-id="1ad50-213">Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="1ad50-214">Create the IngestManifest</span><span class="sxs-lookup"><span data-stu-id="1ad50-214">Create the IngestManifest</span></span>
<span data-ttu-id="1ad50-215">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span><span class="sxs-lookup"><span data-stu-id="1ad50-215">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="1ad50-216">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="1ad50-216">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="1ad50-217">Create assets</span><span class="sxs-lookup"><span data-stu-id="1ad50-217">Create assets</span></span>
<span data-ttu-id="1ad50-218">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span><span class="sxs-lookup"><span data-stu-id="1ad50-218">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="1ad50-219">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span><span class="sxs-lookup"><span data-stu-id="1ad50-219">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="1ad50-220">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span><span class="sxs-lookup"><span data-stu-id="1ad50-220">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="1ad50-221">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-221">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="1ad50-222">Create the IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="1ad50-222">Create the IngestManifestAssets</span></span>
<span data-ttu-id="1ad50-223">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span><span class="sxs-lookup"><span data-stu-id="1ad50-223">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="1ad50-224">The basically link the asset to the manifest.</span><span class="sxs-lookup"><span data-stu-id="1ad50-224">The basically link the asset to the manifest.</span></span> <span data-ttu-id="1ad50-225">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="1ad50-225">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="1ad50-226">Once these files are uploaded, the asset is completed.</span><span class="sxs-lookup"><span data-stu-id="1ad50-226">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="1ad50-227">You can create a new IngestManifestAsset with a HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="1ad50-227">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="1ad50-228">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span><span class="sxs-lookup"><span data-stu-id="1ad50-228">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="1ad50-229">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-229">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="1ad50-230">Create the IngestManifestFiles for each Asset</span><span class="sxs-lookup"><span data-stu-id="1ad50-230">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="1ad50-231">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span><span class="sxs-lookup"><span data-stu-id="1ad50-231">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="1ad50-232">Encryption related properties are not required unless the asset is using an encryption option.</span><span class="sxs-lookup"><span data-stu-id="1ad50-232">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="1ad50-233">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span><span class="sxs-lookup"><span data-stu-id="1ad50-233">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="1ad50-234">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-234">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="1ad50-235">Upload the Files to Blob Storage</span><span class="sxs-lookup"><span data-stu-id="1ad50-235">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="1ad50-236">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="1ad50-236">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="1ad50-237">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="1ad50-237">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="1ad50-238">Monitor Bulk Ingest Progress</span><span class="sxs-lookup"><span data-stu-id="1ad50-238">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="1ad50-239">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="1ad50-239">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="1ad50-240">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="1ad50-240">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="1ad50-241">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span><span class="sxs-lookup"><span data-stu-id="1ad50-241">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="1ad50-242">Create ContentKeys used for encryption</span><span class="sxs-lookup"><span data-stu-id="1ad50-242">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="1ad50-243">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span><span class="sxs-lookup"><span data-stu-id="1ad50-243">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="1ad50-244">For storage encryption, the following properties should be included in the request body.</span><span class="sxs-lookup"><span data-stu-id="1ad50-244">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="1ad50-245">Request body property</span><span class="sxs-lookup"><span data-stu-id="1ad50-245">Request body property</span></span> | <span data-ttu-id="1ad50-246">Description</span><span class="sxs-lookup"><span data-stu-id="1ad50-246">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1ad50-247">Id</span><span class="sxs-lookup"><span data-stu-id="1ad50-247">Id</span></span> |<span data-ttu-id="1ad50-248">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span><span class="sxs-lookup"><span data-stu-id="1ad50-248">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="1ad50-249">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="1ad50-249">ContentKeyType</span></span> |<span data-ttu-id="1ad50-250">This is the content key type as an integer for this content key.</span><span class="sxs-lookup"><span data-stu-id="1ad50-250">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="1ad50-251">We pass the value 1 for storage encryption.</span><span class="sxs-lookup"><span data-stu-id="1ad50-251">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="1ad50-252">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="1ad50-252">EncryptedContentKey</span></span> |<span data-ttu-id="1ad50-253">We create a new content key value which is a 256-bit (32 byte) value.</span><span class="sxs-lookup"><span data-stu-id="1ad50-253">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="1ad50-254">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span><span class="sxs-lookup"><span data-stu-id="1ad50-254">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="1ad50-255">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="1ad50-255">ProtectionKeyId</span></span> |<span data-ttu-id="1ad50-256">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span><span class="sxs-lookup"><span data-stu-id="1ad50-256">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="1ad50-257">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="1ad50-257">ProtectionKeyType</span></span> |<span data-ttu-id="1ad50-258">This is the encryption type for the protection key that was used to encrypt the content key.</span><span class="sxs-lookup"><span data-stu-id="1ad50-258">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="1ad50-259">This value is StorageEncryption(1) for our example.</span><span class="sxs-lookup"><span data-stu-id="1ad50-259">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="1ad50-260">Checksum</span><span class="sxs-lookup"><span data-stu-id="1ad50-260">Checksum</span></span> |<span data-ttu-id="1ad50-261">The MD5 calculated checksum for the content key.</span><span class="sxs-lookup"><span data-stu-id="1ad50-261">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="1ad50-262">It is computed by encrypting the content Id with the content key.</span><span class="sxs-lookup"><span data-stu-id="1ad50-262">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="1ad50-263">The example code demonstrates how to calculate the checksum.</span><span class="sxs-lookup"><span data-stu-id="1ad50-263">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="1ad50-264">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-264">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="1ad50-265">Link the ContentKey to the Asset</span><span class="sxs-lookup"><span data-stu-id="1ad50-265">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="1ad50-266">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span><span class="sxs-lookup"><span data-stu-id="1ad50-266">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="1ad50-267">The following request is an example to link the example ContentKey to the example asset by Id.</span><span class="sxs-lookup"><span data-stu-id="1ad50-267">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="1ad50-268">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-268">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="1ad50-269">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="1ad50-269">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="1ad50-270">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ad50-270">Next steps</span></span>

<span data-ttu-id="1ad50-271">You can now encode your uploaded assets.</span><span class="sxs-lookup"><span data-stu-id="1ad50-271">You can now encode your uploaded assets.</span></span> <span data-ttu-id="1ad50-272">For more information, see [Encode assets](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="1ad50-272">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="1ad50-273">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span><span class="sxs-lookup"><span data-stu-id="1ad50-273">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="1ad50-274">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="1ad50-274">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1ad50-275">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="1ad50-275">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1ad50-276">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="1ad50-276">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

