---
title: Avanced Media Encoder Premium Workflow tutorials
description: This document contains walkthroughs that show how to perform advanced tasks with Media Encoder Premium Workflow and also how to create complex workflows with Workflow Designer.
services: media-services
documentationcenter: ''
author: xstof
manager: erikre
editor: ''
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 5eddc95b1f13b53fa66cc1972154e528641fe710
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671296"
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="798c5-103">Advanced Media Encoder Premium Workflow tutorials</span><span class="sxs-lookup"><span data-stu-id="798c5-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="798c5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="798c5-104">Overview</span></span>
<span data-ttu-id="798c5-105">This document contains walkthroughs that show how to customize workflows with  **Workflow Designer**.</span><span class="sxs-lookup"><span data-stu-id="798c5-105">This document contains walkthroughs that show how to customize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="798c5-106">You can find the actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="798c5-106">You can find the actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="798c5-107">TOC</span><span class="sxs-lookup"><span data-stu-id="798c5-107">TOC</span></span>
<span data-ttu-id="798c5-108">The following topics are covered:</span><span class="sxs-lookup"><span data-stu-id="798c5-108">The following topics are covered:</span></span>

* [<span data-ttu-id="798c5-109">Encoding MXF into a single bitrate MP4</span><span class="sxs-lookup"><span data-stu-id="798c5-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="798c5-110">Starting a new workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="798c5-111">Using the Media File Input</span><span class="sxs-lookup"><span data-stu-id="798c5-111">Using the Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="798c5-112">Inspecting media streams</span><span class="sxs-lookup"><span data-stu-id="798c5-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="798c5-113">Adding a video encoder for .MP4 file generation</span><span class="sxs-lookup"><span data-stu-id="798c5-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="798c5-114">Encoding the audio stream</span><span class="sxs-lookup"><span data-stu-id="798c5-114">Encoding the audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="798c5-115">Multiplexing Audio and Video streams into an MP4 container</span><span class="sxs-lookup"><span data-stu-id="798c5-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="798c5-116">Writing the MP4 file</span><span class="sxs-lookup"><span data-stu-id="798c5-116">Writing the MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="798c5-117">Creating a Media Services Asset from the output file</span><span class="sxs-lookup"><span data-stu-id="798c5-117">Creating a Media Services Asset from the output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="798c5-118">Test the finished workflow locally</span><span class="sxs-lookup"><span data-stu-id="798c5-118">Test the finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="798c5-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span><span class="sxs-lookup"><span data-stu-id="798c5-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="798c5-120">Adding one or more additional MP4 outputs</span><span class="sxs-lookup"><span data-stu-id="798c5-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="798c5-121">Configuring the file output names</span><span class="sxs-lookup"><span data-stu-id="798c5-121">Configuring the file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="798c5-122">Adding a separate Audio Track</span><span class="sxs-lookup"><span data-stu-id="798c5-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="798c5-123">Adding the .ISM SMIL File</span><span class="sxs-lookup"><span data-stu-id="798c5-123">Adding the .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="798c5-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span><span class="sxs-lookup"><span data-stu-id="798c5-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="798c5-125">Workflow overview to enhance</span><span class="sxs-lookup"><span data-stu-id="798c5-125">Workflow overview to enhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="798c5-126">File Naming Conventions</span><span class="sxs-lookup"><span data-stu-id="798c5-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="798c5-127">Publishing component properties onto the workflow root</span><span class="sxs-lookup"><span data-stu-id="798c5-127">Publishing component properties onto the workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="798c5-128">Have generated output file names rely on published property values</span><span class="sxs-lookup"><span data-stu-id="798c5-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="798c5-129">Adding thumbnails to multibitrate MP4 output</span><span class="sxs-lookup"><span data-stu-id="798c5-129">Adding thumbnails to multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="798c5-130">Workflow overview to add thumbnails to</span><span class="sxs-lookup"><span data-stu-id="798c5-130">Workflow overview to add thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="798c5-131">Adding JPG Encoding</span><span class="sxs-lookup"><span data-stu-id="798c5-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="798c5-132">Dealing with Color Space conversion</span><span class="sxs-lookup"><span data-stu-id="798c5-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="798c5-133">Writing the thumbnails</span><span class="sxs-lookup"><span data-stu-id="798c5-133">Writing the thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="798c5-134">Detecting errors in a workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="798c5-135">Finished Workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="798c5-136">Time-based trimming of multibitrate MP4 output</span><span class="sxs-lookup"><span data-stu-id="798c5-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="798c5-137">Workflow overview to start adding trimming to</span><span class="sxs-lookup"><span data-stu-id="798c5-137">Workflow overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="798c5-138">Using the Stream Trimmer</span><span class="sxs-lookup"><span data-stu-id="798c5-138">Using the Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="798c5-139">Finished Workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="798c5-140">Introducing the Scripted Component</span><span class="sxs-lookup"><span data-stu-id="798c5-140">Introducing the Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="798c5-141">Scripting within a workflow: hello world</span><span class="sxs-lookup"><span data-stu-id="798c5-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="798c5-142">Frame-based trimming of multibitrate MP4 output</span><span class="sxs-lookup"><span data-stu-id="798c5-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="798c5-143">Blueprint overview to start adding trimming to</span><span class="sxs-lookup"><span data-stu-id="798c5-143">Blueprint overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="798c5-144">Using the Clip List XML</span><span class="sxs-lookup"><span data-stu-id="798c5-144">Using the Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="798c5-145">Modifying the clip list from a Scripted Component</span><span class="sxs-lookup"><span data-stu-id="798c5-145">Modifying the clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="798c5-146">Adding a ClippingEnabled convenience property</span><span class="sxs-lookup"><span data-stu-id="798c5-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a><span data-ttu-id="798c5-147">Encoding MXF into a single bitrate MP4</span><span class="sxs-lookup"><span data-stu-id="798c5-147">Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="798c5-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span><span class="sxs-lookup"><span data-stu-id="798c5-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <a id="MXF_to_MP4_start_new"></a><span data-ttu-id="798c5-149">Starting a new workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-149">Starting a new workflow</span></span>
<span data-ttu-id="798c5-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span><span class="sxs-lookup"><span data-stu-id="798c5-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="798c5-151">The new workflow will show 3 elements:</span><span class="sxs-lookup"><span data-stu-id="798c5-151">The new workflow will show 3 elements:</span></span>

* <span data-ttu-id="798c5-152">Primary Source File</span><span class="sxs-lookup"><span data-stu-id="798c5-152">Primary Source File</span></span>
* <span data-ttu-id="798c5-153">Clip List XML</span><span class="sxs-lookup"><span data-stu-id="798c5-153">Clip List XML</span></span>
* <span data-ttu-id="798c5-154">Output File/Asset</span><span class="sxs-lookup"><span data-stu-id="798c5-154">Output File/Asset</span></span>  

![New Encoding Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="798c5-156">*New Encoding Workflow*</span><span class="sxs-lookup"><span data-stu-id="798c5-156">*New Encoding Workflow*</span></span>

### <a id="MXF_to_MP4_with_file_input"></a><span data-ttu-id="798c5-157">Using the Media File Input</span><span class="sxs-lookup"><span data-stu-id="798c5-157">Using the Media File Input</span></span>
<span data-ttu-id="798c5-158">In order to accept our input media file, one starts with adding a Media File Input component.</span><span class="sxs-lookup"><span data-stu-id="798c5-158">In order to accept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="798c5-159">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span><span class="sxs-lookup"><span data-stu-id="798c5-159">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span> <span data-ttu-id="798c5-160">Do this for the Media File Input and connect the Primary Source File component to the Filename input pin from the Media File Input.</span><span class="sxs-lookup"><span data-stu-id="798c5-160">Do this for the Media File Input and connect the Primary Source File component to the Filename input pin from the Media File Input.</span></span>

![Connected Media File Input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="798c5-162">*Connected Media File Input*</span><span class="sxs-lookup"><span data-stu-id="798c5-162">*Connected Media File Input*</span></span>

<span data-ttu-id="798c5-163">Before we can do much else, we'll first need to indicate to the workflow designer what sample file we'd like to use to design our workflow with.</span><span class="sxs-lookup"><span data-stu-id="798c5-163">Before we can do much else, we'll first need to indicate to the workflow designer what sample file we'd like to use to design our workflow with.</span></span> <span data-ttu-id="798c5-164">To do so, click the designer pane background and look for the Primary Source File property on the right-hand property pane.</span><span class="sxs-lookup"><span data-stu-id="798c5-164">To do so, click the designer pane background and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="798c5-165">Click the folder icon and select the desired file to test the workflow with.</span><span class="sxs-lookup"><span data-stu-id="798c5-165">Click the folder icon and select the desired file to test the workflow with.</span></span> <span data-ttu-id="798c5-166">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file it inspected.</span><span class="sxs-lookup"><span data-stu-id="798c5-166">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file it inspected.</span></span>

![Populated Media File Input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="798c5-168">*Populated Media File Input*</span><span class="sxs-lookup"><span data-stu-id="798c5-168">*Populated Media File Input*</span></span>

<span data-ttu-id="798c5-169">While this specifies with what input we'd like to work with, it doesn't tell yet where the encoded output should go to.</span><span class="sxs-lookup"><span data-stu-id="798c5-169">While this specifies with what input we'd like to work with, it doesn't tell yet where the encoded output should go to.</span></span> <span data-ttu-id="798c5-170">Similar to how the Primary Source File was configured, now configure the Output Folder Variable property, just below it.</span><span class="sxs-lookup"><span data-stu-id="798c5-170">Similar to how the Primary Source File was configured, now configure the Output Folder Variable property, just below it.</span></span>

![Configured Input and Output properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="798c5-172">*Configured Input and Output properties*</span><span class="sxs-lookup"><span data-stu-id="798c5-172">*Configured Input and Output properties*</span></span>

### <a id="MXF_to_MP4_streams"></a><span data-ttu-id="798c5-173">Inspecting media streams</span><span class="sxs-lookup"><span data-stu-id="798c5-173">Inspecting media streams</span></span>
<span data-ttu-id="798c5-174">Often it's desired to know how the stream looks like that flows through the workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-174">Often it's desired to know how the stream looks like that flows through the workflow.</span></span> <span data-ttu-id="798c5-175">To inspect a stream at any point in the workflow, just click an output or input pin on any of the components.</span><span class="sxs-lookup"><span data-stu-id="798c5-175">To inspect a stream at any point in the workflow, just click an output or input pin on any of the components.</span></span> <span data-ttu-id="798c5-176">In this case, try clicking on the Uncompressed Video output pin from our Media File Input.</span><span class="sxs-lookup"><span data-stu-id="798c5-176">In this case, try clicking on the Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="798c5-177">A dialog will open up that allows to inspect the outbound video.</span><span class="sxs-lookup"><span data-stu-id="798c5-177">A dialog will open up that allows to inspect the outbound video.</span></span>

![Inspecting the Uncompressed Video output pin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="798c5-179">*Inspecting the Uncompressed Video output pin*</span><span class="sxs-lookup"><span data-stu-id="798c5-179">*Inspecting the Uncompressed Video output pin*</span></span>

<span data-ttu-id="798c5-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="798c5-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <a id="MXF_to_MP4_file_generation"></a><span data-ttu-id="798c5-181">Adding a video encoder for .MP4 file generation</span><span class="sxs-lookup"><span data-stu-id="798c5-181">Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="798c5-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span><span class="sxs-lookup"><span data-stu-id="798c5-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="798c5-183">In order to encode the inbound video, we need an encoding component - in this case for generating .MP4 files.</span><span class="sxs-lookup"><span data-stu-id="798c5-183">In order to encode the inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="798c5-184">To encode the video stream to H.264, add the AVC Video Encoder component to the designer surface.</span><span class="sxs-lookup"><span data-stu-id="798c5-184">To encode the video stream to H.264, add the AVC Video Encoder component to the designer surface.</span></span> <span data-ttu-id="798c5-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span><span class="sxs-lookup"><span data-stu-id="798c5-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Unconnected AVC Encoder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="798c5-187">*Unconnected AVC Encoder*</span><span class="sxs-lookup"><span data-stu-id="798c5-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="798c5-188">Its properties determine how the encoding exactly happens.</span><span class="sxs-lookup"><span data-stu-id="798c5-188">Its properties determine how the encoding exactly happens.</span></span> <span data-ttu-id="798c5-189">Let's have a look at some of the more important settings:</span><span class="sxs-lookup"><span data-stu-id="798c5-189">Let's have a look at some of the more important settings:</span></span>

* <span data-ttu-id="798c5-190">Output width and Output height: these determine the resolution of the encoded video.</span><span class="sxs-lookup"><span data-stu-id="798c5-190">Output width and Output height: these determine the resolution of the encoded video.</span></span> <span data-ttu-id="798c5-191">In our case let's go with 640x360</span><span class="sxs-lookup"><span data-stu-id="798c5-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="798c5-192">Frame Rate: when set to passthrough it will just adopt the source frame rate, it's possible to override this though.</span><span class="sxs-lookup"><span data-stu-id="798c5-192">Frame Rate: when set to passthrough it will just adopt the source frame rate, it's possible to override this though.</span></span> <span data-ttu-id="798c5-193">Note that such framerate conversion is not motion-compensated.</span><span class="sxs-lookup"><span data-stu-id="798c5-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="798c5-194">Profile and Level: these determine the AVC profile and level.</span><span class="sxs-lookup"><span data-stu-id="798c5-194">Profile and Level: these determine the AVC profile and level.</span></span> <span data-ttu-id="798c5-195">To conveniently get more information about the different levels and profiles, click the question mark icon on the AVC Video Encoder component and the help page will show more detail about each of the levels.</span><span class="sxs-lookup"><span data-stu-id="798c5-195">To conveniently get more information about the different levels and profiles, click the question mark icon on the AVC Video Encoder component and the help page will show more detail about each of the levels.</span></span> <span data-ttu-id="798c5-196">For our sample, let's go with Main Profile at level 3.2 (the default).</span><span class="sxs-lookup"><span data-stu-id="798c5-196">For our sample, let's go with Main Profile at level 3.2 (the default).</span></span>
* <span data-ttu-id="798c5-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span><span class="sxs-lookup"><span data-stu-id="798c5-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="798c5-198">Video Format: this is about the VUI (Video Usability Information) that gets written into the H.264 stream (side information that might be used by a decoder to enhance the display but not essential to correctly decode):</span><span class="sxs-lookup"><span data-stu-id="798c5-198">Video Format: this is about the VUI (Video Usability Information) that gets written into the H.264 stream (side information that might be used by a decoder to enhance the display but not essential to correctly decode):</span></span>
* <span data-ttu-id="798c5-199">NTSC (typical for US or Japan, using 30 fps)</span><span class="sxs-lookup"><span data-stu-id="798c5-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="798c5-200">PAL (typical for Europe, using 25 fps)</span><span class="sxs-lookup"><span data-stu-id="798c5-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="798c5-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span><span class="sxs-lookup"><span data-stu-id="798c5-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="798c5-202">This ensures compatibility with the dynamic packaging Azure Media Services provides.</span><span class="sxs-lookup"><span data-stu-id="798c5-202">This ensures compatibility with the dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="798c5-203">To feed our AVC encoder, connect the Uncompressed Video output pin from the Media File Input component to the Uncompressed Video input pin from the AVC encoder.</span><span class="sxs-lookup"><span data-stu-id="798c5-203">To feed our AVC encoder, connect the Uncompressed Video output pin from the Media File Input component to the Uncompressed Video input pin from the AVC encoder.</span></span>

![Connected AVC Encoder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="798c5-205">*Connected AVC Main encoder*</span><span class="sxs-lookup"><span data-stu-id="798c5-205">*Connected AVC Main encoder*</span></span>

### <a id="MXF_to_MP4_audio"></a><span data-ttu-id="798c5-206">Encoding the audio stream</span><span class="sxs-lookup"><span data-stu-id="798c5-206">Encoding the audio stream</span></span>
<span data-ttu-id="798c5-207">At this point, we have encoded video but the original uncompressed audio stream still needs to be compressed.</span><span class="sxs-lookup"><span data-stu-id="798c5-207">At this point, we have encoded video but the original uncompressed audio stream still needs to be compressed.</span></span> <span data-ttu-id="798c5-208">For this we'll go with AAC encoding by the AAC Encoder (Dolby) component.</span><span class="sxs-lookup"><span data-stu-id="798c5-208">For this we'll go with AAC encoding by the AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="798c5-209">Add it to the workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-209">Add it to the workflow.</span></span>

![Unconnected AVC Encoder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="798c5-211">*Unconnected AAC encoder*</span><span class="sxs-lookup"><span data-stu-id="798c5-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="798c5-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from the AAC Encoder while more than likely the Media File Input will have two different uncompressed audio stream available: one for the left audio channel and one for the right.</span><span class="sxs-lookup"><span data-stu-id="798c5-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from the AAC Encoder while more than likely the Media File Input will have two different uncompressed audio stream available: one for the left audio channel and one for the right.</span></span> <span data-ttu-id="798c5-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible to directly connect the audio from the Media File Input source into the AAC audio encoder.</span><span class="sxs-lookup"><span data-stu-id="798c5-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible to directly connect the audio from the Media File Input source into the AAC audio encoder.</span></span> <span data-ttu-id="798c5-214">The AAC component expects a so-called "interleaved" audio stream: a single stream that has both the left and the right channels interleaved with each other.</span><span class="sxs-lookup"><span data-stu-id="798c5-214">The AAC component expects a so-called "interleaved" audio stream: a single stream that has both the left and the right channels interleaved with each other.</span></span> <span data-ttu-id="798c5-215">Once we know from our source media file which audio tracks are on what position in the source, we can generate such interleaved audio stream with the correctly assigned speaker positions for left and right.</span><span class="sxs-lookup"><span data-stu-id="798c5-215">Once we know from our source media file which audio tracks are on what position in the source, we can generate such interleaved audio stream with the correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="798c5-216">First one will want to generated an interleaved stream from the required source audio channels.</span><span class="sxs-lookup"><span data-stu-id="798c5-216">First one will want to generated an interleaved stream from the required source audio channels.</span></span> <span data-ttu-id="798c5-217">The Audio Stream Interleaver component will handle this for us.</span><span class="sxs-lookup"><span data-stu-id="798c5-217">The Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="798c5-218">Add it to the workflow and connect the audio outputs from the Media File Input into it.</span><span class="sxs-lookup"><span data-stu-id="798c5-218">Add it to the workflow and connect the audio outputs from the Media File Input into it.</span></span>

![Connected Audio Stream Interleaver](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="798c5-220">*Connected Audio Stream Interleaver*</span><span class="sxs-lookup"><span data-stu-id="798c5-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="798c5-221">Now that we have an interleaved audio stream, we still didn't specify where to assign the left or right speaker positions to.</span><span class="sxs-lookup"><span data-stu-id="798c5-221">Now that we have an interleaved audio stream, we still didn't specify where to assign the left or right speaker positions to.</span></span> <span data-ttu-id="798c5-222">In order to specify this, we can leverage the Speaker Position Assigner.</span><span class="sxs-lookup"><span data-stu-id="798c5-222">In order to specify this, we can leverage the Speaker Position Assigner.</span></span>

![Adding a Speaker Position Assigner](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="798c5-224">*Adding a Speaker Position Assigner*</span><span class="sxs-lookup"><span data-stu-id="798c5-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="798c5-225">Configure the Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and the Channel Preset called "2.0 (L,R)".</span><span class="sxs-lookup"><span data-stu-id="798c5-225">Configure the Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and the Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="798c5-226">(This will assign the left speaker position to channel 1 and the right speaker position to channel 2.)</span><span class="sxs-lookup"><span data-stu-id="798c5-226">(This will assign the left speaker position to channel 1 and the right speaker position to channel 2.)</span></span>

<span data-ttu-id="798c5-227">Connect the output of the Speaker Position Assigner to the input of the AAC Encoder.</span><span class="sxs-lookup"><span data-stu-id="798c5-227">Connect the output of the Speaker Position Assigner to the input of the AAC Encoder.</span></span> <span data-ttu-id="798c5-228">Then, tell the AAC Encoder to work with a "2.0 (L,R)" Channel Preset, so it knows to deal with stereo audio as input.</span><span class="sxs-lookup"><span data-stu-id="798c5-228">Then, tell the AAC Encoder to work with a "2.0 (L,R)" Channel Preset, so it knows to deal with stereo audio as input.</span></span>

### <a id="MXF_to_MP4_audio_and_fideo"></a><span data-ttu-id="798c5-229">Multiplexing Audio and Video streams into an MP4 container</span><span class="sxs-lookup"><span data-stu-id="798c5-229">Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="798c5-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span><span class="sxs-lookup"><span data-stu-id="798c5-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="798c5-231">The process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span><span class="sxs-lookup"><span data-stu-id="798c5-231">The process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="798c5-232">In this case we're interleaving the audio and the video streams in a single coherent .MP4 package.</span><span class="sxs-lookup"><span data-stu-id="798c5-232">In this case we're interleaving the audio and the video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="798c5-233">The component that coordinates this for an .MP4 container is called the ISO MPEG-4 Multiplexer.</span><span class="sxs-lookup"><span data-stu-id="798c5-233">The component that coordinates this for an .MP4 container is called the ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="798c5-234">Add one to the designer surface and connect both the AVC Video Encoder and the AAC Encoder to its inputs.</span><span class="sxs-lookup"><span data-stu-id="798c5-234">Add one to the designer surface and connect both the AVC Video Encoder and the AAC Encoder to its inputs.</span></span>

![Connected MPEG4 Multiplexer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="798c5-236">*Connected MPEG4 Multiplexer*</span><span class="sxs-lookup"><span data-stu-id="798c5-236">*Connected MPEG4 Multiplexer*</span></span>

### <a id="MXF_to_MP4_writing_mp4"></a><span data-ttu-id="798c5-237">Writing the MP4 file</span><span class="sxs-lookup"><span data-stu-id="798c5-237">Writing the MP4 file</span></span>
<span data-ttu-id="798c5-238">When writing an output file, the File Output component is used.</span><span class="sxs-lookup"><span data-stu-id="798c5-238">When writing an output file, the File Output component is used.</span></span> <span data-ttu-id="798c5-239">We can connect this to the output of the ISO MPEG-4 Multiplexer so that its output gets written to disk.</span><span class="sxs-lookup"><span data-stu-id="798c5-239">We can connect this to the output of the ISO MPEG-4 Multiplexer so that its output gets written to disk.</span></span> <span data-ttu-id="798c5-240">To do this, connect the Container (MPEG-4) output pin to the Write input pin of the File Output.</span><span class="sxs-lookup"><span data-stu-id="798c5-240">To do this, connect the Container (MPEG-4) output pin to the Write input pin of the File Output.</span></span>

![Connected File Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="798c5-242">*Connected File Output*</span><span class="sxs-lookup"><span data-stu-id="798c5-242">*Connected File Output*</span></span>

<span data-ttu-id="798c5-243">The filename that will be used is determined by the File property.</span><span class="sxs-lookup"><span data-stu-id="798c5-243">The filename that will be used is determined by the File property.</span></span> <span data-ttu-id="798c5-244">While that property can be hardcoded to a given value, most likely one will want to set it through an expression instead.</span><span class="sxs-lookup"><span data-stu-id="798c5-244">While that property can be hardcoded to a given value, most likely one will want to set it through an expression instead.</span></span>

<span data-ttu-id="798c5-245">To have the workflow automatically determine the output File name property from an expression, click the buton next to the File name (next to the folder icon).</span><span class="sxs-lookup"><span data-stu-id="798c5-245">To have the workflow automatically determine the output File name property from an expression, click the buton next to the File name (next to the folder icon).</span></span> <span data-ttu-id="798c5-246">From the drop down menu then select "Expression".</span><span class="sxs-lookup"><span data-stu-id="798c5-246">From the drop down menu then select "Expression".</span></span> <span data-ttu-id="798c5-247">This will bring up the expression editor.</span><span class="sxs-lookup"><span data-stu-id="798c5-247">This will bring up the expression editor.</span></span> <span data-ttu-id="798c5-248">Clear the contents of the editor first.</span><span class="sxs-lookup"><span data-stu-id="798c5-248">Clear the contents of the editor first.</span></span>

![Empty Expression Editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="798c5-250">*Empty Expression Editor*</span><span class="sxs-lookup"><span data-stu-id="798c5-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="798c5-251">The expression editor allows to enter any literal value, mixed with one or more variables.</span><span class="sxs-lookup"><span data-stu-id="798c5-251">The expression editor allows to enter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="798c5-252">Variables start with a dollar sign.</span><span class="sxs-lookup"><span data-stu-id="798c5-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="798c5-253">As you hit the $ key, the editor will show a dropdown box with a choice of available variables.</span><span class="sxs-lookup"><span data-stu-id="798c5-253">As you hit the $ key, the editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="798c5-254">In our case we'll use a combination of the output directory variable and the base input file name variable:</span><span class="sxs-lookup"><span data-stu-id="798c5-254">In our case we'll use a combination of the output directory variable and the base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Filled out Expression Editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="798c5-256">*Filled out Expression Editor*</span><span class="sxs-lookup"><span data-stu-id="798c5-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="798c5-257">In order to see see an output file of your encoding job in Azure, you must provide a value in the expression editor.</span><span class="sxs-lookup"><span data-stu-id="798c5-257">In order to see see an output file of your encoding job in Azure, you must provide a value in the expression editor.</span></span>
>
>

<span data-ttu-id="798c5-258">When you confirm the expression by hitting ok, the property window will preview to what value the File property resolves at this point in time.</span><span class="sxs-lookup"><span data-stu-id="798c5-258">When you confirm the expression by hitting ok, the property window will preview to what value the File property resolves at this point in time.</span></span>

![File Expression resolves output dir](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="798c5-260">*File Expression resolves output dir*</span><span class="sxs-lookup"><span data-stu-id="798c5-260">*File Expression resolves output dir*</span></span>

### <a id="MXF_to_MP4_asset_from_output"></a><span data-ttu-id="798c5-261">Creating a Media Services Asset from the output file</span><span class="sxs-lookup"><span data-stu-id="798c5-261">Creating a Media Services Asset from the output file</span></span>
<span data-ttu-id="798c5-262">While we have written an MP4 output file, we still need to indicate that this file belongs to the output asset which media services will generate as a result of executing this workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-262">While we have written an MP4 output file, we still need to indicate that this file belongs to the output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="798c5-263">To this end, the Output File/Asset node on the workflow canvas is used.</span><span class="sxs-lookup"><span data-stu-id="798c5-263">To this end, the Output File/Asset node on the workflow canvas is used.</span></span> <span data-ttu-id="798c5-264">All incoming files into this node will make part of the resulting Azure Media Services asset.</span><span class="sxs-lookup"><span data-stu-id="798c5-264">All incoming files into this node will make part of the resulting Azure Media Services asset.</span></span>

<span data-ttu-id="798c5-265">Connect the File Output component to the Output File/Asset component to finish the workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-265">Connect the File Output component to the Output File/Asset component to finish the workflow.</span></span>

![Finished Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="798c5-267">*Finished Workflow*</span><span class="sxs-lookup"><span data-stu-id="798c5-267">*Finished Workflow*</span></span>

### <a id="MXF_to_MP4_test"></a><span data-ttu-id="798c5-268">Test the finished workflow locally</span><span class="sxs-lookup"><span data-stu-id="798c5-268">Test the finished workflow locally</span></span>
<span data-ttu-id="798c5-269">To test the workflow locally, hit the play button in the toolbar at the top.</span><span class="sxs-lookup"><span data-stu-id="798c5-269">To test the workflow locally, hit the play button in the toolbar at the top.</span></span> <span data-ttu-id="798c5-270">When the workflow finished executing, inspect the output generated in the configured output folder.</span><span class="sxs-lookup"><span data-stu-id="798c5-270">When the workflow finished executing, inspect the output generated in the configured output folder.</span></span> <span data-ttu-id="798c5-271">You'll see the finished MP4 output file that was encoded from the MXF input source file.</span><span class="sxs-lookup"><span data-stu-id="798c5-271">You'll see the finished MP4 output file that was encoded from the MXF input source file.</span></span>

## <a id="MXF_to_MP4_with_dyn_packaging"></a><span data-ttu-id="798c5-272">Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span><span class="sxs-lookup"><span data-stu-id="798c5-272">Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="798c5-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span><span class="sxs-lookup"><span data-stu-id="798c5-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="798c5-274">When a multi-bitrate asset output is desired for use in combination with the Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need to be generated.</span><span class="sxs-lookup"><span data-stu-id="798c5-274">When a multi-bitrate asset output is desired for use in combination with the Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need to be generated.</span></span> <span data-ttu-id="798c5-275">To do so, the [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span><span class="sxs-lookup"><span data-stu-id="798c5-275">To do so, the [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Starting Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="798c5-277">*Starting Workflow*</span><span class="sxs-lookup"><span data-stu-id="798c5-277">*Starting Workflow*</span></span>

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a><span data-ttu-id="798c5-278">Adding one or more additional MP4 outputs</span><span class="sxs-lookup"><span data-stu-id="798c5-278">Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="798c5-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span><span class="sxs-lookup"><span data-stu-id="798c5-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="798c5-280">Let's add one or more MP4 output files to the workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-280">Let's add one or more MP4 output files to the workflow.</span></span>

<span data-ttu-id="798c5-281">To make sure we have all our video encoders created with the same settings, it's most convenient to duplicate the already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span><span class="sxs-lookup"><span data-stu-id="798c5-281">To make sure we have all our video encoders created with the same settings, it's most convenient to duplicate the already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="798c5-282">To duplicate the existing encoder, copy paste it on the designer surface.</span><span class="sxs-lookup"><span data-stu-id="798c5-282">To duplicate the existing encoder, copy paste it on the designer surface.</span></span>

<span data-ttu-id="798c5-283">Connect the Uncompressed Video output pin of the Media File Input into our new AVC component.</span><span class="sxs-lookup"><span data-stu-id="798c5-283">Connect the Uncompressed Video output pin of the Media File Input into our new AVC component.</span></span>

![Second AVC encoder connected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="798c5-285">*Second AVC encoder connected*</span><span class="sxs-lookup"><span data-stu-id="798c5-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="798c5-286">Now adapt the configuration for our new AVC encoder to output 960x540 at 2,5 Mbps.</span><span class="sxs-lookup"><span data-stu-id="798c5-286">Now adapt the configuration for our new AVC encoder to output 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="798c5-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span><span class="sxs-lookup"><span data-stu-id="798c5-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="798c5-288">Given we want to use the resulting asset together with Azure Media Services' dynamic packaging, the streaming endpoint needs to be capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned to each other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span><span class="sxs-lookup"><span data-stu-id="798c5-288">Given we want to use the resulting asset together with Azure Media Services' dynamic packaging, the streaming endpoint needs to be capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned to each other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="798c5-289">To make that happen, we need to ensure that, in the properties of both AVC encoders the GOP ("group of pictures") size for both MP4 files is set to 2 seconds, which can be done by:</span><span class="sxs-lookup"><span data-stu-id="798c5-289">To make that happen, we need to ensure that, in the properties of both AVC encoders the GOP ("group of pictures") size for both MP4 files is set to 2 seconds, which can be done by:</span></span>

* <span data-ttu-id="798c5-290">setting the GOP Size Mode to Fixed GOP size and</span><span class="sxs-lookup"><span data-stu-id="798c5-290">setting the GOP Size Mode to Fixed GOP size and</span></span>
* <span data-ttu-id="798c5-291">the Key Frame Interval to two seconds.</span><span class="sxs-lookup"><span data-stu-id="798c5-291">the Key Frame Interval to two seconds.</span></span>
* <span data-ttu-id="798c5-292">also set the GOP IDR Control to Closed GOP to ensure all GOP's are standing on their own without dependencies</span><span class="sxs-lookup"><span data-stu-id="798c5-292">also set the GOP IDR Control to Closed GOP to ensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="798c5-293">To make our workflow convenient to understand, rename the first AVC encoder to "AVC Video Encoder 640x360 1200kbps" and the second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span><span class="sxs-lookup"><span data-stu-id="798c5-293">To make our workflow convenient to understand, rename the first AVC encoder to "AVC Video Encoder 640x360 1200kbps" and the second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="798c5-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span><span class="sxs-lookup"><span data-stu-id="798c5-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="798c5-295">Connect the multiplexer to the new AVC encoder and make sure its output is directed into the File Output.</span><span class="sxs-lookup"><span data-stu-id="798c5-295">Connect the multiplexer to the new AVC encoder and make sure its output is directed into the File Output.</span></span> <span data-ttu-id="798c5-296">Then also connect the AAC audio encoder output to the new multiplexer's input.</span><span class="sxs-lookup"><span data-stu-id="798c5-296">Then also connect the AAC audio encoder output to the new multiplexer's input.</span></span> <span data-ttu-id="798c5-297">The File Output in turn can then be connected to the Output File/Asset node to add it to the Media Services Asset that will be created.</span><span class="sxs-lookup"><span data-stu-id="798c5-297">The File Output in turn can then be connected to the Output File/Asset node to add it to the Media Services Asset that will be created.</span></span>

![Second Muxer and File Output connected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="798c5-299">*Second Muxer and File Output connected*</span><span class="sxs-lookup"><span data-stu-id="798c5-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="798c5-300">For compatibility with Azure Media Services dynamic packaging, configure the multiplexer's Chunk Mode to GOP count or duration and set the GOPs per chunk to 1.</span><span class="sxs-lookup"><span data-stu-id="798c5-300">For compatibility with Azure Media Services dynamic packaging, configure the multiplexer's Chunk Mode to GOP count or duration and set the GOPs per chunk to 1.</span></span> <span data-ttu-id="798c5-301">(This should be the default.)</span><span class="sxs-lookup"><span data-stu-id="798c5-301">(This should be the default.)</span></span>

![Muxer Chunk Modes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="798c5-303">*Muxer Chunk Modes*</span><span class="sxs-lookup"><span data-stu-id="798c5-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="798c5-304">Note: you may want to repeat this process for any other bitrate and resolution combinations you want to have added to the asset output.</span><span class="sxs-lookup"><span data-stu-id="798c5-304">Note: you may want to repeat this process for any other bitrate and resolution combinations you want to have added to the asset output.</span></span>

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a><span data-ttu-id="798c5-305">Configuring the file output names</span><span class="sxs-lookup"><span data-stu-id="798c5-305">Configuring the file output names</span></span>
<span data-ttu-id="798c5-306">We have more than one single file added to the output asset.</span><span class="sxs-lookup"><span data-stu-id="798c5-306">We have more than one single file added to the output asset.</span></span> <span data-ttu-id="798c5-307">This provides a need to make sure the filenames for each of the output files are different from each other and maybe even apply a file-naming convention so it becomes clear from the file name what you're dealing with.</span><span class="sxs-lookup"><span data-stu-id="798c5-307">This provides a need to make sure the filenames for each of the output files are different from each other and maybe even apply a file-naming convention so it becomes clear from the file name what you're dealing with.</span></span>

<span data-ttu-id="798c5-308">File output naming can be controlled through expressions in the designer.</span><span class="sxs-lookup"><span data-stu-id="798c5-308">File output naming can be controlled through expressions in the designer.</span></span> <span data-ttu-id="798c5-309">Open the property pane for one of the File Output components and open the expression editor for the File property.</span><span class="sxs-lookup"><span data-stu-id="798c5-309">Open the property pane for one of the File Output components and open the expression editor for the File property.</span></span> <span data-ttu-id="798c5-310">Our first output file was configured through the following expression (see the tutorial for going from [MXF to a single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="798c5-310">Our first output file was configured through the following expression (see the tutorial for going from [MXF to a single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="798c5-311">This means that our filename is determined by two variables: the output directory to write in and the source file base name.</span><span class="sxs-lookup"><span data-stu-id="798c5-311">This means that our filename is determined by two variables: the output directory to write in and the source file base name.</span></span> <span data-ttu-id="798c5-312">The former is exposed as a property on the workflow root and the latter is determined by the incoming file.</span><span class="sxs-lookup"><span data-stu-id="798c5-312">The former is exposed as a property on the workflow root and the latter is determined by the incoming file.</span></span> <span data-ttu-id="798c5-313">Note that the output directory is what you use for local testing; this property will be overridden by the workflow engine when the workflow is executed by the cloud-based media processor in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="798c5-313">Note that the output directory is what you use for local testing; this property will be overridden by the workflow engine when the workflow is executed by the cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="798c5-314">To give both our output files a consistent output naming, change the first file naming expression to:</span><span class="sxs-lookup"><span data-stu-id="798c5-314">To give both our output files a consistent output naming, change the first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="798c5-315">and the second to:</span><span class="sxs-lookup"><span data-stu-id="798c5-315">and the second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="798c5-316">Execute an intermediate test run to make sure both MP4 output files are properly generated.</span><span class="sxs-lookup"><span data-stu-id="798c5-316">Execute an intermediate test run to make sure both MP4 output files are properly generated.</span></span>

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a><span data-ttu-id="798c5-317">Adding a separate Audio Track</span><span class="sxs-lookup"><span data-stu-id="798c5-317">Adding a separate Audio Track</span></span>
<span data-ttu-id="798c5-318">As we'll see later when we generate an .ism file to go with our MP4 output files, we will also require a audio-only MP4 file as the audio track for our adaptive streaming.</span><span class="sxs-lookup"><span data-stu-id="798c5-318">As we'll see later when we generate an .ism file to go with our MP4 output files, we will also require a audio-only MP4 file as the audio track for our adaptive streaming.</span></span> <span data-ttu-id="798c5-319">To create this file, add an additional muxer to the workflow (ISO-MPEG-4 Multiplexer) and connect the AAC encoder's output pin with its input pin for Track 1.</span><span class="sxs-lookup"><span data-stu-id="798c5-319">To create this file, add an additional muxer to the workflow (ISO-MPEG-4 Multiplexer) and connect the AAC encoder's output pin with its input pin for Track 1.</span></span>

![Audio Muxer Added](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="798c5-321">*Audio Muxer Added*</span><span class="sxs-lookup"><span data-stu-id="798c5-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="798c5-322">Create a third File Output component to output the outbound stream from the muxer and configure the file naming expression as:</span><span class="sxs-lookup"><span data-stu-id="798c5-322">Create a third File Output component to output the outbound stream from the muxer and configure the file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Audio Muxer creating File Output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="798c5-324">*Audio Muxer creating File Output*</span><span class="sxs-lookup"><span data-stu-id="798c5-324">*Audio Muxer creating File Output*</span></span>

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a><span data-ttu-id="798c5-325">Adding the .ISM SMIL File</span><span class="sxs-lookup"><span data-stu-id="798c5-325">Adding the .ISM SMIL File</span></span>
<span data-ttu-id="798c5-326">For the dynamic packaging to work in combination with both MP4 files (and the audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span><span class="sxs-lookup"><span data-stu-id="798c5-326">For the dynamic packaging to work in combination with both MP4 files (and the audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="798c5-327">This file indicates to Azure Media Services what MP4 files are available for dynamic packaging and which of those to consider for the audio streaming.</span><span class="sxs-lookup"><span data-stu-id="798c5-327">This file indicates to Azure Media Services what MP4 files are available for dynamic packaging and which of those to consider for the audio streaming.</span></span> <span data-ttu-id="798c5-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span><span class="sxs-lookup"><span data-stu-id="798c5-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="798c5-329">The .ism file contains within a switch statement, a reference to each of the individual MP4 video files and in addition to those also one (or more) audio file references to an MP4 that only contains the audio.</span><span class="sxs-lookup"><span data-stu-id="798c5-329">The .ism file contains within a switch statement, a reference to each of the individual MP4 video files and in addition to those also one (or more) audio file references to an MP4 that only contains the audio.</span></span>

<span data-ttu-id="798c5-330">Generating the manifest file for our set of MP4's can be done through a component called the "AMS Manifest Writer".</span><span class="sxs-lookup"><span data-stu-id="798c5-330">Generating the manifest file for our set of MP4's can be done through a component called the "AMS Manifest Writer".</span></span> <span data-ttu-id="798c5-331">To use it, drag it onto the surface and connect the "Write Complete" output pins from the three File Output components to the AMS Manifest Writer input.</span><span class="sxs-lookup"><span data-stu-id="798c5-331">To use it, drag it onto the surface and connect the "Write Complete" output pins from the three File Output components to the AMS Manifest Writer input.</span></span> <span data-ttu-id="798c5-332">Then make sure to connect the output of the AMS Manifest Writer to the Output File/Asset.</span><span class="sxs-lookup"><span data-stu-id="798c5-332">Then make sure to connect the output of the AMS Manifest Writer to the Output File/Asset.</span></span>

<span data-ttu-id="798c5-333">As with our other file output components, configure the .ism file output name with an expression:</span><span class="sxs-lookup"><span data-stu-id="798c5-333">As with our other file output components, configure the .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="798c5-334">Our finished workflow looks like the below:</span><span class="sxs-lookup"><span data-stu-id="798c5-334">Our finished workflow looks like the below:</span></span>

![Finished MXF to multibitrate MP4 workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="798c5-336">*Finished MXF to multibitrate MP4 workflow*</span><span class="sxs-lookup"><span data-stu-id="798c5-336">*Finished MXF to multibitrate MP4 workflow*</span></span>

## <a id="MXF_to__multibitrate_MP4"></a><span data-ttu-id="798c5-337">Encoding MXF into multibitrate MP4 - enhanced blueprint</span><span class="sxs-lookup"><span data-stu-id="798c5-337">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="798c5-338">In the [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span><span class="sxs-lookup"><span data-stu-id="798c5-338">In the [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="798c5-339">This walkthrough will show how some of the aspects can be enhanced and made more convenient.</span><span class="sxs-lookup"><span data-stu-id="798c5-339">This walkthrough will show how some of the aspects can be enhanced and made more convenient.</span></span>

### <a id="MXF_to_multibitrate_MP4_overview"></a><span data-ttu-id="798c5-340">Workflow overview to enhance</span><span class="sxs-lookup"><span data-stu-id="798c5-340">Workflow overview to enhance</span></span>
![Multibitrate MP4 workflow to enhance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="798c5-342">*Multibitrate MP4 workflow to enhance*</span><span class="sxs-lookup"><span data-stu-id="798c5-342">*Multibitrate MP4 workflow to enhance*</span></span>

### <a id="MXF_to__multibitrate_MP4_file_naming"></a><span data-ttu-id="798c5-343">File Naming Conventions</span><span class="sxs-lookup"><span data-stu-id="798c5-343">File Naming Conventions</span></span>
<span data-ttu-id="798c5-344">In the previous workflow we specified a simple expression as the basis for generating output file names.</span><span class="sxs-lookup"><span data-stu-id="798c5-344">In the previous workflow we specified a simple expression as the basis for generating output file names.</span></span> <span data-ttu-id="798c5-345">We have some duplication though: all of the the individual output file components specified such expression.</span><span class="sxs-lookup"><span data-stu-id="798c5-345">We have some duplication though: all of the the individual output file components specified such expression.</span></span>

<span data-ttu-id="798c5-346">For example, our file output component for the first video file is configured with this expression:</span><span class="sxs-lookup"><span data-stu-id="798c5-346">For example, our file output component for the first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="798c5-347">While for the second output video, we have an expression like:</span><span class="sxs-lookup"><span data-stu-id="798c5-347">While for the second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="798c5-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span><span class="sxs-lookup"><span data-stu-id="798c5-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="798c5-349">Luckily we can: the designer's expression capabilities in combination with the ability to create custom properties on our workflow root will give us an added layer of convenience.</span><span class="sxs-lookup"><span data-stu-id="798c5-349">Luckily we can: the designer's expression capabilities in combination with the ability to create custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="798c5-350">Let's assume we'll drive filename configuration from the bitrates of the individual MP4 files.</span><span class="sxs-lookup"><span data-stu-id="798c5-350">Let's assume we'll drive filename configuration from the bitrates of the individual MP4 files.</span></span> <span data-ttu-id="798c5-351">These bitrates we'll aim to configure in one central place (on the root of our graph), from where they'll be accessed to configure and drive file name generation.</span><span class="sxs-lookup"><span data-stu-id="798c5-351">These bitrates we'll aim to configure in one central place (on the root of our graph), from where they'll be accessed to configure and drive file name generation.</span></span> <span data-ttu-id="798c5-352">To do this, we start by publishing the bitrate property from both AVC encoders to the root of our workflow, so that it becomes accessible from both the root as well as from the AVC encoders.</span><span class="sxs-lookup"><span data-stu-id="798c5-352">To do this, we start by publishing the bitrate property from both AVC encoders to the root of our workflow, so that it becomes accessible from both the root as well as from the AVC encoders.</span></span> <span data-ttu-id="798c5-353">(Even if displayed in two different spots, there's only one underlying value.)</span><span class="sxs-lookup"><span data-stu-id="798c5-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <a id="MXF_to__multibitrate_MP4_publishing"></a><span data-ttu-id="798c5-354">Publishing component properties onto the workflow root</span><span class="sxs-lookup"><span data-stu-id="798c5-354">Publishing component properties onto the workflow root</span></span>
<span data-ttu-id="798c5-355">Open the first AVC encoder, go to the Bitrate (kbps) property and from the dropdown choose Publish.</span><span class="sxs-lookup"><span data-stu-id="798c5-355">Open the first AVC encoder, go to the Bitrate (kbps) property and from the dropdown choose Publish.</span></span>

![Publishing the bitrate property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="798c5-357">*Publishing the bitrate property*</span><span class="sxs-lookup"><span data-stu-id="798c5-357">*Publishing the bitrate property*</span></span>

<span data-ttu-id="798c5-358">Configure the publish dialog to publish to the root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span><span class="sxs-lookup"><span data-stu-id="798c5-358">Configure the publish dialog to publish to the root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="798c5-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span><span class="sxs-lookup"><span data-stu-id="798c5-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Publishing the bitrate property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="798c5-361">*Publishing dialog for bitrate property*</span><span class="sxs-lookup"><span data-stu-id="798c5-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="798c5-362">Repeat the same for the bitrate property of the second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in the same custom group "Streaming Bitrates".</span><span class="sxs-lookup"><span data-stu-id="798c5-362">Repeat the same for the bitrate property of the second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in the same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="798c5-363">If we now inspect the workflow root properties, we'll see our custom group with the two published properties show up.</span><span class="sxs-lookup"><span data-stu-id="798c5-363">If we now inspect the workflow root properties, we'll see our custom group with the two published properties show up.</span></span> <span data-ttu-id="798c5-364">Both are reflecting the value of their respective AVC encoder bitrate.</span><span class="sxs-lookup"><span data-stu-id="798c5-364">Both are reflecting the value of their respective AVC encoder bitrate.</span></span>

![Published bitrate props on workflow root](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="798c5-366">Whenever we want to access these properties from code or from an expression, we can do so like this:</span><span class="sxs-lookup"><span data-stu-id="798c5-366">Whenever we want to access these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="798c5-367">from inline code from a component right below the root: node.getPropertyAsString('../video1bitrate',null)</span><span class="sxs-lookup"><span data-stu-id="798c5-367">from inline code from a component right below the root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="798c5-368">within an expression: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="798c5-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="798c5-369">Let's complete the "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span><span class="sxs-lookup"><span data-stu-id="798c5-369">Let's complete the "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="798c5-370">Within the properties of the AAC Encoder, search for the Bitrate setting and select Publish from the dropdown next to it.</span><span class="sxs-lookup"><span data-stu-id="798c5-370">Within the properties of the AAC Encoder, search for the Bitrate setting and select Publish from the dropdown next to it.</span></span> <span data-ttu-id="798c5-371">Publish to the root of the graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span><span class="sxs-lookup"><span data-stu-id="798c5-371">Publish to the root of the graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Publishing dialog for audio bitrate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="798c5-373">*Publishing dialog for audio bitrate*</span><span class="sxs-lookup"><span data-stu-id="798c5-373">*Publishing dialog for audio bitrate*</span></span>

![Resulting video and audio props on root](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="798c5-375">*Resulting video and audio props on root*</span><span class="sxs-lookup"><span data-stu-id="798c5-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="798c5-376">Note that changing any of those three values also re-configures and changes the values on the respective components they are linked with (and where published from).</span><span class="sxs-lookup"><span data-stu-id="798c5-376">Note that changing any of those three values also re-configures and changes the values on the respective components they are linked with (and where published from).</span></span>

### <a id="MXF_to__multibitrate_MP4_output_files"></a><span data-ttu-id="798c5-377">Have generated output file names rely on published property values</span><span class="sxs-lookup"><span data-stu-id="798c5-377">Have generated output file names rely on published property values</span></span>
<span data-ttu-id="798c5-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of the File Output components to rely on the bitrate properties we just published on the graph root.</span><span class="sxs-lookup"><span data-stu-id="798c5-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of the File Output components to rely on the bitrate properties we just published on the graph root.</span></span> <span data-ttu-id="798c5-379">Starting with our first file output, find the File property and edit the expression like this:</span><span class="sxs-lookup"><span data-stu-id="798c5-379">Starting with our first file output, find the File property and edit the expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="798c5-380">The different parameters in this expression can be accessed and entered by hitting the dollar sign on the keyboard while in the expression window.</span><span class="sxs-lookup"><span data-stu-id="798c5-380">The different parameters in this expression can be accessed and entered by hitting the dollar sign on the keyboard while in the expression window.</span></span> <span data-ttu-id="798c5-381">One of the available parameters is our video1bitrate property which we published earlier.</span><span class="sxs-lookup"><span data-stu-id="798c5-381">One of the available parameters is our video1bitrate property which we published earlier.</span></span>

![Accessing parameters within an expression](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="798c5-383">*Accessing parameters within an expression*</span><span class="sxs-lookup"><span data-stu-id="798c5-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="798c5-384">Do the same for the file output for our second video:</span><span class="sxs-lookup"><span data-stu-id="798c5-384">Do the same for the file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="798c5-385">and for the audio-only file output:</span><span class="sxs-lookup"><span data-stu-id="798c5-385">and for the audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="798c5-386">If we now change the bitrate for any of the video or audio files, the respective encoder will be reconfigured and the bitrate-based file name convention will be honored all automatic.</span><span class="sxs-lookup"><span data-stu-id="798c5-386">If we now change the bitrate for any of the video or audio files, the respective encoder will be reconfigured and the bitrate-based file name convention will be honored all automatic.</span></span>

## <a id="thumbnails_to__multibitrate_MP4"></a><span data-ttu-id="798c5-387">Adding thumbnails to multibitrate MP4 output</span><span class="sxs-lookup"><span data-stu-id="798c5-387">Adding thumbnails to multibitrate MP4 output</span></span>
<span data-ttu-id="798c5-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails to the output.</span><span class="sxs-lookup"><span data-stu-id="798c5-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails to the output.</span></span>

### <a id="thumbnails_to__multibitrate_MP4_overview"></a><span data-ttu-id="798c5-389">Workflow overview to add thumbnails to</span><span class="sxs-lookup"><span data-stu-id="798c5-389">Workflow overview to add thumbnails to</span></span>
![Multibitrate MP4 workflow to start from](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="798c5-391">*Multibitrate MP4 workflow to start from*</span><span class="sxs-lookup"><span data-stu-id="798c5-391">*Multibitrate MP4 workflow to start from*</span></span>

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a><span data-ttu-id="798c5-392">Adding JPG Encoding</span><span class="sxs-lookup"><span data-stu-id="798c5-392">Adding JPG Encoding</span></span>
<span data-ttu-id="798c5-393">The heart of our thumbnail generation will be the JPG Encoder component, able to output JPG files.</span><span class="sxs-lookup"><span data-stu-id="798c5-393">The heart of our thumbnail generation will be the JPG Encoder component, able to output JPG files.</span></span>

![JPG Encoder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="798c5-395">*JPG Encoder*</span><span class="sxs-lookup"><span data-stu-id="798c5-395">*JPG Encoder*</span></span>

<span data-ttu-id="798c5-396">We cannot however directly connect our Uncompressed Video stream from the Media File Input into the JPG encoder.</span><span class="sxs-lookup"><span data-stu-id="798c5-396">We cannot however directly connect our Uncompressed Video stream from the Media File Input into the JPG encoder.</span></span> <span data-ttu-id="798c5-397">Instead, it expects to be handed individual frames.</span><span class="sxs-lookup"><span data-stu-id="798c5-397">Instead, it expects to be handed individual frames.</span></span> <span data-ttu-id="798c5-398">This, we can do through the Video Frame Gate component.</span><span class="sxs-lookup"><span data-stu-id="798c5-398">This, we can do through the Video Frame Gate component.</span></span>

![Connecting a frame gate to the JPG encoder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="798c5-400">*Connecting a frame gate to the JPG encoder*</span><span class="sxs-lookup"><span data-stu-id="798c5-400">*Connecting a frame gate to the JPG encoder*</span></span>

<span data-ttu-id="798c5-401">The frame gate once every so many seconds or frames allows a video frame to pass.</span><span class="sxs-lookup"><span data-stu-id="798c5-401">The frame gate once every so many seconds or frames allows a video frame to pass.</span></span> <span data-ttu-id="798c5-402">The interval and the time offset with which this happens is configurable in the properties.</span><span class="sxs-lookup"><span data-stu-id="798c5-402">The interval and the time offset with which this happens is configurable in the properties.</span></span>

![Video Frame Gate properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="798c5-404">*Video Frame Gate properties*</span><span class="sxs-lookup"><span data-stu-id="798c5-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="798c5-405">Let's create a thumbnail every minute by setting the mode to Time (seconds) and the Interval to 60.</span><span class="sxs-lookup"><span data-stu-id="798c5-405">Let's create a thumbnail every minute by setting the mode to Time (seconds) and the Interval to 60.</span></span>

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a><span data-ttu-id="798c5-406">Dealing with Color Space conversion</span><span class="sxs-lookup"><span data-stu-id="798c5-406">Dealing with Color Space conversion</span></span>
<span data-ttu-id="798c5-407">While it would seem logical both Uncompressed Video pins of the frame gate and the Media File Input can now be connected, we would get a warning if we would do so.</span><span class="sxs-lookup"><span data-stu-id="798c5-407">While it would seem logical both Uncompressed Video pins of the frame gate and the Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Input color space error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="798c5-409">*Input color space error*</span><span class="sxs-lookup"><span data-stu-id="798c5-409">*Input color space error*</span></span>

<span data-ttu-id="798c5-410">This is because the way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what the JPG Encoder is expecting.</span><span class="sxs-lookup"><span data-stu-id="798c5-410">This is because the way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what the JPG Encoder is expecting.</span></span> <span data-ttu-id="798c5-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected to flow in.</span><span class="sxs-lookup"><span data-stu-id="798c5-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected to flow in.</span></span> <span data-ttu-id="798c5-412">This means that the Video Frame Gate's inbound video stream will need to have a conversion applied regarding its color space first.</span><span class="sxs-lookup"><span data-stu-id="798c5-412">This means that the Video Frame Gate's inbound video stream will need to have a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="798c5-413">Drag onto the workflow the Color Space Converter - Intel and connect it to our frame gate.</span><span class="sxs-lookup"><span data-stu-id="798c5-413">Drag onto the workflow the Color Space Converter - Intel and connect it to our frame gate.</span></span>

![Connecting a Color Space Convertor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="798c5-415">*Connecting a Color Space Convertor*</span><span class="sxs-lookup"><span data-stu-id="798c5-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="798c5-416">In the properties window, pick the BGR 24 entry from the Preset list.</span><span class="sxs-lookup"><span data-stu-id="798c5-416">In the properties window, pick the BGR 24 entry from the Preset list.</span></span>

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a><span data-ttu-id="798c5-417">Writing the thumbnails</span><span class="sxs-lookup"><span data-stu-id="798c5-417">Writing the thumbnails</span></span>
<span data-ttu-id="798c5-418">Different from our MP4 video's, the JPG Encoder component will output more than one file.</span><span class="sxs-lookup"><span data-stu-id="798c5-418">Different from our MP4 video's, the JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="798c5-419">In order to deal with this, a Scene Search JPG File Writer component can be used: it will take the incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span><span class="sxs-lookup"><span data-stu-id="798c5-419">In order to deal with this, a Scene Search JPG File Writer component can be used: it will take the incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="798c5-420">(The number typically indicating the number of seconds/units in the stream which the thumbnail was drawn from.)</span><span class="sxs-lookup"><span data-stu-id="798c5-420">(The number typically indicating the number of seconds/units in the stream which the thumbnail was drawn from.)</span></span>

![Introducing the Scene Search JPG File Writer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="798c5-422">*Introducing the Scene Search JPG File Writer*</span><span class="sxs-lookup"><span data-stu-id="798c5-422">*Introducing the Scene Search JPG File Writer*</span></span>

<span data-ttu-id="798c5-423">Configure the Output Folder Path property with the expression: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="798c5-423">Configure the Output Folder Path property with the expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="798c5-424">and the Filename Prefix property with:</span><span class="sxs-lookup"><span data-stu-id="798c5-424">and the Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="798c5-425">The prefix will determine how the thumbnail files are being named.</span><span class="sxs-lookup"><span data-stu-id="798c5-425">The prefix will determine how the thumbnail files are being named.</span></span> <span data-ttu-id="798c5-426">They will be suffixed with a number indicating the thumb's position in the stream.</span><span class="sxs-lookup"><span data-stu-id="798c5-426">They will be suffixed with a number indicating the thumb's position in the stream.</span></span>

![Scene Search JPG File Writer properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="798c5-428">*Scene Search JPG File Writer properties*</span><span class="sxs-lookup"><span data-stu-id="798c5-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="798c5-429">Connect the Scene Search JPG File Writer to the Output File/Asset node.</span><span class="sxs-lookup"><span data-stu-id="798c5-429">Connect the Scene Search JPG File Writer to the Output File/Asset node.</span></span>

### <a id="thumbnails_to__multibitrate_MP4_errors"></a><span data-ttu-id="798c5-430">Detecting errors in a workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-430">Detecting errors in a workflow</span></span>
<span data-ttu-id="798c5-431">Connect the input of the color space converter to the raw uncompressed video output.</span><span class="sxs-lookup"><span data-stu-id="798c5-431">Connect the input of the color space converter to the raw uncompressed video output.</span></span> <span data-ttu-id="798c5-432">Now perform a local test run for the workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-432">Now perform a local test run for the workflow.</span></span> <span data-ttu-id="798c5-433">There's a good chance the workflow will suddenly stop executing and indicate with a red outline on the component that encountered an error:</span><span class="sxs-lookup"><span data-stu-id="798c5-433">There's a good chance the workflow will suddenly stop executing and indicate with a red outline on the component that encountered an error:</span></span>

![Color Space Converter error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="798c5-435">*Color Space Converter error*</span><span class="sxs-lookup"><span data-stu-id="798c5-435">*Color Space Converter error*</span></span>

<span data-ttu-id="798c5-436">Click the little red "E" icon in the top right corner of the Color Space Converter component to see what's the reason the encoding attempt failed.</span><span class="sxs-lookup"><span data-stu-id="798c5-436">Click the little red "E" icon in the top right corner of the Color Space Converter component to see what's the reason the encoding attempt failed.</span></span>

![Color Space Converter error dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="798c5-438">*Color Space Converter error dialog*</span><span class="sxs-lookup"><span data-stu-id="798c5-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="798c5-439">It turns out, as you can see, that the incoming color space standard for the color space converter has to be rec601 for our requested conversion of YUV to RGB.</span><span class="sxs-lookup"><span data-stu-id="798c5-439">It turns out, as you can see, that the incoming color space standard for the color space converter has to be rec601 for our requested conversion of YUV to RGB.</span></span> <span data-ttu-id="798c5-440">Apparently our stream doesn't indicate it's rec601.</span><span class="sxs-lookup"><span data-stu-id="798c5-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="798c5-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span><span class="sxs-lookup"><span data-stu-id="798c5-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="798c5-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span><span class="sxs-lookup"><span data-stu-id="798c5-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="798c5-443">The color encoding system is known as YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="798c5-443">The color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="798c5-444">To fix this, we'll indicate on the metadata of our stream that we're dealing with rec601 content.</span><span class="sxs-lookup"><span data-stu-id="798c5-444">To fix this, we'll indicate on the metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="798c5-445">To do so we'll use a Video Data Type Updater component, which we'll put in between our raw source and the color space conversion component.</span><span class="sxs-lookup"><span data-stu-id="798c5-445">To do so we'll use a Video Data Type Updater component, which we'll put in between our raw source and the color space conversion component.</span></span> <span data-ttu-id="798c5-446">This data type updater allows for the manual update of certain video data type properties.</span><span class="sxs-lookup"><span data-stu-id="798c5-446">This data type updater allows for the manual update of certain video data type properties.</span></span> <span data-ttu-id="798c5-447">Configure it to indicate a Color Space Standard of "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="798c5-447">Configure it to indicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="798c5-448">This will cause the Video Data Type Updater to tag the stream with the "Rec 601" color space if there was no color space defined yet.</span><span class="sxs-lookup"><span data-stu-id="798c5-448">This will cause the Video Data Type Updater to tag the stream with the "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="798c5-449">(It will not override any existing metadata, unless the Override checkbox was checked.)</span><span class="sxs-lookup"><span data-stu-id="798c5-449">(It will not override any existing metadata, unless the Override checkbox was checked.)</span></span>

![Updating Color Space Standard on the Data Type Updater](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="798c5-451">*Updating Color Space Standard on the Data Type Updater*</span><span class="sxs-lookup"><span data-stu-id="798c5-451">*Updating Color Space Standard on the Data Type Updater*</span></span>

### <a id="thumbnails_to__multibitrate_MP4_finish"></a><span data-ttu-id="798c5-452">Finished Workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-452">Finished Workflow</span></span>
<span data-ttu-id="798c5-453">Now that our our workflow is finished, do another test run to see it pass.</span><span class="sxs-lookup"><span data-stu-id="798c5-453">Now that our our workflow is finished, do another test run to see it pass.</span></span>

![Finished workflow for multi-mp4 output with thumbnails](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="798c5-455">*Finished workflow for multi-mp4 output with thumbnails*</span><span class="sxs-lookup"><span data-stu-id="798c5-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <a id="time_based_trim"></a><span data-ttu-id="798c5-456">Time-based trimming of multibitrate MP4 output</span><span class="sxs-lookup"><span data-stu-id="798c5-456">Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="798c5-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on time-stamps.</span><span class="sxs-lookup"><span data-stu-id="798c5-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on time-stamps.</span></span>

### <a id="time_based_trim_start"></a><span data-ttu-id="798c5-458">Workflow overview to start adding trimming to</span><span class="sxs-lookup"><span data-stu-id="798c5-458">Workflow overview to start adding trimming to</span></span>
![Starting workflow to add trimming to](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="798c5-460">*Starting workflow to add trimming to*</span><span class="sxs-lookup"><span data-stu-id="798c5-460">*Starting workflow to add trimming to*</span></span>

### <a id="time_based_trim_use_stream_trimmer"></a><span data-ttu-id="798c5-461">Using the Stream Trimmer</span><span class="sxs-lookup"><span data-stu-id="798c5-461">Using the Stream Trimmer</span></span>
<span data-ttu-id="798c5-462">The Stream Trimmer component allows to trim the beginning and ending of an input stream base on timing information (seconds, minutes, ...). The trimmer does not support frame-based trimming.</span><span class="sxs-lookup"><span data-stu-id="798c5-462">The Stream Trimmer component allows to trim the beginning and ending of an input stream base on timing information (seconds, minutes, ...). The trimmer does not support frame-based trimming.</span></span>

![Stream Trimmer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="798c5-464">*Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="798c5-464">*Stream Trimmer*</span></span>

<span data-ttu-id="798c5-465">Instead of linking the AVC encoders and speaker position assigner to the Media File Input directly, we'll put in between those the stream trimmer.</span><span class="sxs-lookup"><span data-stu-id="798c5-465">Instead of linking the AVC encoders and speaker position assigner to the Media File Input directly, we'll put in between those the stream trimmer.</span></span> <span data-ttu-id="798c5-466">(One for the video signal and one for the interleaved audio signal.)</span><span class="sxs-lookup"><span data-stu-id="798c5-466">(One for the video signal and one for the interleaved audio signal.)</span></span>

![Put Stream Trimmer in between](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="798c5-468">*Put Stream Trimmer in between*</span><span class="sxs-lookup"><span data-stu-id="798c5-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="798c5-469">Let's configure the trimmer so that we will only process video and audio between 15 seconds and 60 seconds in the video.</span><span class="sxs-lookup"><span data-stu-id="798c5-469">Let's configure the trimmer so that we will only process video and audio between 15 seconds and 60 seconds in the video.</span></span>

<span data-ttu-id="798c5-470">Go to the properties of the Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span><span class="sxs-lookup"><span data-stu-id="798c5-470">Go to the properties of the Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="798c5-471">To make sure both our audio and video trimmer are always configured to the same start and end values, we will publish those to the root of the workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-471">To make sure both our audio and video trimmer are always configured to the same start and end values, we will publish those to the root of the workflow.</span></span>

![Publish start time property from Stream Trimmer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="798c5-473">*Publish start time property from Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="798c5-473">*Publish start time property from Stream Trimmer*</span></span>

![Publish property dialog for start time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="798c5-475">*Publish property dialog for start time*</span><span class="sxs-lookup"><span data-stu-id="798c5-475">*Publish property dialog for start time*</span></span>

![Publish property dialog for end time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="798c5-477">*Publish property dialog for end time*</span><span class="sxs-lookup"><span data-stu-id="798c5-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="798c5-478">If we now inspect the root of our workflow, both properties will be neatly displayed and configurable from there.</span><span class="sxs-lookup"><span data-stu-id="798c5-478">If we now inspect the root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Published properties available on root](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="798c5-480">*Published properties available on root*</span><span class="sxs-lookup"><span data-stu-id="798c5-480">*Published properties available on root*</span></span>

<span data-ttu-id="798c5-481">Now open the trimming properties from the audio trimmer and configure both start and end times with an expression that refers to the published properties on the root of our workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-481">Now open the trimming properties from the audio trimmer and configure both start and end times with an expression that refers to the published properties on the root of our workflow.</span></span>

<span data-ttu-id="798c5-482">For the audio trimming start time:</span><span class="sxs-lookup"><span data-stu-id="798c5-482">For the audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="798c5-483">and for its end time:</span><span class="sxs-lookup"><span data-stu-id="798c5-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a><span data-ttu-id="798c5-484">Finished Workflow</span><span class="sxs-lookup"><span data-stu-id="798c5-484">Finished Workflow</span></span>
![Finished Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="798c5-486">*Finished Workflow*</span><span class="sxs-lookup"><span data-stu-id="798c5-486">*Finished Workflow*</span></span>

## <a id="scripting"></a><span data-ttu-id="798c5-487">Introducing the Scripted Component</span><span class="sxs-lookup"><span data-stu-id="798c5-487">Introducing the Scripted Component</span></span>
<span data-ttu-id="798c5-488">Scripted Components can execute arbitrary scripts during the execution phases of our workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-488">Scripted Components can execute arbitrary scripts during the execution phases of our workflow.</span></span> <span data-ttu-id="798c5-489">There are four different scripts that can be executed, each with specific characteristics and their own place in the workflow life-cycle:</span><span class="sxs-lookup"><span data-stu-id="798c5-489">There are four different scripts that can be executed, each with specific characteristics and their own place in the workflow life-cycle:</span></span>

* <span data-ttu-id="798c5-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="798c5-490">**commandScript**</span></span>
* <span data-ttu-id="798c5-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="798c5-491">**realizeScript**</span></span>
* <span data-ttu-id="798c5-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="798c5-492">**processInputScript**</span></span>
* <span data-ttu-id="798c5-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="798c5-493">**lifeCycleScript**</span></span>

<span data-ttu-id="798c5-494">The documentation of the Scripted Component goes in more detail for each of the above.</span><span class="sxs-lookup"><span data-stu-id="798c5-494">The documentation of the Scripted Component goes in more detail for each of the above.</span></span> <span data-ttu-id="798c5-495">In [the following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), the **realizeScript** scripting component is used to construct a cliplist xml on the fly when the workflow starts.</span><span class="sxs-lookup"><span data-stu-id="798c5-495">In [the following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), the **realizeScript** scripting component is used to construct a cliplist xml on the fly when the workflow starts.</span></span> <span data-ttu-id="798c5-496">This script is called during the component setup, which happens only once in it's lifecycle.</span><span class="sxs-lookup"><span data-stu-id="798c5-496">This script is called during the component setup, which happens only once in it's lifecycle.</span></span>

### <a id="scripting_hello_world"></a><span data-ttu-id="798c5-497">Scripting within a workflow: hello world</span><span class="sxs-lookup"><span data-stu-id="798c5-497">Scripting within a workflow: hello world</span></span>
<span data-ttu-id="798c5-498">Drag a Scripted Component onto the designer surface and rename it (for example, "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="798c5-498">Drag a Scripted Component onto the designer surface and rename it (for example, "SetClipListXML").</span></span>

![Adding a Scripted Component](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="798c5-500">*Adding a Scripted Component*</span><span class="sxs-lookup"><span data-stu-id="798c5-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="798c5-501">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span><span class="sxs-lookup"><span data-stu-id="798c5-501">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![Scripted Component properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="798c5-503">*Scripted Component properties*</span><span class="sxs-lookup"><span data-stu-id="798c5-503">*Scripted Component properties*</span></span>

<span data-ttu-id="798c5-504">Clear the processInputScript and open the editor for the realizeScript.</span><span class="sxs-lookup"><span data-stu-id="798c5-504">Clear the processInputScript and open the editor for the realizeScript.</span></span> <span data-ttu-id="798c5-505">Now we're set up and ready to start scripting.</span><span class="sxs-lookup"><span data-stu-id="798c5-505">Now we're set up and ready to start scripting.</span></span>

<span data-ttu-id="798c5-506">Scripts are written in Groovy, a dynamically compiled scripting language for the Java platform that retains compatibility with Java.</span><span class="sxs-lookup"><span data-stu-id="798c5-506">Scripts are written in Groovy, a dynamically compiled scripting language for the Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="798c5-507">Actually, most Java code is valid Groovy code.</span><span class="sxs-lookup"><span data-stu-id="798c5-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="798c5-508">Let's write a simple hello world groovy script in the context of our realizeScript.</span><span class="sxs-lookup"><span data-stu-id="798c5-508">Let's write a simple hello world groovy script in the context of our realizeScript.</span></span> <span data-ttu-id="798c5-509">Enter the following in the editor:</span><span class="sxs-lookup"><span data-stu-id="798c5-509">Enter the following in the editor:</span></span>

    node.log("hello world");

<span data-ttu-id="798c5-510">Now execute a local test run.</span><span class="sxs-lookup"><span data-stu-id="798c5-510">Now execute a local test run.</span></span> <span data-ttu-id="798c5-511">After this run, inspect (through the System tab on the Scripted Component) the Logs property.</span><span class="sxs-lookup"><span data-stu-id="798c5-511">After this run, inspect (through the System tab on the Scripted Component) the Logs property.</span></span>

![Hello world log output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="798c5-513">*Hello world log output*</span><span class="sxs-lookup"><span data-stu-id="798c5-513">*Hello world log output*</span></span>

<span data-ttu-id="798c5-514">The node object we call the log method on, refers to our current "node" or the component we're scripting within.</span><span class="sxs-lookup"><span data-stu-id="798c5-514">The node object we call the log method on, refers to our current "node" or the component we're scripting within.</span></span> <span data-ttu-id="798c5-515">Every component as such has the ability to output logging data, available through the system tab. In this case, we output the string literal "hello world".</span><span class="sxs-lookup"><span data-stu-id="798c5-515">Every component as such has the ability to output logging data, available through the system tab. In this case, we output the string literal "hello world".</span></span> <span data-ttu-id="798c5-516">Important to understand here is that this can prove to be an invaluable debugging tool, providing you with insight on what the script is actually doing.</span><span class="sxs-lookup"><span data-stu-id="798c5-516">Important to understand here is that this can prove to be an invaluable debugging tool, providing you with insight on what the script is actually doing.</span></span>

<span data-ttu-id="798c5-517">From within our scripting environment, we also have access to properties on other components.</span><span class="sxs-lookup"><span data-stu-id="798c5-517">From within our scripting environment, we also have access to properties on other components.</span></span> <span data-ttu-id="798c5-518">Try this:</span><span class="sxs-lookup"><span data-stu-id="798c5-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up to other nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="798c5-519">Our log window will show us the following:</span><span class="sxs-lookup"><span data-stu-id="798c5-519">Our log window will show us the following:</span></span>

![Log output for accessing node paths](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="798c5-521">*Log output for accessing node paths*</span><span class="sxs-lookup"><span data-stu-id="798c5-521">*Log output for accessing node paths*</span></span>

## <a id="frame_based_trim"></a><span data-ttu-id="798c5-522">Frame-based trimming of multibitrate MP4 output</span><span class="sxs-lookup"><span data-stu-id="798c5-522">Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="798c5-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on frame counts.</span><span class="sxs-lookup"><span data-stu-id="798c5-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on frame counts.</span></span>

### <a id="frame_based_trim_start"></a><span data-ttu-id="798c5-524">Blueprint overview to start adding trimming to</span><span class="sxs-lookup"><span data-stu-id="798c5-524">Blueprint overview to start adding trimming to</span></span>
![Workflow to start adding trimming to](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="798c5-526">*Workflow to start adding trimming to*</span><span class="sxs-lookup"><span data-stu-id="798c5-526">*Workflow to start adding trimming to*</span></span>

### <a id="frame_based_trim_clip_list"></a><span data-ttu-id="798c5-527">Using the Clip List XML</span><span class="sxs-lookup"><span data-stu-id="798c5-527">Using the Clip List XML</span></span>
<span data-ttu-id="798c5-528">In all previous workflow tutorials, we used the Media File Input component as our video input source.</span><span class="sxs-lookup"><span data-stu-id="798c5-528">In all previous workflow tutorials, we used the Media File Input component as our video input source.</span></span> <span data-ttu-id="798c5-529">For this specific scenario though, we'll be using the Clip List Source component instead.</span><span class="sxs-lookup"><span data-stu-id="798c5-529">For this specific scenario though, we'll be using the Clip List Source component instead.</span></span> <span data-ttu-id="798c5-530">Note that this should not be the preferred way of working; only use the Clip List Source when there's a real reason to do so (like in the below case, where we're making use of the clip list trimming capabilities).</span><span class="sxs-lookup"><span data-stu-id="798c5-530">Note that this should not be the preferred way of working; only use the Clip List Source when there's a real reason to do so (like in the below case, where we're making use of the clip list trimming capabilities).</span></span>

<span data-ttu-id="798c5-531">To switch from our Media File Input to the Clip List Source, drag the Clip List Source component onto the design surface and connect the Clip List XML pin to the Clip List XML node of the workflow designer.</span><span class="sxs-lookup"><span data-stu-id="798c5-531">To switch from our Media File Input to the Clip List Source, drag the Clip List Source component onto the design surface and connect the Clip List XML pin to the Clip List XML node of the workflow designer.</span></span> <span data-ttu-id="798c5-532">This should populate the Clip List Source with output pins, according to our input video.</span><span class="sxs-lookup"><span data-stu-id="798c5-532">This should populate the Clip List Source with output pins, according to our input video.</span></span> <span data-ttu-id="798c5-533">Now connect the Uncompressed Video and Uncompressed Audio pins from the the Clip List Source to the respective AVC Encoders and Audio Stream Interleaver.</span><span class="sxs-lookup"><span data-stu-id="798c5-533">Now connect the Uncompressed Video and Uncompressed Audio pins from the the Clip List Source to the respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="798c5-534">Now remove the Media File Input.</span><span class="sxs-lookup"><span data-stu-id="798c5-534">Now remove the Media File Input.</span></span>

![Replaced the Media File Input with the Clip List Source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="798c5-536">*Replaced the Media File Input with the Clip List Source*</span><span class="sxs-lookup"><span data-stu-id="798c5-536">*Replaced the Media File Input with the Clip List Source*</span></span>

<span data-ttu-id="798c5-537">The Clip List Source component takes as its input a "Clip List XML".</span><span class="sxs-lookup"><span data-stu-id="798c5-537">The Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="798c5-538">When selecting the source file to test with locally, this clip list xml is auto-populated for you.</span><span class="sxs-lookup"><span data-stu-id="798c5-538">When selecting the source file to test with locally, this clip list xml is auto-populated for you.</span></span>

![Auto-populated Clip List XML property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="798c5-540">*Auto-populated Clip List XML property*</span><span class="sxs-lookup"><span data-stu-id="798c5-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="798c5-541">Looking a bit closer to the xml, this is how it looks like:</span><span class="sxs-lookup"><span data-stu-id="798c5-541">Looking a bit closer to the xml, this is how it looks like:</span></span>

![Edit clip list dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="798c5-543">*Edit clip list dialog*</span><span class="sxs-lookup"><span data-stu-id="798c5-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="798c5-544">This however does not reflect the capabilities of the clip list xml.</span><span class="sxs-lookup"><span data-stu-id="798c5-544">This however does not reflect the capabilities of the clip list xml.</span></span> <span data-ttu-id="798c5-545">One option we have is to add a "Trim" element under both the video and audio source, like this:</span><span class="sxs-lookup"><span data-stu-id="798c5-545">One option we have is to add a "Trim" element under both the video and audio source, like this:</span></span>

![Adding a trim element to the clip list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="798c5-547">*Adding a trim element to the clip list*</span><span class="sxs-lookup"><span data-stu-id="798c5-547">*Adding a trim element to the clip list*</span></span>

<span data-ttu-id="798c5-548">If you modify the clip list xml like this above and perform a local test run, you'll see the video correctly been trimmed between 10 and 20 seconds in the video.</span><span class="sxs-lookup"><span data-stu-id="798c5-548">If you modify the clip list xml like this above and perform a local test run, you'll see the video correctly been trimmed between 10 and 20 seconds in the video.</span></span>

<span data-ttu-id="798c5-549">Contrary to what happens when you do a local run though, this very same cliplist xml would not have the same effect when applied in a workflow that runs in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="798c5-549">Contrary to what happens when you do a local run though, this very same cliplist xml would not have the same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="798c5-550">When Azure Premium Encoder starts, the cliplist xml is generated every time again, based on the input file the encoding job was given.</span><span class="sxs-lookup"><span data-stu-id="798c5-550">When Azure Premium Encoder starts, the cliplist xml is generated every time again, based on the input file the encoding job was given.</span></span> <span data-ttu-id="798c5-551">This means that any changes we do on the xml would unfortunately be overridden.</span><span class="sxs-lookup"><span data-stu-id="798c5-551">This means that any changes we do on the xml would unfortunately be overridden.</span></span>

<span data-ttu-id="798c5-552">To counter the cliplist xml being wiped when an encoding job is started, we can re-generate it on the fly just after the start of our workflow.</span><span class="sxs-lookup"><span data-stu-id="798c5-552">To counter the cliplist xml being wiped when an encoding job is started, we can re-generate it on the fly just after the start of our workflow.</span></span> <span data-ttu-id="798c5-553">Such custom actions can be taken through what is called a "Scripted Component".</span><span class="sxs-lookup"><span data-stu-id="798c5-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="798c5-554">For more information, see [Introducing the Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="798c5-554">For more information, see [Introducing the Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="798c5-555">Drag a Scripted Component onto the designer surface and rename it to "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="798c5-555">Drag a Scripted Component onto the designer surface and rename it to "SetClipListXML".</span></span>

![Adding a Scripted Component](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="798c5-557">*Adding a Scripted Component*</span><span class="sxs-lookup"><span data-stu-id="798c5-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="798c5-558">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span><span class="sxs-lookup"><span data-stu-id="798c5-558">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![Scripted Component properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="798c5-560">*Scripted Component properties*</span><span class="sxs-lookup"><span data-stu-id="798c5-560">*Scripted Component properties*</span></span>

### <a id="frame_based_trim_modify_clip_list"></a><span data-ttu-id="798c5-561">Modifying the clip list from a Scripted Component</span><span class="sxs-lookup"><span data-stu-id="798c5-561">Modifying the clip list from a Scripted Component</span></span>
<span data-ttu-id="798c5-562">Before we can re-write the cliplist xml that is generated during workflow startup, we'll need to have access to the cliplist xml property and contents.</span><span class="sxs-lookup"><span data-stu-id="798c5-562">Before we can re-write the cliplist xml that is generated during workflow startup, we'll need to have access to the cliplist xml property and contents.</span></span> <span data-ttu-id="798c5-563">We can do so like this:</span><span class="sxs-lookup"><span data-stu-id="798c5-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Incoming clip list being logged](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="798c5-565">*Incoming clip list being logged*</span><span class="sxs-lookup"><span data-stu-id="798c5-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="798c5-566">First we need a way to determine from which point till which point we want to trim the video.</span><span class="sxs-lookup"><span data-stu-id="798c5-566">First we need a way to determine from which point till which point we want to trim the video.</span></span> <span data-ttu-id="798c5-567">To make this convenient to the less-technical user of the workflow, publish two properties to the root of the graph.</span><span class="sxs-lookup"><span data-stu-id="798c5-567">To make this convenient to the less-technical user of the workflow, publish two properties to the root of the graph.</span></span> <span data-ttu-id="798c5-568">To do this, right click the designer surface and select "Add Property":</span><span class="sxs-lookup"><span data-stu-id="798c5-568">To do this, right click the designer surface and select "Add Property":</span></span>

* <span data-ttu-id="798c5-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="798c5-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="798c5-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span><span class="sxs-lookup"><span data-stu-id="798c5-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Add Property dialog for clipping start time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="798c5-572">*Add Property dialog for clipping start time*</span><span class="sxs-lookup"><span data-stu-id="798c5-572">*Add Property dialog for clipping start time*</span></span>

![Published clipping time props on workflow root](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="798c5-574">*Published clipping time props on workflow root*</span><span class="sxs-lookup"><span data-stu-id="798c5-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="798c5-575">Configure both properties to a suitable value:</span><span class="sxs-lookup"><span data-stu-id="798c5-575">Configure both properties to a suitable value:</span></span>

![Configure the clipping start and end properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="798c5-577">*Configure the clipping start and end properties*</span><span class="sxs-lookup"><span data-stu-id="798c5-577">*Configure the clipping start and end properties*</span></span>

<span data-ttu-id="798c5-578">Now, from within our script, we can access both properties, like this:</span><span class="sxs-lookup"><span data-stu-id="798c5-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Log window showing start and end of clipping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="798c5-580">*Log window showing start and end of clipping*</span><span class="sxs-lookup"><span data-stu-id="798c5-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="798c5-581">Let's parse the timecode strings into a more convenient to use form, using a simple regular expression:</span><span class="sxs-lookup"><span data-stu-id="798c5-581">Let's parse the timecode strings into a more convenient to use form, using a simple regular expression:</span></span>

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Log window with output of parsed timecode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="798c5-583">*Log window with output of parsed timecode*</span><span class="sxs-lookup"><span data-stu-id="798c5-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="798c5-584">With this information at hand, we can now modify the cliplist xml to reflect the start and end times for the desired frame-accurate clipping of the movie.</span><span class="sxs-lookup"><span data-stu-id="798c5-584">With this information at hand, we can now modify the cliplist xml to reflect the start and end times for the desired frame-accurate clipping of the movie.</span></span>

![Script code to add trim elements](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="798c5-586">*Script code to add trim elements*</span><span class="sxs-lookup"><span data-stu-id="798c5-586">*Script code to add trim elements*</span></span>

<span data-ttu-id="798c5-587">This was done through normal string manipulation operations.</span><span class="sxs-lookup"><span data-stu-id="798c5-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="798c5-588">The resulting modified clip list xml is written back to the clipListXML property on the workflow root through the "setProperty" method.</span><span class="sxs-lookup"><span data-stu-id="798c5-588">The resulting modified clip list xml is written back to the clipListXML property on the workflow root through the "setProperty" method.</span></span> <span data-ttu-id="798c5-589">The log window after another test run would show us the following:</span><span class="sxs-lookup"><span data-stu-id="798c5-589">The log window after another test run would show us the following:</span></span>

![Logging the resulting clip list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="798c5-591">*Logging the resulting clip list*</span><span class="sxs-lookup"><span data-stu-id="798c5-591">*Logging the resulting clip list*</span></span>

<span data-ttu-id="798c5-592">Do a test-run to see how the video and audio streams have been clipped.</span><span class="sxs-lookup"><span data-stu-id="798c5-592">Do a test-run to see how the video and audio streams have been clipped.</span></span> <span data-ttu-id="798c5-593">As you'll do more than one test-run with different values for the trimming points, you'll notice that those will not be taken into account however!</span><span class="sxs-lookup"><span data-stu-id="798c5-593">As you'll do more than one test-run with different values for the trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="798c5-594">The reason for this is that the designer, unlike the Azure runtime, does NOT override the cliplist xml every run.</span><span class="sxs-lookup"><span data-stu-id="798c5-594">The reason for this is that the designer, unlike the Azure runtime, does NOT override the cliplist xml every run.</span></span> <span data-ttu-id="798c5-595">This means that only the very first time you have set the in and out points, will cause the xml to transform, all the other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent the workflow from adding another trim element when there's already one present.</span><span class="sxs-lookup"><span data-stu-id="798c5-595">This means that only the very first time you have set the in and out points, will cause the xml to transform, all the other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent the workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="798c5-596">To make our workflow convenient to test locally, we best add some house-keeping code that inspects if a trim element was already present.</span><span class="sxs-lookup"><span data-stu-id="798c5-596">To make our workflow convenient to test locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="798c5-597">If so, we can remove it before continuing by modifying the xml with the new values.</span><span class="sxs-lookup"><span data-stu-id="798c5-597">If so, we can remove it before continuing by modifying the xml with the new values.</span></span> <span data-ttu-id="798c5-598">Rather than using plain string manipulations, it's probably safer to do this through real xml object model parsing.</span><span class="sxs-lookup"><span data-stu-id="798c5-598">Rather than using plain string manipulations, it's probably safer to do this through real xml object model parsing.</span></span>

<span data-ttu-id="798c5-599">Before we can add such code though, we'll need to add a number of import statements at the start of our script first:</span><span class="sxs-lookup"><span data-stu-id="798c5-599">Before we can add such code though, we'll need to add a number of import statements at the start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="798c5-600">After this, we can add the required cleaning code:</span><span class="sxs-lookup"><span data-stu-id="798c5-600">After this, we can add the required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from the clip list xml by parsing the xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
     //delete the trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="798c5-601">This code goes just above the point at which we add the trim elements to the cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="798c5-601">This code goes just above the point at which we add the trim elements to the cliplist xml.</span></span>

<span data-ttu-id="798c5-602">At this point, we can run and modify our workflow as much as we want while having the changes applied ever time.</span><span class="sxs-lookup"><span data-stu-id="798c5-602">At this point, we can run and modify our workflow as much as we want while having the changes applied ever time.</span></span>    

### <a id="frame_based_trim_clippingenabled_prop"></a><span data-ttu-id="798c5-603">Adding a ClippingEnabled convenience property</span><span class="sxs-lookup"><span data-stu-id="798c5-603">Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="798c5-604">As you might not always want trimming to happen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want to enable trimming / clipping.</span><span class="sxs-lookup"><span data-stu-id="798c5-604">As you might not always want trimming to happen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want to enable trimming / clipping.</span></span>

<span data-ttu-id="798c5-605">Just as before, publish a new property to the root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span><span class="sxs-lookup"><span data-stu-id="798c5-605">Just as before, publish a new property to the root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Published a property for enabling clipping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="798c5-607">*Published a property for enabling clipping*</span><span class="sxs-lookup"><span data-stu-id="798c5-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="798c5-608">With the below simple guard clause, we can check if trimming is required and decide if our clip list as such needs to be modified or not.</span><span class="sxs-lookup"><span data-stu-id="798c5-608">With the below simple guard clause, we can check if trimming is required and decide if our clip list as such needs to be modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a><span data-ttu-id="798c5-609">Complete code</span><span class="sxs-lookup"><span data-stu-id="798c5-609">Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from the clip list xml by parsing the xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
    //delete the trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements to cliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="798c5-610">Also see</span><span class="sxs-lookup"><span data-stu-id="798c5-610">Also see</span></span>
[<span data-ttu-id="798c5-611">Introducing Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="798c5-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="798c5-612">How to Use Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="798c5-612">How to Use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="798c5-613">Encoding On-Demand Content with Azure Media Service</span><span class="sxs-lookup"><span data-stu-id="798c5-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="798c5-614">Media Encoder Premium Workflow Formats and Codecs</span><span class="sxs-lookup"><span data-stu-id="798c5-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="798c5-615">Sample workflow files</span><span class="sxs-lookup"><span data-stu-id="798c5-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="798c5-616">Azure Media Services Explorer tool</span><span class="sxs-lookup"><span data-stu-id="798c5-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="798c5-617">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="798c5-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="798c5-618">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="798c5-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]






































































