---
title: Custom Vision ONNX model with Windows ML - Cognitive Services | Microsoft Docs
description: Learn how to create a Windows UWP app that uses an ONNX model exported from Cognitive Services.
services: cognitive-services
author: larryfr
manager: cgronlun
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: conceptual
ms.date: 06/19/2018
ms.author: larryfr
ms.openlocfilehash: 0b128ba1800e74c20c09a9c5711c8473f1dd00d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864955"
---
# <a name="tutorial-use-an-onnx-model-from-custom-vision-with-windows-ml-preview"></a><span data-ttu-id="9394e-103">Tutorial: Use an ONNX model from Custom Vision with Windows ML (preview)</span><span class="sxs-lookup"><span data-stu-id="9394e-103">Tutorial: Use an ONNX model from Custom Vision with Windows ML (preview)</span></span>

<span data-ttu-id="9394e-104">Learn how to use an ONNX model exported from the Custom Vision service with Windows ML (preview).</span><span class="sxs-lookup"><span data-stu-id="9394e-104">Learn how to use an ONNX model exported from the Custom Vision service with Windows ML (preview).</span></span>

<span data-ttu-id="9394e-105">The information in this document demonstrates how to use an ONNX file exported from the Custom Vision Service with Windows ML.</span><span class="sxs-lookup"><span data-stu-id="9394e-105">The information in this document demonstrates how to use an ONNX file exported from the Custom Vision Service with Windows ML.</span></span> <span data-ttu-id="9394e-106">An example Windows UWP application is provided.</span><span class="sxs-lookup"><span data-stu-id="9394e-106">An example Windows UWP application is provided.</span></span> <span data-ttu-id="9394e-107">A trained model that can recognize dogs and cats is included with the example.</span><span class="sxs-lookup"><span data-stu-id="9394e-107">A trained model that can recognize dogs and cats is included with the example.</span></span> <span data-ttu-id="9394e-108">Steps are also provided on how you can use your own model with this example.</span><span class="sxs-lookup"><span data-stu-id="9394e-108">Steps are also provided on how you can use your own model with this example.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9394e-109">About the example app</span><span class="sxs-lookup"><span data-stu-id="9394e-109">About the example app</span></span>
> * <span data-ttu-id="9394e-110">Get the example code</span><span class="sxs-lookup"><span data-stu-id="9394e-110">Get the example code</span></span>
> * <span data-ttu-id="9394e-111">Run the example</span><span class="sxs-lookup"><span data-stu-id="9394e-111">Run the example</span></span>
> * <span data-ttu-id="9394e-112">Use your own model</span><span class="sxs-lookup"><span data-stu-id="9394e-112">Use your own model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9394e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9394e-113">Prerequisites</span></span>

* <span data-ttu-id="9394e-114">A Windows 10 device with:</span><span class="sxs-lookup"><span data-stu-id="9394e-114">A Windows 10 device with:</span></span>

    * <span data-ttu-id="9394e-115">A camera.</span><span class="sxs-lookup"><span data-stu-id="9394e-115">A camera.</span></span>

    * <span data-ttu-id="9394e-116">Visual Studio 2017 version 15.7 or later with the __Universal Windows Platform development__ workload enabled.</span><span class="sxs-lookup"><span data-stu-id="9394e-116">Visual Studio 2017 version 15.7 or later with the __Universal Windows Platform development__ workload enabled.</span></span>

    * <span data-ttu-id="9394e-117">Developer mode enabled.</span><span class="sxs-lookup"><span data-stu-id="9394e-117">Developer mode enabled.</span></span> <span data-ttu-id="9394e-118">For more information, see the [Enable your device for development](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) document.</span><span class="sxs-lookup"><span data-stu-id="9394e-118">For more information, see the [Enable your device for development](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) document.</span></span>

