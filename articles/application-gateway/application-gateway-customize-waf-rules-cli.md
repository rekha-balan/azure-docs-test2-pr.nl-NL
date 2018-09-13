---
title: Customize web application firewall rules in Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs
description: This article provides information on how to customize web application firewall rules in Application Gateway with the Azure CLI 2.0.
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: ''
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: victorh
ms.openlocfilehash: b0bd79bb7ce584a9abaffbb6c30d6fbfe64f87c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868185"
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="0f9f5-103">Customize web application firewall rules through the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0f9f5-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="0f9f5-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span><span class="sxs-lookup"><span data-stu-id="0f9f5-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="0f9f5-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span><span class="sxs-lookup"><span data-stu-id="0f9f5-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="0f9f5-109">Some rules can cause false positives and block real traffic.</span><span class="sxs-lookup"><span data-stu-id="0f9f5-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="0f9f5-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span><span class="sxs-lookup"><span data-stu-id="0f9f5-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="0f9f5-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0f9f5-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="0f9f5-112">View rule groups and rules</span><span class="sxs-lookup"><span data-stu-id="0f9f5-112">View rule groups and rules</span></span>

<span data-ttu-id="0f9f5-113">The following code examples show how to view rules and rule groups that are configurable.</span><span class="sxs-lookup"><span data-stu-id="0f9f5-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="0f9f5-114">View rule groups</span><span class="sxs-lookup"><span data-stu-id="0f9f5-114">View rule groups</span></span>

<span data-ttu-id="0f9f5-115">The following example shows how to view the rule groups:</span><span class="sxs-lookup"><span data-stu-id="0f9f5-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="0f9f5-116">The following output is a truncated response from the preceding example:</span><span class="sxs-lookup"><span data-stu-id="0f9f5-116">The following output is a truncated response from the preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="0f9f5-117">View rules in a rule group</span><span class="sxs-lookup"><span data-stu-id="0f9f5-117">View rules in a rule group</span></span>

<span data-ttu-id="0f9f5-118">The following example shows how to view rules in a specified rule group:</span><span class="sxs-lookup"><span data-stu-id="0f9f5-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="0f9f5-119">The following output is a truncated response from the preceding example:</span><span class="sxs-lookup"><span data-stu-id="0f9f5-119">The following output is a truncated response from the preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="0f9f5-120">Disable rules</span><span class="sxs-lookup"><span data-stu-id="0f9f5-120">Disable rules</span></span>

<span data-ttu-id="0f9f5-121">The following example disables rules `910018` and `910017` on an application gateway:</span><span class="sxs-lookup"><span data-stu-id="0f9f5-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="0f9f5-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f9f5-122">Next steps</span></span>

<span data-ttu-id="0f9f5-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span><span class="sxs-lookup"><span data-stu-id="0f9f5-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="0f9f5-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="0f9f5-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
