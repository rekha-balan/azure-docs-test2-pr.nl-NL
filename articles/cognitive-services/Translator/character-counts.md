---
title: Microsoft Translator Text API Character Counts | Microsoft Docs
description: How the Microsoft Translator Text API counts characters.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/20/2017
ms.author: v-jansko
ms.openlocfilehash: 9348fc9c57288fdb738cda67d5de90c99a3044af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967604"
---
# <a name="how-the-microsoft-translator-text-api-counts-characters"></a><span data-ttu-id="3aa87-103">How the Microsoft Translator Text API counts characters</span><span class="sxs-lookup"><span data-stu-id="3aa87-103">How the Microsoft Translator Text API counts characters</span></span>

<span data-ttu-id="3aa87-104">Microsoft Translator counts every character of the input.</span><span class="sxs-lookup"><span data-stu-id="3aa87-104">Microsoft Translator counts every character of the input.</span></span> <span data-ttu-id="3aa87-105">Characters in the Unicode sense, not bytes.</span><span class="sxs-lookup"><span data-stu-id="3aa87-105">Characters in the Unicode sense, not bytes.</span></span> <span data-ttu-id="3aa87-106">Unicode surrogates count as two characters.</span><span class="sxs-lookup"><span data-stu-id="3aa87-106">Unicode surrogates count as two characters.</span></span> <span data-ttu-id="3aa87-107">White space and markup count as characters.</span><span class="sxs-lookup"><span data-stu-id="3aa87-107">White space and markup count as characters.</span></span> <span data-ttu-id="3aa87-108">The length of the response does not matter.</span><span class="sxs-lookup"><span data-stu-id="3aa87-108">The length of the response does not matter.</span></span>

<span data-ttu-id="3aa87-109">Calls to the Detect and BreakSentence methods are not counted in the character consumption.</span><span class="sxs-lookup"><span data-stu-id="3aa87-109">Calls to the Detect and BreakSentence methods are not counted in the character consumption.</span></span> <span data-ttu-id="3aa87-110">However, we do expect that the calls to the Detect and BreakSentence methods are in a reasonable proportion to the use of other functions that are counted.</span><span class="sxs-lookup"><span data-stu-id="3aa87-110">However, we do expect that the calls to the Detect and BreakSentence methods are in a reasonable proportion to the use of other functions that are counted.</span></span> <span data-ttu-id="3aa87-111">Microsoft reserves the right to start counting Detect and BreakSentence.</span><span class="sxs-lookup"><span data-stu-id="3aa87-111">Microsoft reserves the right to start counting Detect and BreakSentence.</span></span> 

<span data-ttu-id="3aa87-112">More information about character counts is in the [Microsoft Translator FAQ](https://www.microsoft.com/en-us/translator/faq.aspx).</span><span class="sxs-lookup"><span data-stu-id="3aa87-112">More information about character counts is in the [Microsoft Translator FAQ](https://www.microsoft.com/en-us/translator/faq.aspx).</span></span>
