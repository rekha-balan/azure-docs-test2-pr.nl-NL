---
title: Frequently Asked Questions about Acoustics - Cognitive Services
description: This page provides answers to questions asked frequently about Project Acoustics, including download instructions and bake process.
services: cognitive-services
author: kegodin
manager: noelc
ms.service: cognitive-services
ms.component: acoustics
ms.topic: article
ms.date: 08/17/2018
ms.author: kegodin
ms.openlocfilehash: ea687cb98369c315f3ab236922c4c67f662ac14c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969251"
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="7125f-103">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="7125f-103">Frequently asked questions</span></span>

## <a name="what-is-project-acoustics"></a><span data-ttu-id="7125f-104">What is Project Acoustics?</span><span class="sxs-lookup"><span data-stu-id="7125f-104">What is Project Acoustics?</span></span>

<span data-ttu-id="7125f-105">The Project Acoustics Unity plugin is an acoustics system that calculates sound wave behavior prior to runtime, akin to static lighting.</span><span class="sxs-lookup"><span data-stu-id="7125f-105">The Project Acoustics Unity plugin is an acoustics system that calculates sound wave behavior prior to runtime, akin to static lighting.</span></span> <span data-ttu-id="7125f-106">The cloud does the heavy lifting of wave physics at design time, so runtime CPU cost is low.</span><span class="sxs-lookup"><span data-stu-id="7125f-106">The cloud does the heavy lifting of wave physics at design time, so runtime CPU cost is low.</span></span>  

## <a name="where-can-i-download-the-plugin"></a><span data-ttu-id="7125f-107">Where can I download the plugin?</span><span class="sxs-lookup"><span data-stu-id="7125f-107">Where can I download the plugin?</span></span>

<span data-ttu-id="7125f-108">If you're interested in evaluating the acoustics plugin, register [here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRwMoAEhDCLJNqtVIPwQN6rpUOFRZREJRR0NIQllDOTQ1U0JMNVc4OFNFSy4u) to join the Designer Preview.</span><span class="sxs-lookup"><span data-stu-id="7125f-108">If you're interested in evaluating the acoustics plugin, register [here](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRwMoAEhDCLJNqtVIPwQN6rpUOFRZREJRR0NIQllDOTQ1U0JMNVc4OFNFSy4u) to join the Designer Preview.</span></span>

## <a name="is-azure-used-at-runtime"></a><span data-ttu-id="7125f-109">Is Azure used at runtime?</span><span class="sxs-lookup"><span data-stu-id="7125f-109">Is Azure used at runtime?</span></span>

<span data-ttu-id="7125f-110">No, cloud integration is used only during the precompute stage at design time.</span><span class="sxs-lookup"><span data-stu-id="7125f-110">No, cloud integration is used only during the precompute stage at design time.</span></span>
 
## <a name="what-is-simulation-input"></a><span data-ttu-id="7125f-111">What is simulation input?</span><span class="sxs-lookup"><span data-stu-id="7125f-111">What is simulation input?</span></span> 

<span data-ttu-id="7125f-112">The simulation input is your 3D scene, virtual environment or game level.</span><span class="sxs-lookup"><span data-stu-id="7125f-112">The simulation input is your 3D scene, virtual environment or game level.</span></span> <span data-ttu-id="7125f-113">Project Acoustics performs 3D volumetric wave simulations that model the physics of sound closely, including smooth occlusion and scattering.</span><span class="sxs-lookup"><span data-stu-id="7125f-113">Project Acoustics performs 3D volumetric wave simulations that model the physics of sound closely, including smooth occlusion and scattering.</span></span>
 
## <a name="what-is-the-runtime-cost"></a><span data-ttu-id="7125f-114">What is the runtime cost?</span><span class="sxs-lookup"><span data-stu-id="7125f-114">What is the runtime cost?</span></span>

<span data-ttu-id="7125f-115">Acoustics takes about 0.01% of CPU per source per frame.</span><span class="sxs-lookup"><span data-stu-id="7125f-115">Acoustics takes about 0.01% of CPU per source per frame.</span></span> <span data-ttu-id="7125f-116">RAM usage depends on scene size and can range from 10 to 100 MB.</span><span class="sxs-lookup"><span data-stu-id="7125f-116">RAM usage depends on scene size and can range from 10 to 100 MB.</span></span>
 
