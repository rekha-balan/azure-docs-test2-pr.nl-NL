---
title: Understanding device template versioning for your Azure IoT Central apps | Microsoft Docs
description: Iterate over your device templates by creating new versions and without impacting your live connected devices
author: sandeeppujar
ms.author: sandeepu
ms.date: 01/19/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: b125d822596675b138560c14c76f9a3120ce3424
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855958"
---
# <a name="create-a-new-device-template-version"></a><span data-ttu-id="f7510-103">Create a new device template version</span><span class="sxs-lookup"><span data-stu-id="f7510-103">Create a new device template version</span></span>

<span data-ttu-id="f7510-104">Microsoft Azure IoT Central allows rapid development of IoT Applications.</span><span class="sxs-lookup"><span data-stu-id="f7510-104">Microsoft Azure IoT Central allows rapid development of IoT Applications.</span></span> <span data-ttu-id="f7510-105">You can quickly iterate over your device template designs by adding, editing, or deleting measurements, settings, or properties.</span><span class="sxs-lookup"><span data-stu-id="f7510-105">You can quickly iterate over your device template designs by adding, editing, or deleting measurements, settings, or properties.</span></span> <span data-ttu-id="f7510-106">Some of these changes could be intrusive for the currently connected devices.</span><span class="sxs-lookup"><span data-stu-id="f7510-106">Some of these changes could be intrusive for the currently connected devices.</span></span> <span data-ttu-id="f7510-107">Azure IoT Central identifies these breaking changes and provides a way to safely deploy these updates to the devices.</span><span class="sxs-lookup"><span data-stu-id="f7510-107">Azure IoT Central identifies these breaking changes and provides a way to safely deploy these updates to the devices.</span></span>

<span data-ttu-id="f7510-108">A device template has a version number when you create it.</span><span class="sxs-lookup"><span data-stu-id="f7510-108">A device template has a version number when you create it.</span></span> <span data-ttu-id="f7510-109">By default, the version number is 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="f7510-109">By default, the version number is 1.0.0.</span></span> <span data-ttu-id="f7510-110">If you edit a device template, and if that change could impact live connected devices, Azure IoT Central prompts you to create a new device template version.</span><span class="sxs-lookup"><span data-stu-id="f7510-110">If you edit a device template, and if that change could impact live connected devices, Azure IoT Central prompts you to create a new device template version.</span></span>

> [!NOTE]
> <span data-ttu-id="f7510-111">To learn more about how to create a device template see [Set up a device template](howto-set-up-template.md)</span><span class="sxs-lookup"><span data-stu-id="f7510-111">To learn more about how to create a device template see [Set up a device template](howto-set-up-template.md)</span></span>

## <a name="changes-that-prompt-a-version-change"></a><span data-ttu-id="f7510-112">Changes that prompt a version change</span><span class="sxs-lookup"><span data-stu-id="f7510-112">Changes that prompt a version change</span></span>

<span data-ttu-id="f7510-113">In general changes to settings or properties of your device template prompt a version change.</span><span class="sxs-lookup"><span data-stu-id="f7510-113">In general changes to settings or properties of your device template prompt a version change.</span></span>

> [!NOTE]
> <span data-ttu-id="f7510-114">Changes made to the device template do not prompt for the creation of a new version when no device or at-most one device is connected.</span><span class="sxs-lookup"><span data-stu-id="f7510-114">Changes made to the device template do not prompt for the creation of a new version when no device or at-most one device is connected.</span></span>

<span data-ttu-id="f7510-115">The following list describes the user actions that could require a new version:</span><span class="sxs-lookup"><span data-stu-id="f7510-115">The following list describes the user actions that could require a new version:</span></span>

* <span data-ttu-id="f7510-116">Properties (Required)</span><span class="sxs-lookup"><span data-stu-id="f7510-116">Properties (Required)</span></span>
    * <span data-ttu-id="f7510-117">Adding or deleting a required property</span><span class="sxs-lookup"><span data-stu-id="f7510-117">Adding or deleting a required property</span></span>
    * <span data-ttu-id="f7510-118">Changing the field name of a property, field name that is used by your devices to send messages.</span><span class="sxs-lookup"><span data-stu-id="f7510-118">Changing the field name of a property, field name that is used by your devices to send messages.</span></span>
*  <span data-ttu-id="f7510-119">Properties (Optional)</span><span class="sxs-lookup"><span data-stu-id="f7510-119">Properties (Optional)</span></span>
    * <span data-ttu-id="f7510-120">Deleting an optional property</span><span class="sxs-lookup"><span data-stu-id="f7510-120">Deleting an optional property</span></span>
    * <span data-ttu-id="f7510-121">Changing the field name of a property, field name that is used by your devices to send messages.</span><span class="sxs-lookup"><span data-stu-id="f7510-121">Changing the field name of a property, field name that is used by your devices to send messages.</span></span>
    * <span data-ttu-id="f7510-122">Changing an optional property to a required property</span><span class="sxs-lookup"><span data-stu-id="f7510-122">Changing an optional property to a required property</span></span>
