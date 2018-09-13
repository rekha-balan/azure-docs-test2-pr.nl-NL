---
title: Introduction to acoustics - Cognitive Services
description: The Project Acoustics Unity plugin provides occlusion, reverberation, and spatialization for projects targeting VR and traditional screens.
services: cognitive-services
author: kegodin
manager: noelc
ms.service: cognitive-services
ms.component: acoustics
ms.topic: overview
ms.date: 08/17/2018
ms.author: kegodin
ms.openlocfilehash: d24657a71bcf84b56d65ec3862e02defcb0a220e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857570"
---
# <a name="what-is-project-acoustics"></a><span data-ttu-id="a056a-103">What is Project Acoustics?</span><span class="sxs-lookup"><span data-stu-id="a056a-103">What is Project Acoustics?</span></span>
<span data-ttu-id="a056a-104">The Project Acoustics Unity plugin provides occlusion, reverberation, and spatialization for projects targeting VR and traditional screens.</span><span class="sxs-lookup"><span data-stu-id="a056a-104">The Project Acoustics Unity plugin provides occlusion, reverberation, and spatialization for projects targeting VR and traditional screens.</span></span> <span data-ttu-id="a056a-105">It provides a way to design game acoustics that layers designer intentions over a physics-based wave simulation.</span><span class="sxs-lookup"><span data-stu-id="a056a-105">It provides a way to design game acoustics that layers designer intentions over a physics-based wave simulation.</span></span>

## <a name="why-use-acoustics-in-virtual-environments"></a><span data-ttu-id="a056a-106">Why use acoustics in virtual environments?</span><span class="sxs-lookup"><span data-stu-id="a056a-106">Why use acoustics in virtual environments?</span></span>
<span data-ttu-id="a056a-107">Humans use audio-visual cues to understand the world around them.</span><span class="sxs-lookup"><span data-stu-id="a056a-107">Humans use audio-visual cues to understand the world around them.</span></span> <span data-ttu-id="a056a-108">In virtual worlds, combining spatial audio with acoustics increases user immersion.</span><span class="sxs-lookup"><span data-stu-id="a056a-108">In virtual worlds, combining spatial audio with acoustics increases user immersion.</span></span> <span data-ttu-id="a056a-109">The acoustics tool described here analyzes virtual worlds to create a realistic acoustic simulation, and supports a post-simulation design process.</span><span class="sxs-lookup"><span data-stu-id="a056a-109">The acoustics tool described here analyzes virtual worlds to create a realistic acoustic simulation, and supports a post-simulation design process.</span></span> <span data-ttu-id="a056a-110">The analysis includes both the geometry and the materials for each surface in the world.</span><span class="sxs-lookup"><span data-stu-id="a056a-110">The analysis includes both the geometry and the materials for each surface in the world.</span></span> <span data-ttu-id="a056a-111">The simulation includes parameters such as arrival direction (portaling), reverb power, decay times, and occlusion and obstruction effects.</span><span class="sxs-lookup"><span data-stu-id="a056a-111">The simulation includes parameters such as arrival direction (portaling), reverb power, decay times, and occlusion and obstruction effects.</span></span>

## <a name="how-does-this-approach-to-acoustics-work"></a><span data-ttu-id="a056a-112">How does this approach to acoustics work?</span><span class="sxs-lookup"><span data-stu-id="a056a-112">How does this approach to acoustics work?</span></span>
<span data-ttu-id="a056a-113">The system relies on an offline compute of the virtual world, which allows a more complex simulation than if the analysis was done at run-time.</span><span class="sxs-lookup"><span data-stu-id="a056a-113">The system relies on an offline compute of the virtual world, which allows a more complex simulation than if the analysis was done at run-time.</span></span> <span data-ttu-id="a056a-114">The offline compute produces a lookup table of acoustic parameters.</span><span class="sxs-lookup"><span data-stu-id="a056a-114">The offline compute produces a lookup table of acoustic parameters.</span></span> <span data-ttu-id="a056a-115">A designer specifies rules applied to the parameters at run-time.</span><span class="sxs-lookup"><span data-stu-id="a056a-115">A designer specifies rules applied to the parameters at run-time.</span></span> <span data-ttu-id="a056a-116">Tweaking these rules can achieve hyper-realistic effects for high emotional intensity or hypo-realistic scenes for more background audio sounds.</span><span class="sxs-lookup"><span data-stu-id="a056a-116">Tweaking these rules can achieve hyper-realistic effects for high emotional intensity or hypo-realistic scenes for more background audio sounds.</span></span>

