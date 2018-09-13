---
title: 'Quickstart: Recognize speech in C++ on Linux using the Cognitive Services Speech SDK'
titleSuffix: Microsoft Cognitive Services
description: Learn how to recognize speech in C++ on Linux using the Cognitive Services Speech SDK
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.technology: Speech
ms.topic: quickstart
ms.date: 08/28/2018
ms.author: wolfma
ms.openlocfilehash: c57bfbee1fd96b79adf434a84335278404aa8872
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871685"
---
# <a name="quickstart-recognize-speech-in-c-on-linux-using-the-speech-sdk"></a><span data-ttu-id="dca29-103">Quickstart: Recognize speech in C++ on Linux using the Speech SDK</span><span class="sxs-lookup"><span data-stu-id="dca29-103">Quickstart: Recognize speech in C++ on Linux using the Speech SDK</span></span>

[!INCLUDE [Selector](../../../includes/cognitive-services-speech-service-quickstart-selector.md)]

<span data-ttu-id="dca29-104">In this article, you create a C++ console application for Ubuntu Linux 16.04 using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span><span class="sxs-lookup"><span data-stu-id="dca29-104">In this article, you create a C++ console application for Ubuntu Linux 16.04 using the Cognitive Services [Speech SDK](speech-sdk.md) to transcribe speech to text in real time from your PC's microphone.</span></span> <span data-ttu-id="dca29-105">The application is built with the [Speech SDK for Linux](https://aka.ms/csspeech/linuxbinary) and your Linux distribution's C++ compiler (e.g., `g++`).</span><span class="sxs-lookup"><span data-stu-id="dca29-105">The application is built with the [Speech SDK for Linux](https://aka.ms/csspeech/linuxbinary) and your Linux distribution's C++ compiler (e.g., `g++`).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dca29-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dca29-106">Prerequisites</span></span>

<span data-ttu-id="dca29-107">You need a Speech service subscription key to complete this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="dca29-107">You need a Speech service subscription key to complete this Quickstart.</span></span> <span data-ttu-id="dca29-108">You can get one for free.</span><span class="sxs-lookup"><span data-stu-id="dca29-108">You can get one for free.</span></span> <span data-ttu-id="dca29-109">See [Try the speech service for free](get-started.md) for details.</span><span class="sxs-lookup"><span data-stu-id="dca29-109">See [Try the speech service for free](get-started.md) for details.</span></span>

## <a name="install-speech-sdk"></a><span data-ttu-id="dca29-110">Install Speech SDK</span><span class="sxs-lookup"><span data-stu-id="dca29-110">Install Speech SDK</span></span>

[!INCLUDE [License Notice](../../../includes/cognitive-services-speech-service-license-notice.md)]

<span data-ttu-id="dca29-111">The Speech SDK for Linux can be used to build both 64-bit and 32-bit applications.</span><span class="sxs-lookup"><span data-stu-id="dca29-111">The Speech SDK for Linux can be used to build both 64-bit and 32-bit applications.</span></span> <span data-ttu-id="dca29-112">The required libraries and header files can be downloaded as a tarfile from https://aka.ms/csspeech/linuxbinary.</span><span class="sxs-lookup"><span data-stu-id="dca29-112">The required libraries and header files can be downloaded as a tarfile from https://aka.ms/csspeech/linuxbinary.</span></span>

<span data-ttu-id="dca29-113">Download and install the SDK as follows:</span><span class="sxs-lookup"><span data-stu-id="dca29-113">Download and install the SDK as follows:</span></span>

1. <span data-ttu-id="dca29-114">Make sure the SDK's dependencies are installed.</span><span class="sxs-lookup"><span data-stu-id="dca29-114">Make sure the SDK's dependencies are installed.</span></span>

  ```sh
  sudo apt-get update
  sudo apt-get install build-essential libssl1.0.0 libcurl3 libasound2 wget
  ```

1. <span data-ttu-id="dca29-115">Choose a directory to which the Speech SDK files should be extracted and set the `SPEECHSDK_ROOT` environment variable to point to that directory.</span><span class="sxs-lookup"><span data-stu-id="dca29-115">Choose a directory to which the Speech SDK files should be extracted and set the `SPEECHSDK_ROOT` environment variable to point to that directory.</span></span> <span data-ttu-id="dca29-116">This variable will make it easy to refer to the directory in future commands.</span><span class="sxs-lookup"><span data-stu-id="dca29-116">This variable will make it easy to refer to the directory in future commands.</span></span> <span data-ttu-id="dca29-117">For example, if you want to use the directory `speechsdk` in your home directory, use a command like the one here.</span><span class="sxs-lookup"><span data-stu-id="dca29-117">For example, if you want to use the directory `speechsdk` in your home directory, use a command like the one here.</span></span>

   ```sh
   export SPEECHSDK_ROOT="$HOME/speechsdk"
   ```

1. <span data-ttu-id="dca29-118">Create the directory if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="dca29-118">Create the directory if it doesn't exist yet.</span></span>

   ```sh
   mkdir -p "$SPEECHSDK_ROOT"
   ```

1. <span data-ttu-id="dca29-119">Download and extract the `.tar.gz` archive containing the Speech SDK binaries:</span><span class="sxs-lookup"><span data-stu-id="dca29-119">Download and extract the `.tar.gz` archive containing the Speech SDK binaries:</span></span>

   ```sh
   wget -O SpeechSDK-Linux.tar.gz https://aka.ms/csspeech/linuxbinary
   tar --strip 1 -xzf SpeechSDK-Linux.tar.gz -C "$SPEECHSDK_ROOT"
   ```

1. <span data-ttu-id="dca29-120">Validate the contents of the top-level directory of the extracted package:</span><span class="sxs-lookup"><span data-stu-id="dca29-120">Validate the contents of the top-level directory of the extracted package:</span></span>

   ```sh
   ls -l "$SPEECHSDK_ROOT"
   ```

   <span data-ttu-id="dca29-121">The directory listing should contain the third-party notice and license files, as well as an `include` directory containing header (`.h`) files and a `lib` directory containing libraries.</span><span class="sxs-lookup"><span data-stu-id="dca29-121">The directory listing should contain the third-party notice and license files, as well as an `include` directory containing header (`.h`) files and a `lib` directory containing libraries.</span></span>

   [!INCLUDE [Linux Binary Archive Content](../../../includes/cognitive-services-speech-service-linuxbinary-content.md)]

## <a name="add-sample-code"></a><span data-ttu-id="dca29-122">Add sample code</span><span class="sxs-lookup"><span data-stu-id="dca29-122">Add sample code</span></span>

1. <span data-ttu-id="dca29-123">Create a C++ source file named `helloworld.cpp` and paste the following code into it.</span><span class="sxs-lookup"><span data-stu-id="dca29-123">Create a C++ source file named `helloworld.cpp` and paste the following code into it.</span></span>

  [!code-cpp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/cpp-linux/helloworld.cpp#code)]

1. <span data-ttu-id="dca29-124">In this new file, replace the string `YourSubscriptionKey` with your Speech service subscription key.</span><span class="sxs-lookup"><span data-stu-id="dca29-124">In this new file, replace the string `YourSubscriptionKey` with your Speech service subscription key.</span></span>

1. <span data-ttu-id="dca29-125">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span><span class="sxs-lookup"><span data-stu-id="dca29-125">Also replace the string `YourServiceRegion` with the [region](regions.md) associated with your subscription (for example, `westus` for the free trial subscription).</span></span>

## <a name="build-the-app"></a><span data-ttu-id="dca29-126">Build the app</span><span class="sxs-lookup"><span data-stu-id="dca29-126">Build the app</span></span>

> [!NOTE]
> <span data-ttu-id="dca29-127">Make sure to enter the commands below as a _single command line_.</span><span class="sxs-lookup"><span data-stu-id="dca29-127">Make sure to enter the commands below as a _single command line_.</span></span> <span data-ttu-id="dca29-128">The easiest way to do that is to copy the command using the **Copy** button next to each command, then paste it at your shell prompt.</span><span class="sxs-lookup"><span data-stu-id="dca29-128">The easiest way to do that is to copy the command using the **Copy** button next to each command, then paste it at your shell prompt.</span></span>

* <span data-ttu-id="dca29-129">On an **x64**  (64-bit) system, run the following command to build the application.</span><span class="sxs-lookup"><span data-stu-id="dca29-129">On an **x64**  (64-bit) system, run the following command to build the application.</span></span>

  ```sh
  g++ helloworld.cpp -o helloworld -I "$SPEECHSDK_ROOT/include/cxx_api" -I "$SPEECHSDK_ROOT/include/c_api" --std=c++14 -lpthread -lMicrosoft.CognitiveServices.Speech.core -L "$SPEECHSDK_ROOT/lib/x64" -l:libssl.so.1.0.0 -l:libcurl.so.4 -l:libasound.so.2
  ```

* <span data-ttu-id="dca29-130">On an **x86** (32-bit) system, run the following command to build the application.</span><span class="sxs-lookup"><span data-stu-id="dca29-130">On an **x86** (32-bit) system, run the following command to build the application.</span></span>

  ```sh
  g++ helloworld.cpp -o helloworld -I "$SPEECHSDK_ROOT/include/cxx_api" -I "$SPEECHSDK_ROOT/include/c_api" --std=c++14 -lpthread -lMicrosoft.CognitiveServices.Speech.core -L "$SPEECHSDK_ROOT/lib/x86" -l:libssl.so.1.0.0 -l:libcurl.so.4 -l:libasound.so.2
  ```

## <a name="run-the-app"></a><span data-ttu-id="dca29-131">Run the app</span><span class="sxs-lookup"><span data-stu-id="dca29-131">Run the app</span></span>

1. <span data-ttu-id="dca29-132">Configure the loader's library path to point to the Speech SDK library.</span><span class="sxs-lookup"><span data-stu-id="dca29-132">Configure the loader's library path to point to the Speech SDK library.</span></span>

   * <span data-ttu-id="dca29-133">On an **x64** (64-bit) system, enter the following command.</span><span class="sxs-lookup"><span data-stu-id="dca29-133">On an **x64** (64-bit) system, enter the following command.</span></span>

     ```sh
     export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$SPEECHSDK_ROOT/lib/x64"
     ```

   * <span data-ttu-id="dca29-134">On an **x86** (32-bit) system, enter this command.</span><span class="sxs-lookup"><span data-stu-id="dca29-134">On an **x86** (32-bit) system, enter this command.</span></span>

     ```sh
     export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$SPEECHSDK_ROOT/lib/x86"
     ```

1. <span data-ttu-id="dca29-135">Execute the application.</span><span class="sxs-lookup"><span data-stu-id="dca29-135">Execute the application.</span></span>

   ```sh
   ./helloworld
   ```

1.  <span data-ttu-id="dca29-136">In the console window, a prompt appears requesting that you say something.</span><span class="sxs-lookup"><span data-stu-id="dca29-136">In the console window, a prompt appears requesting that you say something.</span></span> <span data-ttu-id="dca29-137">Speak an English phrase or sentence.</span><span class="sxs-lookup"><span data-stu-id="dca29-137">Speak an English phrase or sentence.</span></span> <span data-ttu-id="dca29-138">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span><span class="sxs-lookup"><span data-stu-id="dca29-138">Your speech is transmitted to the Speech service and transcribed to text, which appears in the same window.</span></span>

   ```text
   Say something...
   We recognized: What's the weather
   ```

[!INCLUDE [Download this sample](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]
<span data-ttu-id="dca29-139">Look for this sample in the `quickstart/cpp-linux` folder.</span><span class="sxs-lookup"><span data-stu-id="dca29-139">Look for this sample in the `quickstart/cpp-linux` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dca29-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="dca29-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dca29-141">Recognize intents from speech by using the Speech SDK for C#</span><span class="sxs-lookup"><span data-stu-id="dca29-141">Recognize intents from speech by using the Speech SDK for C#</span></span>](how-to-recognize-intents-from-speech-csharp.md)

## <a name="see-also"></a><span data-ttu-id="dca29-142">See also</span><span class="sxs-lookup"><span data-stu-id="dca29-142">See also</span></span>

- [<span data-ttu-id="dca29-143">Translate speech</span><span class="sxs-lookup"><span data-stu-id="dca29-143">Translate speech</span></span>](how-to-translate-speech-csharp.md)
- [<span data-ttu-id="dca29-144">Customize acoustic models</span><span class="sxs-lookup"><span data-stu-id="dca29-144">Customize acoustic models</span></span>](how-to-customize-acoustic-models.md)
- [<span data-ttu-id="dca29-145">Customize language models</span><span class="sxs-lookup"><span data-stu-id="dca29-145">Customize language models</span></span>](how-to-customize-language-model.md)
