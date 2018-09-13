---
title: Getting started with Project Acoustics - Cognitive Services
description: This quickstart guide will show you how to integrate the plugin in your Unity project, bake your scene, and apply the acoustics to sound sources.
services: cognitive-services
author: kegodin
manager: noelc
ms.service: cognitive-services
ms.component: acoustics
ms.topic: article
ms.date: 08/17/2018
ms.author: kegodin
ms.openlocfilehash: be2aa63be10b0e7a6f1869afae48c7f15c0b18cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868100"
---
# <a name="getting-started-with-project-acoustics"></a><span data-ttu-id="5c038-103">Getting started with Project Acoustics</span><span class="sxs-lookup"><span data-stu-id="5c038-103">Getting started with Project Acoustics</span></span>
<span data-ttu-id="5c038-104">This quickstart guide will show you how to integrate the plugin in your Unity project, bake your scene, and apply the acoustics to sound sources.</span><span class="sxs-lookup"><span data-stu-id="5c038-104">This quickstart guide will show you how to integrate the plugin in your Unity project, bake your scene, and apply the acoustics to sound sources.</span></span> <span data-ttu-id="5c038-105">For this quickstart, you'll need to first create an [Azure batch account](create-azure-account.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-105">For this quickstart, you'll need to first create an [Azure batch account](create-azure-account.md).</span></span> <span data-ttu-id="5c038-106">This guide assumes some familiarity with Unity.</span><span class="sxs-lookup"><span data-stu-id="5c038-106">This guide assumes some familiarity with Unity.</span></span>

## <a name="download-the-plugin"></a><span data-ttu-id="5c038-107">Download the plugin</span><span class="sxs-lookup"><span data-stu-id="5c038-107">Download the plugin</span></span>
<span data-ttu-id="5c038-108">Register [here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRwMoAEhDCLJNqtVIPwQN6rpUOFRZREJRR0NIQllDOTQ1U0JMNVc4OFNFSy4u) to join the Designer Preview.</span><span class="sxs-lookup"><span data-stu-id="5c038-108">Register [here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRwMoAEhDCLJNqtVIPwQN6rpUOFRZREJRR0NIQllDOTQ1U0JMNVc4OFNFSy4u) to join the Designer Preview.</span></span>