## <a name="design-process-comparison"></a><span data-ttu-id="a056a-117">Design process comparison</span><span class="sxs-lookup"><span data-stu-id="a056a-117">Design process comparison</span></span>
<span data-ttu-id="a056a-118">The Project Acoustics plugin supports a new design process for acoustics in Unity scenes.</span><span class="sxs-lookup"><span data-stu-id="a056a-118">The Project Acoustics plugin supports a new design process for acoustics in Unity scenes.</span></span> <span data-ttu-id="a056a-119">To explain this new design process, let's compare it to one of today's popular approaches to acoustics.</span><span class="sxs-lookup"><span data-stu-id="a056a-119">To explain this new design process, let's compare it to one of today's popular approaches to acoustics.</span></span>

### <a name="typical-approach-to-acoustics-today"></a><span data-ttu-id="a056a-120">Typical approach to acoustics today</span><span class="sxs-lookup"><span data-stu-id="a056a-120">Typical approach to acoustics today</span></span>
<span data-ttu-id="a056a-121">In a typical approach to acoustics today, you draw reverb volumes:</span><span class="sxs-lookup"><span data-stu-id="a056a-121">In a typical approach to acoustics today, you draw reverb volumes:</span></span>

![Design View](media/reverbZonesAltSPace2.png)

<span data-ttu-id="a056a-123">Then tweak parameters for each zone:</span><span class="sxs-lookup"><span data-stu-id="a056a-123">Then tweak parameters for each zone:</span></span>

![Design View](media/TooManyReverbParameters.png)

<span data-ttu-id="a056a-125">Finally, add ray-tracing logic to get the right occlusion and obstruction filtering throughout the scene, and path-searching logic for portaling.</span><span class="sxs-lookup"><span data-stu-id="a056a-125">Finally, add ray-tracing logic to get the right occlusion and obstruction filtering throughout the scene, and path-searching logic for portaling.</span></span> <span data-ttu-id="a056a-126">This code can add a run-time cost.</span><span class="sxs-lookup"><span data-stu-id="a056a-126">This code can add a run-time cost.</span></span> <span data-ttu-id="a056a-127">It also has problems with smoothness around corners and has edge cases in irregularly shaped scenes.</span><span class="sxs-lookup"><span data-stu-id="a056a-127">It also has problems with smoothness around corners and has edge cases in irregularly shaped scenes.</span></span>

### <a name="an-alternative-approach-with-physics-based-design"></a><span data-ttu-id="a056a-128">An alternative approach with physics-based design</span><span class="sxs-lookup"><span data-stu-id="a056a-128">An alternative approach with physics-based design</span></span>
<span data-ttu-id="a056a-129">With the approach provided by Project Acoustics' Unity plugin, you provide a static scene’s shape and materials.</span><span class="sxs-lookup"><span data-stu-id="a056a-129">With the approach provided by Project Acoustics' Unity plugin, you provide a static scene’s shape and materials.</span></span> <span data-ttu-id="a056a-130">Because the scene is voxelized and the process doesn't use ray-tracing, you don't need to provide a simplified or watertight acoustics mesh.</span><span class="sxs-lookup"><span data-stu-id="a056a-130">Because the scene is voxelized and the process doesn't use ray-tracing, you don't need to provide a simplified or watertight acoustics mesh.</span></span> <span data-ttu-id="a056a-131">It also isn't necessary to mark up the scene with reverb volumes.</span><span class="sxs-lookup"><span data-stu-id="a056a-131">It also isn't necessary to mark up the scene with reverb volumes.</span></span> <span data-ttu-id="a056a-132">The plugin uploads the scene to the cloud, where it uses physics based wave simulation.</span><span class="sxs-lookup"><span data-stu-id="a056a-132">The plugin uploads the scene to the cloud, where it uses physics based wave simulation.</span></span> <span data-ttu-id="a056a-133">The result is integrated into your project as a lookup table, and can be modified for aesthetic or gameplay effects.</span><span class="sxs-lookup"><span data-stu-id="a056a-133">The result is integrated into your project as a lookup table, and can be modified for aesthetic or gameplay effects.</span></span>

