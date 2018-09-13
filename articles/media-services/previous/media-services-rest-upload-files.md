---
title: Upload files into an Azure Media Services account using REST  | Microsoft Docs
description: Learn how to get media content into Media Services by creating and uploading assets.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: juliako
ms.openlocfilehash: 1e51439ec0a6c6658b28ae0f02ff3eaeb4c551e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855757"
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="b0072-103">Upload files into a Media Services account using REST</span><span class="sxs-lookup"><span data-stu-id="b0072-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 

<span data-ttu-id="b0072-107">In Media Services, you upload your digital files into an asset.</span><span class="sxs-lookup"><span data-stu-id="b0072-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="b0072-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span><span class="sxs-lookup"><span data-stu-id="b0072-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="b0072-109">In this tutorial, you learn how to upload a file and other operation associated with it:</span><span class="sxs-lookup"><span data-stu-id="b0072-109">In this tutorial, you learn how to upload a file and other operation associated with it:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b0072-110">Set up Postman for all the upload operations</span><span class="sxs-lookup"><span data-stu-id="b0072-110">Set up Postman for all the upload operations</span></span>
> * <span data-ttu-id="b0072-111">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="b0072-111">Connect to Media Services</span></span> 
> * <span data-ttu-id="b0072-112">Create an access policy with write permission</span><span class="sxs-lookup"><span data-stu-id="b0072-112">Create an access policy with write permission</span></span>
> * <span data-ttu-id="b0072-113">Create an asset</span><span class="sxs-lookup"><span data-stu-id="b0072-113">Create an asset</span></span>
> * <span data-ttu-id="b0072-114">Create a SAS locator and create the upload URL</span><span class="sxs-lookup"><span data-stu-id="b0072-114">Create a SAS locator and create the upload URL</span></span>
> * <span data-ttu-id="b0072-115">Upload a file to blob storage using the upload URL</span><span class="sxs-lookup"><span data-stu-id="b0072-115">Upload a file to blob storage using the upload URL</span></span>
> * <span data-ttu-id="b0072-116">Create a metadata in the asset for the media file you uploaded</span><span class="sxs-lookup"><span data-stu-id="b0072-116">Create a metadata in the asset for the media file you uploaded</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0072-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0072-117">Prerequisites</span></span>

