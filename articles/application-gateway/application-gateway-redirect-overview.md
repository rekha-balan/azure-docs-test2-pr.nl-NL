---
title: Redirect overview for Azure Application Gateway | Microsoft Docs
description: Learn about the redirect capability in Azure Application Gateway
services: application-gateway
documentationcenter: na
author: amsriva
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: e6352873ea055965b433fbf3e6e46162890e5fec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868531"
---
# <a name="application-gateway-redirect-overview"></a><span data-ttu-id="00897-103">Application Gateway redirect overview</span><span class="sxs-lookup"><span data-stu-id="00897-103">Application Gateway redirect overview</span></span>

<span data-ttu-id="00897-104">A common scenario for many web applications is to support automatic HTTP to HTTPS redirection to ensure all communication between application and its users occurs over an encrypted path.</span><span class="sxs-lookup"><span data-stu-id="00897-104">A common scenario for many web applications is to support automatic HTTP to HTTPS redirection to ensure all communication between application and its users occurs over an encrypted path.</span></span> <span data-ttu-id="00897-105">In the past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is to redirect requests it receives on HTTP to HTTPS.</span><span class="sxs-lookup"><span data-stu-id="00897-105">In the past, customers have used techniques such as creating a dedicated backend pool whose sole purpose is to redirect requests it receives on HTTP to HTTPS.</span></span>  <span data-ttu-id="00897-106">Application gateway now supports ability to redirect traffic on the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="00897-106">Application gateway now supports ability to redirect traffic on the Application Gateway.</span></span> <span data-ttu-id="00897-107">This simplifies application configuration, optimizes the resource usage, and supports new redirection scenarios including global and path-based redirection.</span><span class="sxs-lookup"><span data-stu-id="00897-107">This simplifies application configuration, optimizes the resource usage, and supports new redirection scenarios including global and path-based redirection.</span></span> <span data-ttu-id="00897-108">Application Gateway redirection support is not limited to HTTP -> HTTPS redirection alone.</span><span class="sxs-lookup"><span data-stu-id="00897-108">Application Gateway redirection support is not limited to HTTP -> HTTPS redirection alone.</span></span> <span data-ttu-id="00897-109">This is a generic redirection mechanism, which allows for redirection of traffic received at one listener to another listener on Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="00897-109">This is a generic redirection mechanism, which allows for redirection of traffic received at one listener to another listener on Application Gateway.</span></span> <span data-ttu-id="00897-110">It also supports redirection to an external site as well.</span><span class="sxs-lookup"><span data-stu-id="00897-110">It also supports redirection to an external site as well.</span></span> <span data-ttu-id="00897-111">Application Gateway redirection support offers the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="00897-111">Application Gateway redirection support offers the following capabilities:</span></span>

1. <span data-ttu-id="00897-112">Global redirection from one listener to another listener on the Gateway.</span><span class="sxs-lookup"><span data-stu-id="00897-112">Global redirection from one listener to another listener on the Gateway.</span></span> <span data-ttu-id="00897-113">This enables HTTP to HTTPS redirection on a site.</span><span class="sxs-lookup"><span data-stu-id="00897-113">This enables HTTP to HTTPS redirection on a site.</span></span>
2. <span data-ttu-id="00897-114">Path-based redirection.</span><span class="sxs-lookup"><span data-stu-id="00897-114">Path-based redirection.</span></span> <span data-ttu-id="00897-115">This type of redirection enables HTTP to HTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/\*.</span><span class="sxs-lookup"><span data-stu-id="00897-115">This type of redirection enables HTTP to HTTPS redirection only on a specific site area, for example a shopping cart area denoted by /cart/\*.</span></span>
3. <span data-ttu-id="00897-116">Redirect to external site.</span><span class="sxs-lookup"><span data-stu-id="00897-116">Redirect to external site.</span></span>

![redirect](./media/application-gateway-redirect-overview/redirect.png)

<span data-ttu-id="00897-118">With this change, customers would need to create a new redirect configuration object, which specifies the target listener or external site to which redirection is desired.</span><span class="sxs-lookup"><span data-stu-id="00897-118">With this change, customers would need to create a new redirect configuration object, which specifies the target listener or external site to which redirection is desired.</span></span> <span data-ttu-id="00897-119">The configuration element also supports options to enable appending the URI path and query string to the redirected URL.</span><span class="sxs-lookup"><span data-stu-id="00897-119">The configuration element also supports options to enable appending the URI path and query string to the redirected URL.</span></span> <span data-ttu-id="00897-120">Customers could also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span><span class="sxs-lookup"><span data-stu-id="00897-120">Customers could also choose whether redirection is a temporary (HTTP status code 302) or a permanent redirect (HTTP status code 301).</span></span> <span data-ttu-id="00897-121">Once created this redirect configuration is attached to the source listener via a new rule.</span><span class="sxs-lookup"><span data-stu-id="00897-121">Once created this redirect configuration is attached to the source listener via a new rule.</span></span> <span data-ttu-id="00897-122">When using a basic rule, the redirect configuration is associated with a source listener and is a global redirect.</span><span class="sxs-lookup"><span data-stu-id="00897-122">When using a basic rule, the redirect configuration is associated with a source listener and is a global redirect.</span></span> <span data-ttu-id="00897-123">When a path-based rule is used, the redirect configuration is defined on the URL path map and hence only applies to the specific path area of a site.</span><span class="sxs-lookup"><span data-stu-id="00897-123">When a path-based rule is used, the redirect configuration is defined on the URL path map and hence only applies to the specific path area of a site.</span></span>

### <a name="next-steps"></a><span data-ttu-id="00897-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="00897-124">Next steps</span></span>

[<span data-ttu-id="00897-125">Configure URL redirection on an application gateway</span><span class="sxs-lookup"><span data-stu-id="00897-125">Configure URL redirection on an application gateway</span></span>](application-gateway-configure-redirect-powershell.md)