![Design View](media/GearsWithVoxels.jpg)

## <a name="requirements"></a><span data-ttu-id="a056a-135">Requirements</span><span class="sxs-lookup"><span data-stu-id="a056a-135">Requirements</span></span>
* <span data-ttu-id="a056a-136">Unity 2018.2+ for acoustics bakes, and Unity 5.2+ for sound design and deployment</span><span class="sxs-lookup"><span data-stu-id="a056a-136">Unity 2018.2+ for acoustics bakes, and Unity 5.2+ for sound design and deployment</span></span>
* <span data-ttu-id="a056a-137">Windows 64-bit Unity Editor</span><span class="sxs-lookup"><span data-stu-id="a056a-137">Windows 64-bit Unity Editor</span></span>
* <span data-ttu-id="a056a-138">Azure Batch subscription for acoustics bakes</span><span class="sxs-lookup"><span data-stu-id="a056a-138">Azure Batch subscription for acoustics bakes</span></span>
* <span data-ttu-id="a056a-139">Unity scripting runtime must be set to '.NET 4.x equivalent'</span><span class="sxs-lookup"><span data-stu-id="a056a-139">Unity scripting runtime must be set to '.NET 4.x equivalent'</span></span>

## <a name="platform-support"></a><span data-ttu-id="a056a-140">Platform support</span><span class="sxs-lookup"><span data-stu-id="a056a-140">Platform support</span></span>
* <span data-ttu-id="a056a-141">Windows desktop (x86 and AMD64)</span><span class="sxs-lookup"><span data-stu-id="a056a-141">Windows desktop (x86 and AMD64)</span></span>
* <span data-ttu-id="a056a-142">Windows UWP (x86, AMD64, and ARM)</span><span class="sxs-lookup"><span data-stu-id="a056a-142">Windows UWP (x86, AMD64, and ARM)</span></span>
* <span data-ttu-id="a056a-143">Android (x86 and ARM64)</span><span class="sxs-lookup"><span data-stu-id="a056a-143">Android (x86 and ARM64)</span></span>

## <a name="download"></a><span data-ttu-id="a056a-144">Download</span><span class="sxs-lookup"><span data-stu-id="a056a-144">Download</span></span>
<span data-ttu-id="a056a-145">If you're interested in evaluating the acoustics plugin, register [here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRwMoAEhDCLJNqtVIPwQN6rpUOFRZREJRR0NIQllDOTQ1U0JMNVc4OFNFSy4u) to join the Designer Preview.</span><span class="sxs-lookup"><span data-stu-id="a056a-145">If you're interested in evaluating the acoustics plugin, register [here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRwMoAEhDCLJNqtVIPwQN6rpUOFRZREJRR0NIQllDOTQ1U0JMNVc4OFNFSy4u) to join the Designer Preview.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a056a-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="a056a-146">Next steps</span></span>
* <span data-ttu-id="a056a-147">Learn more about the [design process](design-process.md)</span><span class="sxs-lookup"><span data-stu-id="a056a-147">Learn more about the [design process](design-process.md)</span></span>
* <span data-ttu-id="a056a-148">Get started [integrating acoustics in your Unity project](getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="a056a-148">Get started [integrating acoustics in your Unity project](getting-started.md)</span></span>

