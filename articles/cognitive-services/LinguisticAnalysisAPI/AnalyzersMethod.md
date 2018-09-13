---
title: The Analyzers method in the Lingistic Analysis API  | Microsoft Docs
description: The analyzers REST API provides a list of analyzers that are currently supported by the service in Microsoft Cognitive Services.
services: cognitive-services
author: RichardSunMS
manager: wkwok
ms.service: cognitive-services
ms.technology: linguistic-analysis-api
ms.topic: article
ms.date: 06/30/2016
ms.author: lesun
ms.openlocfilehash: da74b5fbbb9726805def9cedd297fc1fa5944d75
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540964"
---
# <a name="analyzers-method"></a><span data-ttu-id="f7dbb-103">Analyzers Method</span><span class="sxs-lookup"><span data-stu-id="f7dbb-103">Analyzers Method</span></span>

<span data-ttu-id="f7dbb-104">The **analyzers** REST API provides a list of analyzers currently supported by the service.</span><span class="sxs-lookup"><span data-stu-id="f7dbb-104">The **analyzers** REST API provides a list of analyzers currently supported by the service.</span></span>
<span data-ttu-id="f7dbb-105">The response includes their [names](Analyzer-Names.md) and the languages supported by each (such as "en" for English).</span><span class="sxs-lookup"><span data-stu-id="f7dbb-105">The response includes their [names](Analyzer-Names.md) and the languages supported by each (such as "en" for English).</span></span>

## <a name="request-parameters"></a><span data-ttu-id="f7dbb-106">Request parameters</span><span class="sxs-lookup"><span data-stu-id="f7dbb-106">Request parameters</span></span>
<span data-ttu-id="f7dbb-107">None</span><span class="sxs-lookup"><span data-stu-id="f7dbb-107">None</span></span>

<br>

## <a name="response-parameters"></a><span data-ttu-id="f7dbb-108">Response parameters</span><span class="sxs-lookup"><span data-stu-id="f7dbb-108">Response parameters</span></span>
<span data-ttu-id="f7dbb-109">Name</span><span class="sxs-lookup"><span data-stu-id="f7dbb-109">Name</span></span> | <span data-ttu-id="f7dbb-110">Type</span><span class="sxs-lookup"><span data-stu-id="f7dbb-110">Type</span></span> | <span data-ttu-id="f7dbb-111">Description</span><span class="sxs-lookup"><span data-stu-id="f7dbb-111">Description</span></span>
-----|------|--------------
<span data-ttu-id="f7dbb-112">languages</span><span class="sxs-lookup"><span data-stu-id="f7dbb-112">languages</span></span> | <span data-ttu-id="f7dbb-113">list of strings</span><span class="sxs-lookup"><span data-stu-id="f7dbb-113">list of strings</span></span> | <span data-ttu-id="f7dbb-114">list of two letter ISO language codes for which this analyzer can be used.</span><span class="sxs-lookup"><span data-stu-id="f7dbb-114">list of two letter ISO language codes for which this analyzer can be used.</span></span>
<span data-ttu-id="f7dbb-115">id</span><span class="sxs-lookup"><span data-stu-id="f7dbb-115">id</span></span>   | <span data-ttu-id="f7dbb-116">string</span><span class="sxs-lookup"><span data-stu-id="f7dbb-116">string</span></span> | <span data-ttu-id="f7dbb-117">unique ID for this analyzer</span><span class="sxs-lookup"><span data-stu-id="f7dbb-117">unique ID for this analyzer</span></span>
<span data-ttu-id="f7dbb-118">kind</span><span class="sxs-lookup"><span data-stu-id="f7dbb-118">kind</span></span> | <span data-ttu-id="f7dbb-119">string</span><span class="sxs-lookup"><span data-stu-id="f7dbb-119">string</span></span> | <span data-ttu-id="f7dbb-120">the broad type of analyzer here</span><span class="sxs-lookup"><span data-stu-id="f7dbb-120">the broad type of analyzer here</span></span>
<span data-ttu-id="f7dbb-121">specification</span><span class="sxs-lookup"><span data-stu-id="f7dbb-121">specification</span></span> | <span data-ttu-id="f7dbb-122">string</span><span class="sxs-lookup"><span data-stu-id="f7dbb-122">string</span></span> | <span data-ttu-id="f7dbb-123">the name of the specification used for this analyzer</span><span class="sxs-lookup"><span data-stu-id="f7dbb-123">the name of the specification used for this analyzer</span></span>
<span data-ttu-id="f7dbb-124">implementation</span><span class="sxs-lookup"><span data-stu-id="f7dbb-124">implementation</span></span> | <span data-ttu-id="f7dbb-125">string</span><span class="sxs-lookup"><span data-stu-id="f7dbb-125">string</span></span> | <span data-ttu-id="f7dbb-126">description of the model and/or algorithm behind this analyzer</span><span class="sxs-lookup"><span data-stu-id="f7dbb-126">description of the model and/or algorithm behind this analyzer</span></span>

<br>
## <a name="example"></a><span data-ttu-id="f7dbb-127">Example</span><span class="sxs-lookup"><span data-stu-id="f7dbb-127">Example</span></span>
<span data-ttu-id="f7dbb-128">GET /analyzers</span><span class="sxs-lookup"><span data-stu-id="f7dbb-128">GET /analyzers</span></span>

<span data-ttu-id="f7dbb-129">Response: JSON</span><span class="sxs-lookup"><span data-stu-id="f7dbb-129">Response: JSON</span></span>
```json
[
    {
        "id": "22A6B758-420F-4745-8A3C-46835A67C0D2",
        "languages": ["en"],
        "kind": "Constituency_Tree",  
        "specification": "PennTreebank3", 
        "implementation": "SplitMerge"
    }, 
    {
        "id" : "4FA79AF1-F22C-408D-98BB-B7D7AEEF7F04",
        "languages": ["en"],
        "kind": "POS_Tags", 
        "specification": "PennTreebank3", 
        "implementation": "cmm"
    },
    {
        "id" : "08EA174B-BFDB-4E64-987E-602F85DA7F72",
        "languages": ["en"],
        "kind": "Tokens", 
        "specification":"PennTreebank3", 
        "implementation": "regexes"
    } 
]
```
