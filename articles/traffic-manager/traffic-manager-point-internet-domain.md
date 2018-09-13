---
title: Point a company Internet domain to a Traffic Manager domain name | Microsoft Docs
description: This article will help you point your company domain name to a Traffic Manager domain name.
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: timlt
editor: ''
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 0322b3510cfd4f94031d8c1db8f1cc032b997fa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562720"
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a><span data-ttu-id="f06db-103">Point a company Internet domain to an Azure Traffic Manager domain</span><span class="sxs-lookup"><span data-stu-id="f06db-103">Point a company Internet domain to an Azure Traffic Manager domain</span></span>

<span data-ttu-id="f06db-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span><span class="sxs-lookup"><span data-stu-id="f06db-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="f06db-105">To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="f06db-105">To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="f06db-106">You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="f06db-106">You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.</span></span>

<span data-ttu-id="f06db-107">For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:</span><span class="sxs-lookup"><span data-stu-id="f06db-107">For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="f06db-108">All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="f06db-108">All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f06db-109">You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain.</span><span class="sxs-lookup"><span data-stu-id="f06db-109">You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain.</span></span> <span data-ttu-id="f06db-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span><span class="sxs-lookup"><span data-stu-id="f06db-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f06db-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="f06db-111">Next steps</span></span>

* [<span data-ttu-id="f06db-112">Traffic Manager routing methods</span><span class="sxs-lookup"><span data-stu-id="f06db-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="f06db-113">Traffic Manager - Disable, enable or delete a profile</span><span class="sxs-lookup"><span data-stu-id="f06db-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="f06db-114">Traffic Manager - Disable or enable an endpoint</span><span class="sxs-lookup"><span data-stu-id="f06db-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
