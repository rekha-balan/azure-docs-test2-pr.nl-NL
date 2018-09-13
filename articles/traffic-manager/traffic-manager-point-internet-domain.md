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
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a>Point a company Internet domain to an Azure Traffic Manager domain

When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile. To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile. You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.

For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:

    www.contoso.com IN CNAME contoso.trafficmanager.net

All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.

> [!IMPORTANT]
> You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain. DNS protocol standards do not allow CNAME records for second-level domain names.

## <a name="next-steps"></a>Next steps

* [Traffic Manager routing methods](traffic-manager-routing-methods.md)
* [Traffic Manager - Disable, enable or delete a profile](disable-enable-or-delete-a-profile.md)
* [Traffic Manager - Disable or enable an endpoint](disable-or-enable-an-endpoint.md)
