---
title: Upload images to your Azure IoT Central application | Microsoft Docs
description: As a builder, learn how to prepare and upload images to your Azure IoT Central application.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 7fd9c8ed5559b00bc755e3f04c768dceeb487562
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869054"
---
# <a name="prepare-and-upload-images-to-your-azure-iot-central-application"></a><span data-ttu-id="966be-103">Prepare and upload images to your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="966be-103">Prepare and upload images to your Azure IoT Central application</span></span>

<span data-ttu-id="966be-104">This article describes how, as a builder, you can customize your Microsoft Azure IoT Central application by uploading custom images.</span><span class="sxs-lookup"><span data-stu-id="966be-104">This article describes how, as a builder, you can customize your Microsoft Azure IoT Central application by uploading custom images.</span></span> <span data-ttu-id="966be-105">For example, you can customize a device dashboard with a picture of the device.</span><span class="sxs-lookup"><span data-stu-id="966be-105">For example, you can customize a device dashboard with a picture of the device.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="966be-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="966be-106">Before you begin</span></span>

<span data-ttu-id="966be-107">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="966be-107">To complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="966be-108">An Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="966be-108">An Azure IoT Central application.</span></span> <span data-ttu-id="966be-109">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="966be-109">For more information, see [Create your Azure IoT Central Application](howto-create-application.md).</span></span>
1. <span data-ttu-id="966be-110">A tool for scaling and resizing images files.</span><span class="sxs-lookup"><span data-stu-id="966be-110">A tool for scaling and resizing images files.</span></span>

## <a name="choose-where-to-use-custom-images"></a><span data-ttu-id="966be-111">Choose where to use custom images</span><span class="sxs-lookup"><span data-stu-id="966be-111">Choose where to use custom images</span></span>

<span data-ttu-id="966be-112">You can add custom images to the following locations in an Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="966be-112">You can add custom images to the following locations in an Azure IoT Central application:</span></span>

* <span data-ttu-id="966be-113">The **Application Manager** page</span><span class="sxs-lookup"><span data-stu-id="966be-113">The **Application Manager** page</span></span>

    ![Image on application manager page](media/howto-prepare-images/applicationmanager.png)

* <span data-ttu-id="966be-115">The home page</span><span class="sxs-lookup"><span data-stu-id="966be-115">The home page</span></span>

    ![Image on home page](media/howto-prepare-images/homepage.png)

* <span data-ttu-id="966be-117">A device template</span><span class="sxs-lookup"><span data-stu-id="966be-117">A device template</span></span>

    ![Image on device template](media/howto-prepare-images/devicetemplate.png)

* <span data-ttu-id="966be-119">A tile on a device dashboard</span><span class="sxs-lookup"><span data-stu-id="966be-119">A tile on a device dashboard</span></span>

    ![Image on device tile](media/howto-prepare-images/devicetile.png)

* <span data-ttu-id="966be-121">A tile on a device set dashboard</span><span class="sxs-lookup"><span data-stu-id="966be-121">A tile on a device set dashboard</span></span>

    ![Image on device set tile](media/howto-prepare-images/devicesettile.png)

## <a name="prepare-the-images"></a><span data-ttu-id="966be-123">Prepare the images</span><span class="sxs-lookup"><span data-stu-id="966be-123">Prepare the images</span></span>

<span data-ttu-id="966be-124">In all four locations, you can use either PNG, GIF, or JPEG images.</span><span class="sxs-lookup"><span data-stu-id="966be-124">In all four locations, you can use either PNG, GIF, or JPEG images.</span></span>

<span data-ttu-id="966be-125">The following table summarizes the image sizes you can use:</span><span class="sxs-lookup"><span data-stu-id="966be-125">The following table summarizes the image sizes you can use:</span></span>

