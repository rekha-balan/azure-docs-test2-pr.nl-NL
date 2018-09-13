---
title: Upload, encode, and stream using Azure Media Services | Microsoft Docs
description: Follow the steps of this tutorial to upload a file, and encode the video, and stream your content with Azure Media Services using REST.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: tutorial
ms.custom: mvc
ms.date: 07/16/2018
ms.author: juliako
ms.openlocfilehash: 5cc109467f9affa9cf5f43342203e8d4298269e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856166"
---
# <a name="tutorial-upload-encode-and-stream-videos-with-rest"></a><span data-ttu-id="88e26-103">Tutorial: Upload, encode, and stream videos with REST</span><span class="sxs-lookup"><span data-stu-id="88e26-103">Tutorial: Upload, encode, and stream videos with REST</span></span>

<span data-ttu-id="88e26-104">This tutorial shows you how to upload, encode, and stream video files with Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="88e26-104">This tutorial shows you how to upload, encode, and stream video files with Azure Media Services.</span></span>

<span data-ttu-id="88e26-105">Media Services enables you to encode your media files into formats that can be played on a wide variety of browsers and devices.</span><span class="sxs-lookup"><span data-stu-id="88e26-105">Media Services enables you to encode your media files into formats that can be played on a wide variety of browsers and devices.</span></span> <span data-ttu-id="88e26-106">For example, you might want to stream your content in Apple's HLS or MPEG DASH formats.</span><span class="sxs-lookup"><span data-stu-id="88e26-106">For example, you might want to stream your content in Apple's HLS or MPEG DASH formats.</span></span> <span data-ttu-id="88e26-107">Before streaming, you should encode your high-quality digital media file.</span><span class="sxs-lookup"><span data-stu-id="88e26-107">Before streaming, you should encode your high-quality digital media file.</span></span> <span data-ttu-id="88e26-108">For encoding guidance, see [Encoding concept](encoding-concept.md).</span><span class="sxs-lookup"><span data-stu-id="88e26-108">For encoding guidance, see [Encoding concept](encoding-concept.md).</span></span>

![Play the video](./media/stream-files-tutorial-with-api/final-video.png)

<span data-ttu-id="88e26-110">This tutorial shows you how to:</span><span class="sxs-lookup"><span data-stu-id="88e26-110">This tutorial shows you how to:</span></span>    

> [!div class="checklist"]
> * <span data-ttu-id="88e26-111">Create a Media Services account</span><span class="sxs-lookup"><span data-stu-id="88e26-111">Create a Media Services account</span></span>
> * <span data-ttu-id="88e26-112">Access the Media Services API</span><span class="sxs-lookup"><span data-stu-id="88e26-112">Access the Media Services API</span></span>
> * <span data-ttu-id="88e26-113">Download Postman files</span><span class="sxs-lookup"><span data-stu-id="88e26-113">Download Postman files</span></span>
> * <span data-ttu-id="88e26-114">Configure Postman</span><span class="sxs-lookup"><span data-stu-id="88e26-114">Configure Postman</span></span>
> * <span data-ttu-id="88e26-115">Send reqests using Postman</span><span class="sxs-lookup"><span data-stu-id="88e26-115">Send reqests using Postman</span></span>
> * <span data-ttu-id="88e26-116">Test the streaming URL</span><span class="sxs-lookup"><span data-stu-id="88e26-116">Test the streaming URL</span></span>
> * <span data-ttu-id="88e26-117">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="88e26-117">Clean up resources</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="88e26-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88e26-118">Prerequisites</span></span>

- <span data-ttu-id="88e26-119">Install the [Postman](https://www.getpostman.com/) REST client to execute the REST APIs shown in some of the AMS REST tutorials.</span><span class="sxs-lookup"><span data-stu-id="88e26-119">Install the [Postman](https://www.getpostman.com/) REST client to execute the REST APIs shown in some of the AMS REST tutorials.</span></span> 

    <span data-ttu-id="88e26-120">We are using **Postman** but any REST tool would be suitable.</span><span class="sxs-lookup"><span data-stu-id="88e26-120">We are using **Postman** but any REST tool would be suitable.</span></span> <span data-ttu-id="88e26-121">Other alternatives are: **Visual Studio Code** with the REST plugin or **Telerik Fiddler**.</span><span class="sxs-lookup"><span data-stu-id="88e26-121">Other alternatives are: **Visual Studio Code** with the REST plugin or **Telerik Fiddler**.</span></span> 

## <a name="download-postman-files"></a><span data-ttu-id="88e26-122">Download Postman files</span><span class="sxs-lookup"><span data-stu-id="88e26-122">Download Postman files</span></span>

<span data-ttu-id="88e26-123">Clone a GitHub repository that contains the  Postman collection and environment files.</span><span class="sxs-lookup"><span data-stu-id="88e26-123">Clone a GitHub repository that contains the  Postman collection and environment files.</span></span>

 ```bash
 git clone https://github.com/Azure-Samples/media-services-v3-rest-postman.git
 ```

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [media-services-cli-create-v3-account-include](../../../includes/media-services-cli-create-v3-account-include.md)]