*  <span data-ttu-id="f7510-123">Settings</span><span class="sxs-lookup"><span data-stu-id="f7510-123">Settings</span></span>
    * <span data-ttu-id="f7510-124">Adding or deleting a setting</span><span class="sxs-lookup"><span data-stu-id="f7510-124">Adding or deleting a setting</span></span>
    * <span data-ttu-id="f7510-125">Changing the field name of a setting, field name that is used by your devices to send and receive messages.</span><span class="sxs-lookup"><span data-stu-id="f7510-125">Changing the field name of a setting, field name that is used by your devices to send and receive messages.</span></span>

## <a name="what-happens-on-version-change"></a><span data-ttu-id="f7510-126">What happens on version change?</span><span class="sxs-lookup"><span data-stu-id="f7510-126">What happens on version change?</span></span>

<span data-ttu-id="f7510-127">What happens to rules and device dashboards when there is a version change?</span><span class="sxs-lookup"><span data-stu-id="f7510-127">What happens to rules and device dashboards when there is a version change?</span></span>

<span data-ttu-id="f7510-128">**Rules** could contain conditions that are dependent on properties.</span><span class="sxs-lookup"><span data-stu-id="f7510-128">**Rules** could contain conditions that are dependent on properties.</span></span> <span data-ttu-id="f7510-129">If you have removed one or more of these properties, these rules could be broken in your new device template version.</span><span class="sxs-lookup"><span data-stu-id="f7510-129">If you have removed one or more of these properties, these rules could be broken in your new device template version.</span></span> <span data-ttu-id="f7510-130">You can go to these specific rules and update the conditions to fix the rules.</span><span class="sxs-lookup"><span data-stu-id="f7510-130">You can go to these specific rules and update the conditions to fix the rules.</span></span> <span data-ttu-id="f7510-131">Rules for your previous version should work with no impact.</span><span class="sxs-lookup"><span data-stu-id="f7510-131">Rules for your previous version should work with no impact.</span></span>

<span data-ttu-id="f7510-132">**Device dashboards** can contain several types of tiles.</span><span class="sxs-lookup"><span data-stu-id="f7510-132">**Device dashboards** can contain several types of tiles.</span></span> <span data-ttu-id="f7510-133">Some of the tiles may contain settings and properties.</span><span class="sxs-lookup"><span data-stu-id="f7510-133">Some of the tiles may contain settings and properties.</span></span> <span data-ttu-id="f7510-134">When a property or setting used in a tile is removed, the tile is fully or partially broken.</span><span class="sxs-lookup"><span data-stu-id="f7510-134">When a property or setting used in a tile is removed, the tile is fully or partially broken.</span></span> <span data-ttu-id="f7510-135">You can go to the tile and fix the issue either by removing the tile or updating the contents of the tile.</span><span class="sxs-lookup"><span data-stu-id="f7510-135">You can go to the tile and fix the issue either by removing the tile or updating the contents of the tile.</span></span>

## <a name="migrate-a-device-across-device-template-versions"></a><span data-ttu-id="f7510-136">Migrate a device across device template versions</span><span class="sxs-lookup"><span data-stu-id="f7510-136">Migrate a device across device template versions</span></span>

<span data-ttu-id="f7510-137">You can create multiple versions of the device template.</span><span class="sxs-lookup"><span data-stu-id="f7510-137">You can create multiple versions of the device template.</span></span> <span data-ttu-id="f7510-138">Over time, you will have multiple connected devices using these device templates.</span><span class="sxs-lookup"><span data-stu-id="f7510-138">Over time, you will have multiple connected devices using these device templates.</span></span> <span data-ttu-id="f7510-139">You can migrate devices from one version of your device template to another.</span><span class="sxs-lookup"><span data-stu-id="f7510-139">You can migrate devices from one version of your device template to another.</span></span> <span data-ttu-id="f7510-140">The following steps describe how to migrate a device:</span><span class="sxs-lookup"><span data-stu-id="f7510-140">The following steps describe how to migrate a device:</span></span>

1. <span data-ttu-id="f7510-141">Go to the **Explorer** page.</span><span class="sxs-lookup"><span data-stu-id="f7510-141">Go to the **Explorer** page.</span></span>
1. <span data-ttu-id="f7510-142">Select the device you need to migrate to another version.</span><span class="sxs-lookup"><span data-stu-id="f7510-142">Select the device you need to migrate to another version.</span></span>
1. <span data-ttu-id="f7510-143">Choose **Migrate Device**.</span><span class="sxs-lookup"><span data-stu-id="f7510-143">Choose **Migrate Device**.</span></span>
1. <span data-ttu-id="f7510-144">Select the version number you want to migrate the device to and choose **Migrate**.</span><span class="sxs-lookup"><span data-stu-id="f7510-144">Select the version number you want to migrate the device to and choose **Migrate**.</span></span>

![How to migrate a device](media\howto-version-devicetemplate\pick-version.png)

## <a name="next-steps"></a><span data-ttu-id="f7510-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7510-146">Next steps</span></span>

<span data-ttu-id="f7510-147">Now that you have learned how to use device template versions in your Azure IoT Central application, here is the suggested next step:</span><span class="sxs-lookup"><span data-stu-id="f7510-147">Now that you have learned how to use device template versions in your Azure IoT Central application, here is the suggested next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7510-148">How to create telemetry rules</span><span class="sxs-lookup"><span data-stu-id="f7510-148">How to create telemetry rules</span></span>](howto-create-telemetry-rules.md)