---
title: Get started with the Speech Devices SDK
description: Prerequisites and instructions for getting started with the Speech Devices SDK.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 05/18/2018
ms.author: v-jerkin
ms.openlocfilehash: 068f0a0d9202174faf5d54bebf5cf5f8fae86766
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865040"
---
# <a name="get-started-with-the-speech-devices-sdk"></a><span data-ttu-id="a7442-103">Get started with the Speech Devices SDK</span><span class="sxs-lookup"><span data-stu-id="a7442-103">Get started with the Speech Devices SDK</span></span>

<span data-ttu-id="a7442-104">This article describes how to configure your development PC and Speech device development kit for developing speech-enabled devices by using the Speech Devices SDK.</span><span class="sxs-lookup"><span data-stu-id="a7442-104">This article describes how to configure your development PC and Speech device development kit for developing speech-enabled devices by using the Speech Devices SDK.</span></span> <span data-ttu-id="a7442-105">Then, you build and deploy a sample application to the device.</span><span class="sxs-lookup"><span data-stu-id="a7442-105">Then, you build and deploy a sample application to the device.</span></span> 

<span data-ttu-id="a7442-106">The source code for the sample application is included with the Speech Devices SDK.</span><span class="sxs-lookup"><span data-stu-id="a7442-106">The source code for the sample application is included with the Speech Devices SDK.</span></span> <span data-ttu-id="a7442-107">It's also [available on GitHub](https://github.com/Azure-Samples/Cognitive-Services-Speech-Devices-SDK).</span><span class="sxs-lookup"><span data-stu-id="a7442-107">It's also [available on GitHub](https://github.com/Azure-Samples/Cognitive-Services-Speech-Devices-SDK).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7442-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7442-108">Prerequisites</span></span>

<span data-ttu-id="a7442-109">Before you begin developing with the Speech Devices SDK, gather the information and software you need:</span><span class="sxs-lookup"><span data-stu-id="a7442-109">Before you begin developing with the Speech Devices SDK, gather the information and software you need:</span></span>

* <span data-ttu-id="a7442-110">Get a [development kit from ROOBO](http://ddk.roobo.com/).</span><span class="sxs-lookup"><span data-stu-id="a7442-110">Get a [development kit from ROOBO](http://ddk.roobo.com/).</span></span> <span data-ttu-id="a7442-111">Kits are available with linear or circular microphone array configurations.</span><span class="sxs-lookup"><span data-stu-id="a7442-111">Kits are available with linear or circular microphone array configurations.</span></span> <span data-ttu-id="a7442-112">Choose the correct configuration for your needs.</span><span class="sxs-lookup"><span data-stu-id="a7442-112">Choose the correct configuration for your needs.</span></span>

    |<span data-ttu-id="a7442-113">Development kit configuration</span><span class="sxs-lookup"><span data-stu-id="a7442-113">Development kit configuration</span></span>|<span data-ttu-id="a7442-114">Speaker location</span><span class="sxs-lookup"><span data-stu-id="a7442-114">Speaker location</span></span>|
    |-----------------------------|------------|
    |<span data-ttu-id="a7442-115">Circular</span><span class="sxs-lookup"><span data-stu-id="a7442-115">Circular</span></span>|<span data-ttu-id="a7442-116">Any direction from the device</span><span class="sxs-lookup"><span data-stu-id="a7442-116">Any direction from the device</span></span>|
    |<span data-ttu-id="a7442-117">Linear</span><span class="sxs-lookup"><span data-stu-id="a7442-117">Linear</span></span>|<span data-ttu-id="a7442-118">In front of the device</span><span class="sxs-lookup"><span data-stu-id="a7442-118">In front of the device</span></span>|

* <span data-ttu-id="a7442-119">Get the latest version of the Speech Devices SDK, which includes an Android sample app, from the [Speech Devices SDK download site](https://shares.datatransfer.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a7442-119">Get the latest version of the Speech Devices SDK, which includes an Android sample app, from the [Speech Devices SDK download site](https://shares.datatransfer.microsoft.com/).</span></span> <span data-ttu-id="a7442-120">Extract the .zip file to a local folder, like C:\SDSDK.</span><span class="sxs-lookup"><span data-stu-id="a7442-120">Extract the .zip file to a local folder, like C:\SDSDK.</span></span>

* <span data-ttu-id="a7442-121">Install [Android Studio](https://developer.android.com/studio/) and [Vysor](http://vysor.io/download/) on your PC.</span><span class="sxs-lookup"><span data-stu-id="a7442-121">Install [Android Studio](https://developer.android.com/studio/) and [Vysor](http://vysor.io/download/) on your PC.</span></span>

* <span data-ttu-id="a7442-122">Get a [Speech service subscription key](get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a7442-122">Get a [Speech service subscription key](get-started.md).</span></span> <span data-ttu-id="a7442-123">You can get a 30-day free trial or get a key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7442-123">You can get a 30-day free trial or get a key from your Azure dashboard.</span></span>

* <span data-ttu-id="a7442-124">If you want to use the Speech service's intent recognition, subscribe to the [Language Understanding service](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/) (LUIS) and [get a subscription key](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/azureibizasubscription).</span><span class="sxs-lookup"><span data-stu-id="a7442-124">If you want to use the Speech service's intent recognition, subscribe to the [Language Understanding service](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/) (LUIS) and [get a subscription key](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/azureibizasubscription).</span></span> 

    <span data-ttu-id="a7442-125">You can [create a simple LUIS model](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/) or use the sample LUIS model, LUIS-example.json.</span><span class="sxs-lookup"><span data-stu-id="a7442-125">You can [create a simple LUIS model](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/) or use the sample LUIS model, LUIS-example.json.</span></span> <span data-ttu-id="a7442-126">The sample LUIS model is available from the [Speech Devices SDK download site](https://shares.datatransfer.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a7442-126">The sample LUIS model is available from the [Speech Devices SDK download site](https://shares.datatransfer.microsoft.com/).</span></span> <span data-ttu-id="a7442-127">To upload your model's JSON file to the [LUIS portal](https://www.luis.ai/home), select **Import new app**, and then select the JSON file.</span><span class="sxs-lookup"><span data-stu-id="a7442-127">To upload your model's JSON file to the [LUIS portal](https://www.luis.ai/home), select **Import new app**, and then select the JSON file.</span></span>

## <a name="set-up-the-development-kit"></a><span data-ttu-id="a7442-128">Set up the development kit</span><span class="sxs-lookup"><span data-stu-id="a7442-128">Set up the development kit</span></span>

1. <span data-ttu-id="a7442-129">Connect the dev kit to a PC or power adapter by using a mini USB cable.</span><span class="sxs-lookup"><span data-stu-id="a7442-129">Connect the dev kit to a PC or power adapter by using a mini USB cable.</span></span> <span data-ttu-id="a7442-130">When the dev kit is connected, a green power indicator lights up under the top board.</span><span class="sxs-lookup"><span data-stu-id="a7442-130">When the dev kit is connected, a green power indicator lights up under the top board.</span></span>

1. <span data-ttu-id="a7442-131">Connect the development kit to a computer by using a second mini USB cable.</span><span class="sxs-lookup"><span data-stu-id="a7442-131">Connect the development kit to a computer by using a second mini USB cable.</span></span>

    ![Connecting the dev kit](media/speech-devices-sdk/qsg-1.png)

1. <span data-ttu-id="a7442-133">Orient your development kit for either the circular or linear configuration.</span><span class="sxs-lookup"><span data-stu-id="a7442-133">Orient your development kit for either the circular or linear configuration.</span></span>

    |<span data-ttu-id="a7442-134">Development kit configuration</span><span class="sxs-lookup"><span data-stu-id="a7442-134">Development kit configuration</span></span>|<span data-ttu-id="a7442-135">Orientation</span><span class="sxs-lookup"><span data-stu-id="a7442-135">Orientation</span></span>|
    |-----------------------------|------------|
    |<span data-ttu-id="a7442-136">Circular</span><span class="sxs-lookup"><span data-stu-id="a7442-136">Circular</span></span>|<span data-ttu-id="a7442-137">Upright, with microphones facing the ceiling</span><span class="sxs-lookup"><span data-stu-id="a7442-137">Upright, with microphones facing the ceiling</span></span>|
    |<span data-ttu-id="a7442-138">Linear</span><span class="sxs-lookup"><span data-stu-id="a7442-138">Linear</span></span>|<span data-ttu-id="a7442-139">On its side, with microphones facing you (shown in the following image)</span><span class="sxs-lookup"><span data-stu-id="a7442-139">On its side, with microphones facing you (shown in the following image)</span></span>|

    ![Linear dev kit orientation](media/speech-devices-sdk/qsg-2.png)

1. <span data-ttu-id="a7442-141">Install the certificates and the wake word (keyword) table file, and set the permissions of the sound device.</span><span class="sxs-lookup"><span data-stu-id="a7442-141">Install the certificates and the wake word (keyword) table file, and set the permissions of the sound device.</span></span> <span data-ttu-id="a7442-142">Type the following commands in a Command Prompt window:</span><span class="sxs-lookup"><span data-stu-id="a7442-142">Type the following commands in a Command Prompt window:</span></span>

   ```
   adb push C:\SDSDK\Android-Sample-Release\scripts\roobo_setup.sh /data/ 
   adb shell
   cd /data/ 
   chmod 777 roobo_setup.sh
   ./roobo_setup.sh
   exit
   ```

    > [!NOTE]
    > <span data-ttu-id="a7442-143">These commands use the Android Debug Bridge, adb.exe, which is part of the Android Studio installation.</span><span class="sxs-lookup"><span data-stu-id="a7442-143">These commands use the Android Debug Bridge, adb.exe, which is part of the Android Studio installation.</span></span> <span data-ttu-id="a7442-144">This tool is located in C:\Users\[user name]\AppData\Local\Android\Sdk\platform-tools.</span><span class="sxs-lookup"><span data-stu-id="a7442-144">This tool is located in C:\Users\[user name]\AppData\Local\Android\Sdk\platform-tools.</span></span> <span data-ttu-id="a7442-145">You can add this directory to your path to make it more convenient to invoke `adb`.</span><span class="sxs-lookup"><span data-stu-id="a7442-145">You can add this directory to your path to make it more convenient to invoke `adb`.</span></span> <span data-ttu-id="a7442-146">Otherwise, you must specify the full path to your installation of adb.exe in every command that invokes `adb`.</span><span class="sxs-lookup"><span data-stu-id="a7442-146">Otherwise, you must specify the full path to your installation of adb.exe in every command that invokes `adb`.</span></span>

    > [!TIP]
    > <span data-ttu-id="a7442-147">Mute your PC's microphone and speaker to be sure you are working with the development kit's microphones.</span><span class="sxs-lookup"><span data-stu-id="a7442-147">Mute your PC's microphone and speaker to be sure you are working with the development kit's microphones.</span></span> <span data-ttu-id="a7442-148">This way, you won't accidentally trigger the device with audio from the PC.</span><span class="sxs-lookup"><span data-stu-id="a7442-148">This way, you won't accidentally trigger the device with audio from the PC.</span></span>
    
1.  <span data-ttu-id="a7442-149">Start Vysor on your computer.</span><span class="sxs-lookup"><span data-stu-id="a7442-149">Start Vysor on your computer.</span></span>

    ![Vysor](media/speech-devices-sdk/qsg-3.png)

1.  <span data-ttu-id="a7442-151">Your device should be listed under **Choose a device**.</span><span class="sxs-lookup"><span data-stu-id="a7442-151">Your device should be listed under **Choose a device**.</span></span> <span data-ttu-id="a7442-152">Select the **View** button next to the device.</span><span class="sxs-lookup"><span data-stu-id="a7442-152">Select the **View** button next to the device.</span></span> 
 
1.  <span data-ttu-id="a7442-153">Connect to your wireless network by selecting the folder icon, and then select **Settings** > **WLAN**.</span><span class="sxs-lookup"><span data-stu-id="a7442-153">Connect to your wireless network by selecting the folder icon, and then select **Settings** > **WLAN**.</span></span>

    ![Vysor WLAN](media/speech-devices-sdk/qsg-4.png)
 
    > [!NOTE]
    > <span data-ttu-id="a7442-155">If your company has policies about connecting devices to its Wi-Fi system, you need to obtain the MAC address and contact your IT department about how to connect it to your company's Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a7442-155">If your company has policies about connecting devices to its Wi-Fi system, you need to obtain the MAC address and contact your IT department about how to connect it to your company's Wi-Fi.</span></span> 
    >
    > <span data-ttu-id="a7442-156">To find the MAC address of the dev kit, select the file folder icon on the desktop of the dev kit.</span><span class="sxs-lookup"><span data-stu-id="a7442-156">To find the MAC address of the dev kit, select the file folder icon on the desktop of the dev kit.</span></span>
    >
    >  ![Vysor file folder](media/speech-devices-sdk/qsg-10.png)
    >
    > <span data-ttu-id="a7442-158">Select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a7442-158">Select **Settings**.</span></span> <span data-ttu-id="a7442-159">Search for "mac address", and then select **Mac address** > **Advanced WLAN**.</span><span class="sxs-lookup"><span data-stu-id="a7442-159">Search for "mac address", and then select **Mac address** > **Advanced WLAN**.</span></span> <span data-ttu-id="a7442-160">Write down the MAC address that appears near the bottom of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="a7442-160">Write down the MAC address that appears near the bottom of the dialog box.</span></span> 
    >
    > ![Vysor MAC address](media/speech-devices-sdk/qsg-11.png)
    >
    > <span data-ttu-id="a7442-162">Some companies might have a time limit on how long a device can be connected to their Wi-Fi system.</span><span class="sxs-lookup"><span data-stu-id="a7442-162">Some companies might have a time limit on how long a device can be connected to their Wi-Fi system.</span></span> <span data-ttu-id="a7442-163">You might need to extend the dev kit's registration with your Wi-Fi system after a specific number of days.</span><span class="sxs-lookup"><span data-stu-id="a7442-163">You might need to extend the dev kit's registration with your Wi-Fi system after a specific number of days.</span></span>
    > 
    > <span data-ttu-id="a7442-164">If you want to attach a speaker to the dev kit, you can connect it to the audio line out. You should choose a good-quality, 3.5-mm speaker.</span><span class="sxs-lookup"><span data-stu-id="a7442-164">If you want to attach a speaker to the dev kit, you can connect it to the audio line out. You should choose a good-quality, 3.5-mm speaker.</span></span>
    >
    > ![Vysor audio](media/speech-devices-sdk/qsg-14.png)
 
## <a name="run-a-sample-application"></a><span data-ttu-id="a7442-166">Run a sample application</span><span class="sxs-lookup"><span data-stu-id="a7442-166">Run a sample application</span></span>

<span data-ttu-id="a7442-167">To run the ROOBO tests and validate your development kit setup, build and install the sample application:</span><span class="sxs-lookup"><span data-stu-id="a7442-167">To run the ROOBO tests and validate your development kit setup, build and install the sample application:</span></span>

1.  <span data-ttu-id="a7442-168">Start Android Studio.</span><span class="sxs-lookup"><span data-stu-id="a7442-168">Start Android Studio.</span></span>

1.  <span data-ttu-id="a7442-169">Select **Open an existing Android Studio project**.</span><span class="sxs-lookup"><span data-stu-id="a7442-169">Select **Open an existing Android Studio project**.</span></span>

    ![Android Studio - Open an existing project](media/speech-devices-sdk/qsg-5.png)
 
1.  <span data-ttu-id="a7442-171">Go to C:\SDSDK\Android-Sample-Release\example.</span><span class="sxs-lookup"><span data-stu-id="a7442-171">Go to C:\SDSDK\Android-Sample-Release\example.</span></span> <span data-ttu-id="a7442-172">Select **OK** to open the example project.</span><span class="sxs-lookup"><span data-stu-id="a7442-172">Select **OK** to open the example project.</span></span>
 
1.  <span data-ttu-id="a7442-173">Add your Speech subscription key to the source code.</span><span class="sxs-lookup"><span data-stu-id="a7442-173">Add your Speech subscription key to the source code.</span></span> <span data-ttu-id="a7442-174">If you want to try intent recognition, also add your [Language Understanding service](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/) subscription key and application ID.</span><span class="sxs-lookup"><span data-stu-id="a7442-174">If you want to try intent recognition, also add your [Language Understanding service](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/) subscription key and application ID.</span></span> 

    <span data-ttu-id="a7442-175">Your keys and application information go in the following lines in the source file MainActivity.java:</span><span class="sxs-lookup"><span data-stu-id="a7442-175">Your keys and application information go in the following lines in the source file MainActivity.java:</span></span>

    ```java
    // Subscription
    private static final String SpeechSubscriptionKey = "[your speech key]";
    private static final String SpeechRegion = "westus";
    private static final String LuisSubscriptionKey = "[your LUIS key]";
    private static final String LuisRegion = "westus2.api.cognitive.microsoft.com";
    private static final String LuisAppId = "[your LUIS app ID]"
    ```

1. <span data-ttu-id="a7442-176">The default wake word (keyword) is "Computer".</span><span class="sxs-lookup"><span data-stu-id="a7442-176">The default wake word (keyword) is "Computer".</span></span> <span data-ttu-id="a7442-177">You can also try one of the other provided wake words, like "Machine" or "Assistant".</span><span class="sxs-lookup"><span data-stu-id="a7442-177">You can also try one of the other provided wake words, like "Machine" or "Assistant".</span></span> <span data-ttu-id="a7442-178">The resource files for these alternate wake words are in the Speech Devices SDK, in the keyword folder.</span><span class="sxs-lookup"><span data-stu-id="a7442-178">The resource files for these alternate wake words are in the Speech Devices SDK, in the keyword folder.</span></span> <span data-ttu-id="a7442-179">For example, C:\SDSDK\Android-Sample-Release\keyword\Computer contains the files used for the wake word "Computer".</span><span class="sxs-lookup"><span data-stu-id="a7442-179">For example, C:\SDSDK\Android-Sample-Release\keyword\Computer contains the files used for the wake word "Computer".</span></span>

    <span data-ttu-id="a7442-180">You can also [create a custom wake word](speech-devices-sdk-create-kws.md).</span><span class="sxs-lookup"><span data-stu-id="a7442-180">You can also [create a custom wake word](speech-devices-sdk-create-kws.md).</span></span>

    <span data-ttu-id="a7442-181">To install the wake word you want to use:</span><span class="sxs-lookup"><span data-stu-id="a7442-181">To install the wake word you want to use:</span></span>
 
    * <span data-ttu-id="a7442-182">Create a keyword folder in the data folder on the device by running the following commands in a Command Prompt window:</span><span class="sxs-lookup"><span data-stu-id="a7442-182">Create a keyword folder in the data folder on the device by running the following commands in a Command Prompt window:</span></span>

        ```
        adb shell
        cd /data
        mkdir keyword
        exit
        ```

    * <span data-ttu-id="a7442-183">Copy the files kws.table, kws_g.fst, kws_k.fst, and words_kw.txt to the device's \data\keyword folder.</span><span class="sxs-lookup"><span data-stu-id="a7442-183">Copy the files kws.table, kws_g.fst, kws_k.fst, and words_kw.txt to the device's \data\keyword folder.</span></span> <span data-ttu-id="a7442-184">Run the following commands in a Command Prompt window.</span><span class="sxs-lookup"><span data-stu-id="a7442-184">Run the following commands in a Command Prompt window.</span></span> <span data-ttu-id="a7442-185">If you created a [custom wake word](speech-devices-sdk-create-kws.md), the kws.table file generated from the web is in the same directory as the kws.table, kws_g.fst, kws_k.fst, and words_kw.txt files.</span><span class="sxs-lookup"><span data-stu-id="a7442-185">If you created a [custom wake word](speech-devices-sdk-create-kws.md), the kws.table file generated from the web is in the same directory as the kws.table, kws_g.fst, kws_k.fst, and words_kw.txt files.</span></span> <span data-ttu-id="a7442-186">For a custom wake word, use the `adb push C:\SDSDK\Android-Sample-Release\keyword\[wake_word_name]\kws.table /data/keyword` command to push the kws.table file to the dev kit:</span><span class="sxs-lookup"><span data-stu-id="a7442-186">For a custom wake word, use the `adb push C:\SDSDK\Android-Sample-Release\keyword\[wake_word_name]\kws.table /data/keyword` command to push the kws.table file to the dev kit:</span></span>

        ```
        adb push C:\SDSDK\Android-Sample-Release\keyword\kws.table /data/keyword
        adb push C:\SDSDK\Android-Sample-Release\keyword\Computer\kws_g.fst /data/keyword
        adb push C:\SDSDK\Android-Sample-Release\keyword\Computer\kws_k.fst /data/keyword
        adb push C:\SDSDK\Android-Sample-Release\keyword\Computer\words_kw.txt /data/keyword
        ```
    
    * <span data-ttu-id="a7442-187">Reference these files in the sample application.</span><span class="sxs-lookup"><span data-stu-id="a7442-187">Reference these files in the sample application.</span></span> <span data-ttu-id="a7442-188">Find the following lines in MainActivity.java.</span><span class="sxs-lookup"><span data-stu-id="a7442-188">Find the following lines in MainActivity.java.</span></span> <span data-ttu-id="a7442-189">Make sure that the keyword specified is the one you're using, and that the path points to the `kws.table` file that you pushed to the device.</span><span class="sxs-lookup"><span data-stu-id="a7442-189">Make sure that the keyword specified is the one you're using, and that the path points to the `kws.table` file that you pushed to the device.</span></span>
        
        ```java
        private static final String Keyword = "Computer";
        private static final String KeywordModel = "/data/keyword/kws.table";
        ```

        > [!NOTE]
        > <span data-ttu-id="a7442-190">In your own code, you can use the kws.table file to create a keyword model instance and start recognition:</span><span class="sxs-lookup"><span data-stu-id="a7442-190">In your own code, you can use the kws.table file to create a keyword model instance and start recognition:</span></span>
        >
        > ```java
        > KeywordRecognitionModel km = KeywordRecognitionModel.fromFile(KeywordModel);
        > final Task<?> task = reco.startKeywordRecognitionAsync(km);
        > ```

1.  <span data-ttu-id="a7442-191">Update the following lines, which contain the microphone array geometry settings:</span><span class="sxs-lookup"><span data-stu-id="a7442-191">Update the following lines, which contain the microphone array geometry settings:</span></span>

    ```java
    private static final String DeviceGeometry = "Circular6+1";
    private static final String SelectedGeometry = "Circular6+1";
    ```
    <span data-ttu-id="a7442-192">The following table describes the available values:</span><span class="sxs-lookup"><span data-stu-id="a7442-192">The following table describes the available values:</span></span>
    
    |<span data-ttu-id="a7442-193">Variable</span><span class="sxs-lookup"><span data-stu-id="a7442-193">Variable</span></span>|<span data-ttu-id="a7442-194">Meaning</span><span class="sxs-lookup"><span data-stu-id="a7442-194">Meaning</span></span>|<span data-ttu-id="a7442-195">Available values</span><span class="sxs-lookup"><span data-stu-id="a7442-195">Available values</span></span>|
    |--------|-------|----------------|
    |`DeviceGeometry`|<span data-ttu-id="a7442-196">Physical mic configuration</span><span class="sxs-lookup"><span data-stu-id="a7442-196">Physical mic configuration</span></span>|<span data-ttu-id="a7442-197">For a circular dev kit: `Circular6+1`</span><span class="sxs-lookup"><span data-stu-id="a7442-197">For a circular dev kit: `Circular6+1`</span></span> |
    |||<span data-ttu-id="a7442-198">For a linear dev kit: `Linear4`</span><span class="sxs-lookup"><span data-stu-id="a7442-198">For a linear dev kit: `Linear4`</span></span>|
    |`SelectedGeometry`|<span data-ttu-id="a7442-199">Software mic configuration</span><span class="sxs-lookup"><span data-stu-id="a7442-199">Software mic configuration</span></span>|<span data-ttu-id="a7442-200">For a circular dev kit that uses all mics: `Circular6+1`</span><span class="sxs-lookup"><span data-stu-id="a7442-200">For a circular dev kit that uses all mics: `Circular6+1`</span></span>|
    |||<span data-ttu-id="a7442-201">For a circular dev kit that uses four mics: `Circular3+1`</span><span class="sxs-lookup"><span data-stu-id="a7442-201">For a circular dev kit that uses four mics: `Circular3+1`</span></span>|
    |||<span data-ttu-id="a7442-202">For a linear dev kit that uses all mics: `Linear4`</span><span class="sxs-lookup"><span data-stu-id="a7442-202">For a linear dev kit that uses all mics: `Linear4`</span></span>|
    |||<span data-ttu-id="a7442-203">For a linear dev kit that uses two mics: `Linear2`</span><span class="sxs-lookup"><span data-stu-id="a7442-203">For a linear dev kit that uses two mics: `Linear2`</span></span>|


1.  <span data-ttu-id="a7442-204">To build the application, on the **Run** menu, select **Run 'app'**.</span><span class="sxs-lookup"><span data-stu-id="a7442-204">To build the application, on the **Run** menu, select **Run 'app'**.</span></span> <span data-ttu-id="a7442-205">The **Select Deployment Target** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="a7442-205">The **Select Deployment Target** dialog box appears.</span></span> 

1. <span data-ttu-id="a7442-206">Select your device, and then select **OK** to deploy the application to the device.</span><span class="sxs-lookup"><span data-stu-id="a7442-206">Select your device, and then select **OK** to deploy the application to the device.</span></span>

    ![Select Deployment Target dialog box](media/speech-devices-sdk/qsg-7.png)
 
1.  <span data-ttu-id="a7442-208">The Speech Devices SDK example application starts and displays the following options:</span><span class="sxs-lookup"><span data-stu-id="a7442-208">The Speech Devices SDK example application starts and displays the following options:</span></span>

    ![Sample Speech Devices SDK example application and options](media/speech-devices-sdk/qsg-8.png)

1. <span data-ttu-id="a7442-210">Experiment!</span><span class="sxs-lookup"><span data-stu-id="a7442-210">Experiment!</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a7442-211">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a7442-211">Troubleshooting</span></span>

### <a name="certificate-failures"></a><span data-ttu-id="a7442-212">Certificate failures</span><span class="sxs-lookup"><span data-stu-id="a7442-212">Certificate failures</span></span>

<span data-ttu-id="a7442-213">If you get certificate failures when you use the Speech service, make sure that your device has the correct date and time:</span><span class="sxs-lookup"><span data-stu-id="a7442-213">If you get certificate failures when you use the Speech service, make sure that your device has the correct date and time:</span></span>

1. <span data-ttu-id="a7442-214">Go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a7442-214">Go to **Settings**.</span></span> <span data-ttu-id="a7442-215">Under **System**, select **Date & time**.</span><span class="sxs-lookup"><span data-stu-id="a7442-215">Under **System**, select **Date & time**.</span></span>

    ![Under Settings, select Date & time](media/speech-devices-sdk/qsg-12.png)

1. <span data-ttu-id="a7442-217">Keep the **Automatic date & time** option selected.</span><span class="sxs-lookup"><span data-stu-id="a7442-217">Keep the **Automatic date & time** option selected.</span></span> <span data-ttu-id="a7442-218">Under **Select time zone**, select your current time zone.</span><span class="sxs-lookup"><span data-stu-id="a7442-218">Under **Select time zone**, select your current time zone.</span></span> 

    ![Select date and time zone options](media/speech-devices-sdk/qsg-13.png)

    <span data-ttu-id="a7442-220">When you see that the dev kit's time matches the time on your PC, the dev kit is connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="a7442-220">When you see that the dev kit's time matches the time on your PC, the dev kit is connected to the internet.</span></span> 
    
    <span data-ttu-id="a7442-221">For more development information, see the [ROOBO development guide](http://dwn.roo.bo/server_upload/ddk/ROOBO%20Dev%20Kit-User%20Guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="a7442-221">For more development information, see the [ROOBO development guide](http://dwn.roo.bo/server_upload/ddk/ROOBO%20Dev%20Kit-User%20Guide.pdf).</span></span>

### <a name="audio"></a><span data-ttu-id="a7442-222">Audio</span><span class="sxs-lookup"><span data-stu-id="a7442-222">Audio</span></span>

<span data-ttu-id="a7442-223">ROOBO provides a tool that captures all audio to flash memory.</span><span class="sxs-lookup"><span data-stu-id="a7442-223">ROOBO provides a tool that captures all audio to flash memory.</span></span> <span data-ttu-id="a7442-224">It might help you troubleshoot audio issues.</span><span class="sxs-lookup"><span data-stu-id="a7442-224">It might help you troubleshoot audio issues.</span></span> <span data-ttu-id="a7442-225">A version of the tool is provided for each development kit configuration.</span><span class="sxs-lookup"><span data-stu-id="a7442-225">A version of the tool is provided for each development kit configuration.</span></span> <span data-ttu-id="a7442-226">On the  [ROOBO site](http://ddk.roobo.com/), select your device, and then select the **ROOBO Tools** link at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a7442-226">On the  [ROOBO site](http://ddk.roobo.com/), select your device, and then select the **ROOBO Tools** link at the bottom of the page.</span></span>
