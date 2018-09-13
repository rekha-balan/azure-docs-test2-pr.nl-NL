---
title: Multiple input files and component properties with Premium Encoder - Azure | Microsoft Docs
description: This topic explains how to use setRuntimeProperties to use multiple input files and pass custom data to the Media Encoder Premium Workflow media processor.
services: media-services
documentationcenter: ''
author: xpouyat
manager: erikre
editor: ''
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: 5e0f5ee3aff389d20678f779771267593b134f84
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550320"
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="766d8-103">Using multiple input files and component properties with Premium Encoder</span><span class="sxs-lookup"><span data-stu-id="766d8-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="766d8-104">Overview</span><span class="sxs-lookup"><span data-stu-id="766d8-104">Overview</span></span>
<span data-ttu-id="766d8-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span><span class="sxs-lookup"><span data-stu-id="766d8-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="766d8-106">Some examples are:</span><span class="sxs-lookup"><span data-stu-id="766d8-106">Some examples are:</span></span>

* <span data-ttu-id="766d8-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span><span class="sxs-lookup"><span data-stu-id="766d8-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="766d8-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span><span class="sxs-lookup"><span data-stu-id="766d8-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="766d8-109">Overlaying a logo image on the input video while the video is encoded.</span><span class="sxs-lookup"><span data-stu-id="766d8-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="766d8-110">Multiple audio language encoding.</span><span class="sxs-lookup"><span data-stu-id="766d8-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="766d8-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="766d8-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="766d8-112">This topic explains how to use them.</span><span class="sxs-lookup"><span data-stu-id="766d8-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="766d8-113">Configuration string syntax</span><span class="sxs-lookup"><span data-stu-id="766d8-113">Configuration string syntax</span></span>
<span data-ttu-id="766d8-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span><span class="sxs-lookup"><span data-stu-id="766d8-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="766d8-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span><span class="sxs-lookup"><span data-stu-id="766d8-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="766d8-116">Customizing component properties</span><span class="sxs-lookup"><span data-stu-id="766d8-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="766d8-117">Property with a simple value</span><span class="sxs-lookup"><span data-stu-id="766d8-117">Property with a simple value</span></span>
<span data-ttu-id="766d8-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span><span class="sxs-lookup"><span data-stu-id="766d8-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="766d8-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span><span class="sxs-lookup"><span data-stu-id="766d8-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="766d8-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span><span class="sxs-lookup"><span data-stu-id="766d8-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="766d8-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span><span class="sxs-lookup"><span data-stu-id="766d8-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="766d8-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span><span class="sxs-lookup"><span data-stu-id="766d8-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="766d8-123">Example:</span><span class="sxs-lookup"><span data-stu-id="766d8-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="766d8-124">Property with an XML value</span><span class="sxs-lookup"><span data-stu-id="766d8-124">Property with an XML value</span></span>
<span data-ttu-id="766d8-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="766d8-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="766d8-126">Example:</span><span class="sxs-lookup"><span data-stu-id="766d8-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="766d8-127">Make sure not to put a carriage return just after `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="766d8-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="766d8-128">propertyPath value</span><span class="sxs-lookup"><span data-stu-id="766d8-128">propertyPath value</span></span>
<span data-ttu-id="766d8-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="766d8-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="766d8-130">This is, in general, the name of the component, then the name of the property.</span><span class="sxs-lookup"><span data-stu-id="766d8-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="766d8-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span><span class="sxs-lookup"><span data-stu-id="766d8-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="766d8-132">To check the path and property name, use the action button that is immediately beside each property.</span><span class="sxs-lookup"><span data-stu-id="766d8-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="766d8-133">You can click this action button and select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="766d8-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="766d8-134">This will show you the actual name of the property, and immediately above it, the namespace.</span><span class="sxs-lookup"><span data-stu-id="766d8-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![Action/Edit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="766d8-137">Multiple input files</span><span class="sxs-lookup"><span data-stu-id="766d8-137">Multiple input files</span></span>
<span data-ttu-id="766d8-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span><span class="sxs-lookup"><span data-stu-id="766d8-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="766d8-139">The first one is a *Workflow Asset* that contains a workflow file.</span><span class="sxs-lookup"><span data-stu-id="766d8-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="766d8-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="766d8-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="766d8-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span><span class="sxs-lookup"><span data-stu-id="766d8-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="766d8-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span><span class="sxs-lookup"><span data-stu-id="766d8-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="766d8-143">All the media files must be in the same *Media Asset*.</span><span class="sxs-lookup"><span data-stu-id="766d8-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="766d8-144">Using multiple Media Assets is not supported.</span><span class="sxs-lookup"><span data-stu-id="766d8-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="766d8-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span><span class="sxs-lookup"><span data-stu-id="766d8-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="766d8-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span><span class="sxs-lookup"><span data-stu-id="766d8-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="766d8-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span><span class="sxs-lookup"><span data-stu-id="766d8-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="766d8-148">**transcodeSource** is used to specify the Clip List XML content.</span><span class="sxs-lookup"><span data-stu-id="766d8-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="766d8-149">Connections in the workflow:</span><span class="sxs-lookup"><span data-stu-id="766d8-149">Connections in the workflow:</span></span>

* <span data-ttu-id="766d8-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span><span class="sxs-lookup"><span data-stu-id="766d8-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="766d8-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span><span class="sxs-lookup"><span data-stu-id="766d8-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="766d8-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span><span class="sxs-lookup"><span data-stu-id="766d8-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![No connection from Primary Source File to Media File Input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="766d8-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span><span class="sxs-lookup"><span data-stu-id="766d8-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![Connection from Clip List XML to Clip List Source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="766d8-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="766d8-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="766d8-157">Clip List XML customization</span><span class="sxs-lookup"><span data-stu-id="766d8-157">Clip List XML customization</span></span>
<span data-ttu-id="766d8-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span><span class="sxs-lookup"><span data-stu-id="766d8-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="766d8-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span><span class="sxs-lookup"><span data-stu-id="766d8-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="766d8-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span><span class="sxs-lookup"><span data-stu-id="766d8-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="766d8-161">With additional frame-accurate trimming:</span><span class="sxs-lookup"><span data-stu-id="766d8-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="766d8-162">Example 1 : Overlay an image on top of the video</span><span class="sxs-lookup"><span data-stu-id="766d8-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="766d8-163">Presentation</span><span class="sxs-lookup"><span data-stu-id="766d8-163">Presentation</span></span>
<span data-ttu-id="766d8-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span><span class="sxs-lookup"><span data-stu-id="766d8-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="766d8-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span><span class="sxs-lookup"><span data-stu-id="766d8-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="766d8-166">You should perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="766d8-166">You should perform the following steps:</span></span>

* <span data-ttu-id="766d8-167">Create a Workflow Asset with the workflow file (see the following example).</span><span class="sxs-lookup"><span data-stu-id="766d8-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="766d8-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="766d8-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="766d8-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span><span class="sxs-lookup"><span data-stu-id="766d8-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="766d8-170">Configuration:</span><span class="sxs-lookup"><span data-stu-id="766d8-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="766d8-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span><span class="sxs-lookup"><span data-stu-id="766d8-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="766d8-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span><span class="sxs-lookup"><span data-stu-id="766d8-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="766d8-173">The video file name is sent to the primarySourceFile property.</span><span class="sxs-lookup"><span data-stu-id="766d8-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="766d8-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span><span class="sxs-lookup"><span data-stu-id="766d8-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="766d8-175">Step-by-step workflow creation</span><span class="sxs-lookup"><span data-stu-id="766d8-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="766d8-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span><span class="sxs-lookup"><span data-stu-id="766d8-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="766d8-177">It will overlay the image on top of the video.</span><span class="sxs-lookup"><span data-stu-id="766d8-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="766d8-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span><span class="sxs-lookup"><span data-stu-id="766d8-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="766d8-179">The new workflow shows three elements:</span><span class="sxs-lookup"><span data-stu-id="766d8-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="766d8-180">Primary Source File</span><span class="sxs-lookup"><span data-stu-id="766d8-180">Primary Source File</span></span>
* <span data-ttu-id="766d8-181">Clip List XML</span><span class="sxs-lookup"><span data-stu-id="766d8-181">Clip List XML</span></span>
* <span data-ttu-id="766d8-182">Output File/Asset</span><span class="sxs-lookup"><span data-stu-id="766d8-182">Output File/Asset</span></span>  

![New Encoding Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="766d8-184">*New Encoding Workflow*</span><span class="sxs-lookup"><span data-stu-id="766d8-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="766d8-185">In order to accept the input media file, start with adding a Media File Input component.</span><span class="sxs-lookup"><span data-stu-id="766d8-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="766d8-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span><span class="sxs-lookup"><span data-stu-id="766d8-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="766d8-187">Next, add the video file to be used for designing your workflow.</span><span class="sxs-lookup"><span data-stu-id="766d8-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="766d8-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span><span class="sxs-lookup"><span data-stu-id="766d8-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="766d8-189">Click the folder icon and select the appropriate video file.</span><span class="sxs-lookup"><span data-stu-id="766d8-189">Click the folder icon and select the appropriate video file.</span></span>

![Primary File Source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="766d8-191">*Primary File Source*</span><span class="sxs-lookup"><span data-stu-id="766d8-191">*Primary File Source*</span></span>

<span data-ttu-id="766d8-192">Next, specify the video file in the Media File Input component.</span><span class="sxs-lookup"><span data-stu-id="766d8-192">Next, specify the video file in the Media File Input component.</span></span>   

![Media File Input Source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="766d8-194">*Media File Input Source*</span><span class="sxs-lookup"><span data-stu-id="766d8-194">*Media File Input Source*</span></span>

<span data-ttu-id="766d8-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span><span class="sxs-lookup"><span data-stu-id="766d8-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="766d8-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span><span class="sxs-lookup"><span data-stu-id="766d8-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="766d8-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span><span class="sxs-lookup"><span data-stu-id="766d8-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="766d8-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span><span class="sxs-lookup"><span data-stu-id="766d8-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![video Data Type Updater and Format Converter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="766d8-200">*Video Data Type Updater and Format Converter*</span><span class="sxs-lookup"><span data-stu-id="766d8-200">*Video Data Type Updater and Format Converter*</span></span>

![Layout type = Configurable Planar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="766d8-202">*Layout type is Configurable Planar*</span><span class="sxs-lookup"><span data-stu-id="766d8-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="766d8-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span><span class="sxs-lookup"><span data-stu-id="766d8-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="766d8-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span><span class="sxs-lookup"><span data-stu-id="766d8-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="766d8-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span><span class="sxs-lookup"><span data-stu-id="766d8-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![Overlay component and image file source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="766d8-207">*Overlay component and image file source*</span><span class="sxs-lookup"><span data-stu-id="766d8-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="766d8-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span><span class="sxs-lookup"><span data-stu-id="766d8-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="766d8-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span><span class="sxs-lookup"><span data-stu-id="766d8-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![Overlay position](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="766d8-211">*Overlay position*</span><span class="sxs-lookup"><span data-stu-id="766d8-211">*Overlay position*</span></span>

<span data-ttu-id="766d8-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span><span class="sxs-lookup"><span data-stu-id="766d8-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="766d8-213">Connect the pins.</span><span class="sxs-lookup"><span data-stu-id="766d8-213">Connect the pins.</span></span>
<span data-ttu-id="766d8-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="766d8-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Audio and Video Encoders](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="766d8-216">*Audio and Video Encoders*</span><span class="sxs-lookup"><span data-stu-id="766d8-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="766d8-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span><span class="sxs-lookup"><span data-stu-id="766d8-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![MP4 multiplexer and file output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="766d8-219">*MP4 multiplexer and file output*</span><span class="sxs-lookup"><span data-stu-id="766d8-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="766d8-220">You need to set the name for the output file.</span><span class="sxs-lookup"><span data-stu-id="766d8-220">You need to set the name for the output file.</span></span> <span data-ttu-id="766d8-221">Click the **File Output** component and edit the expression for the file:</span><span class="sxs-lookup"><span data-stu-id="766d8-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![File output name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="766d8-223">*File output name*</span><span class="sxs-lookup"><span data-stu-id="766d8-223">*File output name*</span></span>

<span data-ttu-id="766d8-224">You can run the workflow locally to check that it is running correctly.</span><span class="sxs-lookup"><span data-stu-id="766d8-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="766d8-225">After it finishes, you can run it in Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="766d8-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="766d8-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span><span class="sxs-lookup"><span data-stu-id="766d8-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="766d8-227">You can do this by using the .NET or REST API.</span><span class="sxs-lookup"><span data-stu-id="766d8-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="766d8-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="766d8-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="766d8-229">This tutorial shows you how to manage assets with AMSE.</span><span class="sxs-lookup"><span data-stu-id="766d8-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="766d8-230">There are two ways to add files to an asset:</span><span class="sxs-lookup"><span data-stu-id="766d8-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="766d8-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span><span class="sxs-lookup"><span data-stu-id="766d8-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="766d8-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span><span class="sxs-lookup"><span data-stu-id="766d8-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="766d8-233">Make sure to set a primary file in the asset (the main video file).</span><span class="sxs-lookup"><span data-stu-id="766d8-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![Asset files in AMSE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="766d8-235">*Asset files in AMSE*</span><span class="sxs-lookup"><span data-stu-id="766d8-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="766d8-236">Select the asset and choose to encode it with Premium Encoder.</span><span class="sxs-lookup"><span data-stu-id="766d8-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="766d8-237">Upload the workflow and select it.</span><span class="sxs-lookup"><span data-stu-id="766d8-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="766d8-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span><span class="sxs-lookup"><span data-stu-id="766d8-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![Premium Encoder in AMSE](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="766d8-240">*Premium Encoder in AMSE*</span><span class="sxs-lookup"><span data-stu-id="766d8-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="766d8-241">Then, paste the following XML data.</span><span class="sxs-lookup"><span data-stu-id="766d8-241">Then, paste the following XML data.</span></span> <span data-ttu-id="766d8-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="766d8-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="766d8-243">Specify the name of the file name for the logo too.</span><span class="sxs-lookup"><span data-stu-id="766d8-243">Specify the name of the file name for the logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="766d8-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="766d8-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="766d8-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span><span class="sxs-lookup"><span data-stu-id="766d8-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="766d8-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span><span class="sxs-lookup"><span data-stu-id="766d8-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![Overlay on the video](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media-services/media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="766d8-249">*Overlay on the video*</span><span class="sxs-lookup"><span data-stu-id="766d8-249">*Overlay on the video*</span></span>

<span data-ttu-id="766d8-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="766d8-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="766d8-251">Example 2 : Multiple audio language encoding</span><span class="sxs-lookup"><span data-stu-id="766d8-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="766d8-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="766d8-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="766d8-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span><span class="sxs-lookup"><span data-stu-id="766d8-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="766d8-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span><span class="sxs-lookup"><span data-stu-id="766d8-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="766d8-255">To encode, please follow these steps:</span><span class="sxs-lookup"><span data-stu-id="766d8-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="766d8-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span><span class="sxs-lookup"><span data-stu-id="766d8-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="766d8-257">Make sure that the MXF file is set as a primary file.</span><span class="sxs-lookup"><span data-stu-id="766d8-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="766d8-258">Create a job and a task using the Premium Workflow Encoder processor.</span><span class="sxs-lookup"><span data-stu-id="766d8-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="766d8-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="766d8-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="766d8-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span><span class="sxs-lookup"><span data-stu-id="766d8-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="766d8-261">Please update the XML data to specify the correct file names and languages tags.</span><span class="sxs-lookup"><span data-stu-id="766d8-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="766d8-262">The workflow has audio components named Audio 1 to Audio 18.</span><span class="sxs-lookup"><span data-stu-id="766d8-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="766d8-263">RFC5646 is supported for the language tag.</span><span class="sxs-lookup"><span data-stu-id="766d8-263">RFC5646 is supported for the language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="766d8-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="766d8-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="766d8-265">See also</span><span class="sxs-lookup"><span data-stu-id="766d8-265">See also</span></span>
* [<span data-ttu-id="766d8-266">Introducing Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="766d8-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="766d8-267">How to use Premium Encoding in Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="766d8-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="766d8-268">Encoding on-demand content with Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="766d8-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="766d8-269">Media Encoder Premium Workflow formats and codecs</span><span class="sxs-lookup"><span data-stu-id="766d8-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="766d8-270">Sample workflow files</span><span class="sxs-lookup"><span data-stu-id="766d8-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="766d8-271">Azure Media Services Explorer tool</span><span class="sxs-lookup"><span data-stu-id="766d8-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="766d8-272">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="766d8-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="766d8-273">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="766d8-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


















