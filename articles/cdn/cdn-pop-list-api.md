---
title: Retrieve the current Verizon POP list for Azure CDN| Microsoft Docs
description: Learn how to retrieve the current Verizon POP list by using the REST API.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2018
ms.author: v-deasim
ms.custom: ''
ms.openlocfilehash: f796d18a03e14fdf652af72366762e1365523f09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965485"
---
# <a name="retrieve-the-current-verizon-pop-list-for-azure-cdn"></a><span data-ttu-id="1c371-103">Retrieve the current Verizon POP list for Azure CDN</span><span class="sxs-lookup"><span data-stu-id="1c371-103">Retrieve the current Verizon POP list for Azure CDN</span></span>

<span data-ttu-id="1c371-104">You can use the REST API to retrieve the set of IPs for Verizon’s point of presence (POP) servers.</span><span class="sxs-lookup"><span data-stu-id="1c371-104">You can use the REST API to retrieve the set of IPs for Verizon’s point of presence (POP) servers.</span></span> <span data-ttu-id="1c371-105">These POP servers  make requests to origin servers that are associated with Azure Content Delivery Network (CDN) endpoints on a Verizon profile (**Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon**).</span><span class="sxs-lookup"><span data-stu-id="1c371-105">These POP servers  make requests to origin servers that are associated with Azure Content Delivery Network (CDN) endpoints on a Verizon profile (**Azure CDN Standard from Verizon** or **Azure CDN Premium from Verizon**).</span></span> <span data-ttu-id="1c371-106">Note that this set of IPs is different from the IPs that a client would see when making requests to the POPs.</span><span class="sxs-lookup"><span data-stu-id="1c371-106">Note that this set of IPs is different from the IPs that a client would see when making requests to the POPs.</span></span> 

<span data-ttu-id="1c371-107">For the syntax of the REST API operation for retrieving the POP list, see [Edge Nodes - List](https://docs.microsoft.com/rest/api/cdn/edgenodes/list).</span><span class="sxs-lookup"><span data-stu-id="1c371-107">For the syntax of the REST API operation for retrieving the POP list, see [Edge Nodes - List](https://docs.microsoft.com/rest/api/cdn/edgenodes/list).</span></span>

## <a name="typical-use-case"></a><span data-ttu-id="1c371-108">Typical use case</span><span class="sxs-lookup"><span data-stu-id="1c371-108">Typical use case</span></span>

<span data-ttu-id="1c371-109">For security purposes, you can use this IP list to enforce that requests to your origin server are made only from a valid Verizon POP.</span><span class="sxs-lookup"><span data-stu-id="1c371-109">For security purposes, you can use this IP list to enforce that requests to your origin server are made only from a valid Verizon POP.</span></span> <span data-ttu-id="1c371-110">For example, if someone discovered the hostname or IP address for a CDN endpoint's origin server, one could make requests directly to the origin server, therefore bypassing the scaling and security capabilities provided by Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="1c371-110">For example, if someone discovered the hostname or IP address for a CDN endpoint's origin server, one could make requests directly to the origin server, therefore bypassing the scaling and security capabilities provided by Azure CDN.</span></span> <span data-ttu-id="1c371-111">By setting the IPs in the returned list as the only allowed IPs on an origin server, this scenario can be prevented.</span><span class="sxs-lookup"><span data-stu-id="1c371-111">By setting the IPs in the returned list as the only allowed IPs on an origin server, this scenario can be prevented.</span></span> <span data-ttu-id="1c371-112">To ensure they you have the latest POP list, retrieve it at least once a day.</span><span class="sxs-lookup"><span data-stu-id="1c371-112">To ensure they you have the latest POP list, retrieve it at least once a day.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1c371-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c371-113">Next steps</span></span>

<span data-ttu-id="1c371-114">For information about the REST API, see [Azure CDN REST API](https://docs.microsoft.com/en-us/rest/api/cdn/).</span><span class="sxs-lookup"><span data-stu-id="1c371-114">For information about the REST API, see [Azure CDN REST API](https://docs.microsoft.com/en-us/rest/api/cdn/).</span></span>