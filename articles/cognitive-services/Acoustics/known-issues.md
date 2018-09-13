---
title: Known issues with acoustics plugin - Cognitive Services
description: You might encounter the following known issues when using the Designer Preview for Project Acoustics.
services: cognitive-services
author: kylestorck
manager: noelc
ms.service: cognitive-services
ms.component: acoustics
ms.topic: article
ms.date: 08/17/2018
ms.author: kylestorck
ms.openlocfilehash: b42fb73396a1b541c8c57b1257e3bcfca23c6b8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857025"
---
# <a name="known-issues"></a><span data-ttu-id="f9167-103">Known Issues</span><span class="sxs-lookup"><span data-stu-id="f9167-103">Known Issues</span></span>
<span data-ttu-id="f9167-104">You might encounter the following known issues when using the Designer Preview for Project Acoustics.</span><span class="sxs-lookup"><span data-stu-id="f9167-104">You might encounter the following known issues when using the Designer Preview for Project Acoustics.</span></span>

## <a name="acoustic-parameters-are-lost-when-you-rename-a-scene"></a><span data-ttu-id="f9167-105">Acoustic parameters are lost when you rename a scene</span><span class="sxs-lookup"><span data-stu-id="f9167-105">Acoustic parameters are lost when you rename a scene</span></span>

<span data-ttu-id="f9167-106">If you rename a scene, all the acoustic parameters that belong to that scene will not automatically transfer to the new scene.</span><span class="sxs-lookup"><span data-stu-id="f9167-106">If you rename a scene, all the acoustic parameters that belong to that scene will not automatically transfer to the new scene.</span></span> <span data-ttu-id="f9167-107">They will still exist in the old asset file however.</span><span class="sxs-lookup"><span data-stu-id="f9167-107">They will still exist in the old asset file however.</span></span> <span data-ttu-id="f9167-108">Look for the **SceneName_AcousticParameters.asset** file inside the **Editor** directory next to your scene file.</span><span class="sxs-lookup"><span data-stu-id="f9167-108">Look for the **SceneName_AcousticParameters.asset** file inside the **Editor** directory next to your scene file.</span></span> <span data-ttu-id="f9167-109">Rename your file to reflect the new scene name.</span><span class="sxs-lookup"><span data-stu-id="f9167-109">Rename your file to reflect the new scene name.</span></span>

## <a name="the-default-path-for-the-acousticsdata-folder-in-probes-tab-is-an-absolute-path"></a><span data-ttu-id="f9167-110">The default path for the AcousticsData folder in Probes tab is an absolute path</span><span class="sxs-lookup"><span data-stu-id="f9167-110">The default path for the AcousticsData folder in Probes tab is an absolute path</span></span>

<span data-ttu-id="f9167-111">This should default to a relative path to make it easier to share projects between collaborators.</span><span class="sxs-lookup"><span data-stu-id="f9167-111">This should default to a relative path to make it easier to share projects between collaborators.</span></span> <span data-ttu-id="f9167-112">As a workaround, change the path to be relative to project directory.</span><span class="sxs-lookup"><span data-stu-id="f9167-112">As a workaround, change the path to be relative to project directory.</span></span>

## <a name="runtime-voxels-are-a-different-size-than-design-time-voxels"></a><span data-ttu-id="f9167-113">Runtime voxels are a different size than design-time voxels</span><span class="sxs-lookup"><span data-stu-id="f9167-113">Runtime voxels are a different size than design-time voxels</span></span>

<span data-ttu-id="f9167-114">If you do a **Calculate** on the **Probes** tab and view the voxels, then do a bake and view voxels at runtime for the same scene, the voxels are different sizes.</span><span class="sxs-lookup"><span data-stu-id="f9167-114">If you do a **Calculate** on the **Probes** tab and view the voxels, then do a bake and view voxels at runtime for the same scene, the voxels are different sizes.</span></span> <span data-ttu-id="f9167-115">The voxels shown pre-bake are the voxels used in simulation.</span><span class="sxs-lookup"><span data-stu-id="f9167-115">The voxels shown pre-bake are the voxels used in simulation.</span></span> <span data-ttu-id="f9167-116">The voxels shown at runtime are used for interpolation between probe points.</span><span class="sxs-lookup"><span data-stu-id="f9167-116">The voxels shown at runtime are used for interpolation between probe points.</span></span> <span data-ttu-id="f9167-117">This may cause an inconsistency where portals will appear open at runtime that aren't actually open.</span><span class="sxs-lookup"><span data-stu-id="f9167-117">This may cause an inconsistency where portals will appear open at runtime that aren't actually open.</span></span>

## <a name="uwp-builds-not-working"></a><span data-ttu-id="f9167-118">UWP builds not working</span><span class="sxs-lookup"><span data-stu-id="f9167-118">UWP builds not working</span></span>

