---
title: Word alignment information with the Microsoft Translator Text API | Microsoft Docs
description: Receive word alignment information from the Microsoft Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 61e7c2e03af4d1bcca5829ebf64a9eeb07a4368f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857676"
---
# <a name="how-to-receive-word-alignment-information"></a><span data-ttu-id="9d900-103">How to receive word alignment information</span><span class="sxs-lookup"><span data-stu-id="9d900-103">How to receive word alignment information</span></span>

## <a name="receiving-word-alignment-information"></a><span data-ttu-id="9d900-104">Receiving word alignment information</span><span class="sxs-lookup"><span data-stu-id="9d900-104">Receiving word alignment information</span></span>
<span data-ttu-id="9d900-105">To receive alignment information, use the Translate method and include the optional includeAlignment parameter.</span><span class="sxs-lookup"><span data-stu-id="9d900-105">To receive alignment information, use the Translate method and include the optional includeAlignment parameter.</span></span>

## <a name="alignment-information-format"></a><span data-ttu-id="9d900-106">Alignment information format</span><span class="sxs-lookup"><span data-stu-id="9d900-106">Alignment information format</span></span>
<span data-ttu-id="9d900-107">Alignment is returned as a string value of the following format for every word of the source.</span><span class="sxs-lookup"><span data-stu-id="9d900-107">Alignment is returned as a string value of the following format for every word of the source.</span></span> <span data-ttu-id="9d900-108">The information for each word is separated by a space, including for non-space-separated languages (scripts) like Chinese:</span><span class="sxs-lookup"><span data-stu-id="9d900-108">The information for each word is separated by a space, including for non-space-separated languages (scripts) like Chinese:</span></span>

<span data-ttu-id="9d900-109">[[SourceTextStartIndex]:[SourceTextEndIndex]–[TgtTextStartIndex]:[TgtTextEndIndex]] \*</span><span class="sxs-lookup"><span data-stu-id="9d900-109">[[SourceTextStartIndex]:[SourceTextEndIndex]–[TgtTextStartIndex]:[TgtTextEndIndex]] \*</span></span>

<span data-ttu-id="9d900-110">Example alignment string: "0:0-7:10 1:2-11:20 3:4-0:3 3:4-4:6 5:5-21:21".</span><span class="sxs-lookup"><span data-stu-id="9d900-110">Example alignment string: "0:0-7:10 1:2-11:20 3:4-0:3 3:4-4:6 5:5-21:21".</span></span>

<span data-ttu-id="9d900-111">In other words, the colon separates start and end index, the dash separates the languages, and space separates the words.</span><span class="sxs-lookup"><span data-stu-id="9d900-111">In other words, the colon separates start and end index, the dash separates the languages, and space separates the words.</span></span> <span data-ttu-id="9d900-112">One word may align with zero, one, or multiple words in the other language, and the aligned words may be non-contiguous.</span><span class="sxs-lookup"><span data-stu-id="9d900-112">One word may align with zero, one, or multiple words in the other language, and the aligned words may be non-contiguous.</span></span> <span data-ttu-id="9d900-113">When no alignment information is available, the Alignment element will be empty.</span><span class="sxs-lookup"><span data-stu-id="9d900-113">When no alignment information is available, the Alignment element will be empty.</span></span> <span data-ttu-id="9d900-114">The method returns no error in that case.</span><span class="sxs-lookup"><span data-stu-id="9d900-114">The method returns no error in that case.</span></span>

## <a name="restrictions"></a><span data-ttu-id="9d900-115">Restrictions</span><span class="sxs-lookup"><span data-stu-id="9d900-115">Restrictions</span></span>
<span data-ttu-id="9d900-116">Alignment is only returned for a subset of the language pairs at this point:</span><span class="sxs-lookup"><span data-stu-id="9d900-116">Alignment is only returned for a subset of the language pairs at this point:</span></span>
* <span data-ttu-id="9d900-117">from English to any other language;</span><span class="sxs-lookup"><span data-stu-id="9d900-117">from English to any other language;</span></span>
* <span data-ttu-id="9d900-118">from any other language to English except for Chinese Simplified, Chinese Traditional, and Latvian to English</span><span class="sxs-lookup"><span data-stu-id="9d900-118">from any other language to English except for Chinese Simplified, Chinese Traditional, and Latvian to English</span></span>
* <span data-ttu-id="9d900-119">from Japanese to Korean or from Korean to Japanese You will not receive alignment information if the sentence is a canned translation.</span><span class="sxs-lookup"><span data-stu-id="9d900-119">from Japanese to Korean or from Korean to Japanese You will not receive alignment information if the sentence is a canned translation.</span></span> <span data-ttu-id="9d900-120">Example of a canned translation is "This is a test", "I love you", and other high frequency sentences.</span><span class="sxs-lookup"><span data-stu-id="9d900-120">Example of a canned translation is "This is a test", "I love you", and other high frequency sentences.</span></span>

## <a name="example"></a><span data-ttu-id="9d900-121">Example</span><span class="sxs-lookup"><span data-stu-id="9d900-121">Example</span></span>

<span data-ttu-id="9d900-122">Example JSON</span><span class="sxs-lookup"><span data-stu-id="9d900-122">Example JSON</span></span>

```json
[
  {
    "translations": [
      {
        "text": "Kann ich morgen Ihr Auto fahren?",
        "to": "de",
        "alignment": {
          "proj": "0:2-0:3 4:4-5:7 6:10-25:30 12:15-16:18 17:19-20:23 21:28-9:14 29:29-31:31"
        }
      }
    ]
  }
]
```
