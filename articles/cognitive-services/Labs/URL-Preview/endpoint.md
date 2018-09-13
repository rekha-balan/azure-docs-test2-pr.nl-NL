---
title: Project URL Preview endpoint - Microsoft Cognitive Services | Microsoft Docs
description: Summary of the URL Preview endpoint.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.technology: project-url-preview
ms.topic: article
ms.date: 03/29/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: ddd53aa49db01d7a6db397eb285d0854edc59388
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967231"
---
# <a name="project-url-preview-endpoint"></a><span data-ttu-id="2e705-103">Project URL Preview endpoint</span><span class="sxs-lookup"><span data-stu-id="2e705-103">Project URL Preview endpoint</span></span>

<span data-ttu-id="2e705-104">The URL Preview API includes one endpoint.</span><span class="sxs-lookup"><span data-stu-id="2e705-104">The URL Preview API includes one endpoint.</span></span>

## <a name="endpoint"></a><span data-ttu-id="2e705-105">Endpoint</span><span class="sxs-lookup"><span data-stu-id="2e705-105">Endpoint</span></span>
<span data-ttu-id="2e705-106">To get a URL Preview, send a request to the following endpoint.</span><span class="sxs-lookup"><span data-stu-id="2e705-106">To get a URL Preview, send a request to the following endpoint.</span></span> <span data-ttu-id="2e705-107">Use the headers and URL parameters for other specifications.</span><span class="sxs-lookup"><span data-stu-id="2e705-107">Use the headers and URL parameters for other specifications.</span></span>

<span data-ttu-id="2e705-108">GET:</span><span class="sxs-lookup"><span data-stu-id="2e705-108">GET:</span></span>
````
https://api.labs.cognitive.microsoft.com/urlpreview/v7.0/search?q=https://swiftkey.com

````

### <a name="query-parameters"></a><span data-ttu-id="2e705-109">Query parameters</span><span class="sxs-lookup"><span data-stu-id="2e705-109">Query parameters</span></span>
|<span data-ttu-id="2e705-110">Name</span><span class="sxs-lookup"><span data-stu-id="2e705-110">Name</span></span>|<span data-ttu-id="2e705-111">Value</span><span class="sxs-lookup"><span data-stu-id="2e705-111">Value</span></span>|<span data-ttu-id="2e705-112">Type</span><span class="sxs-lookup"><span data-stu-id="2e705-112">Type</span></span>|<span data-ttu-id="2e705-113">Required</span><span class="sxs-lookup"><span data-stu-id="2e705-113">Required</span></span>|  
|----------|-----------|----------|--------------|  
|<span data-ttu-id="2e705-114">q</span><span class="sxs-lookup"><span data-stu-id="2e705-114">q</span></span>|<span data-ttu-id="2e705-115">URL to preview</span><span class="sxs-lookup"><span data-stu-id="2e705-115">URL to preview</span></span>|<span data-ttu-id="2e705-116">String</span><span class="sxs-lookup"><span data-stu-id="2e705-116">String</span></span> |<span data-ttu-id="2e705-117">Yes</span><span class="sxs-lookup"><span data-stu-id="2e705-117">Yes</span></span>|
|<span data-ttu-id="2e705-118">safeSearch</span><span class="sxs-lookup"><span data-stu-id="2e705-118">safeSearch</span></span>|<span data-ttu-id="2e705-119">Illegal adult content, or pirated content, is blocked with error code 400, and the *isFamilyFriendly* flag is not returned.</span><span class="sxs-lookup"><span data-stu-id="2e705-119">Illegal adult content, or pirated content, is blocked with error code 400, and the *isFamilyFriendly* flag is not returned.</span></span> <p><span data-ttu-id="2e705-120">For legal adult content, below is the behavior.</span><span class="sxs-lookup"><span data-stu-id="2e705-120">For legal adult content, below is the behavior.</span></span> <span data-ttu-id="2e705-121">Status code returns 200, and the *isFamilyFriendly* flag is set to false.</span><span class="sxs-lookup"><span data-stu-id="2e705-121">Status code returns 200, and the *isFamilyFriendly* flag is set to false.</span></span><ul><li><span data-ttu-id="2e705-122">safeSearch=strict: Title, description, URL and image will not be returned.</span><span class="sxs-lookup"><span data-stu-id="2e705-122">safeSearch=strict: Title, description, URL and image will not be returned.</span></span></li><li><span data-ttu-id="2e705-123">safeSearch=moderate; Get title, URL and description but not the descriptive image.</span><span class="sxs-lookup"><span data-stu-id="2e705-123">safeSearch=moderate; Get title, URL and description but not the descriptive image.</span></span></li><li><span data-ttu-id="2e705-124">safeSearch=off; Get all the response objects/elements – title, URL, description, and image.</span><span class="sxs-lookup"><span data-stu-id="2e705-124">safeSearch=off; Get all the response objects/elements – title, URL, description, and image.</span></span></li></ul> |<span data-ttu-id="2e705-125">String</span><span class="sxs-lookup"><span data-stu-id="2e705-125">String</span></span>|<span data-ttu-id="2e705-126">Not required.</span><span class="sxs-lookup"><span data-stu-id="2e705-126">Not required.</span></span> </br> <span data-ttu-id="2e705-127">Defaults to safeSearch=strict.</span><span class="sxs-lookup"><span data-stu-id="2e705-127">Defaults to safeSearch=strict.</span></span>| 