| <span data-ttu-id="966be-126">Location</span><span class="sxs-lookup"><span data-stu-id="966be-126">Location</span></span> | <span data-ttu-id="966be-127">Sizes</span><span class="sxs-lookup"><span data-stu-id="966be-127">Sizes</span></span> |
| -------- | ------ |
| <span data-ttu-id="966be-128">**Application Manager**</span><span class="sxs-lookup"><span data-stu-id="966be-128">**Application Manager**</span></span> | <span data-ttu-id="966be-129">268x160 px</span><span class="sxs-lookup"><span data-stu-id="966be-129">268x160 px</span></span> |
| <span data-ttu-id="966be-130">Device template</span><span class="sxs-lookup"><span data-stu-id="966be-130">Device template</span></span> | <span data-ttu-id="966be-131">64x64 px</span><span class="sxs-lookup"><span data-stu-id="966be-131">64x64 px</span></span> |
| <span data-ttu-id="966be-132">Home page and dashboard tiles</span><span class="sxs-lookup"><span data-stu-id="966be-132">Home page and dashboard tiles</span></span> | <span data-ttu-id="966be-133">The smallest sized tile is 200x200 px, larger tiles can be either square or rectangular multiples of small tiles.</span><span class="sxs-lookup"><span data-stu-id="966be-133">The smallest sized tile is 200x200 px, larger tiles can be either square or rectangular multiples of small tiles.</span></span> <span data-ttu-id="966be-134">For example 200x400 px, 400x200 px, or 400x400 px</span><span class="sxs-lookup"><span data-stu-id="966be-134">For example 200x400 px, 400x200 px, or 400x400 px</span></span> |

<span data-ttu-id="966be-135">For the best display in the application, you should create images that match the dimensions shown in the previous table.</span><span class="sxs-lookup"><span data-stu-id="966be-135">For the best display in the application, you should create images that match the dimensions shown in the previous table.</span></span>

## <a name="upload-the-images"></a><span data-ttu-id="966be-136">Upload the images</span><span class="sxs-lookup"><span data-stu-id="966be-136">Upload the images</span></span>

<span data-ttu-id="966be-137">The following sections describe how to upload the images to use in the different locations:</span><span class="sxs-lookup"><span data-stu-id="966be-137">The following sections describe how to upload the images to use in the different locations:</span></span>

### <a name="application-manager"></a><span data-ttu-id="966be-138">Application manager</span><span class="sxs-lookup"><span data-stu-id="966be-138">Application manager</span></span>

<span data-ttu-id="966be-139">To upload an image to use on the **Application Manager**, navigate to the **Application Settings** page in the **Administration** section.</span><span class="sxs-lookup"><span data-stu-id="966be-139">To upload an image to use on the **Application Manager**, navigate to the **Application Settings** page in the **Administration** section.</span></span> <span data-ttu-id="966be-140">You must be an administrator to complete this task:</span><span class="sxs-lookup"><span data-stu-id="966be-140">You must be an administrator to complete this task:</span></span>

![Upload application image](media/howto-prepare-images/uploadapplicationmanager.png)

<span data-ttu-id="966be-142">Click the upload image and then choose the file to upload from your local machine.</span><span class="sxs-lookup"><span data-stu-id="966be-142">Click the upload image and then choose the file to upload from your local machine.</span></span>

### <a name="home-page"></a><span data-ttu-id="966be-143">Home page</span><span class="sxs-lookup"><span data-stu-id="966be-143">Home page</span></span>

<span data-ttu-id="966be-144">To upload an image to use on the home page, navigate to the **Homepage** of your application and switch design mode on.</span><span class="sxs-lookup"><span data-stu-id="966be-144">To upload an image to use on the home page, navigate to the **Homepage** of your application and switch design mode on.</span></span> <span data-ttu-id="966be-145">You must be a builder to complete this task:</span><span class="sxs-lookup"><span data-stu-id="966be-145">You must be a builder to complete this task:</span></span>

![Upload home page image](media/howto-prepare-images/uploadhomepage.png)

<span data-ttu-id="966be-147">Click the upload image and then choose the file to upload from your local machine.</span><span class="sxs-lookup"><span data-stu-id="966be-147">Click the upload image and then choose the file to upload from your local machine.</span></span>

<span data-ttu-id="966be-148">After the image uploads, you can resize it while design mode is switched on.</span><span class="sxs-lookup"><span data-stu-id="966be-148">After the image uploads, you can resize it while design mode is switched on.</span></span>

### <a name="device-template"></a><span data-ttu-id="966be-149">Device template</span><span class="sxs-lookup"><span data-stu-id="966be-149">Device template</span></span>

