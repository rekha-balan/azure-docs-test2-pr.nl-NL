---
title: Microsoft Translator Text API overview - Azure Cognitive Services  | Microsoft Docs
description: Integrate the Microsoft Translator Text API into your applications, websites, tools, and other solutions to provide multi-language user experiences.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.service: cognitive-services
ms.component: translator-text
ms.topic: overview
ms.date: 05/10/2018
ms.author: nolachar
ms.openlocfilehash: bfbb316ac41045add7f424b5d478581aa226fc19
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821332"
---
# <a name="what-is-microsoft-translator"></a><span data-ttu-id="8c7f6-103">What is Microsoft Translator?</span><span class="sxs-lookup"><span data-stu-id="8c7f6-103">What is Microsoft Translator?</span></span>

<span data-ttu-id="8c7f6-104">The Microsoft Translator Text API can be seamlessly integrated into your applications, websites, tools, or other solutions to provide multi-language user experiences in [more than 60 languages](languages.md).</span><span class="sxs-lookup"><span data-stu-id="8c7f6-104">The Microsoft Translator Text API can be seamlessly integrated into your applications, websites, tools, or other solutions to provide multi-language user experiences in [more than 60 languages](languages.md).</span></span> <span data-ttu-id="8c7f6-105">It can be used on any hardware platform and with any operating system to perform text to text language translation.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-105">It can be used on any hardware platform and with any operating system to perform text to text language translation.</span></span>

