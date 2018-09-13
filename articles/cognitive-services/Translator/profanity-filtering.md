---
title: Profanity filtering with the Microsoft Translator Text API | Microsoft Docs
description: Use profanity filtering in the Microsoft Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: abccd61e790b53045a439a25e60b2756d3a6e2d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871737"
---
# <a name="how-to-add-profanity-filtering-with-the-microsoft-translator-text-api"></a><span data-ttu-id="d28fe-103">How to add profanity filtering with the Microsoft Translator Text API</span><span class="sxs-lookup"><span data-stu-id="d28fe-103">How to add profanity filtering with the Microsoft Translator Text API</span></span>

<span data-ttu-id="d28fe-104">Normally the Translator service retains profanity that is present in the source in the translation.</span><span class="sxs-lookup"><span data-stu-id="d28fe-104">Normally the Translator service retains profanity that is present in the source in the translation.</span></span> <span data-ttu-id="d28fe-105">The degree of profanity and the context that makes words profane differ between cultures.</span><span class="sxs-lookup"><span data-stu-id="d28fe-105">The degree of profanity and the context that makes words profane differ between cultures.</span></span> <span data-ttu-id="d28fe-106">As a result the degree of profanity in the target language may be amplified or reduced.</span><span class="sxs-lookup"><span data-stu-id="d28fe-106">As a result the degree of profanity in the target language may be amplified or reduced.</span></span>

<span data-ttu-id="d28fe-107">If you want to avoid seeing profanity in the translation (regardless of the presence of profanity in the source text), you can use the profanity filtering option in the Translate() method.</span><span class="sxs-lookup"><span data-stu-id="d28fe-107">If you want to avoid seeing profanity in the translation (regardless of the presence of profanity in the source text), you can use the profanity filtering option in the Translate() method.</span></span> <span data-ttu-id="d28fe-108">The option allows you to choose whether you want to see profanity deleted or marked with appropriate tags, or no action taken.</span><span class="sxs-lookup"><span data-stu-id="d28fe-108">The option allows you to choose whether you want to see profanity deleted or marked with appropriate tags, or no action taken.</span></span>

<span data-ttu-id="d28fe-109">The Translate() method takes an “options” parameter, which contains the new element “ProfanityAction”.</span><span class="sxs-lookup"><span data-stu-id="d28fe-109">The Translate() method takes an “options” parameter, which contains the new element “ProfanityAction”.</span></span> <span data-ttu-id="d28fe-110">The accepted values of ProfanityAction are “NoAction”, “Marked” and “Deleted”.</span><span class="sxs-lookup"><span data-stu-id="d28fe-110">The accepted values of ProfanityAction are “NoAction”, “Marked” and “Deleted”.</span></span>

## <a name="accepted-values-of-profanityaction-and-examples"></a><span data-ttu-id="d28fe-111">Accepted values of ProfanityAction and examples</span><span class="sxs-lookup"><span data-stu-id="d28fe-111">Accepted values of ProfanityAction and examples</span></span>
|<span data-ttu-id="d28fe-112">ProfanityAction value</span><span class="sxs-lookup"><span data-stu-id="d28fe-112">ProfanityAction value</span></span> | <span data-ttu-id="d28fe-113">Action</span><span class="sxs-lookup"><span data-stu-id="d28fe-113">Action</span></span> | <span data-ttu-id="d28fe-114">Example: Source - Japanese</span><span class="sxs-lookup"><span data-stu-id="d28fe-114">Example: Source - Japanese</span></span> | <span data-ttu-id="d28fe-115">Example: Target - English</span><span class="sxs-lookup"><span data-stu-id="d28fe-115">Example: Target - English</span></span>|
| :---|:---|:---|:---|
| <span data-ttu-id="d28fe-116">NoAction</span><span class="sxs-lookup"><span data-stu-id="d28fe-116">NoAction</span></span> | <span data-ttu-id="d28fe-117">Default.</span><span class="sxs-lookup"><span data-stu-id="d28fe-117">Default.</span></span> <span data-ttu-id="d28fe-118">Same as not setting the option.</span><span class="sxs-lookup"><span data-stu-id="d28fe-118">Same as not setting the option.</span></span> <span data-ttu-id="d28fe-119">Profanity passes from source to target.</span><span class="sxs-lookup"><span data-stu-id="d28fe-119">Profanity passes from source to target.</span></span> | <span data-ttu-id="d28fe-120">彼は変態です。</span><span class="sxs-lookup"><span data-stu-id="d28fe-120">彼は変態です。</span></span> | <span data-ttu-id="d28fe-121">He is a jerk.</span><span class="sxs-lookup"><span data-stu-id="d28fe-121">He is a jerk.</span></span> |
| <span data-ttu-id="d28fe-122">Marked</span><span class="sxs-lookup"><span data-stu-id="d28fe-122">Marked</span></span> | <span data-ttu-id="d28fe-123">Profane words are surrounded by XML tags \<profanity> …</span><span class="sxs-lookup"><span data-stu-id="d28fe-123">Profane words are surrounded by XML tags \<profanity> …</span></span> <span data-ttu-id="d28fe-124">\</profanity>.</span><span class="sxs-lookup"><span data-stu-id="d28fe-124">\</profanity>.</span></span> | <span data-ttu-id="d28fe-125">彼は変態です。</span><span class="sxs-lookup"><span data-stu-id="d28fe-125">彼は変態です。</span></span> | <span data-ttu-id="d28fe-126">He is a \<profanity>jerk\</profanity>.</span><span class="sxs-lookup"><span data-stu-id="d28fe-126">He is a \<profanity>jerk\</profanity>.</span></span> |
| <span data-ttu-id="d28fe-127">Deleted</span><span class="sxs-lookup"><span data-stu-id="d28fe-127">Deleted</span></span> | <span data-ttu-id="d28fe-128">Profane words are removed from the output without replacement.</span><span class="sxs-lookup"><span data-stu-id="d28fe-128">Profane words are removed from the output without replacement.</span></span> | <span data-ttu-id="d28fe-129">彼は。</span><span class="sxs-lookup"><span data-stu-id="d28fe-129">彼は。</span></span> | <span data-ttu-id="d28fe-130">He is a.</span><span class="sxs-lookup"><span data-stu-id="d28fe-130">He is a.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d28fe-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="d28fe-131">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d28fe-132">Apply profanity filtering with your Translator API call</span><span class="sxs-lookup"><span data-stu-id="d28fe-132">Apply profanity filtering with your Translator API call</span></span>](reference/v3-0-translate.md)