## <a name="do-i-need-to-simplify-the-level-geometry-control-triangle-count-make-meshes-watertight"></a><span data-ttu-id="7125f-117">Do I need to simplify the level geometry?</span><span class="sxs-lookup"><span data-stu-id="7125f-117">Do I need to simplify the level geometry?</span></span> <span data-ttu-id="7125f-118">Control triangle count?</span><span class="sxs-lookup"><span data-stu-id="7125f-118">Control triangle count?</span></span> <span data-ttu-id="7125f-119">Make meshes watertight?</span><span class="sxs-lookup"><span data-stu-id="7125f-119">Make meshes watertight?</span></span>

<span data-ttu-id="7125f-120">No.</span><span class="sxs-lookup"><span data-stu-id="7125f-120">No.</span></span> <span data-ttu-id="7125f-121">The system will ingest detailed level geometry directly.</span><span class="sxs-lookup"><span data-stu-id="7125f-121">The system will ingest detailed level geometry directly.</span></span> <span data-ttu-id="7125f-122">It will be voxelized for internal processing.</span><span class="sxs-lookup"><span data-stu-id="7125f-122">It will be voxelized for internal processing.</span></span>
 
## <a name="whats-in-the-runtime-lookup-table"></a><span data-ttu-id="7125f-123">What's in the runtime lookup table?</span><span class="sxs-lookup"><span data-stu-id="7125f-123">What's in the runtime lookup table?</span></span>

<span data-ttu-id="7125f-124">The ACE file is a table of acoustic parameters between numerous source and listener location pairs.</span><span class="sxs-lookup"><span data-stu-id="7125f-124">The ACE file is a table of acoustic parameters between numerous source and listener location pairs.</span></span>
 
## <a name="can-it-handle-moving-sources"></a><span data-ttu-id="7125f-125">Can it handle moving sources?</span><span class="sxs-lookup"><span data-stu-id="7125f-125">Can it handle moving sources?</span></span>

<span data-ttu-id="7125f-126">Yes, the **Microsoft Acoustics** Unity spatializer plugin consults the lookup table on each audio processing tick with the current source and listener locations.</span><span class="sxs-lookup"><span data-stu-id="7125f-126">Yes, the **Microsoft Acoustics** Unity spatializer plugin consults the lookup table on each audio processing tick with the current source and listener locations.</span></span> <span data-ttu-id="7125f-127">The spatializer's DSP smoothly updates the acoustic processing parameters on each tick.</span><span class="sxs-lookup"><span data-stu-id="7125f-127">The spatializer's DSP smoothly updates the acoustic processing parameters on each tick.</span></span>
 
## <a name="can-it-handle-dynamic-geometry-closing-doors-walls-blown-away"></a><span data-ttu-id="7125f-128">Can it handle dynamic geometry?</span><span class="sxs-lookup"><span data-stu-id="7125f-128">Can it handle dynamic geometry?</span></span> <span data-ttu-id="7125f-129">Closing doors?</span><span class="sxs-lookup"><span data-stu-id="7125f-129">Closing doors?</span></span> <span data-ttu-id="7125f-130">Walls blown away?</span><span class="sxs-lookup"><span data-stu-id="7125f-130">Walls blown away?</span></span>

<span data-ttu-id="7125f-131">No.</span><span class="sxs-lookup"><span data-stu-id="7125f-131">No.</span></span> <span data-ttu-id="7125f-132">The acoustic parameters are precomputed based on the static state of a game level.</span><span class="sxs-lookup"><span data-stu-id="7125f-132">The acoustic parameters are precomputed based on the static state of a game level.</span></span> <span data-ttu-id="7125f-133">We suggest leaving door geometry out of acoustics, and then apply additional occlusion based on the state of destructible and movable game objects using established techniques.</span><span class="sxs-lookup"><span data-stu-id="7125f-133">We suggest leaving door geometry out of acoustics, and then apply additional occlusion based on the state of destructible and movable game objects using established techniques.</span></span>
 
