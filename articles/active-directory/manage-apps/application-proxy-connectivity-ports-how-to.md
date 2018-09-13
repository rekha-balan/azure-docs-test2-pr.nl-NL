---
title: How to open the firewall ports required for an Application Proxy application | Microsoft Docs
description: Find out what ports to open for the Azure AD Application Proxy to work correctly
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/21/2018
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: af43b1dd0a6ccb60ba6911bce8dd540aed5c0db4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867555"
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a>How to open the firewall ports required for an Application Proxy application

To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](application-proxy-enable.md). note that Application Proxy only uses outbound ports.

You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network. More green checkmarks means greater resiliency. 

## <a name="app-proxy-regions"></a>App Proxy regions

We are working on a way to let you know which of these regions needs to be green for you. For now, make sure they all are. Central US is also required regardless of which region you are in.

To make sure the tool gives you the right results, be sure to:

-   Open the tool on a browser from the server where you have installed the Connector.

-   Ensure that any proxies or firewalls applicable to your Connector are also applied to this page. This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**. On this page, you see the field “Use a Proxy Server for your LAN”. Select this box, and put the proxy address into the “Address” field.

## <a name="next-steps"></a>Next steps
[Understand Azure AD Application Proxy connectors](application-proxy-connectors.md)