<span data-ttu-id="8c7f6-106">Microsoft Translator Text API is part of the Microsoft [Cognitive Services API](https://docs.microsoft.com/azure/#pivot=products&panel=ai) collection of machine learning and AI algorithms in the cloud, readily consumable in your development projects.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-106">Microsoft Translator Text API is part of the Microsoft [Cognitive Services API](https://docs.microsoft.com/azure/#pivot=products&panel=ai) collection of machine learning and AI algorithms in the cloud, readily consumable in your development projects.</span></span>

## <a name="about-microsoft-translator"></a><span data-ttu-id="8c7f6-107">About Microsoft Translator</span><span class="sxs-lookup"><span data-stu-id="8c7f6-107">About Microsoft Translator</span></span>

<span data-ttu-id="8c7f6-108">Microsoft Translator is a cloud-based machine translation service.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-108">Microsoft Translator is a cloud-based machine translation service.</span></span> <span data-ttu-id="8c7f6-109">At the core of this service are the Translator Text API and [Translator Speech API](https://docs.microsoft.com/azure/cognitive-services/speech-service/speech-translation) which power various Microsoft products and services and are used by thousands of businesses worldwide in their applications and workflows, allowing their content to reach a worldwide audience.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-109">At the core of this service are the Translator Text API and [Translator Speech API](https://docs.microsoft.com/azure/cognitive-services/speech-service/speech-translation) which power various Microsoft products and services and are used by thousands of businesses worldwide in their applications and workflows, allowing their content to reach a worldwide audience.</span></span>

<span data-ttu-id="8c7f6-110">Speech translation is also available through the [Cognitive Services Speech preview](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/), which combines existing Translator Speech API, Bing Speech API, and Custom Speech Service (preview) into a unified and fully customizable service.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-110">Speech translation is also available through the [Cognitive Services Speech preview](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/), which combines existing Translator Speech API, Bing Speech API, and Custom Speech Service (preview) into a unified and fully customizable service.</span></span>  

<span data-ttu-id="8c7f6-111">Learn more about the [Microsoft Translator service](https://www.microsoft.com/en-us/translator/home.aspx)</span><span class="sxs-lookup"><span data-stu-id="8c7f6-111">Learn more about the [Microsoft Translator service](https://www.microsoft.com/en-us/translator/home.aspx)</span></span>

## <a name="language-customization"></a><span data-ttu-id="8c7f6-112">Language customization</span><span class="sxs-lookup"><span data-stu-id="8c7f6-112">Language customization</span></span>

<span data-ttu-id="8c7f6-113">An extension of the core Microsoft Translator service, Custom Translator can be used in conjunction with the Translator Text API to help you customize the neural translation system and improve the translation for your specific terminology and style.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-113">An extension of the core Microsoft Translator service, Custom Translator can be used in conjunction with the Translator Text API to help you customize the neural translation system and improve the translation for your specific terminology and style.</span></span>

<span data-ttu-id="8c7f6-114">With Custom Translator, you can build translation systems that handle the terminology used in your own business or industry.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-114">With Custom Translator, you can build translation systems that handle the terminology used in your own business or industry.</span></span> <span data-ttu-id="8c7f6-115">Your customized translation system will then easily integrate into your existing applications, workflows, and websites, across multiple types of devices, through the regular Microsoft Translator Text API, by using the category parameter.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-115">Your customized translation system will then easily integrate into your existing applications, workflows, and websites, across multiple types of devices, through the regular Microsoft Translator Text API, by using the category parameter.</span></span> 

<span data-ttu-id="8c7f6-116">Learn more about [language customization](customization.md)</span><span class="sxs-lookup"><span data-stu-id="8c7f6-116">Learn more about [language customization](customization.md)</span></span>

## <a name="microsoft-translator-neural-machine-translation"></a><span data-ttu-id="8c7f6-117">Microsoft Translator Neural Machine Translation</span><span class="sxs-lookup"><span data-stu-id="8c7f6-117">Microsoft Translator Neural Machine Translation</span></span>

<span data-ttu-id="8c7f6-118">Neural Machine Translation (NMT) is the new standard for high-quality AI-powered machine translations.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-118">Neural Machine Translation (NMT) is the new standard for high-quality AI-powered machine translations.</span></span> <span data-ttu-id="8c7f6-119">It replaces the legacy Statistical Machine Translation (SMT) technology that reached a quality plateau in the mid-2010s.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-119">It replaces the legacy Statistical Machine Translation (SMT) technology that reached a quality plateau in the mid-2010s.</span></span>

<span data-ttu-id="8c7f6-120">NMT provides better translations than SMT not only from a raw translation quality scoring standpoint but also because they will sound more fluent and human.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-120">NMT provides better translations than SMT not only from a raw translation quality scoring standpoint but also because they will sound more fluent and human.</span></span> <span data-ttu-id="8c7f6-121">The key reason for this fluidity is that NMT uses the full context of a sentence to translate words.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-121">The key reason for this fluidity is that NMT uses the full context of a sentence to translate words.</span></span> <span data-ttu-id="8c7f6-122">SMT only took the immediate context of a few words before and after each word.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-122">SMT only took the immediate context of a few words before and after each word.</span></span>

<span data-ttu-id="8c7f6-123">NMT models are at the core of the API and are not visible to end users.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-123">NMT models are at the core of the API and are not visible to end users.</span></span> <span data-ttu-id="8c7f6-124">The only noticeable difference is improved translation quality, especially for languages such as Chinese, Japanese, and Arabic.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-124">The only noticeable difference is improved translation quality, especially for languages such as Chinese, Japanese, and Arabic.</span></span> 

<span data-ttu-id="8c7f6-125">Learn more about [how NMT works](https://www.microsoft.com/en-us/translator/mt.aspx#nnt)</span><span class="sxs-lookup"><span data-stu-id="8c7f6-125">Learn more about [how NMT works](https://www.microsoft.com/en-us/translator/mt.aspx#nnt)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c7f6-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c7f6-126">Next steps</span></span>

- <span data-ttu-id="8c7f6-127">Read about [pricing details](https://azure.microsoft.com/pricing/details/cognitive-services/translator-text-api/).</span><span class="sxs-lookup"><span data-stu-id="8c7f6-127">Read about [pricing details](https://azure.microsoft.com/pricing/details/cognitive-services/translator-text-api/).</span></span>

- <span data-ttu-id="8c7f6-128">[Sign up](translator-text-how-to-signup.md) for an access key.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-128">[Sign up](translator-text-how-to-signup.md) for an access key.</span></span>

- <span data-ttu-id="8c7f6-129">[Quickstart](quickstarts/csharp.md) is a walkthrough of the REST API calls written in C#.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-129">[Quickstart](quickstarts/csharp.md) is a walkthrough of the REST API calls written in C#.</span></span> <span data-ttu-id="8c7f6-130">Learn how to translate text from one language to another with minimal code.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-130">Learn how to translate text from one language to another with minimal code.</span></span>

- <span data-ttu-id="8c7f6-131">[API reference documentation](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference) provides the technical documentation for the APIs.</span><span class="sxs-lookup"><span data-stu-id="8c7f6-131">[API reference documentation](https://docs.microsoft.com/azure/cognitive-services/Translator/reference/v3-0-reference) provides the technical documentation for the APIs.</span></span>

## <a name="see-also"></a><span data-ttu-id="8c7f6-132">See also</span><span class="sxs-lookup"><span data-stu-id="8c7f6-132">See also</span></span>

- [<span data-ttu-id="8c7f6-133">Cognitive Services Documentation page</span><span class="sxs-lookup"><span data-stu-id="8c7f6-133">Cognitive Services Documentation page</span></span>](https://docs.microsoft.com/azure/#pivot=products&panel=ai)
- [<span data-ttu-id="8c7f6-134">Cognitive Services Product page</span><span class="sxs-lookup"><span data-stu-id="8c7f6-134">Cognitive Services Product page</span></span>](https://azure.microsoft.com/services/cognitive-services/)
- [<span data-ttu-id="8c7f6-135">Solution and pricing information</span><span class="sxs-lookup"><span data-stu-id="8c7f6-135">Solution and pricing information</span></span>](https://www.microsoft.com/en-us/translator/default.aspx)
