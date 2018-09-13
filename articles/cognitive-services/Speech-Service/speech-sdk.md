---
title: About the Cognitive Services Speech SDK
description: An overview of the SDKs available for the Speech service.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 08/16/2018
ms.author: v-jerkin
ms.openlocfilehash: c26aeb1d29c3b2c8b5b43d1a1face818295e9d2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857067"
---
# <a name="about-the-cognitive-services-speech-sdk"></a><span data-ttu-id="891ba-103">About the Cognitive Services Speech SDK</span><span class="sxs-lookup"><span data-stu-id="891ba-103">About the Cognitive Services Speech SDK</span></span>

<span data-ttu-id="891ba-104">The Cognitive Services Speech Software Development Kit (SDK) provides your applications native access to the functions of the Speech service, making it easier to develop software.</span><span class="sxs-lookup"><span data-stu-id="891ba-104">The Cognitive Services Speech Software Development Kit (SDK) provides your applications native access to the functions of the Speech service, making it easier to develop software.</span></span> <span data-ttu-id="891ba-105">Currently, the SDK provides access to **Speech to Text**, **Speech Translation**, and **Intent Recognition**.</span><span class="sxs-lookup"><span data-stu-id="891ba-105">Currently, the SDK provides access to **Speech to Text**, **Speech Translation**, and **Intent Recognition**.</span></span>

[!INCLUDE [Speech SDK Platforms](../../../includes/cognitive-services-speech-service-speech-sdk-platforms.md)]

[!INCLUDE [License Notice](../../../includes/cognitive-services-speech-service-license-notice.md)]

## <a name="get-the-sdk"></a><span data-ttu-id="891ba-106">Get the SDK</span><span class="sxs-lookup"><span data-stu-id="891ba-106">Get the SDK</span></span>

### <a name="windows"></a><span data-ttu-id="891ba-107">Windows</span><span class="sxs-lookup"><span data-stu-id="891ba-107">Windows</span></span>

<span data-ttu-id="891ba-108">For Windows we support the following languages:</span><span class="sxs-lookup"><span data-stu-id="891ba-108">For Windows we support the following languages:</span></span>

* <span data-ttu-id="891ba-109">C# (UWP and .NET), C++: You can reference and use the latest version of our Speech SDK NuGet package.</span><span class="sxs-lookup"><span data-stu-id="891ba-109">C# (UWP and .NET), C++: You can reference and use the latest version of our Speech SDK NuGet package.</span></span>
  <span data-ttu-id="891ba-110">The package includes 32-bit and 64-bit client libraries as well as managed (.NET) libraries.</span><span class="sxs-lookup"><span data-stu-id="891ba-110">The package includes 32-bit and 64-bit client libraries as well as managed (.NET) libraries.</span></span>
  <span data-ttu-id="891ba-111">The SDK can be installed in Visual Studio using NuGet; simply search for `Microsoft.CognitiveServices.Speech`.</span><span class="sxs-lookup"><span data-stu-id="891ba-111">The SDK can be installed in Visual Studio using NuGet; simply search for `Microsoft.CognitiveServices.Speech`.</span></span>

* <span data-ttu-id="891ba-112">Java: You can reference and use the latest version of our Speech SDK Maven package, which supports Windows x64 only.</span><span class="sxs-lookup"><span data-stu-id="891ba-112">Java: You can reference and use the latest version of our Speech SDK Maven package, which supports Windows x64 only.</span></span>
  <span data-ttu-id="891ba-113">In your Maven project, add `https://csspeechstorage.blob.core.windows.net/maven/` as an additional repository, and reference `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0` as a dependency.</span><span class="sxs-lookup"><span data-stu-id="891ba-113">In your Maven project, add `https://csspeechstorage.blob.core.windows.net/maven/` as an additional repository, and reference `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0` as a dependency.</span></span> 

### <a name="linux"></a><span data-ttu-id="891ba-114">Linux</span><span class="sxs-lookup"><span data-stu-id="891ba-114">Linux</span></span>

> [!NOTE]
> <span data-ttu-id="891ba-115">Currently, we only support Ubuntu 16.04 on a PC (x86 or x64 for C++ development, x64 for .NET Core and Java).</span><span class="sxs-lookup"><span data-stu-id="891ba-115">Currently, we only support Ubuntu 16.04 on a PC (x86 or x64 for C++ development, x64 for .NET Core and Java).</span></span>

<span data-ttu-id="891ba-116">Make sure you have the required compiler and libraries installed by running the following shell commands:</span><span class="sxs-lookup"><span data-stu-id="891ba-116">Make sure you have the required compiler and libraries installed by running the following shell commands:</span></span>

```sh
sudo apt-get update
sudo apt-get install build-essential libssl1.0.0 libcurl3 libasound2
```

* <span data-ttu-id="891ba-117">C#: You can reference and use the latest version of our Speech SDK NuGet package.</span><span class="sxs-lookup"><span data-stu-id="891ba-117">C#: You can reference and use the latest version of our Speech SDK NuGet package.</span></span>
  <span data-ttu-id="891ba-118">To reference the SDK, add the following package reference into your project:</span><span class="sxs-lookup"><span data-stu-id="891ba-118">To reference the SDK, add the following package reference into your project:</span></span>

  ```xml
  <PackageReference Include="Microsoft.CognitiveServices.Speech" Version="0.6.0" />
  ```

