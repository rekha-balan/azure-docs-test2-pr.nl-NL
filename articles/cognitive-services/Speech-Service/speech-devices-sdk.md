---
title: About the Speech Devices SDK
description: Get an introduction to the Speech Devices SDK.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jerkin
ms.openlocfilehash: ea1f2248feaa6b96f757b251d293860ad40ff8ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871637"
---
# <a name="about-the-speech-devices-sdk-preview"></a><span data-ttu-id="52ae9-103">About the Speech Devices SDK (Preview)</span><span class="sxs-lookup"><span data-stu-id="52ae9-103">About the Speech Devices SDK (Preview)</span></span>

<span data-ttu-id="52ae9-104">The [Microsoft Speech service](overview.md) works with a wide variety of devices and audio sources.</span><span class="sxs-lookup"><span data-stu-id="52ae9-104">The [Microsoft Speech service](overview.md) works with a wide variety of devices and audio sources.</span></span> <span data-ttu-id="52ae9-105">Now, you can take your speech applications to the next level with matched hardware and software.</span><span class="sxs-lookup"><span data-stu-id="52ae9-105">Now, you can take your speech applications to the next level with matched hardware and software.</span></span> <span data-ttu-id="52ae9-106">The Speech Devices SDK is a pretuned library that's paired with purpose-built, microphone array development kits.</span><span class="sxs-lookup"><span data-stu-id="52ae9-106">The Speech Devices SDK is a pretuned library that's paired with purpose-built, microphone array development kits.</span></span> 

<span data-ttu-id="52ae9-107">The Speech Devices SDK can help you:</span><span class="sxs-lookup"><span data-stu-id="52ae9-107">The Speech Devices SDK can help you:</span></span>
* <span data-ttu-id="52ae9-108">Rapidly test new voice scenarios.</span><span class="sxs-lookup"><span data-stu-id="52ae9-108">Rapidly test new voice scenarios.</span></span>
* <span data-ttu-id="52ae9-109">More easily integrate the cloud-based Speech service into your device.</span><span class="sxs-lookup"><span data-stu-id="52ae9-109">More easily integrate the cloud-based Speech service into your device.</span></span>
* <span data-ttu-id="52ae9-110">Create an exceptional user experience for your customers.</span><span class="sxs-lookup"><span data-stu-id="52ae9-110">Create an exceptional user experience for your customers.</span></span> 

<span data-ttu-id="52ae9-111">The Speech Devices SDK consumes the [Speech SDK](speech-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="52ae9-111">The Speech Devices SDK consumes the [Speech SDK](speech-sdk.md).</span></span> <span data-ttu-id="52ae9-112">It uses the Speech SDK to send the audio that's processed by our advanced audio processing algorithm from the device's microphone array to the [Speech service](overview.md).</span><span class="sxs-lookup"><span data-stu-id="52ae9-112">It uses the Speech SDK to send the audio that's processed by our advanced audio processing algorithm from the device's microphone array to the [Speech service](overview.md).</span></span> <span data-ttu-id="52ae9-113">It uses multichannel audio to provide more accurate far-field [speech recognition](speech-to-text.md) via noise suppression, echo cancellation, beamforming, and dereverberation.</span><span class="sxs-lookup"><span data-stu-id="52ae9-113">It uses multichannel audio to provide more accurate far-field [speech recognition](speech-to-text.md) via noise suppression, echo cancellation, beamforming, and dereverberation.</span></span>

<span data-ttu-id="52ae9-114">You can also use the Speech Devices SDK to build ambient devices that have your own [customized wake word](speech-devices-sdk-create-kws.md)—so the cue that initiates a user interaction is unique to your brand.</span><span class="sxs-lookup"><span data-stu-id="52ae9-114">You can also use the Speech Devices SDK to build ambient devices that have your own [customized wake word](speech-devices-sdk-create-kws.md)—so the cue that initiates a user interaction is unique to your brand.</span></span> 

<span data-ttu-id="52ae9-115">The Speech Devices SDK facilitates a variety of voice-enabled scenarios, such as drive-thru ordering systems, in-store or in-home assistants, and smart speakers.</span><span class="sxs-lookup"><span data-stu-id="52ae9-115">The Speech Devices SDK facilitates a variety of voice-enabled scenarios, such as drive-thru ordering systems, in-store or in-home assistants, and smart speakers.</span></span> <span data-ttu-id="52ae9-116">You can respond to users with text, speak back to them in a default or [custom voice](how-to-customize-voice-font.md), provide search results, [translate](speech-translation.md) to other languages, and more.</span><span class="sxs-lookup"><span data-stu-id="52ae9-116">You can respond to users with text, speak back to them in a default or [custom voice](how-to-customize-voice-font.md), provide search results, [translate](speech-translation.md) to other languages, and more.</span></span> <span data-ttu-id="52ae9-117">We look forward to seeing what you build!</span><span class="sxs-lookup"><span data-stu-id="52ae9-117">We look forward to seeing what you build!</span></span>

## <a name="development-kit-providers"></a><span data-ttu-id="52ae9-118">Development kit providers</span><span class="sxs-lookup"><span data-stu-id="52ae9-118">Development kit providers</span></span>

<span data-ttu-id="52ae9-119">Currently, these complete, end-to-end system reference designs are available:</span><span class="sxs-lookup"><span data-stu-id="52ae9-119">Currently, these complete, end-to-end system reference designs are available:</span></span> 

|||
|-|-|
|<span data-ttu-id="52ae9-120">[![ROOBO logo](media/speech-devices-sdk/roobo-logo.png)](http://ddk.roobo.com/)</span><span class="sxs-lookup"><span data-stu-id="52ae9-120">[![ROOBO logo](media/speech-devices-sdk/roobo-logo.png)](http://ddk.roobo.com/)</span></span>|<span data-ttu-id="52ae9-121">ROOBO provides complete artificial intelligence (AI) system solutions for household electric appliances, automobiles, robots, toys, and other industries.</span><span class="sxs-lookup"><span data-stu-id="52ae9-121">ROOBO provides complete artificial intelligence (AI) system solutions for household electric appliances, automobiles, robots, toys, and other industries.</span></span> <span data-ttu-id="52ae9-122">ROOBO's reference designs greatly reduce development time-to-market via integration with the Microsoft Speech service.</span><span class="sxs-lookup"><span data-stu-id="52ae9-122">ROOBO's reference designs greatly reduce development time-to-market via integration with the Microsoft Speech service.</span></span> <span data-ttu-id="52ae9-123">[Visit ROOBO](http://ddk.roobo.com/).</span><span class="sxs-lookup"><span data-stu-id="52ae9-123">[Visit ROOBO](http://ddk.roobo.com/).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="52ae9-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="52ae9-124">Next steps</span></span>

<span data-ttu-id="52ae9-125">To get started, get a [free Azure account](https://azure.microsoft.com/free/ai/) and sign up for the Speech Devices SDK.</span><span class="sxs-lookup"><span data-stu-id="52ae9-125">To get started, get a [free Azure account](https://azure.microsoft.com/free/ai/) and sign up for the Speech Devices SDK.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52ae9-126">Sign up for the Speech Devices SDK</span><span class="sxs-lookup"><span data-stu-id="52ae9-126">Sign up for the Speech Devices SDK</span></span>](get-speech-devices-sdk.md)

