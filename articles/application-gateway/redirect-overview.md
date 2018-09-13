---
title: Redirect overview for Azure Application Gateway
description: Learn about the redirect capability in Azure Application Gateway
services: application-gateway
documentationcenter: na
author: amsriva
manager: jpconnock
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 3/19/2018
ms.author: amsriva
ms.openlocfilehash: 65c631ca9beb5eab5d8fe2b7e71daa0cf3b768fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867496"
---
# <a name="application-gateway-redirect-overview"></a><span data-ttu-id="b6fc1-103">Application Gateway redirect overview</span><span class="sxs-lookup"><span data-stu-id="b6fc1-103">Application Gateway redirect overview</span></span>

<span data-ttu-id="b6fc1-104">A common scenario for many web applications is to support automatic HTTP to HTTPS redirection to ensure all communication between application and its users occurs over an encrypted path.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-104">A common scenario for many web applications is to support automatic HTTP to HTTPS redirection to ensure all communication between application and its users occurs over an encrypted path.</span></span> <span data-ttu-id="b6fc1-105">In the past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is to redirect requests it receives on HTTP to HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-105">In the past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is to redirect requests it receives on HTTP to HTTPS.</span></span>

<span data-ttu-id="b6fc1-106">Application Gateway now supports the ability to redirect traffic on the gateway.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-106">Application Gateway now supports the ability to redirect traffic on the gateway.</span></span> <span data-ttu-id="b6fc1-107">This simplifies application configuration, optimizes the resource usage, and supports new redirection scenarios including global and path-based redirection.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-107">This simplifies application configuration, optimizes the resource usage, and supports new redirection scenarios including global and path-based redirection.</span></span> <span data-ttu-id="b6fc1-108">Application Gateway redirection support is not limited to HTTP -> HTTPS redirection alone.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-108">Application Gateway redirection support is not limited to HTTP -> HTTPS redirection alone.</span></span> <span data-ttu-id="b6fc1-109">It has a generic redirection mechanism, which allows for traffic redirection received at one listener to another listener on Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-109">It has a generic redirection mechanism, which allows for traffic redirection received at one listener to another listener on Application Gateway.</span></span> <span data-ttu-id="b6fc1-110">External site redirection is also supported.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-110">External site redirection is also supported.</span></span>

<span data-ttu-id="b6fc1-111">Application Gateway redirection support offers the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="b6fc1-111">Application Gateway redirection support offers the following capabilities:</span></span>

-  <span data-ttu-id="b6fc1-112">**Global redirection**</span><span class="sxs-lookup"><span data-stu-id="b6fc1-112">**Global redirection**</span></span>

   <span data-ttu-id="b6fc1-113">Redirects from one listener to another listener on the gateway.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-113">Redirects from one listener to another listener on the gateway.</span></span> <span data-ttu-id="b6fc1-114">This enables HTTP to HTTPS redirection on a site.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-114">This enables HTTP to HTTPS redirection on a site.</span></span>
- <span data-ttu-id="b6fc1-115">**Path-based redirection**</span><span class="sxs-lookup"><span data-stu-id="b6fc1-115">**Path-based redirection**</span></span>

   <span data-ttu-id="b6fc1-116">This type of redirection enables HTTP to HTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/\*.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-116">This type of redirection enables HTTP to HTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/\*.</span></span>
- <span data-ttu-id="b6fc1-117">**Redirect to external site**</span><span class="sxs-lookup"><span data-stu-id="b6fc1-117">**Redirect to external site**</span></span>

![redirect](./media/redirect-overview/redirect.png)

<span data-ttu-id="b6fc1-119">With this change, customers need to create a new redirect configuration object, which specifies the target listener or external site to which redirection is desired.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-119">With this change, customers need to create a new redirect configuration object, which specifies the target listener or external site to which redirection is desired.</span></span> <span data-ttu-id="b6fc1-120">The configuration element also supports options to enable appending the URI path and query string to the redirected URL.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-120">The configuration element also supports options to enable appending the URI path and query string to the redirected URL.</span></span> <span data-ttu-id="b6fc1-121">You can also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span><span class="sxs-lookup"><span data-stu-id="b6fc1-121">You can also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span></span> <span data-ttu-id="b6fc1-122">Once created, this redirect configuration is attached to the source listener via a new rule.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-122">Once created, this redirect configuration is attached to the source listener via a new rule.</span></span> <span data-ttu-id="b6fc1-123">When using a basic rule, the redirect configuration is associated with a source listener and is a global redirect.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-123">When using a basic rule, the redirect configuration is associated with a source listener and is a global redirect.</span></span> <span data-ttu-id="b6fc1-124">When a path-based rule is used, the redirect configuration is defined on the URL path map.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-124">When a path-based rule is used, the redirect configuration is defined on the URL path map.</span></span> <span data-ttu-id="b6fc1-125">So it only applies to the specific path area of a site.</span><span class="sxs-lookup"><span data-stu-id="b6fc1-125">So it only applies to the specific path area of a site.</span></span>

### <a name="next-steps"></a><span data-ttu-id="b6fc1-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6fc1-126">Next steps</span></span>

[<span data-ttu-id="b6fc1-127">Configure URL redirection on an application gateway</span><span class="sxs-lookup"><span data-stu-id="b6fc1-127">Configure URL redirection on an application gateway</span></span>](tutorial-url-redirect-powershell.md)
