---
title: About Text to Speech
description: An overview of the capabilities of Text to Speech.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 05/07/2018
ms.author: v-jerkin
ms.openlocfilehash: d111a9f852b849df15dbd056a7210fac82cee190
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870762"
---
# <a name="about-the-text-to-speech-api"></a><span data-ttu-id="db6af-103">About the Text to Speech API</span><span class="sxs-lookup"><span data-stu-id="db6af-103">About the Text to Speech API</span></span>

<span data-ttu-id="db6af-104">The **Text to Speech** (TTS) API of the Speech service converts input text into natural-sounding speech (also called *speech synthesis*).</span><span class="sxs-lookup"><span data-stu-id="db6af-104">The **Text to Speech** (TTS) API of the Speech service converts input text into natural-sounding speech (also called *speech synthesis*).</span></span>

<span data-ttu-id="db6af-105">To generate speech, your application sends HTTP POST requests to the Speech service.</span><span class="sxs-lookup"><span data-stu-id="db6af-105">To generate speech, your application sends HTTP POST requests to the Speech service.</span></span> <span data-ttu-id="db6af-106">There, text is synthesized into human-sounding speech and returned as an audio file.</span><span class="sxs-lookup"><span data-stu-id="db6af-106">There, text is synthesized into human-sounding speech and returned as an audio file.</span></span> <span data-ttu-id="db6af-107">A variety of voices and languages are supported.</span><span class="sxs-lookup"><span data-stu-id="db6af-107">A variety of voices and languages are supported.</span></span>

<span data-ttu-id="db6af-108">Scenarios in which speech synthesis is being adopted include:</span><span class="sxs-lookup"><span data-stu-id="db6af-108">Scenarios in which speech synthesis is being adopted include:</span></span>

* <span data-ttu-id="db6af-109">*Improving accessibility:* **Text to Speech** technology enables content owners and publishers to respond to the different ways people interact with their content.</span><span class="sxs-lookup"><span data-stu-id="db6af-109">*Improving accessibility:* **Text to Speech** technology enables content owners and publishers to respond to the different ways people interact with their content.</span></span> <span data-ttu-id="db6af-110">People with visual impairment or reading difficulties appreciate being able to consume content aurally.</span><span class="sxs-lookup"><span data-stu-id="db6af-110">People with visual impairment or reading difficulties appreciate being able to consume content aurally.</span></span> <span data-ttu-id="db6af-111">Voice output also makes it easier for people to enjoy textual content, such as newspapers or blogs, on mobile devices while commuting or exercising.</span><span class="sxs-lookup"><span data-stu-id="db6af-111">Voice output also makes it easier for people to enjoy textual content, such as newspapers or blogs, on mobile devices while commuting or exercising.</span></span>

* <span data-ttu-id="db6af-112">*Responding in multitasking scenarios:* **Text to Speech** enables people to absorb important information quickly and comfortably while driving or otherwise outside a convenient reading environment.</span><span class="sxs-lookup"><span data-stu-id="db6af-112">*Responding in multitasking scenarios:* **Text to Speech** enables people to absorb important information quickly and comfortably while driving or otherwise outside a convenient reading environment.</span></span> <span data-ttu-id="db6af-113">Navigation is a common application in this area.</span><span class="sxs-lookup"><span data-stu-id="db6af-113">Navigation is a common application in this area.</span></span> 

* <span data-ttu-id="db6af-114">*Enhancing learning with multiple modes:* Different people learn best in different ways.</span><span class="sxs-lookup"><span data-stu-id="db6af-114">*Enhancing learning with multiple modes:* Different people learn best in different ways.</span></span> <span data-ttu-id="db6af-115">Online learning experts have shown that providing voice and text together can help make information easier to learn and retain.</span><span class="sxs-lookup"><span data-stu-id="db6af-115">Online learning experts have shown that providing voice and text together can help make information easier to learn and retain.</span></span>

* <span data-ttu-id="db6af-116">*Delivering intuitive bots or assistants:* The ability to talk can be an integral part of an intelligent chat bot or a virtual assistant.</span><span class="sxs-lookup"><span data-stu-id="db6af-116">*Delivering intuitive bots or assistants:* The ability to talk can be an integral part of an intelligent chat bot or a virtual assistant.</span></span> <span data-ttu-id="db6af-117">More and more companies are developing chat bots to provide engaging customer service experiences for their customers.</span><span class="sxs-lookup"><span data-stu-id="db6af-117">More and more companies are developing chat bots to provide engaging customer service experiences for their customers.</span></span> <span data-ttu-id="db6af-118">Voice adds another dimension by allowing the bot's responses to be received aurally (for example, by phone).</span><span class="sxs-lookup"><span data-stu-id="db6af-118">Voice adds another dimension by allowing the bot's responses to be received aurally (for example, by phone).</span></span>

## <a name="voice-support"></a><span data-ttu-id="db6af-119">Voice support</span><span class="sxs-lookup"><span data-stu-id="db6af-119">Voice support</span></span>

<span data-ttu-id="db6af-120">The Microsoft **Text-to-Speech** service offers more than 75 voices in more than 45 languages and locales.</span><span class="sxs-lookup"><span data-stu-id="db6af-120">The Microsoft **Text-to-Speech** service offers more than 75 voices in more than 45 languages and locales.</span></span> <span data-ttu-id="db6af-121">To use these standard "voice fonts", you only need to specify the voice name with a few other parameters when you call the service's REST API.</span><span class="sxs-lookup"><span data-stu-id="db6af-121">To use these standard "voice fonts", you only need to specify the voice name with a few other parameters when you call the service's REST API.</span></span> <span data-ttu-id="db6af-122">For the details of the voices supported, see [Supported languages](https://docs.microsoft.com/azure/cognitive-services/speech-service/supported-languages#text-to-speech).</span><span class="sxs-lookup"><span data-stu-id="db6af-122">For the details of the voices supported, see [Supported languages](https://docs.microsoft.com/azure/cognitive-services/speech-service/supported-languages#text-to-speech).</span></span> 

<span data-ttu-id="db6af-123">If you want a unique voice for your application, you can create [custom voice fonts](how-to-customize-voice-font.md) from your own speech samples.</span><span class="sxs-lookup"><span data-stu-id="db6af-123">If you want a unique voice for your application, you can create [custom voice fonts](how-to-customize-voice-font.md) from your own speech samples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db6af-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="db6af-124">Next steps</span></span>

* [<span data-ttu-id="db6af-125">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="db6af-125">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="db6af-126">See how to synthesize speech via the REST API</span><span class="sxs-lookup"><span data-stu-id="db6af-126">See how to synthesize speech via the REST API</span></span>](how-to-text-to-speech.md)
