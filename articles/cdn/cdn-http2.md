---
title: HTTP/2 support in Azure CDN | Microsoft Docs
description: Learn about HTTP/2 and CDN support.
services: cdn
documentationcenter: ''
author: lichard
manager: erikre
editor: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: b4751320af82a29fb13dc6012c1b197ebc2b1f9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866749"
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="48c05-103">HTTP/2 Support in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="48c05-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="48c05-104">HTTP/2 is a major revision to HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="48c05-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="48c05-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span><span class="sxs-lookup"><span data-stu-id="48c05-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="48c05-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span><span class="sxs-lookup"><span data-stu-id="48c05-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

### <a name="http2-benefits"></a><span data-ttu-id="48c05-107">HTTP/2 Benefits</span><span class="sxs-lookup"><span data-stu-id="48c05-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="48c05-108">The benefits of HTTP/2 include:</span><span class="sxs-lookup"><span data-stu-id="48c05-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="48c05-109">**Multiplexing and concurrency**</span><span class="sxs-lookup"><span data-stu-id="48c05-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="48c05-110">Using HTTP 1.1, making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span><span class="sxs-lookup"><span data-stu-id="48c05-110">Using HTTP 1.1, making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="48c05-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span><span class="sxs-lookup"><span data-stu-id="48c05-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="48c05-112">**Header compression**</span><span class="sxs-lookup"><span data-stu-id="48c05-112">**Header compression**</span></span>

    <span data-ttu-id="48c05-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span><span class="sxs-lookup"><span data-stu-id="48c05-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="48c05-114">**Stream dependencies**</span><span class="sxs-lookup"><span data-stu-id="48c05-114">**Stream dependencies**</span></span>

    <span data-ttu-id="48c05-115">Stream dependencies allow the client to indicate to the server which resources have priority.</span><span class="sxs-lookup"><span data-stu-id="48c05-115">Stream dependencies allow the client to indicate to the server which resources have priority.</span></span>


## <a name="http2-browser-support"></a><span data-ttu-id="48c05-116">HTTP/2 Browser Support</span><span class="sxs-lookup"><span data-stu-id="48c05-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="48c05-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span><span class="sxs-lookup"><span data-stu-id="48c05-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="48c05-118">Non-supported browsers automatically fallback to HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="48c05-118">Non-supported browsers automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="48c05-119">Browser</span><span class="sxs-lookup"><span data-stu-id="48c05-119">Browser</span></span>|<span data-ttu-id="48c05-120">Minimum Version</span><span class="sxs-lookup"><span data-stu-id="48c05-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="48c05-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="48c05-121">Microsoft Edge</span></span>| <span data-ttu-id="48c05-122">12</span><span class="sxs-lookup"><span data-stu-id="48c05-122">12</span></span>|
|<span data-ttu-id="48c05-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="48c05-123">Google Chrome</span></span>| <span data-ttu-id="48c05-124">43</span><span class="sxs-lookup"><span data-stu-id="48c05-124">43</span></span>|
|<span data-ttu-id="48c05-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="48c05-125">Mozilla Firefox</span></span>| <span data-ttu-id="48c05-126">38</span><span class="sxs-lookup"><span data-stu-id="48c05-126">38</span></span>|
|<span data-ttu-id="48c05-127">Opera</span><span class="sxs-lookup"><span data-stu-id="48c05-127">Opera</span></span>| <span data-ttu-id="48c05-128">32</span><span class="sxs-lookup"><span data-stu-id="48c05-128">32</span></span>|
|<span data-ttu-id="48c05-129">Safari</span><span class="sxs-lookup"><span data-stu-id="48c05-129">Safari</span></span>| <span data-ttu-id="48c05-130">9</span><span class="sxs-lookup"><span data-stu-id="48c05-130">9</span></span>|

## <a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="48c05-131">Enabling HTTP/2 Support in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="48c05-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="48c05-132">Currently, HTTP/2 support is active for all Azure CDN profiles.</span><span class="sxs-lookup"><span data-stu-id="48c05-132">Currently, HTTP/2 support is active for all Azure CDN profiles.</span></span> <span data-ttu-id="48c05-133">No further action is required from customers.</span><span class="sxs-lookup"><span data-stu-id="48c05-133">No further action is required from customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48c05-134">Next Steps</span><span class="sxs-lookup"><span data-stu-id="48c05-134">Next Steps</span></span>

<span data-ttu-id="48c05-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="48c05-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="48c05-136">To learn more about HTTP/2, visit the following resources:</span><span class="sxs-lookup"><span data-stu-id="48c05-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="48c05-137">HTTP/2 specification homepage</span><span class="sxs-lookup"><span data-stu-id="48c05-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="48c05-138">Official HTTP/2 FAQ</span><span class="sxs-lookup"><span data-stu-id="48c05-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="48c05-139">Akamai HTTP/2 information</span><span class="sxs-lookup"><span data-stu-id="48c05-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="48c05-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="48c05-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>