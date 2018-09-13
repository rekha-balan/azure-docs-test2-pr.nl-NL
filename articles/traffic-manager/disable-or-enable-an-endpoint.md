---
title: Disable or Enable a Traffic Manager endpoint | Microsoft Docs
description: This article will help disable or enable your Traffic Manager profile endpoints.
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 9b2264ce-be06-43b2-a00b-5c724e5d71fd
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: kumud
ms.openlocfilehash: b09ef7842d628c68439fbb9215c97429b4956f71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551284"
---
<!-- repub for nofollow -->

# <a name="disable-or-enable-a-traffic-manager-endpoint"></a>Disable or Enable a Traffic Manager Endpoint
You can also disable individual endpoints that are part of a Traffic Manager profile. Endpoints include both cloud services and websites. Disabling an endpoint leaves it as part of the profile, but the profile acts as if the endpoint is not included in it. This action is very useful for temporarily removing an endpoint that is in maintenance mode or being redeployed. Once the endpoint is up and running again, it can be enabled

> [!NOTE]
> **Disabling an endpoint has nothing to do with its deployment state in Azure. A healthy endpoint will remain up and able to receive traffic even when disabled in Traffic Manager. Additionally, disabling an endpoint in one profile does not affect its status in another profile.**
> 
> 

## <a name="to-disable-an-endpoint"></a>To disable an endpoint
1. On the Traffic Manager pane in the Azure classic portal, locate the Traffic Manager profile that contains the endpoint settings that you want to modify, and then click the arrow to the right of the profile name. This will open the settings page for the profile.
2. At the top of the page, click **Endpoints** to view the endpoints that are included in your configuration.
3. Click the endpoint that you want to disable, and then click **Disable** at the bottom of the page.
4. Traffic will stop flowing to the endpoint based on the DNS Time-to-Live (TTL) configured for the Traffic Manager domain name. You can change the TTL from the Configuration page of the Traffic Manager profile.

## <a name="to-enable-an-endpoint"></a>To enable an endpoint
1. On the Traffic Manager pane in the Azure classic portal, locate the Traffic Manager profile that contains the endpoint settings that you want to modify, and then click the arrow to the right of the profile name. This will open the settings page for the profile.
2. At the top of the page, click **Endpoints** to view the endpoints that are included in your configuration.
3. Click the endpoint that you want to enable, and then click **Enable** at the bottom of the page.
4. Traffic will start flowing to the service again as dictated by the profile.

## <a name="next-steps"></a>Next Steps
[Traffic Manager - Disable, enable or delete a profile](disable-enable-or-delete-a-profile.md)

[Troubleshooting Traffic Manager degraded state](traffic-manager-troubleshooting-degraded.md)

[Traffic Manager performance considerations](traffic-manager-performance-considerations.md)