[!INCLUDE [media-services-v3-cli-access-api-include](../../../includes/media-services-v3-cli-access-api-include.md)]

## <a name="configure-postman"></a><span data-ttu-id="88e26-124">Configure Postman</span><span class="sxs-lookup"><span data-stu-id="88e26-124">Configure Postman</span></span>

<span data-ttu-id="88e26-125">This section configures the Postman.</span><span class="sxs-lookup"><span data-stu-id="88e26-125">This section configures the Postman.</span></span>

### <a name="configure-the-environment"></a><span data-ttu-id="88e26-126">Configure the environment</span><span class="sxs-lookup"><span data-stu-id="88e26-126">Configure the environment</span></span> 

1. <span data-ttu-id="88e26-127">Open the **Postman**.</span><span class="sxs-lookup"><span data-stu-id="88e26-127">Open the **Postman**.</span></span>
2. <span data-ttu-id="88e26-128">On the right of the screen, select the **Manage environment** option.</span><span class="sxs-lookup"><span data-stu-id="88e26-128">On the right of the screen, select the **Manage environment** option.</span></span>

    ![Manage env](./media/develop-with-postman/postman-import-env.png)
4. <span data-ttu-id="88e26-130">From the **Manage environment** dialog, click **Import**.</span><span class="sxs-lookup"><span data-stu-id="88e26-130">From the **Manage environment** dialog, click **Import**.</span></span>
2. <span data-ttu-id="88e26-131">Browse to the `Azure Media Service v3 Environment.postman_environment.json` file that was downloaded when you cloned `https://github.com/Azure-Samples/media-services-v3-rest-postman.git`.</span><span class="sxs-lookup"><span data-stu-id="88e26-131">Browse to the `Azure Media Service v3 Environment.postman_environment.json` file that was downloaded when you cloned `https://github.com/Azure-Samples/media-services-v3-rest-postman.git`.</span></span>
6. <span data-ttu-id="88e26-132">The **Azure Media Service v3 Environment** environment is added.</span><span class="sxs-lookup"><span data-stu-id="88e26-132">The **Azure Media Service v3 Environment** environment is added.</span></span>

    > [!Note]
    > <span data-ttu-id="88e26-133">Update access variables with values you got from the **Access the Media Services API** section above.</span><span class="sxs-lookup"><span data-stu-id="88e26-133">Update access variables with values you got from the **Access the Media Services API** section above.</span></span>