* <span data-ttu-id="9394e-119">(Optional) An ONNX file exported from the Custom Vision service.</span><span class="sxs-lookup"><span data-stu-id="9394e-119">(Optional) An ONNX file exported from the Custom Vision service.</span></span> <span data-ttu-id="9394e-120">For more information, see the [Export your model for use with mobile devices](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) document.</span><span class="sxs-lookup"><span data-stu-id="9394e-120">For more information, see the [Export your model for use with mobile devices](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) document.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9394e-121">To use your own model, follow the steps in the [Use your own model](#use-your-own-model) section.</span><span class="sxs-lookup"><span data-stu-id="9394e-121">To use your own model, follow the steps in the [Use your own model](#use-your-own-model) section.</span></span>

## <a name="about-the-example-app"></a><span data-ttu-id="9394e-122">About the example app</span><span class="sxs-lookup"><span data-stu-id="9394e-122">About the example app</span></span>

<span data-ttu-id="9394e-123">The application is a generic Windows UWP application.</span><span class="sxs-lookup"><span data-stu-id="9394e-123">The application is a generic Windows UWP application.</span></span> <span data-ttu-id="9394e-124">It uses the camera on your Windows 10 device to supply images to the model.</span><span class="sxs-lookup"><span data-stu-id="9394e-124">It uses the camera on your Windows 10 device to supply images to the model.</span></span> <span data-ttu-id="9394e-125">The tags and scores returned by the model are displayed beneath the video preview.</span><span class="sxs-lookup"><span data-stu-id="9394e-125">The tags and scores returned by the model are displayed beneath the video preview.</span></span>