<span data-ttu-id="966be-150">To upload an image to use on a device template, navigate to **Device Explorer**, choose the device template and then a device, and switch design mode on.</span><span class="sxs-lookup"><span data-stu-id="966be-150">To upload an image to use on a device template, navigate to **Device Explorer**, choose the device template and then a device, and switch design mode on.</span></span> <span data-ttu-id="966be-151">You must be a builder to complete this task:</span><span class="sxs-lookup"><span data-stu-id="966be-151">You must be a builder to complete this task:</span></span>

![Upload device template image](media/howto-prepare-images/uploaddevicetemplate.png)

<span data-ttu-id="966be-153">Click the upload image and then choose the file to upload from your local machine.</span><span class="sxs-lookup"><span data-stu-id="966be-153">Click the upload image and then choose the file to upload from your local machine.</span></span>

### <a name="device-dashboard"></a><span data-ttu-id="966be-154">Device dashboard</span><span class="sxs-lookup"><span data-stu-id="966be-154">Device dashboard</span></span>

<span data-ttu-id="966be-155">To upload an image to use on a device dashboard, navigate to **Device Explorer**, choose the device template, and then a device.</span><span class="sxs-lookup"><span data-stu-id="966be-155">To upload an image to use on a device dashboard, navigate to **Device Explorer**, choose the device template, and then a device.</span></span> <span data-ttu-id="966be-156">Then choose the **Dashboard** page and switch design mode on.</span><span class="sxs-lookup"><span data-stu-id="966be-156">Then choose the **Dashboard** page and switch design mode on.</span></span> <span data-ttu-id="966be-157">You must be a builder to complete this task:</span><span class="sxs-lookup"><span data-stu-id="966be-157">You must be a builder to complete this task:</span></span>

![Upload device dashboard image](media/howto-prepare-images/uploaddevicedashboard.png)

<span data-ttu-id="966be-159">Click the upload image and then choose the file to upload from your local machine.</span><span class="sxs-lookup"><span data-stu-id="966be-159">Click the upload image and then choose the file to upload from your local machine.</span></span>

<span data-ttu-id="966be-160">After the image uploads, you can resize and reposition it while **Design Mode** is switched on.</span><span class="sxs-lookup"><span data-stu-id="966be-160">After the image uploads, you can resize and reposition it while **Design Mode** is switched on.</span></span>

### <a name="device-set-dashboard"></a><span data-ttu-id="966be-161">Device set dashboard</span><span class="sxs-lookup"><span data-stu-id="966be-161">Device set dashboard</span></span>

<span data-ttu-id="966be-162">To upload an image to use on a device set dashboard, navigate to **Device Sets** and choose the device set, and then a device.</span><span class="sxs-lookup"><span data-stu-id="966be-162">To upload an image to use on a device set dashboard, navigate to **Device Sets** and choose the device set, and then a device.</span></span> <span data-ttu-id="966be-163">Then choose the **Dashboard** page and switch **Design Mode** on:</span><span class="sxs-lookup"><span data-stu-id="966be-163">Then choose the **Dashboard** page and switch **Design Mode** on:</span></span>

![Upload device set dashboard image](media/howto-prepare-images/uploaddevicesetdashboard.png)

<span data-ttu-id="966be-165">Click the upload image and then choose the file to upload from your local machine.</span><span class="sxs-lookup"><span data-stu-id="966be-165">Click the upload image and then choose the file to upload from your local machine.</span></span>

<span data-ttu-id="966be-166">After the image uploads, you can resize and reposition it while design mode is switched on.</span><span class="sxs-lookup"><span data-stu-id="966be-166">After the image uploads, you can resize and reposition it while design mode is switched on.</span></span>

## <a name="next-steps"></a><span data-ttu-id="966be-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="966be-167">Next steps</span></span>

<span data-ttu-id="966be-168">Now that you have learned how to prepare and upload images to your Azure IoT Central application, here is the suggested next step:</span><span class="sxs-lookup"><span data-stu-id="966be-168">Now that you have learned how to prepare and upload images to your Azure IoT Central application, here is the suggested next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="966be-169">Manage devices in your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="966be-169">Manage devices in your Azure IoT Central application</span></span>](howto-manage-devices.md)