## <a name="does-it-handle-materials"></a><span data-ttu-id="7125f-134">Does it handle materials?</span><span class="sxs-lookup"><span data-stu-id="7125f-134">Does it handle materials?</span></span>

<span data-ttu-id="7125f-135">Yes.</span><span class="sxs-lookup"><span data-stu-id="7125f-135">Yes.</span></span> <span data-ttu-id="7125f-136">Materials are picked from the physical material names in your level, driving absorptivity.</span><span class="sxs-lookup"><span data-stu-id="7125f-136">Materials are picked from the physical material names in your level, driving absorptivity.</span></span>
 
## <a name="what-do-the-probes-represent"></a><span data-ttu-id="7125f-137">What do the "probes" represent?</span><span class="sxs-lookup"><span data-stu-id="7125f-137">What do the "probes" represent?</span></span>

<span data-ttu-id="7125f-138">Probes are a sampling of possible player locations.</span><span class="sxs-lookup"><span data-stu-id="7125f-138">Probes are a sampling of possible player locations.</span></span> <span data-ttu-id="7125f-139">Each probe represents a separate wave simulation of the scene originating at the probe location.</span><span class="sxs-lookup"><span data-stu-id="7125f-139">Each probe represents a separate wave simulation of the scene originating at the probe location.</span></span> <span data-ttu-id="7125f-140">At runtime, acoustic parameters for the listener location are interpolated from nearby probe locations.</span><span class="sxs-lookup"><span data-stu-id="7125f-140">At runtime, acoustic parameters for the listener location are interpolated from nearby probe locations.</span></span>
 
## <a name="why-spend-so-much-compute-in-the-cloud-what-does-it-buy-me"></a><span data-ttu-id="7125f-141">Why spend so much compute in the cloud?</span><span class="sxs-lookup"><span data-stu-id="7125f-141">Why spend so much compute in the cloud?</span></span> <span data-ttu-id="7125f-142">What does it buy me?</span><span class="sxs-lookup"><span data-stu-id="7125f-142">What does it buy me?</span></span>

<span data-ttu-id="7125f-143">Project Acoustics provides accurate and reliable acoustic parameters even for ultra-complex virtual environments, taking every architectural aspect into account.</span><span class="sxs-lookup"><span data-stu-id="7125f-143">Project Acoustics provides accurate and reliable acoustic parameters even for ultra-complex virtual environments, taking every architectural aspect into account.</span></span> <span data-ttu-id="7125f-144">It provides smooth occlusion/obstruction without all the manual work and dynamic reverb variation without drawing volumes.</span><span class="sxs-lookup"><span data-stu-id="7125f-144">It provides smooth occlusion/obstruction without all the manual work and dynamic reverb variation without drawing volumes.</span></span> <span data-ttu-id="7125f-145">All while remaining light on CPU during runtime.</span><span class="sxs-lookup"><span data-stu-id="7125f-145">All while remaining light on CPU during runtime.</span></span>

## <a name="what-exactly-happens-during-baking"></a><span data-ttu-id="7125f-146">What exactly happens during "baking"?</span><span class="sxs-lookup"><span data-stu-id="7125f-146">What exactly happens during "baking"?</span></span>

<span data-ttu-id="7125f-147">The system considers potential player locations to generate a set of uniformly spaced "probe" sample positions.</span><span class="sxs-lookup"><span data-stu-id="7125f-147">The system considers potential player locations to generate a set of uniformly spaced "probe" sample positions.</span></span> <span data-ttu-id="7125f-148">A bake for a level consists of independent tasks for each probe: The system considers a cuboid "Simulation Region" centered at the probe and does a detailed wave simulation within that region at up to 25 cm resolution.</span><span class="sxs-lookup"><span data-stu-id="7125f-148">A bake for a level consists of independent tasks for each probe: The system considers a cuboid "Simulation Region" centered at the probe and does a detailed wave simulation within that region at up to 25 cm resolution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7125f-149">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7125f-149">Next Steps</span></span>
* <span data-ttu-id="7125f-150">Explore the [sample scene](sample-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="7125f-150">Explore the [sample scene](sample-walkthrough.md)</span></span>

