---
title: Azure Cognitive Services, Cognitive Services Speech SDK API Documentation - Tutorials, API Reference
description: Learn how to create and develop apps with the Cognitive Services Speech SDK
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: wolfma61
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 06/07/2018
ms.author: wolfma
ms.openlocfilehash: 65ff0e47cf7a53d519bfd0c50ea4c3ebd09a5766
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866339"
---
# <a name="shipping-an-application"></a><span data-ttu-id="5d211-103">Shipping an application</span><span class="sxs-lookup"><span data-stu-id="5d211-103">Shipping an application</span></span>

<span data-ttu-id="5d211-104">Observe the [Speech SDK license](license.md), as well as the [third party software notices](third-party-notices.md) when distributing the Cognitive Services Speech SDK.</span><span class="sxs-lookup"><span data-stu-id="5d211-104">Observe the [Speech SDK license](license.md), as well as the [third party software notices](third-party-notices.md) when distributing the Cognitive Services Speech SDK.</span></span> <span data-ttu-id="5d211-105">Also, review the [Microsoft Privacy Statement](https://aka.ms/csspeech/privacy).</span><span class="sxs-lookup"><span data-stu-id="5d211-105">Also, review the [Microsoft Privacy Statement](https://aka.ms/csspeech/privacy).</span></span>

<span data-ttu-id="5d211-106">Depending on the platform, different dependencies exist to execute your application.</span><span class="sxs-lookup"><span data-stu-id="5d211-106">Depending on the platform, different dependencies exist to execute your application.</span></span>

## <a name="windows"></a><span data-ttu-id="5d211-107">Windows</span><span class="sxs-lookup"><span data-stu-id="5d211-107">Windows</span></span>

<span data-ttu-id="5d211-108">The Cognitive Services Speech SDK is tested on Windows 10 and on Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5d211-108">The Cognitive Services Speech SDK is tested on Windows 10 and on Windows Server 2016.</span></span>

<span data-ttu-id="5d211-109">The Cognitive Services Speech SDK requires the [Microsoft Visual C++ Redistributable for Visual Studio 2017](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) on the system.</span><span class="sxs-lookup"><span data-stu-id="5d211-109">The Cognitive Services Speech SDK requires the [Microsoft Visual C++ Redistributable for Visual Studio 2017](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) on the system.</span></span> <span data-ttu-id="5d211-110">You can download installers for the latest version of the `Microsoft Visual C++ Redistributable for Visual Studio 2017` here:</span><span class="sxs-lookup"><span data-stu-id="5d211-110">You can download installers for the latest version of the `Microsoft Visual C++ Redistributable for Visual Studio 2017` here:</span></span>

- [<span data-ttu-id="5d211-111">Win32</span><span class="sxs-lookup"><span data-stu-id="5d211-111">Win32</span></span>](https://aka.ms/vs/15/release/vc_redist.x86.exe)
- [<span data-ttu-id="5d211-112">x64</span><span class="sxs-lookup"><span data-stu-id="5d211-112">x64</span></span>](https://aka.ms/vs/15/release/vc_redist.x64.exe)

<span data-ttu-id="5d211-113">If your application is using managed code, the `.NET Framework 4.6.1` or later is required on the target machine.</span><span class="sxs-lookup"><span data-stu-id="5d211-113">If your application is using managed code, the `.NET Framework 4.6.1` or later is required on the target machine.</span></span>

<span data-ttu-id="5d211-114">For microphone input, the Media Foundation Libraries need to be installed.</span><span class="sxs-lookup"><span data-stu-id="5d211-114">For microphone input, the Media Foundation Libraries need to be installed.</span></span> <span data-ttu-id="5d211-115">These libraries are part of Windows 10 and Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5d211-115">These libraries are part of Windows 10 and Windows Server 2016.</span></span> <span data-ttu-id="5d211-116">It is possible to use the Speech SDK without these libraries, as long as microphone is not used as the audio input device.</span><span class="sxs-lookup"><span data-stu-id="5d211-116">It is possible to use the Speech SDK without these libraries, as long as microphone is not used as the audio input device.</span></span>

<span data-ttu-id="5d211-117">The required Speech SDK files can be deployed in the same directory as your application.</span><span class="sxs-lookup"><span data-stu-id="5d211-117">The required Speech SDK files can be deployed in the same directory as your application.</span></span> <span data-ttu-id="5d211-118">This way your application can directly access the libraries.</span><span class="sxs-lookup"><span data-stu-id="5d211-118">This way your application can directly access the libraries.</span></span> <span data-ttu-id="5d211-119">Make sure you select the correct version (Win32/x64) matching your application.</span><span class="sxs-lookup"><span data-stu-id="5d211-119">Make sure you select the correct version (Win32/x64) matching your application.</span></span>

| <span data-ttu-id="5d211-120">Name</span><span class="sxs-lookup"><span data-stu-id="5d211-120">Name</span></span> | <span data-ttu-id="5d211-121">Function</span><span class="sxs-lookup"><span data-stu-id="5d211-121">Function</span></span>
|:-----|:----|
| `Microsoft.CognitiveServices.Speech.core.dll` | <span data-ttu-id="5d211-122">core SDK, required for native and managed deployment</span><span class="sxs-lookup"><span data-stu-id="5d211-122">core SDK, required for native and managed deployment</span></span>
| `Microsoft.CognitiveServices.Speech.csharp.bindings.dll` | <span data-ttu-id="5d211-123">required for managed deployment</span><span class="sxs-lookup"><span data-stu-id="5d211-123">required for managed deployment</span></span>
| `Microsoft.CognitiveServices.Speech.csharp.dll` | <span data-ttu-id="5d211-124">required for managed deployment</span><span class="sxs-lookup"><span data-stu-id="5d211-124">required for managed deployment</span></span>

## <a name="linux"></a><span data-ttu-id="5d211-125">Linux</span><span class="sxs-lookup"><span data-stu-id="5d211-125">Linux</span></span>

<span data-ttu-id="5d211-126">For a native application you need to ship the Speech SDK library, `libMicrosoft.CognitiveServices.Speech.core.so`.</span><span class="sxs-lookup"><span data-stu-id="5d211-126">For a native application you need to ship the Speech SDK library, `libMicrosoft.CognitiveServices.Speech.core.so`.</span></span>
<span data-ttu-id="5d211-127">Make sure you select the version (x86, x64) matching your application.</span><span class="sxs-lookup"><span data-stu-id="5d211-127">Make sure you select the version (x86, x64) matching your application.</span></span> <span data-ttu-id="5d211-128">Depending on the Linux version, you may also need to include the following dependencies:</span><span class="sxs-lookup"><span data-stu-id="5d211-128">Depending on the Linux version, you may also need to include the following dependencies:</span></span>

* <span data-ttu-id="5d211-129">The shared libraries of the GNU C Library (including the POSIX Threads Programming library, `libpthreads`)</span><span class="sxs-lookup"><span data-stu-id="5d211-129">The shared libraries of the GNU C Library (including the POSIX Threads Programming library, `libpthreads`)</span></span>
* <span data-ttu-id="5d211-130">The OpenSSL library (`libssl.so.1.0.0`)</span><span class="sxs-lookup"><span data-stu-id="5d211-130">The OpenSSL library (`libssl.so.1.0.0`)</span></span>
* <span data-ttu-id="5d211-131">The cURL library (`libcurl.so.4`)</span><span class="sxs-lookup"><span data-stu-id="5d211-131">The cURL library (`libcurl.so.4`)</span></span>
* <span data-ttu-id="5d211-132">The shared library for ALSA applications (`libasound.so.2`)</span><span class="sxs-lookup"><span data-stu-id="5d211-132">The shared library for ALSA applications (`libasound.so.2`)</span></span>

<span data-ttu-id="5d211-133">On Ubuntu 16.04, for example, the GNU C libraries should already be installed by default.</span><span class="sxs-lookup"><span data-stu-id="5d211-133">On Ubuntu 16.04, for example, the GNU C libraries should already be installed by default.</span></span> <span data-ttu-id="5d211-134">The last three can be installed using these commands:</span><span class="sxs-lookup"><span data-stu-id="5d211-134">The last three can be installed using these commands:</span></span>

```sh
sudo apt-get update
sudo apt-get install libssl1.0.0 libcurl3 libasound2 wget
```

## <a name="next-steps"></a><span data-ttu-id="5d211-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d211-135">Next steps</span></span>

* [<span data-ttu-id="5d211-136">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="5d211-136">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="5d211-137">See how to recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="5d211-137">See how to recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