## <a name="response-object"></a><span data-ttu-id="2e705-128">Response object</span><span class="sxs-lookup"><span data-stu-id="2e705-128">Response object</span></span>

<span data-ttu-id="2e705-129">The response includes HTTP headers and WebPage object with attributes as shown in the following example: `name`, `url`, `description`, `isFamilyFriendly`, and `primaryImageOfPage`.</span><span class="sxs-lookup"><span data-stu-id="2e705-129">The response includes HTTP headers and WebPage object with attributes as shown in the following example: `name`, `url`, `description`, `isFamilyFriendly`, and `primaryImageOfPage`.</span></span>

````
BingAPIs-TraceId: 15AFE52A97AA422F960433A94803F6CE
BingAPIs-SessionId: 40587764F42142D3A8BA99F66B2B3BB6
X-MSEdge-ClientID: 0389E3EDED106B5E1424E82FEC436A56
BingAPIs-Market: en-US
X-MSEdge-Ref: Ref A: 15AFE52A97AA422F960433A94803F6CE Ref B: PAOEDGE0418 Ref C: 2018-03-30T16:36:27Z
{
  "_type": "WebPage",
  "name": "SwiftKey - Smart prediction technology for easier mobile ...",
  "url": "https://swiftkey.com/",
   "description": "Discover the best Android and iPhone and iPad apps for faster, easier typing with emoji, colorful themes and more - download SwiftKey Keyboard free today.",
  "isFamilyFriendly": true,
  "primaryImageOfPage": {
    "contentUrl": "https://swiftkey.com/images/og/default.jpg"
  }
}

````

## <a name="next-steps"></a><span data-ttu-id="2e705-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="2e705-130">Next steps</span></span>
- [<span data-ttu-id="2e705-131">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="2e705-131">C# quickstart</span></span>](csharp.md)
- [<span data-ttu-id="2e705-132">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="2e705-132">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="2e705-133">JavaScript quickstart</span><span class="sxs-lookup"><span data-stu-id="2e705-133">JavaScript quickstart</span></span>](javascript.md)
- [<span data-ttu-id="2e705-134">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="2e705-134">Node quickstart</span></span>](node-quickstart.md)
- [<span data-ttu-id="2e705-135">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="2e705-135">Python quickstart</span></span>](python-quickstart.md)
