---
title: Customize web application firewall rules in Azure Application Gateway - Portal | Microsoft Docs
description: This page provides information on how to customize web application firewall rules in Application Gateway with the portal.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: ''
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 742ec41f95550c148de69569f5e0fa6d7c7fedc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563777"
---
# <a name="customize-web-application-firewall-rules-through-the-portal"></a>Customize web application firewall rules through the portal

Application Gateway web application firewall provides protection for web applications. These protections are provided by OWASP CRS rulesets. Some rules can cause false positives and block real traffic.  For this reason application gateway provides the capability to customize rulegroups and rules on a web application firewall enabled application gateway. For more information on the specific rule groups and rules, visit [web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md)

>[!NOTE]
> If your application gateway is not using the WAF tier, you are presented the option to upgrade the application gateway to the WAF tier as shown in the following image:

![enable waf][fig1]

## <a name="view-rule-groups-and-rules"></a>View rule groups and rules

Navigate to an application gateway and select **Web application firewall**.  Click **Advanced rule configuration**.  This shows a table on the page of all the rule groups provided with the rule set chosen.

![configure disabled rules][1]

## <a name="search-for-rules-to-disable"></a>Search for rules to disable

The web application firewall settings blade provides the capability to filter the rules by a text search. The result displays only rule groups and rules that contain the text that is being searched for.

![search for rules][2]

## <a name="disable-rule-groups-and-rules"></a>Disable rule groups and rules

When disabling rules you can disable an entire rule group, or specific rules under one or more rule groups.  Once the rules that you want to disable are unchecked, click **Save**.  This saves the changes to the application gateway.

![save changes][3]

## <a name="next-steps"></a>Next steps

Once you configure your disabled rules, learn how to view your WAF logs by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging)

[fig1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-customize-waf-rules-portal/1.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-customize-waf-rules-portal/figure3.png



