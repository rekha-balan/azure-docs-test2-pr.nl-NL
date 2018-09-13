---
title: The Speech Synthesis Markup Language
description: Using the Speech Synthesis Markup language to control pronunciation and prosody in text-to-speech.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 04/28/2018
ms.author: v-jerkin
ms.openlocfilehash: ed085bcd92c4ef550ee596a3aefea3af9bfef104
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869634"
---
# <a name="speech-synthesis-markup-language"></a><span data-ttu-id="a3cf9-103">Speech Synthesis Markup Language</span><span class="sxs-lookup"><span data-stu-id="a3cf9-103">Speech Synthesis Markup Language</span></span>

<span data-ttu-id="a3cf9-104">The Speech Synthesis Markup Language (SSML) is an XML-based markup language that provides a way to control the pronunciation and *prosody* of text-to-speech.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-104">The Speech Synthesis Markup Language (SSML) is an XML-based markup language that provides a way to control the pronunciation and *prosody* of text-to-speech.</span></span> <span data-ttu-id="a3cf9-105">(Prosody refers to the rhythm and pitch of speech—its music, if you will).</span><span class="sxs-lookup"><span data-stu-id="a3cf9-105">(Prosody refers to the rhythm and pitch of speech—its music, if you will).</span></span> <span data-ttu-id="a3cf9-106">You can specify words phonetically, provide hints for interpreting numbers, insert pauses, control pitch, volume, and rate, and more.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-106">You can specify words phonetically, provide hints for interpreting numbers, insert pauses, control pitch, volume, and rate, and more.</span></span>

<span data-ttu-id="a3cf9-107">For more information, see [Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/2009/REC-speech-synthesis-20090303/) at the W3C.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-107">For more information, see [Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/2009/REC-speech-synthesis-20090303/) at the W3C.</span></span>

<span data-ttu-id="a3cf9-108">The following examples show how to use SSML for common speech synthesis needs.</span><span class="sxs-lookup"><span data-stu-id="a3cf9-108">The following examples show how to use SSML for common speech synthesis needs.</span></span>

## <a name="add-a-break"></a><span data-ttu-id="a3cf9-109">Add a break</span><span class="sxs-lookup"><span data-stu-id="a3cf9-109">Add a break</span></span>
```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, Jessa24kRUS)'>
    Welcome to Microsoft Cognitive Services <break time="100ms" /> Text-to-Speech API.
</voice> </speak>
```

## <a name="change-speaking-rate"></a><span data-ttu-id="a3cf9-110">Change speaking rate</span><span class="sxs-lookup"><span data-stu-id="a3cf9-110">Change speaking rate</span></span>
```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, Guy24kRUS)'>
<prosody rate="+30.00%">
    Welcome to Microsoft Cognitive Services Text-to-Speech API.
</prosody></voice> </speak>
```

## <a name="pronunciation"></a><span data-ttu-id="a3cf9-111">Pronunciation</span><span class="sxs-lookup"><span data-stu-id="a3cf9-111">Pronunciation</span></span>
```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, Jessa24kRUS)'>
    <phoneme alphabet="ipa" ph="t&#x259;mei&#x325;&#x27E;ou&#x325;"> tomato </phoneme>
</voice> </speak>
```

## <a name="change-volume"></a><span data-ttu-id="a3cf9-112">Change volume</span><span class="sxs-lookup"><span data-stu-id="a3cf9-112">Change volume</span></span>
```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, JessaRUS)'>
<prosody volume="+20.00%">
    Welcome to Microsoft Cognitive Services Text-to-Speech API.
</prosody></voice> </speak>
```

## <a name="change-pitch"></a><span data-ttu-id="a3cf9-113">Change pitch</span><span class="sxs-lookup"><span data-stu-id="a3cf9-113">Change pitch</span></span>
```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
    <voice  name='Microsoft Server Speech Text to Speech Voice (en-US, Guy24kRUS)'>
    Welcome to <prosody pitch="high">Microsoft Cognitive Services Text-to-Speech API.</prosody>
</voice> </speak>
```

## <a name="change-pitch-contour"></a><span data-ttu-id="a3cf9-114">Change pitch contour</span><span class="sxs-lookup"><span data-stu-id="a3cf9-114">Change pitch contour</span></span>
```xml
<speak version='1.0' xmlns="http://www.w3.org/2001/10/synthesis" xml:lang='en-US'>
<voice  name='Microsoft Server Speech Text to Speech Voice (en-US, JessaRUS)'>
<prosody contour="(80%,+20%) (90%,+30%)" >
    Good morning.
</prosody></voice> </speak>
```

## <a name="next-steps"></a><span data-ttu-id="a3cf9-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3cf9-115">Next steps</span></span>

* [<span data-ttu-id="a3cf9-116">Get your Speech trial subscription</span><span class="sxs-lookup"><span data-stu-id="a3cf9-116">Get your Speech trial subscription</span></span>](https://azure.microsoft.com/try/cognitive-services/)
* [<span data-ttu-id="a3cf9-117">See how to recognize speech in C#</span><span class="sxs-lookup"><span data-stu-id="a3cf9-117">See how to recognize speech in C#</span></span>](quickstart-csharp-dotnet-windows.md)