* <span data-ttu-id="891ba-119">Java: You can reference and use the latest version of our Speech SDK Maven package.</span><span class="sxs-lookup"><span data-stu-id="891ba-119">Java: You can reference and use the latest version of our Speech SDK Maven package.</span></span>
  <span data-ttu-id="891ba-120">In your Maven project, add `https://csspeechstorage.blob.core.windows.net/maven/` as an additional repository, and reference `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0` as a dependency.</span><span class="sxs-lookup"><span data-stu-id="891ba-120">In your Maven project, add `https://csspeechstorage.blob.core.windows.net/maven/` as an additional repository, and reference `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0` as a dependency.</span></span> 

* <span data-ttu-id="891ba-121">C++: download the SDK as a [.tar package](https://aka.ms/csspeech/linuxbinary) and unpack the files in into a directory of your choice.</span><span class="sxs-lookup"><span data-stu-id="891ba-121">C++: download the SDK as a [.tar package](https://aka.ms/csspeech/linuxbinary) and unpack the files in into a directory of your choice.</span></span> <span data-ttu-id="891ba-122">The following table shows the SDK folder structure.</span><span class="sxs-lookup"><span data-stu-id="891ba-122">The following table shows the SDK folder structure.</span></span>

  |<span data-ttu-id="891ba-123">Path</span><span class="sxs-lookup"><span data-stu-id="891ba-123">Path</span></span>|<span data-ttu-id="891ba-124">Description</span><span class="sxs-lookup"><span data-stu-id="891ba-124">Description</span></span>|
  |-|-|
  |`license.md`|<span data-ttu-id="891ba-125">License</span><span class="sxs-lookup"><span data-stu-id="891ba-125">License</span></span>|
  |`ThirdPartyNotices.md`|<span data-ttu-id="891ba-126">Third-party notices</span><span class="sxs-lookup"><span data-stu-id="891ba-126">Third-party notices</span></span>|
  |`include`|<span data-ttu-id="891ba-127">Header files for C and C++</span><span class="sxs-lookup"><span data-stu-id="891ba-127">Header files for C and C++</span></span>|
  |`lib/x64`|<span data-ttu-id="891ba-128">Native x64 library for linking with your application</span><span class="sxs-lookup"><span data-stu-id="891ba-128">Native x64 library for linking with your application</span></span>|
  |`lib/x86`|<span data-ttu-id="891ba-129">Native x86 library for linking with your application</span><span class="sxs-lookup"><span data-stu-id="891ba-129">Native x86 library for linking with your application</span></span>|

  <span data-ttu-id="891ba-130">To create an application, copy or move the required binaries (and libraries) into your development environment, and include them as required into your build process.</span><span class="sxs-lookup"><span data-stu-id="891ba-130">To create an application, copy or move the required binaries (and libraries) into your development environment, and include them as required into your build process.</span></span>

### <a name="android"></a><span data-ttu-id="891ba-131">Android</span><span class="sxs-lookup"><span data-stu-id="891ba-131">Android</span></span>

<span data-ttu-id="891ba-132">The Java SDK for Android is packaged as an [AAR (Android Library)](https://developer.android.com/studio/projects/android-library), which includes the necessary libraries as well as required Android permissions for using it.</span><span class="sxs-lookup"><span data-stu-id="891ba-132">The Java SDK for Android is packaged as an [AAR (Android Library)](https://developer.android.com/studio/projects/android-library), which includes the necessary libraries as well as required Android permissions for using it.</span></span>
<span data-ttu-id="891ba-133">It is hosted in a Maven repository at `https://csspeechstorage.blob.core.windows.net/maven/` as package `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0`.</span><span class="sxs-lookup"><span data-stu-id="891ba-133">It is hosted in a Maven repository at `https://csspeechstorage.blob.core.windows.net/maven/` as package `com.microsoft.cognitiveservices.speech:client-sdk:0.6.0`.</span></span>
<span data-ttu-id="891ba-134">To consume the package from your Android Studio project make the following changes:</span><span class="sxs-lookup"><span data-stu-id="891ba-134">To consume the package from your Android Studio project make the following changes:</span></span>

* <span data-ttu-id="891ba-135">In the project-level `build.gradle` file, add the following into the `repository` section:</span><span class="sxs-lookup"><span data-stu-id="891ba-135">In the project-level `build.gradle` file, add the following into the `repository` section:</span></span>

  ```text
  maven { url 'https://csspeechstorage.blob.core.windows.net/maven/' }
  ```

* <span data-ttu-id="891ba-136">In the module-level `build.gradle` file, add the following into the `dependencies` section:</span><span class="sxs-lookup"><span data-stu-id="891ba-136">In the module-level `build.gradle` file, add the following into the `dependencies` section:</span></span>

  ```text
  implementation 'com.microsoft.cognitiveservices.speech:client-sdk:0.6.0'
  ```

<span data-ttu-id="891ba-137">The Java SDK is also part of the [Speech Devices SDK](speech-devices-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="891ba-137">The Java SDK is also part of the [Speech Devices SDK](speech-devices-sdk.md).</span></span>

[!INCLUDE [Get the samples](../../../includes/cognitive-services-speech-service-speech-sdk-sample-download-h2.md)]

## <a name="next-steps"></a><span data-ttu-id="891ba-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="891ba-138">Next steps</span></span>

* [<span data-ttu-id="891ba-139">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="891ba-139">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="891ba-140">See how to recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="891ba-140">See how to recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