## <a name="supported-platforms-for-quickstart"></a><span data-ttu-id="5c038-109">Supported platforms for quickstart</span><span class="sxs-lookup"><span data-stu-id="5c038-109">Supported platforms for quickstart</span></span>
* [<span data-ttu-id="5c038-110">Unity 2018.2+</span><span class="sxs-lookup"><span data-stu-id="5c038-110">Unity 2018.2+</span></span>](http://www.unity3d.com)
  * <span data-ttu-id="5c038-111">Requires setting your project to the **.NET 4.x Equivalent** scripting runtime version</span><span class="sxs-lookup"><span data-stu-id="5c038-111">Requires setting your project to the **.NET 4.x Equivalent** scripting runtime version</span></span> 
  * <span data-ttu-id="5c038-112">Requires the Windows-based Unity editor</span><span class="sxs-lookup"><span data-stu-id="5c038-112">Requires the Windows-based Unity editor</span></span>

## <a name="import-the-plugin"></a><span data-ttu-id="5c038-113">Import the plugin</span><span class="sxs-lookup"><span data-stu-id="5c038-113">Import the plugin</span></span>
<span data-ttu-id="5c038-114">Import the acoustics UnityPackage to your project.</span><span class="sxs-lookup"><span data-stu-id="5c038-114">Import the acoustics UnityPackage to your project.</span></span> 
* <span data-ttu-id="5c038-115">In Unity, go to **Assets > Import Package > Custom Package...**</span><span class="sxs-lookup"><span data-stu-id="5c038-115">In Unity, go to **Assets > Import Package > Custom Package...**</span></span>

![Import Package](media/ImportPackage.png)  

* <span data-ttu-id="5c038-117">Choose **MicrosoftAcoustics.unitypackage**</span><span class="sxs-lookup"><span data-stu-id="5c038-117">Choose **MicrosoftAcoustics.unitypackage**</span></span>

<span data-ttu-id="5c038-118">If you're importing the plugin into an existing project, your project may already have an **mcs.rsp** file in the project root, which specifies options to the C# compiler.</span><span class="sxs-lookup"><span data-stu-id="5c038-118">If you're importing the plugin into an existing project, your project may already have an **mcs.rsp** file in the project root, which specifies options to the C# compiler.</span></span> <span data-ttu-id="5c038-119">You'll need to merge the contents of that file with the mcs.rsp file that comes with the Project Acoustics plugin.</span><span class="sxs-lookup"><span data-stu-id="5c038-119">You'll need to merge the contents of that file with the mcs.rsp file that comes with the Project Acoustics plugin.</span></span>

## <a name="enable-the-plugin"></a><span data-ttu-id="5c038-120">Enable the plugin</span><span class="sxs-lookup"><span data-stu-id="5c038-120">Enable the plugin</span></span>
<span data-ttu-id="5c038-121">The bake portion of the acoustics toolkit requires the .NET 4.x scripting runtime version.</span><span class="sxs-lookup"><span data-stu-id="5c038-121">The bake portion of the acoustics toolkit requires the .NET 4.x scripting runtime version.</span></span> <span data-ttu-id="5c038-122">Package import will update your Unity player settings.</span><span class="sxs-lookup"><span data-stu-id="5c038-122">Package import will update your Unity player settings.</span></span> <span data-ttu-id="5c038-123">Restart Unity for this setting to take effect.</span><span class="sxs-lookup"><span data-stu-id="5c038-123">Restart Unity for this setting to take effect.</span></span>

![Player Settings](media/PlayerSettings.png)

![.NET 4.5](media/Net45.png)

## <a name="create-a-navigation-mesh"></a><span data-ttu-id="5c038-126">Create a navigation mesh</span><span class="sxs-lookup"><span data-stu-id="5c038-126">Create a navigation mesh</span></span>
<span data-ttu-id="5c038-127">Use the standard [Unity workflow](https://docs.unity3d.com/Manual/nav-BuildingNavMesh.html) to create a navigation mesh for your project.</span><span class="sxs-lookup"><span data-stu-id="5c038-127">Use the standard [Unity workflow](https://docs.unity3d.com/Manual/nav-BuildingNavMesh.html) to create a navigation mesh for your project.</span></span> <span data-ttu-id="5c038-128">For information on how to use your own navigation meshes, see the [bake UI walk through](bake-ui-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-128">For information on how to use your own navigation meshes, see the [bake UI walk through](bake-ui-walkthrough.md).</span></span>

## <a name="mark-static-meshes-for-acoustics"></a><span data-ttu-id="5c038-129">Mark static meshes for acoustics</span><span class="sxs-lookup"><span data-stu-id="5c038-129">Mark static meshes for acoustics</span></span>
<span data-ttu-id="5c038-130">Bring up the acoustics window using **Window > Acoustics** in Unity.</span><span class="sxs-lookup"><span data-stu-id="5c038-130">Bring up the acoustics window using **Window > Acoustics** in Unity.</span></span> <span data-ttu-id="5c038-131">This window can be docked next to the Inspector.</span><span class="sxs-lookup"><span data-stu-id="5c038-131">This window can be docked next to the Inspector.</span></span>

![Open Acoustics Window](media/WindowAcoustics.png)

<span data-ttu-id="5c038-133">In Unity's hierarchy window, de-select any selected items.</span><span class="sxs-lookup"><span data-stu-id="5c038-133">In Unity's hierarchy window, de-select any selected items.</span></span> <span data-ttu-id="5c038-134">In the acoustics **Object** tab click the "Acoustics Geometry" checkbox to mark all meshes and terrains in your scene as acoustics geometry.</span><span class="sxs-lookup"><span data-stu-id="5c038-134">In the acoustics **Object** tab click the "Acoustics Geometry" checkbox to mark all meshes and terrains in your scene as acoustics geometry.</span></span>

<span data-ttu-id="5c038-135">On the **Materials** tab, assign the acoustic materials to materials used in your scene.</span><span class="sxs-lookup"><span data-stu-id="5c038-135">On the **Materials** tab, assign the acoustic materials to materials used in your scene.</span></span> <span data-ttu-id="5c038-136">The **Default** material has absorption equivalent to concrete.</span><span class="sxs-lookup"><span data-stu-id="5c038-136">The **Default** material has absorption equivalent to concrete.</span></span> <span data-ttu-id="5c038-137">For more information on specifying your own materials properties, see the [design process page](design-process.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-137">For more information on specifying your own materials properties, see the [design process page](design-process.md).</span></span>

![Materials Tab](media/MaterialsTab.png)

## <a name="preview-the-probes"></a><span data-ttu-id="5c038-139">Preview the probes</span><span class="sxs-lookup"><span data-stu-id="5c038-139">Preview the probes</span></span>
<span data-ttu-id="5c038-140">On the **Probes** tab, click **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="5c038-140">On the **Probes** tab, click **Calculate**.</span></span> <span data-ttu-id="5c038-141">This calculation may take a few minutes, depending on scene size.</span><span class="sxs-lookup"><span data-stu-id="5c038-141">This calculation may take a few minutes, depending on scene size.</span></span> <span data-ttu-id="5c038-142">When calculation is complete, you'll see floating spheres in the scene view, which mark the locations for acoustics simulation, called "probe points".</span><span class="sxs-lookup"><span data-stu-id="5c038-142">When calculation is complete, you'll see floating spheres in the scene view, which mark the locations for acoustics simulation, called "probe points".</span></span> <span data-ttu-id="5c038-143">If you get close enough to an object in the scene window, you can also see the scene voxelization.</span><span class="sxs-lookup"><span data-stu-id="5c038-143">If you get close enough to an object in the scene window, you can also see the scene voxelization.</span></span> <span data-ttu-id="5c038-144">The green voxels should line up with the objects you marked as geometry.</span><span class="sxs-lookup"><span data-stu-id="5c038-144">The green voxels should line up with the objects you marked as geometry.</span></span> <span data-ttu-id="5c038-145">The probe points and voxel displays can be toggled in the Gizmos menu in the top right of the scene view.</span><span class="sxs-lookup"><span data-stu-id="5c038-145">The probe points and voxel displays can be toggled in the Gizmos menu in the top right of the scene view.</span></span>

![GizmosPreview](media/BakePreviewWithGizmos.png)

## <a name="bake-the-scene"></a><span data-ttu-id="5c038-147">Bake the scene</span><span class="sxs-lookup"><span data-stu-id="5c038-147">Bake the scene</span></span>
<span data-ttu-id="5c038-148">In the **Bake** tab, enter your Azure credentials and click **Bake**.</span><span class="sxs-lookup"><span data-stu-id="5c038-148">In the **Bake** tab, enter your Azure credentials and click **Bake**.</span></span> <span data-ttu-id="5c038-149">If you don't have an Azure Batch account, see [this walkthrough for our recommended account setup](create-azure-account.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-149">If you don't have an Azure Batch account, see [this walkthrough for our recommended account setup](create-azure-account.md).</span></span>
<span data-ttu-id="5c038-150">When the bake is finished, the data file will automatically be downloaded to the **Assets/AcousticsData** directory in your project.</span><span class="sxs-lookup"><span data-stu-id="5c038-150">When the bake is finished, the data file will automatically be downloaded to the **Assets/AcousticsData** directory in your project.</span></span>

## <a name="set-up-audio-runtime-dsp"></a><span data-ttu-id="5c038-151">Set up audio runtime DSP</span><span class="sxs-lookup"><span data-stu-id="5c038-151">Set up audio runtime DSP</span></span>
<span data-ttu-id="5c038-152">We embed the audio runtime DSP for acoustics in Unity's spatializer framework and integrate it with HRTF-based spatialization.</span><span class="sxs-lookup"><span data-stu-id="5c038-152">We embed the audio runtime DSP for acoustics in Unity's spatializer framework and integrate it with HRTF-based spatialization.</span></span> <span data-ttu-id="5c038-153">To enable acoustics processing, switch to the **Microsoft Acoustics** spatializer by going to **Edit > Project Settings > Audio**, and select **Microsoft Acoustics** as the **Spatializer Plugin** for your project.</span><span class="sxs-lookup"><span data-stu-id="5c038-153">To enable acoustics processing, switch to the **Microsoft Acoustics** spatializer by going to **Edit > Project Settings > Audio**, and select **Microsoft Acoustics** as the **Spatializer Plugin** for your project.</span></span> <span data-ttu-id="5c038-154">Also, make sure the **DSP Buffer Size** is set to Best Performance.</span><span class="sxs-lookup"><span data-stu-id="5c038-154">Also, make sure the **DSP Buffer Size** is set to Best Performance.</span></span>

![Project Settings](media/ProjectSettings.png)  

![Project Acoustics Spatializer](media/ChooseSpatializer.png)

<span data-ttu-id="5c038-157">Open the Audio Mixer (**Window > Audio Mixer**).</span><span class="sxs-lookup"><span data-stu-id="5c038-157">Open the Audio Mixer (**Window > Audio Mixer**).</span></span> <span data-ttu-id="5c038-158">Make sure you have at least one Mixer, with one group.</span><span class="sxs-lookup"><span data-stu-id="5c038-158">Make sure you have at least one Mixer, with one group.</span></span> <span data-ttu-id="5c038-159">If you don't, Click the '+' button to the right of **Mixers**.</span><span class="sxs-lookup"><span data-stu-id="5c038-159">If you don't, Click the '+' button to the right of **Mixers**.</span></span> <span data-ttu-id="5c038-160">Right-click the bottom of the channel strip in the effects section, and add the **Microsoft Acoustics Mixer** effect.</span><span class="sxs-lookup"><span data-stu-id="5c038-160">Right-click the bottom of the channel strip in the effects section, and add the **Microsoft Acoustics Mixer** effect.</span></span> <span data-ttu-id="5c038-161">Note that only one Project Acoustics Mixer is supported at a time.</span><span class="sxs-lookup"><span data-stu-id="5c038-161">Note that only one Project Acoustics Mixer is supported at a time.</span></span>

![Audio Mixer](media/AudioMixer.png)

## <a name="set-up-the-acoustics-lookup-table"></a><span data-ttu-id="5c038-163">Set up the acoustics lookup table</span><span class="sxs-lookup"><span data-stu-id="5c038-163">Set up the acoustics lookup table</span></span>
<span data-ttu-id="5c038-164">Drag and drop the **Microsoft Acoustics** prefab from the project panel into your scene:</span><span class="sxs-lookup"><span data-stu-id="5c038-164">Drag and drop the **Microsoft Acoustics** prefab from the project panel into your scene:</span></span>

![Acoustics Prefab](media/AcousticsPrefab.png)

<span data-ttu-id="5c038-166">Click on the **ProjectAcoustics** Game Object and go to its inspector panel.</span><span class="sxs-lookup"><span data-stu-id="5c038-166">Click on the **ProjectAcoustics** Game Object and go to its inspector panel.</span></span> <span data-ttu-id="5c038-167">Specify the location of your bake result (the .ACE file, in **Assets/AcousticsData**) by drag-and-dropping it into the Acoustics Manager script, or by clicking on the circle button next to the text box.</span><span class="sxs-lookup"><span data-stu-id="5c038-167">Specify the location of your bake result (the .ACE file, in **Assets/AcousticsData**) by drag-and-dropping it into the Acoustics Manager script, or by clicking on the circle button next to the text box.</span></span>

![Acoustics Manager](media/AcousticsManager.png)  

## <a name="apply-acoustics-to-sound-sources"></a><span data-ttu-id="5c038-169">Apply acoustics to sound sources</span><span class="sxs-lookup"><span data-stu-id="5c038-169">Apply acoustics to sound sources</span></span>
<span data-ttu-id="5c038-170">Create an audio source.</span><span class="sxs-lookup"><span data-stu-id="5c038-170">Create an audio source.</span></span> <span data-ttu-id="5c038-171">Click the checkbox at the bottom of the AudioSource's inspector panel that says **Spatialize**.</span><span class="sxs-lookup"><span data-stu-id="5c038-171">Click the checkbox at the bottom of the AudioSource's inspector panel that says **Spatialize**.</span></span> <span data-ttu-id="5c038-172">Make sure **Spatial Blend** is set to full 3D.</span><span class="sxs-lookup"><span data-stu-id="5c038-172">Make sure **Spatial Blend** is set to full 3D.</span></span>  

![Audio Source](media/AudioSource.png)

## <a name="apply-post-bake-design"></a><span data-ttu-id="5c038-174">Apply post-bake design</span><span class="sxs-lookup"><span data-stu-id="5c038-174">Apply post-bake design</span></span>
<span data-ttu-id="5c038-175">You can attach the script **AcousticsSourceCustomization** to a sound source in your scene to enable additional source design parameters, by clicking **Add Component** and choosing **Scripts > Acoustics Source Customization**:</span><span class="sxs-lookup"><span data-stu-id="5c038-175">You can attach the script **AcousticsSourceCustomization** to a sound source in your scene to enable additional source design parameters, by clicking **Add Component** and choosing **Scripts > Acoustics Source Customization**:</span></span>

![Source Customization](media/SourceCustomization.png)

<span data-ttu-id="5c038-177">There are also parameters on the **Microsoft Acoustics Mixer**.</span><span class="sxs-lookup"><span data-stu-id="5c038-177">There are also parameters on the **Microsoft Acoustics Mixer**.</span></span> <span data-ttu-id="5c038-178">For more information about post-bake design, see [design parameters](design-process.md).</span><span class="sxs-lookup"><span data-stu-id="5c038-178">For more information about post-bake design, see [design parameters](design-process.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c038-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c038-179">Next steps</span></span>
* <span data-ttu-id="5c038-180">Try the [sample scene](sample-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="5c038-180">Try the [sample scene](sample-walkthrough.md)</span></span>
* <span data-ttu-id="5c038-181">Learn about the full set of [bake features](bake-ui-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="5c038-181">Learn about the full set of [bake features](bake-ui-walkthrough.md)</span></span>
* <span data-ttu-id="5c038-182">Explore more detailed [design parameters](design-process.md)</span><span class="sxs-lookup"><span data-stu-id="5c038-182">Explore more detailed [design parameters](design-process.md)</span></span>

