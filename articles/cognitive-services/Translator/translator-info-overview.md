---
title: Overview of Microsoft Translator API in Cognitive Services | Microsoft Docs
description: Integrate Microsoft Translator APIs into your applications, websites, tools, and other solutions to provide multi-language user experiences.
services: cognitive-services
author: chriswendt1
manager: arulm
ms.service: cognitive-services
ms.technology: translator
ms.topic: article
ms.date: 11/21/2016
ms.author: christw
ms.openlocfilehash: 7f1b610dc7184ee72a58eaf49b422b2deb9907d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662511"
---
# <a name="microsoft-translator-api"></a><span data-ttu-id="1658b-103">Microsoft Translator API</span><span class="sxs-lookup"><span data-stu-id="1658b-103">Microsoft Translator API</span></span>
<span data-ttu-id="1658b-104">Microsoft Translator APIs can be seamlessly integrated into your applications, websites, tools, or other solutions to provide multi-language user experiences.</span><span class="sxs-lookup"><span data-stu-id="1658b-104">Microsoft Translator APIs can be seamlessly integrated into your applications, websites, tools, or other solutions to provide multi-language user experiences.</span></span> <span data-ttu-id="1658b-105">Leveraging industry standards, it can be used on any hardware platform and with any operating system to perform language translation and other language-related operations such as speech to speech translation, text language detection or text to speech.</span><span class="sxs-lookup"><span data-stu-id="1658b-105">Leveraging industry standards, it can be used on any hardware platform and with any operating system to perform language translation and other language-related operations such as speech to speech translation, text language detection or text to speech.</span></span>

## <a name="microsoft-translator-deep-neural-network-translation"></a><span data-ttu-id="1658b-106">Microsoft Translator Deep Neural Network translation</span><span class="sxs-lookup"><span data-stu-id="1658b-106">Microsoft Translator Deep Neural Network translation</span></span>
<span data-ttu-id="1658b-107">Microsoft Translator API has been using Statistical Machine Translation (SMT) technology since it started.</span><span class="sxs-lookup"><span data-stu-id="1658b-107">Microsoft Translator API has been using Statistical Machine Translation (SMT) technology since it started.</span></span> <span data-ttu-id="1658b-108">The technology has reached a plateau in terms of performance improvement.</span><span class="sxs-lookup"><span data-stu-id="1658b-108">The technology has reached a plateau in terms of performance improvement.</span></span> <span data-ttu-id="1658b-109">Translation quality is no longer improving with SMT.</span><span class="sxs-lookup"><span data-stu-id="1658b-109">Translation quality is no longer improving with SMT.</span></span>
<span data-ttu-id="1658b-110">A new AI-based translation technology is gaining momentum based on Deep Neural Networks (DNN).</span><span class="sxs-lookup"><span data-stu-id="1658b-110">A new AI-based translation technology is gaining momentum based on Deep Neural Networks (DNN).</span></span>

<span data-ttu-id="1658b-111">DNN enabled translations will first appear for users of the Microsoft Translator Speech API, and will spread from there to eventually include all languages and APIs.</span><span class="sxs-lookup"><span data-stu-id="1658b-111">DNN enabled translations will first appear for users of the Microsoft Translator Speech API, and will spread from there to eventually include all languages and APIs.</span></span>

## <a name="technology"></a><span data-ttu-id="1658b-112">Technology</span><span class="sxs-lookup"><span data-stu-id="1658b-112">Technology</span></span>
<span data-ttu-id="1658b-113">DNN models are at the core of the API and are not visible to end users.</span><span class="sxs-lookup"><span data-stu-id="1658b-113">DNN models are at the core of the API and are not visible to end users.</span></span> <span data-ttu-id="1658b-114">The only noticeable differences will be:</span><span class="sxs-lookup"><span data-stu-id="1658b-114">The only noticeable differences will be:</span></span>
-   <span data-ttu-id="1658b-115">The improved translation quality, especially for languages such as Chinese and Japanese.</span><span class="sxs-lookup"><span data-stu-id="1658b-115">The improved translation quality, especially for languages such as Chinese and Japanese.</span></span> 
-   <span data-ttu-id="1658b-116">The incompatibility with the existing Hub and CTF customization features</span><span class="sxs-lookup"><span data-stu-id="1658b-116">The incompatibility with the existing Hub and CTF customization features</span></span>