<span data-ttu-id="f9167-119">On the latest versions of Unity (2018.2+), UWP builds are not succeeding.</span><span class="sxs-lookup"><span data-stu-id="f9167-119">On the latest versions of Unity (2018.2+), UWP builds are not succeeding.</span></span> <span data-ttu-id="f9167-120">The run phase of the build will stall and you will get "Unity extensions are not yet initialized" errors.</span><span class="sxs-lookup"><span data-stu-id="f9167-120">The run phase of the build will stall and you will get "Unity extensions are not yet initialized" errors.</span></span> <span data-ttu-id="f9167-121">This is tracked by [this Unity issue](https://fogbugz.unity3d.com/default.asp?1070491_1rgf14bakv5u779d).</span><span class="sxs-lookup"><span data-stu-id="f9167-121">This is tracked by [this Unity issue](https://fogbugz.unity3d.com/default.asp?1070491_1rgf14bakv5u779d).</span></span>

## <a name="unity-crashes-when-closing-project"></a><span data-ttu-id="f9167-122">Unity crashes when closing project</span><span class="sxs-lookup"><span data-stu-id="f9167-122">Unity crashes when closing project</span></span>

<span data-ttu-id="f9167-123">On the latest versions of Unity (2018.2+), there is a known bug where Unity will crash when you close your project.</span><span class="sxs-lookup"><span data-stu-id="f9167-123">On the latest versions of Unity (2018.2+), there is a known bug where Unity will crash when you close your project.</span></span> <span data-ttu-id="f9167-124">This is tracked by [this Unity issue](https://issuetracker.unity3d.com/issues/crash-on-assetdatabase-getassetimporterversions-when-closing-a-specific-unity-project).</span><span class="sxs-lookup"><span data-stu-id="f9167-124">This is tracked by [this Unity issue](https://issuetracker.unity3d.com/issues/crash-on-assetdatabase-getassetimporterversions-when-closing-a-specific-unity-project).</span></span>

## <a name="trouble-deploying-to-android"></a><span data-ttu-id="f9167-125">Trouble deploying to Android</span><span class="sxs-lookup"><span data-stu-id="f9167-125">Trouble deploying to Android</span></span>
<span data-ttu-id="f9167-126">To use Project Acoustics on Android, change your build target to Android.</span><span class="sxs-lookup"><span data-stu-id="f9167-126">To use Project Acoustics on Android, change your build target to Android.</span></span> <span data-ttu-id="f9167-127">Some versions of Unity have a bug with deploying audio plugins -- make sure you are not using a version affected by [this bug](https://issuetracker.unity3d.com/issues/android-ios-audiosource-playing-through-google-resonance-audio-sdk-with-spatializer-enabled-does-not-play-on-built-player).</span><span class="sxs-lookup"><span data-stu-id="f9167-127">Some versions of Unity have a bug with deploying audio plugins -- make sure you are not using a version affected by [this bug](https://issuetracker.unity3d.com/issues/android-ios-audiosource-playing-through-google-resonance-audio-sdk-with-spatializer-enabled-does-not-play-on-built-player).</span></span>

## <a name="i-get-an-error-that-could-not-find-metadata-file-systemsecuritydll"></a><span data-ttu-id="f9167-128">I get an error that 'could not find metadata file System.Security.dll'</span><span class="sxs-lookup"><span data-stu-id="f9167-128">I get an error that 'could not find metadata file System.Security.dll'</span></span>

<span data-ttu-id="f9167-129">Ensure the Scripting Runtime Version in Player settings is set to **.NET 4.x Equivalent**, and restart Unity.</span><span class="sxs-lookup"><span data-stu-id="f9167-129">Ensure the Scripting Runtime Version in Player settings is set to **.NET 4.x Equivalent**, and restart Unity.</span></span>

## <a name="im-having-authentication-problems-when-connecting-to-azure"></a><span data-ttu-id="f9167-130">I'm having authentication problems when connecting to Azure</span><span class="sxs-lookup"><span data-stu-id="f9167-130">I'm having authentication problems when connecting to Azure</span></span>

<span data-ttu-id="f9167-131">Double-check you've used the correct credentials for your Azure account, that your account supports the type of node requested in the bake, and that your system clock is accurate.</span><span class="sxs-lookup"><span data-stu-id="f9167-131">Double-check you've used the correct credentials for your Azure account, that your account supports the type of node requested in the bake, and that your system clock is accurate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9167-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9167-132">Next steps</span></span>
* <span data-ttu-id="f9167-133">Get started [integrating acoustics in your Unity project](getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="f9167-133">Get started [integrating acoustics in your Unity project](getting-started.md)</span></span>