- <span data-ttu-id="b0072-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="b0072-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
- <span data-ttu-id="b0072-119">[Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-119">[Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="b0072-120">Review the [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md) article.</span><span class="sxs-lookup"><span data-stu-id="b0072-120">Review the [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md) article.</span></span>
- <span data-ttu-id="b0072-121">Configure **Postman** as described in [Configure Postman for Media Services REST API calls](media-rest-apis-with-postman.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-121">Configure **Postman** as described in [Configure Postman for Media Services REST API calls](media-rest-apis-with-postman.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="b0072-122">Considerations</span><span class="sxs-lookup"><span data-stu-id="b0072-122">Considerations</span></span>

<span data-ttu-id="b0072-123">The following considerations apply when using Media Services REST API:</span><span class="sxs-lookup"><span data-stu-id="b0072-123">The following considerations apply when using Media Services REST API:</span></span>
 
* <span data-ttu-id="b0072-124">When accessing entities using Media Services REST API, you must set specific header fields and values in your HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="b0072-124">When accessing entities using Media Services REST API, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b0072-125">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-125">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> <br/><span data-ttu-id="b0072-126">The Postman collection used in this tutorial takes care of setting all the necessary headers.</span><span class="sxs-lookup"><span data-stu-id="b0072-126">The Postman collection used in this tutorial takes care of setting all the necessary headers.</span></span>
* <span data-ttu-id="b0072-127">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span><span class="sxs-lookup"><span data-stu-id="b0072-127">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="b0072-128">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !\*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="b0072-128">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !\*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="b0072-129">Also, there can only be one '.' for the file name extension.</span><span class="sxs-lookup"><span data-stu-id="b0072-129">Also, there can only be one '.' for the file name extension.</span></span>
* <span data-ttu-id="b0072-130">The length of the name should not be greater than 260 characters.</span><span class="sxs-lookup"><span data-stu-id="b0072-130">The length of the name should not be greater than 260 characters.</span></span>
* <span data-ttu-id="b0072-131">There is a limit to the maximum file size supported for processing in Media Services.</span><span class="sxs-lookup"><span data-stu-id="b0072-131">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="b0072-132">See [this](media-services-quotas-and-limitations.md) article for details about the file size limitation.</span><span class="sxs-lookup"><span data-stu-id="b0072-132">See [this](media-services-quotas-and-limitations.md) article for details about the file size limitation.</span></span>

## <a name="set-up-postman"></a><span data-ttu-id="b0072-133">Set up Postman</span><span class="sxs-lookup"><span data-stu-id="b0072-133">Set up Postman</span></span>

<span data-ttu-id="b0072-134">For steps on how to set up Postman for this tutorial, see [Configure Postman](media-rest-apis-with-postman.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-134">For steps on how to set up Postman for this tutorial, see [Configure Postman](media-rest-apis-with-postman.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="b0072-135">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="b0072-135">Connect to Media Services</span></span>

1. <span data-ttu-id="b0072-136">Add connection values to your environment.</span><span class="sxs-lookup"><span data-stu-id="b0072-136">Add connection values to your environment.</span></span> 

    <span data-ttu-id="b0072-137">Some variables that are part of the **MediaServices** [environment](postman-environment.md) need to be set manually before you can start executing operations defined in the [collection](postman-collection.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-137">Some variables that are part of the **MediaServices** [environment](postman-environment.md) need to be set manually before you can start executing operations defined in the [collection](postman-collection.md).</span></span>

    <span data-ttu-id="b0072-138">To get values for the first five variables, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-138">To get values for the first five variables, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    ![Upload a file](./media/media-services-rest-upload-files/postman-import-env.png)
2. <span data-ttu-id="b0072-140">Specify the value for the **MediaFileName** environment variable.</span><span class="sxs-lookup"><span data-stu-id="b0072-140">Specify the value for the **MediaFileName** environment variable.</span></span>

    <span data-ttu-id="b0072-141">Specify the file name of the media you are planning to upload.</span><span class="sxs-lookup"><span data-stu-id="b0072-141">Specify the file name of the media you are planning to upload.</span></span> <span data-ttu-id="b0072-142">In this example, we are going to upload the BigBuckBunny.mp4.</span><span class="sxs-lookup"><span data-stu-id="b0072-142">In this example, we are going to upload the BigBuckBunny.mp4.</span></span> 
3. <span data-ttu-id="b0072-143">Examine the **AzureMediaServices.postman_environment.json** file.</span><span class="sxs-lookup"><span data-stu-id="b0072-143">Examine the **AzureMediaServices.postman_environment.json** file.</span></span> <span data-ttu-id="b0072-144">You will see that almost all operations in the collection execute a "test" script.</span><span class="sxs-lookup"><span data-stu-id="b0072-144">You will see that almost all operations in the collection execute a "test" script.</span></span> <span data-ttu-id="b0072-145">The scripts take some values returned by the response and set appropriate environment variables.</span><span class="sxs-lookup"><span data-stu-id="b0072-145">The scripts take some values returned by the response and set appropriate environment variables.</span></span>

    <span data-ttu-id="b0072-146">For example, the first operation gets an access token and set it on the **AccessToken** environment variable that is used in all other operations.</span><span class="sxs-lookup"><span data-stu-id="b0072-146">For example, the first operation gets an access token and set it on the **AccessToken** environment variable that is used in all other operations.</span></span>

    ```    
    "listen": "test",
    "script": {
        "type": "text/javascript",
        "exec": [
            "var json = JSON.parse(responseBody);",
            "postman.setEnvironmentVariable(\"AccessToken\", json.access_token);"
        ]
    }
    ```
4. <span data-ttu-id="b0072-147">On the left of the **Postman** window, click on **1. Get AAD Auth token** -> **Get Azure AD Token for Service Principal**.</span><span class="sxs-lookup"><span data-stu-id="b0072-147">On the left of the **Postman** window, click on **1. Get AAD Auth token** -> **Get Azure AD Token for Service Principal**.</span></span>

    <span data-ttu-id="b0072-148">The URL portion is filled with the **AzureADSTSEndpoint** environment variable (earlier in the tutorial, you set the values of [environment variables](#configure-the-environment) that support the [collection](#configure-the-collection)).</span><span class="sxs-lookup"><span data-stu-id="b0072-148">The URL portion is filled with the **AzureADSTSEndpoint** environment variable (earlier in the tutorial, you set the values of [environment variables](#configure-the-environment) that support the [collection](#configure-the-collection)).</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postment-get-token.png)

5. <span data-ttu-id="b0072-150">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="b0072-150">Press **Send**.</span></span>

    <span data-ttu-id="b0072-151">You can see the response that contains "access_token".</span><span class="sxs-lookup"><span data-stu-id="b0072-151">You can see the response that contains "access_token".</span></span> <span data-ttu-id="b0072-152">The "test" script takes this value and sets the **AccessToken** environment variable (as described above).</span><span class="sxs-lookup"><span data-stu-id="b0072-152">The "test" script takes this value and sets the **AccessToken** environment variable (as described above).</span></span> <span data-ttu-id="b0072-153">If you examine your environment variables, you will see that this variable now contains the access token (bearer token) value that is used in the rest of the operations.</span><span class="sxs-lookup"><span data-stu-id="b0072-153">If you examine your environment variables, you will see that this variable now contains the access token (bearer token) value that is used in the rest of the operations.</span></span> 

    <span data-ttu-id="b0072-154">If the token expires go through the "Get Azure AD Token for Service Principal" step again.</span><span class="sxs-lookup"><span data-stu-id="b0072-154">If the token expires go through the "Get Azure AD Token for Service Principal" step again.</span></span> 

## <a name="create-an-access-policy-with-write-permission"></a><span data-ttu-id="b0072-155">Create an access policy with write permission</span><span class="sxs-lookup"><span data-stu-id="b0072-155">Create an access policy with write permission</span></span>

### <a name="overview"></a><span data-ttu-id="b0072-156">Overview</span><span class="sxs-lookup"><span data-stu-id="b0072-156">Overview</span></span> 

>[!NOTE]
><span data-ttu-id="b0072-157">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b0072-157">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b0072-158">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span><span class="sxs-lookup"><span data-stu-id="b0072-158">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b0072-159">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.</span><span class="sxs-lookup"><span data-stu-id="b0072-159">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) article.</span></span>

<span data-ttu-id="b0072-160">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span><span class="sxs-lookup"><span data-stu-id="b0072-160">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="b0072-161">To do that, POST an HTTP request to the AccessPolicies entity set.</span><span class="sxs-lookup"><span data-stu-id="b0072-161">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="b0072-162">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span><span class="sxs-lookup"><span data-stu-id="b0072-162">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="b0072-163">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="b0072-163">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="b0072-164">Create an access policy</span><span class="sxs-lookup"><span data-stu-id="b0072-164">Create an access policy</span></span>

1. <span data-ttu-id="b0072-165">Select **AccessPolicy** -> **Create AccessPolicy for Upload**.</span><span class="sxs-lookup"><span data-stu-id="b0072-165">Select **AccessPolicy** -> **Create AccessPolicy for Upload**.</span></span>
2. <span data-ttu-id="b0072-166">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="b0072-166">Press **Send**.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-access-policy.png)

    <span data-ttu-id="b0072-168">The "test" script gets the AccessPolicy Id and sets the appropriate environment variable.</span><span class="sxs-lookup"><span data-stu-id="b0072-168">The "test" script gets the AccessPolicy Id and sets the appropriate environment variable.</span></span>

## <a name="create-an-asset"></a><span data-ttu-id="b0072-169">Create an asset</span><span class="sxs-lookup"><span data-stu-id="b0072-169">Create an asset</span></span>

### <a name="overview"></a><span data-ttu-id="b0072-170">Overview</span><span class="sxs-lookup"><span data-stu-id="b0072-170">Overview</span></span>

<span data-ttu-id="b0072-171">An [asset](https://docs.microsoft.com/rest/api/media/operations/asset) is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span><span class="sxs-lookup"><span data-stu-id="b0072-171">An [asset](https://docs.microsoft.com/rest/api/media/operations/asset) is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="b0072-172">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span><span class="sxs-lookup"><span data-stu-id="b0072-172">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="b0072-173">One of the properties that you can add when creating an asset is **Options**.</span><span class="sxs-lookup"><span data-stu-id="b0072-173">One of the properties that you can add when creating an asset is **Options**.</span></span> <span data-ttu-id="b0072-174">You can specify one of the following encryption options: **None** (default, no encryption is used), **StorageEncrypted** (for content that has been pre-encrypted with client-side storage encryption), **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="b0072-174">You can specify one of the following encryption options: **None** (default, no encryption is used), **StorageEncrypted** (for content that has been pre-encrypted with client-side storage encryption), **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> <span data-ttu-id="b0072-175">When you have an encrypted asset, you need to configure a delivery policy.</span><span class="sxs-lookup"><span data-stu-id="b0072-175">When you have an encrypted asset, you need to configure a delivery policy.</span></span> <span data-ttu-id="b0072-176">For more information, see [Configuring asset delivery policies](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-176">For more information, see [Configuring asset delivery policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="b0072-177">If your asset is encrypted, you must create a **ContentKey** and link it to your asset as described in the following article: [How to create a ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-177">If your asset is encrypted, you must create a **ContentKey** and link it to your asset as described in the following article: [How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="b0072-178">After you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span><span class="sxs-lookup"><span data-stu-id="b0072-178">After you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="b0072-179">Do it by using the **MERGE** HTTP request.</span><span class="sxs-lookup"><span data-stu-id="b0072-179">Do it by using the **MERGE** HTTP request.</span></span> 

<span data-ttu-id="b0072-180">In this example, we are creating an unencrypted asset.</span><span class="sxs-lookup"><span data-stu-id="b0072-180">In this example, we are creating an unencrypted asset.</span></span> 

### <a name="create-an-asset"></a><span data-ttu-id="b0072-181">Create an asset</span><span class="sxs-lookup"><span data-stu-id="b0072-181">Create an asset</span></span>

1. <span data-ttu-id="b0072-182">Select **Assets** -> **Create Asset**.</span><span class="sxs-lookup"><span data-stu-id="b0072-182">Select **Assets** -> **Create Asset**.</span></span>
2. <span data-ttu-id="b0072-183">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="b0072-183">Press **Send**.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-create-asset.png)

    <span data-ttu-id="b0072-185">The "test" script gets the Asset Id and sets the appropriate environment variable.</span><span class="sxs-lookup"><span data-stu-id="b0072-185">The "test" script gets the Asset Id and sets the appropriate environment variable.</span></span>

## <a name="create-a-sas-locator-and-create-the-upload-url"></a><span data-ttu-id="b0072-186">Create a SAS locator and create the Upload URL</span><span class="sxs-lookup"><span data-stu-id="b0072-186">Create a SAS locator and create the Upload URL</span></span>

### <a name="overview"></a><span data-ttu-id="b0072-187">Overview</span><span class="sxs-lookup"><span data-stu-id="b0072-187">Overview</span></span>

<span data-ttu-id="b0072-188">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span><span class="sxs-lookup"><span data-stu-id="b0072-188">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="b0072-189">You must upload the files as block blobs.</span><span class="sxs-lookup"><span data-stu-id="b0072-189">You must upload the files as block blobs.</span></span> <span data-ttu-id="b0072-190">Page blobs are not supported by Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b0072-190">Page blobs are not supported by Azure Media Services.</span></span>  

<span data-ttu-id="b0072-191">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="b0072-191">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="b0072-192">To receive the actual upload URL, create a SAS Locator (shown below).</span><span class="sxs-lookup"><span data-stu-id="b0072-192">To receive the actual upload URL, create a SAS Locator (shown below).</span></span> <span data-ttu-id="b0072-193">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span><span class="sxs-lookup"><span data-stu-id="b0072-193">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="b0072-194">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span><span class="sxs-lookup"><span data-stu-id="b0072-194">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="b0072-195">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span><span class="sxs-lookup"><span data-stu-id="b0072-195">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="b0072-196">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="b0072-196">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="b0072-197">A SAS URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="b0072-197">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

### <a name="considerations"></a><span data-ttu-id="b0072-198">Considerations</span><span class="sxs-lookup"><span data-stu-id="b0072-198">Considerations</span></span>

<span data-ttu-id="b0072-199">Some considerations apply:</span><span class="sxs-lookup"><span data-stu-id="b0072-199">Some considerations apply:</span></span>

* <span data-ttu-id="b0072-200">You cannot have more than five unique Locators associated with a given Asset at one time.</span><span class="sxs-lookup"><span data-stu-id="b0072-200">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="b0072-201">For more information, see Locator.</span><span class="sxs-lookup"><span data-stu-id="b0072-201">For more information, see Locator.</span></span>
* <span data-ttu-id="b0072-202">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span><span class="sxs-lookup"><span data-stu-id="b0072-202">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="b0072-203">This is because there may be clock skew between your client machine and Media Services.</span><span class="sxs-lookup"><span data-stu-id="b0072-203">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="b0072-204">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="b0072-204">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="b0072-205">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span><span class="sxs-lookup"><span data-stu-id="b0072-205">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span>

### <a name="create-a-sas-locator"></a><span data-ttu-id="b0072-206">Create a SAS locator</span><span class="sxs-lookup"><span data-stu-id="b0072-206">Create a SAS locator</span></span>

1. <span data-ttu-id="b0072-207">Select **Locator** -> **Create SAS Locator**.</span><span class="sxs-lookup"><span data-stu-id="b0072-207">Select **Locator** -> **Create SAS Locator**.</span></span>
2. <span data-ttu-id="b0072-208">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="b0072-208">Press **Send**.</span></span>

    <span data-ttu-id="b0072-209">The "test" script creates the "Upload URL" based on the media file name you specified and SAS locator information and sets the appropriate environment variable.</span><span class="sxs-lookup"><span data-stu-id="b0072-209">The "test" script creates the "Upload URL" based on the media file name you specified and SAS locator information and sets the appropriate environment variable.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-create-sas-locator.png)

## <a name="upload-a-file-to-blob-storage-using-the-upload-url"></a><span data-ttu-id="b0072-211">Upload a file to blob storage using the upload URL</span><span class="sxs-lookup"><span data-stu-id="b0072-211">Upload a file to blob storage using the upload URL</span></span>

### <a name="overview"></a><span data-ttu-id="b0072-212">Overview</span><span class="sxs-lookup"><span data-stu-id="b0072-212">Overview</span></span>

<span data-ttu-id="b0072-213">Now that you have the upload URL, you need to write some code using the Azure Blob APIs directly to upload your file to the SAS container.</span><span class="sxs-lookup"><span data-stu-id="b0072-213">Now that you have the upload URL, you need to write some code using the Azure Blob APIs directly to upload your file to the SAS container.</span></span> <span data-ttu-id="b0072-214">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="b0072-214">For more information, see the following articles:</span></span>

- [<span data-ttu-id="b0072-215">Using the Azure Storage REST API</span><span class="sxs-lookup"><span data-stu-id="b0072-215">Using the Azure Storage REST API</span></span>](https://docs.microsoft.com/azure/storage/common/storage-rest-api-auth?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
- [<span data-ttu-id="b0072-216">PUT Blob</span><span class="sxs-lookup"><span data-stu-id="b0072-216">PUT Blob</span></span>](https://docs.microsoft.com/rest/api/storageservices/put-blob)
- [<span data-ttu-id="b0072-217">Upload blobs to Blob storage</span><span class="sxs-lookup"><span data-stu-id="b0072-217">Upload blobs to Blob storage</span></span>](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy#upload-blobs-to-blob-storage)

### <a name="upload-a-file-with-postman"></a><span data-ttu-id="b0072-218">Upload a file with Postman</span><span class="sxs-lookup"><span data-stu-id="b0072-218">Upload a file with Postman</span></span>

<span data-ttu-id="b0072-219">As an example, we use Postman to upload a small .mp4 file.</span><span class="sxs-lookup"><span data-stu-id="b0072-219">As an example, we use Postman to upload a small .mp4 file.</span></span> <span data-ttu-id="b0072-220">There may be a file size limit on uploading binary through Postman.</span><span class="sxs-lookup"><span data-stu-id="b0072-220">There may be a file size limit on uploading binary through Postman.</span></span>

<span data-ttu-id="b0072-221">The upload request is not part of the **AzureMedia** collection.</span><span class="sxs-lookup"><span data-stu-id="b0072-221">The upload request is not part of the **AzureMedia** collection.</span></span> 

<span data-ttu-id="b0072-222">Create and set up a new request:</span><span class="sxs-lookup"><span data-stu-id="b0072-222">Create and set up a new request:</span></span>
1. <span data-ttu-id="b0072-223">Press **+**, to create a new request tab.</span><span class="sxs-lookup"><span data-stu-id="b0072-223">Press **+**, to create a new request tab.</span></span>
2. <span data-ttu-id="b0072-224">Select **PUT** operation and paste **{{UploadURL}}** in the URL.</span><span class="sxs-lookup"><span data-stu-id="b0072-224">Select **PUT** operation and paste **{{UploadURL}}** in the URL.</span></span>
2. <span data-ttu-id="b0072-225">Leave **Authorization** tab as is (do not set it to the **Bearer Token**).</span><span class="sxs-lookup"><span data-stu-id="b0072-225">Leave **Authorization** tab as is (do not set it to the **Bearer Token**).</span></span>
3. <span data-ttu-id="b0072-226">In the **Headers** tab, specify: **Key**: "x-ms-blob-type" and **Value**: "BlockBlob".</span><span class="sxs-lookup"><span data-stu-id="b0072-226">In the **Headers** tab, specify: **Key**: "x-ms-blob-type" and **Value**: "BlockBlob".</span></span>
2. <span data-ttu-id="b0072-227">In the **Body** tab, click **binary**.</span><span class="sxs-lookup"><span data-stu-id="b0072-227">In the **Body** tab, click **binary**.</span></span>
4. <span data-ttu-id="b0072-228">Choose the file with the name that you specified in the **MediaFileName** environment variable.</span><span class="sxs-lookup"><span data-stu-id="b0072-228">Choose the file with the name that you specified in the **MediaFileName** environment variable.</span></span>
5. <span data-ttu-id="b0072-229">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="b0072-229">Press **Send**.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-upload-file.png)

##  <a name="create-a-metadata-in-the-asset"></a><span data-ttu-id="b0072-231">Create a metadata in the asset</span><span class="sxs-lookup"><span data-stu-id="b0072-231">Create a metadata in the asset</span></span>

<span data-ttu-id="b0072-232">Once the file has been uploaded, you need to create a metadata in the asset for the media file you uploaded into the blob storage associated with your asset.</span><span class="sxs-lookup"><span data-stu-id="b0072-232">Once the file has been uploaded, you need to create a metadata in the asset for the media file you uploaded into the blob storage associated with your asset.</span></span>

1. <span data-ttu-id="b0072-233">Select **AssetFiles** -> **CreateFileInfos**.</span><span class="sxs-lookup"><span data-stu-id="b0072-233">Select **AssetFiles** -> **CreateFileInfos**.</span></span>
2. <span data-ttu-id="b0072-234">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="b0072-234">Press **Send**.</span></span>

    ![Upload a file](./media/media-services-rest-upload-files/postman-create-file-info.png)

<span data-ttu-id="b0072-236">The file should be uploaded and its metadata set.</span><span class="sxs-lookup"><span data-stu-id="b0072-236">The file should be uploaded and its metadata set.</span></span>

## <a name="validate"></a><span data-ttu-id="b0072-237">Validate</span><span class="sxs-lookup"><span data-stu-id="b0072-237">Validate</span></span>

<span data-ttu-id="b0072-238">To validate that the file has been uploaded successfully, you might want to query the [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) and compare the **ContentFileSize** (or other details) to what you expect to see in the new asset.</span><span class="sxs-lookup"><span data-stu-id="b0072-238">To validate that the file has been uploaded successfully, you might want to query the [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) and compare the **ContentFileSize** (or other details) to what you expect to see in the new asset.</span></span> 

<span data-ttu-id="b0072-239">For example, the following **GET** operation brings file data for your asset file (in or case, the BigBuckBunny.mp4 file).</span><span class="sxs-lookup"><span data-stu-id="b0072-239">For example, the following **GET** operation brings file data for your asset file (in or case, the BigBuckBunny.mp4 file).</span></span> <span data-ttu-id="b0072-240">The query is using the [environment variables](postman-environment.md) that you set earlier.</span><span class="sxs-lookup"><span data-stu-id="b0072-240">The query is using the [environment variables](postman-environment.md) that you set earlier.</span></span>

    {{RESTAPIEndpoint}}/Assets('{{LastAssetId}}')/Files

<span data-ttu-id="b0072-241">Response will contain size, name, and other information.</span><span class="sxs-lookup"><span data-stu-id="b0072-241">Response will contain size, name, and other information.</span></span>

    "Id": "nb:cid:UUID:69e72ede-2886-4f2a-8d36-80a59da09913",
    "Name": "BigBuckBunny.mp4",
    "ContentFileSize": "3186542",
    "ParentAssetId": "nb:cid:UUID:0b8f3b04-72fb-4f38-8e7b-d7dd78888938",
            
## <a name="next-steps"></a><span data-ttu-id="b0072-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0072-242">Next steps</span></span>

<span data-ttu-id="b0072-243">You can now encode your uploaded assets.</span><span class="sxs-lookup"><span data-stu-id="b0072-243">You can now encode your uploaded assets.</span></span> <span data-ttu-id="b0072-244">For more information, see [Encode assets](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="b0072-244">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="b0072-245">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span><span class="sxs-lookup"><span data-stu-id="b0072-245">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="b0072-246">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="b0072-246">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