7. <span data-ttu-id="88e26-134">Double-click on the selected file and enter values that you got by following the [accessing API](#access-the-media-services-api) steps.</span><span class="sxs-lookup"><span data-stu-id="88e26-134">Double-click on the selected file and enter values that you got by following the [accessing API](#access-the-media-services-api) steps.</span></span>
8. <span data-ttu-id="88e26-135">Close the dialog.</span><span class="sxs-lookup"><span data-stu-id="88e26-135">Close the dialog.</span></span>
9. <span data-ttu-id="88e26-136">Select the **Azure Media Service v3 Environment** environment from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="88e26-136">Select the **Azure Media Service v3 Environment** environment from the dropdown.</span></span>

    ![Choose env](./media/develop-with-postman/choose-env.png)
   
### <a name="configure-the-collection"></a><span data-ttu-id="88e26-138">Configure the collection</span><span class="sxs-lookup"><span data-stu-id="88e26-138">Configure the collection</span></span>

1. <span data-ttu-id="88e26-139">Click **Import** to import the collection file.</span><span class="sxs-lookup"><span data-stu-id="88e26-139">Click **Import** to import the collection file.</span></span>
1. <span data-ttu-id="88e26-140">Browse to the `Media Services v3.postman_collection.json` file that was downloaded when you cloned `https://github.com/Azure-Samples/media-services-v3-rest-postman.git`</span><span class="sxs-lookup"><span data-stu-id="88e26-140">Browse to the `Media Services v3.postman_collection.json` file that was downloaded when you cloned `https://github.com/Azure-Samples/media-services-v3-rest-postman.git`</span></span>
3. <span data-ttu-id="88e26-141">Choose the **Media Services v3.postman_collection.json** file.</span><span class="sxs-lookup"><span data-stu-id="88e26-141">Choose the **Media Services v3.postman_collection.json** file.</span></span>

    ![Import a file](./media/develop-with-postman/postman-import-collection.png)

## <a name="send-requests-using-postman"></a><span data-ttu-id="88e26-143">Send requests using Postman</span><span class="sxs-lookup"><span data-stu-id="88e26-143">Send requests using Postman</span></span>

<span data-ttu-id="88e26-144">In this section, we send requests that are relevant to encoding and creating URLs so you can stream your file.</span><span class="sxs-lookup"><span data-stu-id="88e26-144">In this section, we send requests that are relevant to encoding and creating URLs so you can stream your file.</span></span> <span data-ttu-id="88e26-145">Specifically, the following requests are sent:</span><span class="sxs-lookup"><span data-stu-id="88e26-145">Specifically, the following requests are sent:</span></span>

1. <span data-ttu-id="88e26-146">Get Azure AD Token for Service Principal Authentication</span><span class="sxs-lookup"><span data-stu-id="88e26-146">Get Azure AD Token for Service Principal Authentication</span></span>
2. <span data-ttu-id="88e26-147">Create an output asset</span><span class="sxs-lookup"><span data-stu-id="88e26-147">Create an output asset</span></span>
3. <span data-ttu-id="88e26-148">Create a transform</span><span class="sxs-lookup"><span data-stu-id="88e26-148">Create a transform</span></span>
4. <span data-ttu-id="88e26-149">Create a job</span><span class="sxs-lookup"><span data-stu-id="88e26-149">Create a job</span></span> 
5. <span data-ttu-id="88e26-150">Create a streaming locator</span><span class="sxs-lookup"><span data-stu-id="88e26-150">Create a streaming locator</span></span>
6. <span data-ttu-id="88e26-151">List paths of the streaming locator</span><span class="sxs-lookup"><span data-stu-id="88e26-151">List paths of the streaming locator</span></span>

> [!Note]
>  <span data-ttu-id="88e26-152">This tutorial assumes you are creating all resources with unique names.</span><span class="sxs-lookup"><span data-stu-id="88e26-152">This tutorial assumes you are creating all resources with unique names.</span></span>  

### <a name="get-azure-ad-token"></a><span data-ttu-id="88e26-153">Get Azure AD Token</span><span class="sxs-lookup"><span data-stu-id="88e26-153">Get Azure AD Token</span></span> 

1. <span data-ttu-id="88e26-154">In the left window of the Postman, select "Step 1: Get AAD Auth token".</span><span class="sxs-lookup"><span data-stu-id="88e26-154">In the left window of the Postman, select "Step 1: Get AAD Auth token".</span></span>
2. <span data-ttu-id="88e26-155">Then, select "Get Azure AD Token for Service Principal Authentication".</span><span class="sxs-lookup"><span data-stu-id="88e26-155">Then, select "Get Azure AD Token for Service Principal Authentication".</span></span>
3. <span data-ttu-id="88e26-156">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="88e26-156">Press **Send**.</span></span>

    <span data-ttu-id="88e26-157">The following **POST** operation is sent.</span><span class="sxs-lookup"><span data-stu-id="88e26-157">The following **POST** operation is sent.</span></span>

    ```
    https://login.microsoftonline.com/:tenantId/oauth2/token
    ```

4. <span data-ttu-id="88e26-158">The response comes back with the token and sets the "AccessToken" environment variable to the token value.</span><span class="sxs-lookup"><span data-stu-id="88e26-158">The response comes back with the token and sets the "AccessToken" environment variable to the token value.</span></span> <span data-ttu-id="88e26-159">To see the code that sets "AccessToken" , click on the **Tests** tab.</span><span class="sxs-lookup"><span data-stu-id="88e26-159">To see the code that sets "AccessToken" , click on the **Tests** tab.</span></span> 

    ![Get AAD token](./media/develop-with-postman/postman-get-aad-auth-token.png)

### <a name="create-an-output-asset"></a><span data-ttu-id="88e26-161">Create an output asset</span><span class="sxs-lookup"><span data-stu-id="88e26-161">Create an output asset</span></span>

<span data-ttu-id="88e26-162">The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your encoding job.</span><span class="sxs-lookup"><span data-stu-id="88e26-162">The output [Asset](https://docs.microsoft.com/rest/api/media/assets) stores the result of your encoding job.</span></span> 

1. <span data-ttu-id="88e26-163">In the left window of the Postman, select "Assets".</span><span class="sxs-lookup"><span data-stu-id="88e26-163">In the left window of the Postman, select "Assets".</span></span>
2. <span data-ttu-id="88e26-164">Then, select "Create or update an Asset".</span><span class="sxs-lookup"><span data-stu-id="88e26-164">Then, select "Create or update an Asset".</span></span>
3. <span data-ttu-id="88e26-165">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="88e26-165">Press **Send**.</span></span>

    * <span data-ttu-id="88e26-166">The following **PUT** operation is sent:</span><span class="sxs-lookup"><span data-stu-id="88e26-166">The following **PUT** operation is sent:</span></span>

        ```
        https://management.azure.com/subscriptions/:subscriptionId/resourceGroups/:resourceGroupName/providers/Microsoft.Media/mediaServices/:accountName/assets/:assetName?api-version={{api-version}}
        ```
    * <span data-ttu-id="88e26-167">The operation has the following  body:</span><span class="sxs-lookup"><span data-stu-id="88e26-167">The operation has the following  body:</span></span>

        ```json
        {
        "properties": {
            "description": "My Asset",
            "alternateId" : "some GUID"
         }
        }
        ```

### <a name="create-a-transform"></a><span data-ttu-id="88e26-168">Create a transform</span><span class="sxs-lookup"><span data-stu-id="88e26-168">Create a transform</span></span>

<span data-ttu-id="88e26-169">When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe.</span><span class="sxs-lookup"><span data-stu-id="88e26-169">When encoding or processing content in Media Services, it is a common pattern to set up the encoding settings as a recipe.</span></span> <span data-ttu-id="88e26-170">You would then submit a **Job** to apply that recipe to a video.</span><span class="sxs-lookup"><span data-stu-id="88e26-170">You would then submit a **Job** to apply that recipe to a video.</span></span> <span data-ttu-id="88e26-171">By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library.</span><span class="sxs-lookup"><span data-stu-id="88e26-171">By submitting new Jobs for each new video, you are applying that recipe to all the videos in your library.</span></span> <span data-ttu-id="88e26-172">A recipe in Media Services is called as a **Transform**.</span><span class="sxs-lookup"><span data-stu-id="88e26-172">A recipe in Media Services is called as a **Transform**.</span></span> <span data-ttu-id="88e26-173">For more information, see [Transforms and jobs](transform-concept.md).</span><span class="sxs-lookup"><span data-stu-id="88e26-173">For more information, see [Transforms and jobs](transform-concept.md).</span></span> <span data-ttu-id="88e26-174">The sample described in this tutorial defines a recipe that encodes the video in order to stream it to a variety of iOS and Android devices.</span><span class="sxs-lookup"><span data-stu-id="88e26-174">The sample described in this tutorial defines a recipe that encodes the video in order to stream it to a variety of iOS and Android devices.</span></span> 

<span data-ttu-id="88e26-175">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output.</span><span class="sxs-lookup"><span data-stu-id="88e26-175">When creating a new [Transform](https://docs.microsoft.com/rest/api/media/transforms) instance, you need to specify what you want it to produce as an output.</span></span> <span data-ttu-id="88e26-176">The required parameter is a **TransformOutput** object.</span><span class="sxs-lookup"><span data-stu-id="88e26-176">The required parameter is a **TransformOutput** object.</span></span> <span data-ttu-id="88e26-177">Each **TransformOutput** contains a **Preset**.</span><span class="sxs-lookup"><span data-stu-id="88e26-177">Each **TransformOutput** contains a **Preset**.</span></span> <span data-ttu-id="88e26-178">**Preset** describes the step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span><span class="sxs-lookup"><span data-stu-id="88e26-178">**Preset** describes the step-by-step instructions of video and/or audio processing operations that are to be used to generate the desired **TransformOutput**.</span></span> <span data-ttu-id="88e26-179">The sample described in this article uses a built-in Preset called **AdaptiveStreaming**.</span><span class="sxs-lookup"><span data-stu-id="88e26-179">The sample described in this article uses a built-in Preset called **AdaptiveStreaming**.</span></span> <span data-ttu-id="88e26-180">The Preset encodes the input video into an auto-generated bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate, and produces ISO MP4 files with H.264 video and AAC audio corresponding to each bitrate-resolution pair.</span><span class="sxs-lookup"><span data-stu-id="88e26-180">The Preset encodes the input video into an auto-generated bitrate ladder (bitrate-resolution pairs) based on the input resolution and bitrate, and produces ISO MP4 files with H.264 video and AAC audio corresponding to each bitrate-resolution pair.</span></span> <span data-ttu-id="88e26-181">For information about this Preset, see [auto-generating bitrate ladder](autogen-bitrate-ladder.md).</span><span class="sxs-lookup"><span data-stu-id="88e26-181">For information about this Preset, see [auto-generating bitrate ladder](autogen-bitrate-ladder.md).</span></span>

<span data-ttu-id="88e26-182">You can use a built-in EncoderNamedPreset or use custom presets.</span><span class="sxs-lookup"><span data-stu-id="88e26-182">You can use a built-in EncoderNamedPreset or use custom presets.</span></span> 

> [!Note]
> <span data-ttu-id="88e26-183">When creating a [Transform](https://docs.microsoft.com/rest/api/media/transforms), you should first check if one already exists using the **Get** method.</span><span class="sxs-lookup"><span data-stu-id="88e26-183">When creating a [Transform](https://docs.microsoft.com/rest/api/media/transforms), you should first check if one already exists using the **Get** method.</span></span> <span data-ttu-id="88e26-184">This tutorial assumes you are creating the transform with a unique name.</span><span class="sxs-lookup"><span data-stu-id="88e26-184">This tutorial assumes you are creating the transform with a unique name.</span></span>

1. <span data-ttu-id="88e26-185">In the left window of the Postman, select "Encoding and Analysis".</span><span class="sxs-lookup"><span data-stu-id="88e26-185">In the left window of the Postman, select "Encoding and Analysis".</span></span>
2. <span data-ttu-id="88e26-186">Then, select "Create Transform".</span><span class="sxs-lookup"><span data-stu-id="88e26-186">Then, select "Create Transform".</span></span>
3. <span data-ttu-id="88e26-187">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="88e26-187">Press **Send**.</span></span>

    * <span data-ttu-id="88e26-188">The following **PUT** operation is sent.</span><span class="sxs-lookup"><span data-stu-id="88e26-188">The following **PUT** operation is sent.</span></span>

        ```
        https://management.azure.com/subscriptions/:subscriptionId/resourceGroups/:resourceGroupName/providers/Microsoft.Media/mediaServices/:accountName/transforms/:transformName?api-version={{api-version}}
        ```
    * <span data-ttu-id="88e26-189">The operation has the following body:</span><span class="sxs-lookup"><span data-stu-id="88e26-189">The operation has the following body:</span></span>

        ```json
        {
            "properties": {
                "description": "Basic Transform using an Adaptive Streaming encoding preset from the libray of built-in Standard Encoder presets",
                "outputs": [
                    {
                    "onError": "StopProcessingJob",
                "relativePriority": "Normal",
                    "preset": {
                        "@odata.type": "#Microsoft.Media.BuiltInStandardEncoderPreset",
                        "presetName": "AdaptiveStreaming"
                    }
                    }
                ]
            }
        }
        ```

### <a name="create-a-job"></a><span data-ttu-id="88e26-190">Create a job</span><span class="sxs-lookup"><span data-stu-id="88e26-190">Create a job</span></span>

<span data-ttu-id="88e26-191">A [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply the created **Transform** to a given input video or audio content.</span><span class="sxs-lookup"><span data-stu-id="88e26-191">A [Job](https://docs.microsoft.com/rest/api/media/jobs) is the actual request to Media Services to apply the created **Transform** to a given input video or audio content.</span></span> <span data-ttu-id="88e26-192">The **Job** specifies information like the location of the input video, and the location for the output.</span><span class="sxs-lookup"><span data-stu-id="88e26-192">The **Job** specifies information like the location of the input video, and the location for the output.</span></span>

<span data-ttu-id="88e26-193">In this example, the job's input is based on an HTTPS URL ("https://nimbuscdn-nimbuspm.streaming.mediaservices.windows.net/2b533311-b215-4409-80af-529c3e853622/").</span><span class="sxs-lookup"><span data-stu-id="88e26-193">In this example, the job's input is based on an HTTPS URL ("https://nimbuscdn-nimbuspm.streaming.mediaservices.windows.net/2b533311-b215-4409-80af-529c3e853622/").</span></span>

1. <span data-ttu-id="88e26-194">In the left window of the Postman, select "Encoding and Analysis".</span><span class="sxs-lookup"><span data-stu-id="88e26-194">In the left window of the Postman, select "Encoding and Analysis".</span></span>
2. <span data-ttu-id="88e26-195">Then, select "Create or Update Job".</span><span class="sxs-lookup"><span data-stu-id="88e26-195">Then, select "Create or Update Job".</span></span>
3. <span data-ttu-id="88e26-196">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="88e26-196">Press **Send**.</span></span>

    * <span data-ttu-id="88e26-197">The following **PUT** operation is sent.</span><span class="sxs-lookup"><span data-stu-id="88e26-197">The following **PUT** operation is sent.</span></span>

        ```
        https://management.azure.com/subscriptions/:subscriptionId/resourceGroups/:resourceGroupName/providers/Microsoft.Media/mediaServices/:accountName/transforms/:transformName/jobs/:jobName?api-version={{api-version}}
        ```
    * <span data-ttu-id="88e26-198">The operation has the following body:</span><span class="sxs-lookup"><span data-stu-id="88e26-198">The operation has the following body:</span></span>

        ```json
        {
        "properties": {
            "input": {
            "@odata.type": "#Microsoft.Media.JobInputHttp",
            "baseUri": "https://nimbuscdn-nimbuspm.streaming.mediaservices.windows.net/2b533311-b215-4409-80af-529c3e853622/",
            "files": [
                    "Ignite-short.mp4"
                ]
            },
            "outputs": [
            {
                "@odata.type": "#Microsoft.Media.JobOutputAsset",
                "assetName": "testAsset1"
            }
            ]
        }
        }
        ```

<span data-ttu-id="88e26-199">The job takes some time to complete and when it does you want to be notified.</span><span class="sxs-lookup"><span data-stu-id="88e26-199">The job takes some time to complete and when it does you want to be notified.</span></span> <span data-ttu-id="88e26-200">To see the progress of the job, we recommend using Event Grid.</span><span class="sxs-lookup"><span data-stu-id="88e26-200">To see the progress of the job, we recommend using Event Grid.</span></span> <span data-ttu-id="88e26-201">It is designed for high availability, consistent performance, and dynamic scale.</span><span class="sxs-lookup"><span data-stu-id="88e26-201">It is designed for high availability, consistent performance, and dynamic scale.</span></span> <span data-ttu-id="88e26-202">With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources.</span><span class="sxs-lookup"><span data-stu-id="88e26-202">With Event Grid, your apps can listen for and react to events from virtually all Azure services, as well as custom sources.</span></span> <span data-ttu-id="88e26-203">Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events.</span><span class="sxs-lookup"><span data-stu-id="88e26-203">Simple, HTTP-based reactive event handling helps you build efficient solutions through intelligent filtering and routing of events.</span></span>  <span data-ttu-id="88e26-204">See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="88e26-204">See [Route events to a custom web endpoint](job-state-events-cli-how-to.md).</span></span>

<span data-ttu-id="88e26-205">The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state).</span><span class="sxs-lookup"><span data-stu-id="88e26-205">The **Job** usually goes through the following states: **Scheduled**, **Queued**, **Processing**, **Finished** (the final state).</span></span> <span data-ttu-id="88e26-206">If the job has encountered an error, you get the **Error** state.</span><span class="sxs-lookup"><span data-stu-id="88e26-206">If the job has encountered an error, you get the **Error** state.</span></span> <span data-ttu-id="88e26-207">If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.</span><span class="sxs-lookup"><span data-stu-id="88e26-207">If the job is in the process of being canceled, you get **Canceling** and **Canceled** when it is done.</span></span>

### <a name="create-a-streaming-locator"></a><span data-ttu-id="88e26-208">Create a streaming locator</span><span class="sxs-lookup"><span data-stu-id="88e26-208">Create a streaming locator</span></span>

<span data-ttu-id="88e26-209">After the encoding job is complete, the next step is to make the video in the output Asset available to clients for playback.</span><span class="sxs-lookup"><span data-stu-id="88e26-209">After the encoding job is complete, the next step is to make the video in the output Asset available to clients for playback.</span></span> <span data-ttu-id="88e26-210">You can accomplish this in two steps: first, create a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), and second, build the streaming URLs that clients can use.</span><span class="sxs-lookup"><span data-stu-id="88e26-210">You can accomplish this in two steps: first, create a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), and second, build the streaming URLs that clients can use.</span></span> 

<span data-ttu-id="88e26-211">The process of creating a **StreamingLocator** is called publishing.</span><span class="sxs-lookup"><span data-stu-id="88e26-211">The process of creating a **StreamingLocator** is called publishing.</span></span> <span data-ttu-id="88e26-212">By default, the **StreamingLocator** is valid immediately after you make the API calls, and lasts until it is deleted, unless you configure the optional start and end times.</span><span class="sxs-lookup"><span data-stu-id="88e26-212">By default, the **StreamingLocator** is valid immediately after you make the API calls, and lasts until it is deleted, unless you configure the optional start and end times.</span></span> 

<span data-ttu-id="88e26-213">When creating a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), you will need to specify the desired **StreamingPolicyName**.</span><span class="sxs-lookup"><span data-stu-id="88e26-213">When creating a [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators), you will need to specify the desired **StreamingPolicyName**.</span></span> <span data-ttu-id="88e26-214">In this example, you will be streaming in-the-clear (or non-encrypted) content, so the predefined clear streaming policy (**PredefinedStreamingPolicy.ClearStreamingOnly**) is used.</span><span class="sxs-lookup"><span data-stu-id="88e26-214">In this example, you will be streaming in-the-clear (or non-encrypted) content, so the predefined clear streaming policy (**PredefinedStreamingPolicy.ClearStreamingOnly**) is used.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88e26-215">When using a custom [StreamingPolicy](https://docs.microsoft.com/rest/api/media/streamingpolicies), you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed.</span><span class="sxs-lookup"><span data-stu-id="88e26-215">When using a custom [StreamingPolicy](https://docs.microsoft.com/rest/api/media/streamingpolicies), you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed.</span></span> 

<span data-ttu-id="88e26-216">Your Media Service account has a quota for the number of StreamingPolicy entries.</span><span class="sxs-lookup"><span data-stu-id="88e26-216">Your Media Service account has a quota for the number of StreamingPolicy entries.</span></span> <span data-ttu-id="88e26-217">You should not be creating a new StreamingPolicy for each StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="88e26-217">You should not be creating a new StreamingPolicy for each StreamingLocator.</span></span>

1. <span data-ttu-id="88e26-218">In the left window of the Postman, select "Streaming Policies".</span><span class="sxs-lookup"><span data-stu-id="88e26-218">In the left window of the Postman, select "Streaming Policies".</span></span>
2. <span data-ttu-id="88e26-219">Then, select "Create a Streaming Locator".</span><span class="sxs-lookup"><span data-stu-id="88e26-219">Then, select "Create a Streaming Locator".</span></span>
3. <span data-ttu-id="88e26-220">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="88e26-220">Press **Send**.</span></span>

    * <span data-ttu-id="88e26-221">The following **PUT** operation is sent.</span><span class="sxs-lookup"><span data-stu-id="88e26-221">The following **PUT** operation is sent.</span></span>

        ```
        https://management.azure.com/subscriptions/:subscriptionId/resourceGroups/:resourceGroupName/providers/Microsoft.Media/mediaServices/:accountName/streamingPolicies/:streamingPolicyName?api-version={{api-version}}
        ```
    * <span data-ttu-id="88e26-222">The operation has the following body:</span><span class="sxs-lookup"><span data-stu-id="88e26-222">The operation has the following body:</span></span>

        ```json
        {
            "properties":{
            "assetName": "{{assetName}}",
            "streamingPolicyName": "{{streamingPolicyName}}"
            }
        }
        ```

### <a name="list-paths-and-build-streaming-urls"></a><span data-ttu-id="88e26-223">List paths and build streaming URLs</span><span class="sxs-lookup"><span data-stu-id="88e26-223">List paths and build streaming URLs</span></span>

#### <a name="list-paths"></a><span data-ttu-id="88e26-224">List paths</span><span class="sxs-lookup"><span data-stu-id="88e26-224">List paths</span></span>

<span data-ttu-id="88e26-225">Now that the [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators) has been created, you can get the streaming URLs</span><span class="sxs-lookup"><span data-stu-id="88e26-225">Now that the [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators) has been created, you can get the streaming URLs</span></span>

1. <span data-ttu-id="88e26-226">In the left window of the Postman, select "Streaming Policies".</span><span class="sxs-lookup"><span data-stu-id="88e26-226">In the left window of the Postman, select "Streaming Policies".</span></span>
2. <span data-ttu-id="88e26-227">Then, select "List Paths".</span><span class="sxs-lookup"><span data-stu-id="88e26-227">Then, select "List Paths".</span></span>
3. <span data-ttu-id="88e26-228">Press **Send**.</span><span class="sxs-lookup"><span data-stu-id="88e26-228">Press **Send**.</span></span>

    * <span data-ttu-id="88e26-229">The following **POST** operation is sent.</span><span class="sxs-lookup"><span data-stu-id="88e26-229">The following **POST** operation is sent.</span></span>

        ```
        https://management.azure.com/subscriptions/:subscriptionId/resourceGroups/:resourceGroupName/providers/Microsoft.Media/mediaServices/:accountName/streamingLocators/:streamingLocatorName/listPaths?api-version={{api-version}}
        ```
        
    * <span data-ttu-id="88e26-230">The operation has no body:</span><span class="sxs-lookup"><span data-stu-id="88e26-230">The operation has no body:</span></span>
        
4. <span data-ttu-id="88e26-231">Note one of the paths you want to use for streaming, you will use it in the next section.</span><span class="sxs-lookup"><span data-stu-id="88e26-231">Note one of the paths you want to use for streaming, you will use it in the next section.</span></span> <span data-ttu-id="88e26-232">In this case, the following paths were returned:</span><span class="sxs-lookup"><span data-stu-id="88e26-232">In this case, the following paths were returned:</span></span>
    
    ```
    "streamingPaths": [
        {
            "streamingProtocol": "Hls",
            "encryptionScheme": "NoEncryption",
            "paths": [
                "/cdb80234-1d94-42a9-b056-0eefa78e5c63/Ignite-short.ism/manifest(format=m3u8-aapl)"
            ]
        },
        {
            "streamingProtocol": "Dash",
            "encryptionScheme": "NoEncryption",
            "paths": [
                "/cdb80234-1d94-42a9-b056-0eefa78e5c63/Ignite-short.ism/manifest(format=mpd-time-csf)"
            ]
        },
        {
            "streamingProtocol": "SmoothStreaming",
            "encryptionScheme": "NoEncryption",
            "paths": [
                "/cdb80234-1d94-42a9-b056-0eefa78e5c63/Ignite-short.ism/manifest"
            ]
        }
    ]
    ```

#### <a name="build-the-streaming-urls"></a><span data-ttu-id="88e26-233">Build the streaming URLs</span><span class="sxs-lookup"><span data-stu-id="88e26-233">Build the streaming URLs</span></span>

<span data-ttu-id="88e26-234">In this section, let's build an HLS streaming URL.</span><span class="sxs-lookup"><span data-stu-id="88e26-234">In this section, let's build an HLS streaming URL.</span></span> <span data-ttu-id="88e26-235">URLs consist of the following values:</span><span class="sxs-lookup"><span data-stu-id="88e26-235">URLs consist of the following values:</span></span>

1. <span data-ttu-id="88e26-236">The protocol over which data is sent.</span><span class="sxs-lookup"><span data-stu-id="88e26-236">The protocol over which data is sent.</span></span> <span data-ttu-id="88e26-237">In this case "https".</span><span class="sxs-lookup"><span data-stu-id="88e26-237">In this case "https".</span></span>

    > [!NOTE]
    > <span data-ttu-id="88e26-238">If a player is hosted on an https site, make sure to update the URL to "https".</span><span class="sxs-lookup"><span data-stu-id="88e26-238">If a player is hosted on an https site, make sure to update the URL to "https".</span></span>

2. <span data-ttu-id="88e26-239">StreamingEndpoint's hostname.</span><span class="sxs-lookup"><span data-stu-id="88e26-239">StreamingEndpoint's hostname.</span></span> <span data-ttu-id="88e26-240">In this case, the name is "amsaccount-usw22.streaming.media.azure.net".</span><span class="sxs-lookup"><span data-stu-id="88e26-240">In this case, the name is "amsaccount-usw22.streaming.media.azure.net".</span></span>

    <span data-ttu-id="88e26-241">To get the hostname you can use the following GET operation:</span><span class="sxs-lookup"><span data-stu-id="88e26-241">To get the hostname you can use the following GET operation:</span></span>
    
    ```
    https://management.azure.com/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/amsResourceGroup/providers/Microsoft.Media/mediaservices/amsaccount/streamingEndpoints/default?api-version={{api-version}}
    ```
    
3. <span data-ttu-id="88e26-242">A path that you got in the previous (List paths) section.</span><span class="sxs-lookup"><span data-stu-id="88e26-242">A path that you got in the previous (List paths) section.</span></span>  

<span data-ttu-id="88e26-243">As a result, the following HLS URL was built</span><span class="sxs-lookup"><span data-stu-id="88e26-243">As a result, the following HLS URL was built</span></span>

```
https://amsaccount-usw22.streaming.media.azure.net/cdb80234-1d94-42a9-b056-0eefa78e5c63/Ignite-short.ism/manifest(format=m3u8-aapl)
```

## <a name="test-the-streaming-url"></a><span data-ttu-id="88e26-244">Test the streaming URL</span><span class="sxs-lookup"><span data-stu-id="88e26-244">Test the streaming URL</span></span>


> [!NOTE]
> <span data-ttu-id="88e26-245">Make sure the streaming endpoint from which you want to stream is running.</span><span class="sxs-lookup"><span data-stu-id="88e26-245">Make sure the streaming endpoint from which you want to stream is running.</span></span>

<span data-ttu-id="88e26-246">To test the stream, this article uses Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="88e26-246">To test the stream, this article uses Azure Media Player.</span></span> 

1. <span data-ttu-id="88e26-247">Open a web browser and navigate to [https://aka.ms/azuremediaplayer/](https://aka.ms/azuremediaplayer/).</span><span class="sxs-lookup"><span data-stu-id="88e26-247">Open a web browser and navigate to [https://aka.ms/azuremediaplayer/](https://aka.ms/azuremediaplayer/).</span></span>
2. <span data-ttu-id="88e26-248">In the **URL:** box, paste the URL you built.</span><span class="sxs-lookup"><span data-stu-id="88e26-248">In the **URL:** box, paste the URL you built.</span></span> 
3. <span data-ttu-id="88e26-249">Press **Update Player**.</span><span class="sxs-lookup"><span data-stu-id="88e26-249">Press **Update Player**.</span></span>

<span data-ttu-id="88e26-250">Azure Media Player can be used for testing but should not be used in a production environment.</span><span class="sxs-lookup"><span data-stu-id="88e26-250">Azure Media Player can be used for testing but should not be used in a production environment.</span></span> 

## <a name="clean-up-resources-in-your-media-services-account"></a><span data-ttu-id="88e26-251">Clean up resources in your Media Services account</span><span class="sxs-lookup"><span data-stu-id="88e26-251">Clean up resources in your Media Services account</span></span>

<span data-ttu-id="88e26-252">Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms, and you will persist StreamingLocators, etc.).</span><span class="sxs-lookup"><span data-stu-id="88e26-252">Generally, you should clean up everything except objects that you are planning to reuse (typically, you will reuse Transforms, and you will persist StreamingLocators, etc.).</span></span> <span data-ttu-id="88e26-253">If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse.</span><span class="sxs-lookup"><span data-stu-id="88e26-253">If you want for your account to be clean after experimenting, you should delete the resources that you do not plan to reuse.</span></span>  

<span data-ttu-id="88e26-254">To delete a resource, select "Delete ..." operation under whichever resource you want to delete.</span><span class="sxs-lookup"><span data-stu-id="88e26-254">To delete a resource, select "Delete ..." operation under whichever resource you want to delete.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="88e26-255">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="88e26-255">Clean up resources</span></span>

<span data-ttu-id="88e26-256">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span><span class="sxs-lookup"><span data-stu-id="88e26-256">If you no longer need any of the resources in your resource group, including the Media Services and storage accounts you created for this tutorial, delete the resource group you created earlier.</span></span> <span data-ttu-id="88e26-257">You can use the **CloudShell** tool.</span><span class="sxs-lookup"><span data-stu-id="88e26-257">You can use the **CloudShell** tool.</span></span>

<span data-ttu-id="88e26-258">In the **CloudShell**, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="88e26-258">In the **CloudShell**, execute the following command:</span></span>

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="88e26-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="88e26-259">Next steps</span></span>

<span data-ttu-id="88e26-260">Now that you know how to upload, encode, and stream your video, see the following article:</span><span class="sxs-lookup"><span data-stu-id="88e26-260">Now that you know how to upload, encode, and stream your video, see the following article:</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="88e26-261">Analyze videos</span><span class="sxs-lookup"><span data-stu-id="88e26-261">Analyze videos</span></span>](analyze-videos-tutorial-with-api.md)