## <a name="high-level-product-architecture"></a><span data-ttu-id="1658b-117">High-level product architecture</span><span class="sxs-lookup"><span data-stu-id="1658b-117">High-level product architecture</span></span>

[<span data-ttu-id="1658b-118">How DNN works</span><span class="sxs-lookup"><span data-stu-id="1658b-118">How DNN works</span></span>](http://translator.microsoft.com)

<span data-ttu-id="1658b-119">DNN will provide better translations not only from a raw translation quality scoring standpoint but also because they will sound more fluid, more human, than SMT ones.</span><span class="sxs-lookup"><span data-stu-id="1658b-119">DNN will provide better translations not only from a raw translation quality scoring standpoint but also because they will sound more fluid, more human, than SMT ones.</span></span> <span data-ttu-id="1658b-120">The key reason for this fluidity is that DNN translation uses the full context of a sentence to translate words contrary to SMT that only takes the context of a few words before and after each word.</span><span class="sxs-lookup"><span data-stu-id="1658b-120">The key reason for this fluidity is that DNN translation uses the full context of a sentence to translate words contrary to SMT that only takes the context of a few words before and after each word.</span></span>
<span data-ttu-id="1658b-121">Use cases Although DNN translation can be used for all types of translations the improvements are particularly impressive for languages where translation quality has previously lagged.</span><span class="sxs-lookup"><span data-stu-id="1658b-121">Use cases Although DNN translation can be used for all types of translations the improvements are particularly impressive for languages where translation quality has previously lagged.</span></span> <span data-ttu-id="1658b-122">For instance, Japanese, Chinese and Arabic.</span><span class="sxs-lookup"><span data-stu-id="1658b-122">For instance, Japanese, Chinese and Arabic.</span></span>


<span data-ttu-id="1658b-123">The Microsoft Translator Hub service and API lets you customize translations for words and sentences that are specific to a particular domain of knowledge.</span><span class="sxs-lookup"><span data-stu-id="1658b-123">The Microsoft Translator Hub service and API lets you customize translations for words and sentences that are specific to a particular domain of knowledge.</span></span>

<span data-ttu-id="1658b-124">The Microsoft Translator API also offers the unique ability to improve the accuracy of the delivered translations through the use of the Collaborative Translations Framework (CTF), allowing users to recommend alternative translations to those provided by Translator’s automatic translation engine.</span><span class="sxs-lookup"><span data-stu-id="1658b-124">The Microsoft Translator API also offers the unique ability to improve the accuracy of the delivered translations through the use of the Collaborative Translations Framework (CTF), allowing users to recommend alternative translations to those provided by Translator’s automatic translation engine.</span></span>

<span data-ttu-id="1658b-125">To get started, you will first need to [sign up for a subscription](https://www.microsoft.com/en-us/translator/getstarted.aspx) to the text or speech API.</span><span class="sxs-lookup"><span data-stu-id="1658b-125">To get started, you will first need to [sign up for a subscription](https://www.microsoft.com/en-us/translator/getstarted.aspx) to the text or speech API.</span></span> <span data-ttu-id="1658b-126">Free tiers are available for 2 million characters per month for the text API and 2 hours per month for the speech API.</span><span class="sxs-lookup"><span data-stu-id="1658b-126">Free tiers are available for 2 million characters per month for the text API and 2 hours per month for the speech API.</span></span>

<span data-ttu-id="1658b-127">[Solution and pricing information](https://www.microsoft.com/en-us/translator/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="1658b-127">[Solution and pricing information](https://www.microsoft.com/en-us/translator/default.aspx).</span></span>

