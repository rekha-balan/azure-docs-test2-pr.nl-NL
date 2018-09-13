---
title: Azure Media Services v3 release notes | Microsoft Docs
description: To stay up-to-date with the most recent developments, this article provides you with the latest updates on Azure Media Services v3.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: fc6c5ba6cd97c261dd44eade33bf21e8d1b74bf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870380"
---
# <a name="azure-media-services-v3-preview-release-notes"></a><span data-ttu-id="e96c2-103">Azure Media Services v3 (preview) release notes</span><span class="sxs-lookup"><span data-stu-id="e96c2-103">Azure Media Services v3 (preview) release notes</span></span> 

<span data-ttu-id="e96c2-104">To stay up-to-date with the most recent developments, this article provides you with information about:</span><span class="sxs-lookup"><span data-stu-id="e96c2-104">To stay up-to-date with the most recent developments, this article provides you with information about:</span></span>

* <span data-ttu-id="e96c2-105">The latest releases</span><span class="sxs-lookup"><span data-stu-id="e96c2-105">The latest releases</span></span>
* <span data-ttu-id="e96c2-106">Known issues</span><span class="sxs-lookup"><span data-stu-id="e96c2-106">Known issues</span></span>
* <span data-ttu-id="e96c2-107">Bug fixes</span><span class="sxs-lookup"><span data-stu-id="e96c2-107">Bug fixes</span></span>
* <span data-ttu-id="e96c2-108">Deprecated functionality</span><span class="sxs-lookup"><span data-stu-id="e96c2-108">Deprecated functionality</span></span>
* <span data-ttu-id="e96c2-109">Plans for changes</span><span class="sxs-lookup"><span data-stu-id="e96c2-109">Plans for changes</span></span>

## <a name="may-07-2018"></a><span data-ttu-id="e96c2-110">May 07, 2018</span><span class="sxs-lookup"><span data-stu-id="e96c2-110">May 07, 2018</span></span>

### <a name="net-sdk"></a><span data-ttu-id="e96c2-111">.Net SDK</span><span class="sxs-lookup"><span data-stu-id="e96c2-111">.Net SDK</span></span>

<span data-ttu-id="e96c2-112">The following features are present in the .Net SDK:</span><span class="sxs-lookup"><span data-stu-id="e96c2-112">The following features are present in the .Net SDK:</span></span>

1. <span data-ttu-id="e96c2-113">**Transforms** and **Jobs** to encode or analyze media content.</span><span class="sxs-lookup"><span data-stu-id="e96c2-113">**Transforms** and **Jobs** to encode or analyze media content.</span></span> <span data-ttu-id="e96c2-114">For examples, see [Stream files](stream-files-tutorial-with-api.md) and [Analyze](analyze-videos-tutorial-with-api.md).</span><span class="sxs-lookup"><span data-stu-id="e96c2-114">For examples, see [Stream files](stream-files-tutorial-with-api.md) and [Analyze](analyze-videos-tutorial-with-api.md).</span></span>
2. <span data-ttu-id="e96c2-115">**StreamingLocators** for publishing and streaming content to end-user devices</span><span class="sxs-lookup"><span data-stu-id="e96c2-115">**StreamingLocators** for publishing and streaming content to end-user devices</span></span>
3. <span data-ttu-id="e96c2-116">**StreamingPolicies** and **ContentKeyPolicies** to configure key delivery and content protection (DRM) when delivering content.</span><span class="sxs-lookup"><span data-stu-id="e96c2-116">**StreamingPolicies** and **ContentKeyPolicies** to configure key delivery and content protection (DRM) when delivering content.</span></span>
4. <span data-ttu-id="e96c2-117">**LiveEvents** and **LiveOutputs** to configure the ingest and archiving of live streaming content.</span><span class="sxs-lookup"><span data-stu-id="e96c2-117">**LiveEvents** and **LiveOutputs** to configure the ingest and archiving of live streaming content.</span></span>
5. <span data-ttu-id="e96c2-118">**Assets** to store and publish media content in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e96c2-118">**Assets** to store and publish media content in Azure Storage.</span></span> 
6. <span data-ttu-id="e96c2-119">**StreamingEndpoints** to configure and scale dynamic packaging, encryption, and streaming for both live and on-demand media content.</span><span class="sxs-lookup"><span data-stu-id="e96c2-119">**StreamingEndpoints** to configure and scale dynamic packaging, encryption, and streaming for both live and on-demand media content.</span></span>

### <a name="known-issues"></a><span data-ttu-id="e96c2-120">Known issues</span><span class="sxs-lookup"><span data-stu-id="e96c2-120">Known issues</span></span>

<span data-ttu-id="e96c2-121">Known issue:</span><span class="sxs-lookup"><span data-stu-id="e96c2-121">Known issue:</span></span>

<span data-ttu-id="e96c2-122">When submitting a Job with a HTTPS URL (JobInputHttp) pointing to the source content, make sure that the HTTP server supports the ‘HEAD’ request.</span><span class="sxs-lookup"><span data-stu-id="e96c2-122">When submitting a Job with a HTTPS URL (JobInputHttp) pointing to the source content, make sure that the HTTP server supports the ‘HEAD’ request.</span></span> <span data-ttu-id="e96c2-123">Otherwise, the Job will be rejected.</span><span class="sxs-lookup"><span data-stu-id="e96c2-123">Otherwise, the Job will be rejected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e96c2-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="e96c2-124">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e96c2-125">Overview</span><span class="sxs-lookup"><span data-stu-id="e96c2-125">Overview</span></span>](media-services-overview.md)