* <span data-ttu-id="9394e-126">As data comes in though the camera, [MediaFrameReader](https://docs.microsoft.com/uwp/api/windows.media.capture.frames.mediaframereader) is used to extract individual frames.</span><span class="sxs-lookup"><span data-stu-id="9394e-126">As data comes in though the camera, [MediaFrameReader](https://docs.microsoft.com/uwp/api/windows.media.capture.frames.mediaframereader) is used to extract individual frames.</span></span> <span data-ttu-id="9394e-127">The frames are sent to the model for scoring.</span><span class="sxs-lookup"><span data-stu-id="9394e-127">The frames are sent to the model for scoring.</span></span>

* <span data-ttu-id="9394e-128">The model returns the tags that it was trained on, and a float value that indicates how confident it is that the image contains that item.</span><span class="sxs-lookup"><span data-stu-id="9394e-128">The model returns the tags that it was trained on, and a float value that indicates how confident it is that the image contains that item.</span></span>

### <a name="the-ui"></a><span data-ttu-id="9394e-129">The UI</span><span class="sxs-lookup"><span data-stu-id="9394e-129">The UI</span></span>

<span data-ttu-id="9394e-130">The UI for the example application is created using __CaptureElement__ and __TextBlock__ controls.</span><span class="sxs-lookup"><span data-stu-id="9394e-130">The UI for the example application is created using __CaptureElement__ and __TextBlock__ controls.</span></span> <span data-ttu-id="9394e-131">The CaptureElement displays a preview of the video from the camera, and the TextBlock displays the results returned from the model.</span><span class="sxs-lookup"><span data-stu-id="9394e-131">The CaptureElement displays a preview of the video from the camera, and the TextBlock displays the results returned from the model.</span></span> 

### <a name="the-model"></a><span data-ttu-id="9394e-132">The model</span><span class="sxs-lookup"><span data-stu-id="9394e-132">The model</span></span>

<span data-ttu-id="9394e-133">The model (`cat-or-dog.onnx`) supplied with the example was created and trained using the Cognitive Services Custom Vision service.</span><span class="sxs-lookup"><span data-stu-id="9394e-133">The model (`cat-or-dog.onnx`) supplied with the example was created and trained using the Cognitive Services Custom Vision service.</span></span> <span data-ttu-id="9394e-134">The trained model was then exported as an ONNX model.</span><span class="sxs-lookup"><span data-stu-id="9394e-134">The trained model was then exported as an ONNX model.</span></span> <span data-ttu-id="9394e-135">For more information on using this service, see the [How to build a classifier](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier) and [Export your model for use with mobile devices](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) documents.</span><span class="sxs-lookup"><span data-stu-id="9394e-135">For more information on using this service, see the [How to build a classifier](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier) and [Export your model for use with mobile devices](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) documents.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9394e-136">The model provided with the example was trained with a small set of dog and cat images.</span><span class="sxs-lookup"><span data-stu-id="9394e-136">The model provided with the example was trained with a small set of dog and cat images.</span></span> <span data-ttu-id="9394e-137">So it may not be the world's best at recognizing dogs and cats.</span><span class="sxs-lookup"><span data-stu-id="9394e-137">So it may not be the world's best at recognizing dogs and cats.</span></span>

### <a name="the-model-class-file"></a><span data-ttu-id="9394e-138">The model class file</span><span class="sxs-lookup"><span data-stu-id="9394e-138">The model class file</span></span>

<span data-ttu-id="9394e-139">When you add an ONNX file to a Windows UWP application, it creates a .cs file.</span><span class="sxs-lookup"><span data-stu-id="9394e-139">When you add an ONNX file to a Windows UWP application, it creates a .cs file.</span></span> <span data-ttu-id="9394e-140">This file has the same name as the `.onnx` file (`cat-or-dog` in this example) and contains the classes used to work with the model from C#.</span><span class="sxs-lookup"><span data-stu-id="9394e-140">This file has the same name as the `.onnx` file (`cat-or-dog` in this example) and contains the classes used to work with the model from C#.</span></span> <span data-ttu-id="9394e-141">However, the entities in the generated class may have names like `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70ModelInput`.</span><span class="sxs-lookup"><span data-stu-id="9394e-141">However, the entities in the generated class may have names like `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70ModelInput`.</span></span> <span data-ttu-id="9394e-142">You can safely rename these entries (right-click, rename) to a friendly name.</span><span class="sxs-lookup"><span data-stu-id="9394e-142">You can safely rename these entries (right-click, rename) to a friendly name.</span></span>

> [!NOTE]
> <span data-ttu-id="9394e-143">The example code has refactored the generated class and method names to the following:</span><span class="sxs-lookup"><span data-stu-id="9394e-143">The example code has refactored the generated class and method names to the following:</span></span>
>
> * `ModelInput`
> * `ModelOutput`
> * `Model`
> * `CreateModel`

### <a name="camera-access"></a><span data-ttu-id="9394e-144">Camera access</span><span class="sxs-lookup"><span data-stu-id="9394e-144">Camera access</span></span>

<span data-ttu-id="9394e-145">The __Capabilities__ tab in the `Package.appxmanifest` file is configured to allow access to the webcam and microphone.</span><span class="sxs-lookup"><span data-stu-id="9394e-145">The __Capabilities__ tab in the `Package.appxmanifest` file is configured to allow access to the webcam and microphone.</span></span>

> [!NOTE]
> <span data-ttu-id="9394e-146">Even though this example doesn't use audio, I had to enable the microphone before I was able to access the camera on my device.</span><span class="sxs-lookup"><span data-stu-id="9394e-146">Even though this example doesn't use audio, I had to enable the microphone before I was able to access the camera on my device.</span></span>

<span data-ttu-id="9394e-147">The application tries to get the camera on the back of your device if one is available.</span><span class="sxs-lookup"><span data-stu-id="9394e-147">The application tries to get the camera on the back of your device if one is available.</span></span> <span data-ttu-id="9394e-148">It uses the [MediaCapture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) class to start capturing video from the camera.</span><span class="sxs-lookup"><span data-stu-id="9394e-148">It uses the [MediaCapture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) class to start capturing video from the camera.</span></span> <span data-ttu-id="9394e-149">[MediaFrameReader](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.Frames.MediaFrameReader) is used to capture video frames and send them to the model.</span><span class="sxs-lookup"><span data-stu-id="9394e-149">[MediaFrameReader](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.Frames.MediaFrameReader) is used to capture video frames and send them to the model.</span></span>

## <a name="get-the-example-code"></a><span data-ttu-id="9394e-150">Get the example code</span><span class="sxs-lookup"><span data-stu-id="9394e-150">Get the example code</span></span>

<span data-ttu-id="9394e-151">The example application is available at [https://github.com/Azure-Samples/Custom-Vision-ONNX-UWP](https://github.com/Azure-Samples/Custom-Vision-ONNX-UWP).</span><span class="sxs-lookup"><span data-stu-id="9394e-151">The example application is available at [https://github.com/Azure-Samples/Custom-Vision-ONNX-UWP](https://github.com/Azure-Samples/Custom-Vision-ONNX-UWP).</span></span>

## <a name="run-the-example"></a><span data-ttu-id="9394e-152">Run the example</span><span class="sxs-lookup"><span data-stu-id="9394e-152">Run the example</span></span>

1. <span data-ttu-id="9394e-153">Use the `F5` key to start the application from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9394e-153">Use the `F5` key to start the application from Visual Studio.</span></span> <span data-ttu-id="9394e-154">You may be prompted to enable Developer mode.</span><span class="sxs-lookup"><span data-stu-id="9394e-154">You may be prompted to enable Developer mode.</span></span> <span data-ttu-id="9394e-155">For more information, see the [Enable your device for development](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) document.</span><span class="sxs-lookup"><span data-stu-id="9394e-155">For more information, see the [Enable your device for development](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) document.</span></span>

2. <span data-ttu-id="9394e-156">When prompted, allow the application to access the camera and microphone on your device.</span><span class="sxs-lookup"><span data-stu-id="9394e-156">When prompted, allow the application to access the camera and microphone on your device.</span></span>

3. <span data-ttu-id="9394e-157">Point the camera at a dog or cat.</span><span class="sxs-lookup"><span data-stu-id="9394e-157">Point the camera at a dog or cat.</span></span> <span data-ttu-id="9394e-158">The score for whether the image contains a dog or cat is displayed beneath the preview in the application.</span><span class="sxs-lookup"><span data-stu-id="9394e-158">The score for whether the image contains a dog or cat is displayed beneath the preview in the application.</span></span>

    > [!TIP]
    > <span data-ttu-id="9394e-159">If you do not have a dog or cat handy, you can use a photo of a dog or cat.</span><span class="sxs-lookup"><span data-stu-id="9394e-159">If you do not have a dog or cat handy, you can use a photo of a dog or cat.</span></span>

## <a name="use-your-own-model"></a><span data-ttu-id="9394e-160">Use your own model</span><span class="sxs-lookup"><span data-stu-id="9394e-160">Use your own model</span></span>

<span data-ttu-id="9394e-161">To use your own model, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="9394e-161">To use your own model, use the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9394e-162">The steps in this section rename the current model (cat-or-dog.cs) and refactor the class and method names of the new model.</span><span class="sxs-lookup"><span data-stu-id="9394e-162">The steps in this section rename the current model (cat-or-dog.cs) and refactor the class and method names of the new model.</span></span> <span data-ttu-id="9394e-163">This is to avoid naming collisions with the example model.</span><span class="sxs-lookup"><span data-stu-id="9394e-163">This is to avoid naming collisions with the example model.</span></span>

1. <span data-ttu-id="9394e-164">Train a model using the Custom Vision service.</span><span class="sxs-lookup"><span data-stu-id="9394e-164">Train a model using the Custom Vision service.</span></span> <span data-ttu-id="9394e-165">For information on how to train a model, see the [How to build a classifier](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier).</span><span class="sxs-lookup"><span data-stu-id="9394e-165">For information on how to train a model, see the [How to build a classifier](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier).</span></span>

2. <span data-ttu-id="9394e-166">Export the trained model as an ONNX model.</span><span class="sxs-lookup"><span data-stu-id="9394e-166">Export the trained model as an ONNX model.</span></span> <span data-ttu-id="9394e-167">For information on how to export a model, see the [Export your model for use with mobile devices](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) document.</span><span class="sxs-lookup"><span data-stu-id="9394e-167">For information on how to export a model, see the [Export your model for use with mobile devices](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model) document.</span></span>

3. <span data-ttu-id="9394e-168">In Solution Explorer, right-click the __cat-or-dog.cs__ and rename it to __cat-or-dog.txt__.</span><span class="sxs-lookup"><span data-stu-id="9394e-168">In Solution Explorer, right-click the __cat-or-dog.cs__ and rename it to __cat-or-dog.txt__.</span></span> <span data-ttu-id="9394e-169">Renaming it prevents name collisions with the new model.</span><span class="sxs-lookup"><span data-stu-id="9394e-169">Renaming it prevents name collisions with the new model.</span></span>

    > [!TIP]
    > <span data-ttu-id="9394e-170">You could also use different names for the class names in the new model, but reusing the existing names is easier.</span><span class="sxs-lookup"><span data-stu-id="9394e-170">You could also use different names for the class names in the new model, but reusing the existing names is easier.</span></span>

4. <span data-ttu-id="9394e-171">In Solution Explorer, right-click the __VisionApp__ entry and then select __Add__ > __Existing item...__.</span><span class="sxs-lookup"><span data-stu-id="9394e-171">In Solution Explorer, right-click the __VisionApp__ entry and then select __Add__ > __Existing item...__.</span></span>

5. <span data-ttu-id="9394e-172">To generate a class for the model, select the ONNX file to import, and then select the __Add__ button.</span><span class="sxs-lookup"><span data-stu-id="9394e-172">To generate a class for the model, select the ONNX file to import, and then select the __Add__ button.</span></span> <span data-ttu-id="9394e-173">A new class with the same name as the ONNX file (but a `.cs` extension) is added in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="9394e-173">A new class with the same name as the ONNX file (but a `.cs` extension) is added in Solution Explorer.</span></span>

6. <span data-ttu-id="9394e-174">Open the generated .cs file and find the names of the following items:</span><span class="sxs-lookup"><span data-stu-id="9394e-174">Open the generated .cs file and find the names of the following items:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9394e-175">Use the example `cat-or-dog.txt` file as a guide to recognize the classes and functions.</span><span class="sxs-lookup"><span data-stu-id="9394e-175">Use the example `cat-or-dog.txt` file as a guide to recognize the classes and functions.</span></span>

    * <span data-ttu-id="9394e-176">The class that defines the model input.</span><span class="sxs-lookup"><span data-stu-id="9394e-176">The class that defines the model input.</span></span> <span data-ttu-id="9394e-177">The generated name may be similar to `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70ModelInput`.</span><span class="sxs-lookup"><span data-stu-id="9394e-177">The generated name may be similar to `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70ModelInput`.</span></span> <span data-ttu-id="9394e-178">Rename this class to __ModelInput__.</span><span class="sxs-lookup"><span data-stu-id="9394e-178">Rename this class to __ModelInput__.</span></span>
    * <span data-ttu-id="9394e-179">The class that defines the model output.</span><span class="sxs-lookup"><span data-stu-id="9394e-179">The class that defines the model output.</span></span> <span data-ttu-id="9394e-180">The generated name may be similar to `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70ModelOutput`.</span><span class="sxs-lookup"><span data-stu-id="9394e-180">The generated name may be similar to `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70ModelOutput`.</span></span> <span data-ttu-id="9394e-181">Rename this class to __ModelOutput__.</span><span class="sxs-lookup"><span data-stu-id="9394e-181">Rename this class to __ModelOutput__.</span></span>
    * <span data-ttu-id="9394e-182">The class that defines the model.</span><span class="sxs-lookup"><span data-stu-id="9394e-182">The class that defines the model.</span></span> <span data-ttu-id="9394e-183">The generated name may be similar to `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70Model`.</span><span class="sxs-lookup"><span data-stu-id="9394e-183">The generated name may be similar to `_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70Model`.</span></span> <span data-ttu-id="9394e-184">Rename this class to __Model__.</span><span class="sxs-lookup"><span data-stu-id="9394e-184">Rename this class to __Model__.</span></span>
    * <span data-ttu-id="9394e-185">The method that creates the model.</span><span class="sxs-lookup"><span data-stu-id="9394e-185">The method that creates the model.</span></span> <span data-ttu-id="9394e-186">The generated name may be similar to `Create_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70Model`.</span><span class="sxs-lookup"><span data-stu-id="9394e-186">The generated name may be similar to `Create_x0033_04aa07b_x002D_6c8c_x002D_4641_x002D_93a6_x002D_f3152f8740a1_028da4e3_x002D_9c6e_x002D_480b_x002D_b53c_x002D_c1db13d24d70Model`.</span></span> <span data-ttu-id="9394e-187">Rename this method to __CreateModel__.</span><span class="sxs-lookup"><span data-stu-id="9394e-187">Rename this method to __CreateModel__.</span></span>

7. <span data-ttu-id="9394e-188">In Solution Explorer, move the `.onnx` file into the __Assets__ folder.</span><span class="sxs-lookup"><span data-stu-id="9394e-188">In Solution Explorer, move the `.onnx` file into the __Assets__ folder.</span></span> 

8. <span data-ttu-id="9394e-189">To include the ONNX file in the application package, select the `.onnx` file and set __Build Action__ to __Content__ in the properties.</span><span class="sxs-lookup"><span data-stu-id="9394e-189">To include the ONNX file in the application package, select the `.onnx` file and set __Build Action__ to __Content__ in the properties.</span></span>

9. <span data-ttu-id="9394e-190">Open the __MainPage.xaml.cs__ file.</span><span class="sxs-lookup"><span data-stu-id="9394e-190">Open the __MainPage.xaml.cs__ file.</span></span> <span data-ttu-id="9394e-191">Find the following line and change the file name to the new `.onnx` file:</span><span class="sxs-lookup"><span data-stu-id="9394e-191">Find the following line and change the file name to the new `.onnx` file:</span></span>

    ```csharp
    var file = await StorageFile.GetFileFromApplicationUriAsync(new Uri($"ms-appx:///Assets/cat-or-dog.onnx"));
    ```

    <span data-ttu-id="9394e-192">This change loads the new model at runtime.</span><span class="sxs-lookup"><span data-stu-id="9394e-192">This change loads the new model at runtime.</span></span>

10. <span data-ttu-id="9394e-193">Build and run the app.</span><span class="sxs-lookup"><span data-stu-id="9394e-193">Build and run the app.</span></span> <span data-ttu-id="9394e-194">It now uses the new model to score images.</span><span class="sxs-lookup"><span data-stu-id="9394e-194">It now uses the new model to score images.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9394e-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="9394e-195">Next steps</span></span>

<span data-ttu-id="9394e-196">To discover other ways to export and use a Custom Vision model, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="9394e-196">To discover other ways to export and use a Custom Vision model, see the following documents:</span></span>

* [<span data-ttu-id="9394e-197">Export your model</span><span class="sxs-lookup"><span data-stu-id="9394e-197">Export your model</span></span>](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/export-your-model)
* [<span data-ttu-id="9394e-198">Use exported Tensorflow model in an Android application</span><span class="sxs-lookup"><span data-stu-id="9394e-198">Use exported Tensorflow model in an Android application</span></span>](https://github.com/Azure-Samples/cognitive-services-android-customvision-sample)
* [<span data-ttu-id="9394e-199">Use exported CoreML model in a Swift iOS application</span><span class="sxs-lookup"><span data-stu-id="9394e-199">Use exported CoreML model in a Swift iOS application</span></span>](https://go.microsoft.com/fwlink/?linkid=857726)
* [<span data-ttu-id="9394e-200">Use exported CoreML model in an iOS application with Xamarin</span><span class="sxs-lookup"><span data-stu-id="9394e-200">Use exported CoreML model in an iOS application with Xamarin</span></span>](https://github.com/xamarin/ios-samples/tree/master/ios11/CoreMLAzureModel)

<span data-ttu-id="9394e-201">For more information on using ONNX models with Windows ML, see the [Integrate a model into your app with Windows ML](https://docs.microsoft.com/windows/uwp/machine-learning/integrate-model) document.</span><span class="sxs-lookup"><span data-stu-id="9394e-201">For more information on using ONNX models with Windows ML, see the [Integrate a model into your app with Windows ML](https://docs.microsoft.com/windows/uwp/machine-learning/integrate-model) document.</span></span>
