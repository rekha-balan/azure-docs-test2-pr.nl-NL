---
title: Customize web application firewall rules in Azure Application Gateway - PowerShell | Microsoft Docs
description: This article provides information on how to customize web application firewall rules in Application Gateway with PowerShell.
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
ms.openlocfilehash: f992fbf9ab223e18c24c27ce0577b1af2017281a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871641"
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="0fd10-103">Customize web application firewall rules through PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fd10-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="0fd10-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span><span class="sxs-lookup"><span data-stu-id="0fd10-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="0fd10-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span><span class="sxs-lookup"><span data-stu-id="0fd10-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="0fd10-109">Some rules can cause false positives and block real traffic.</span><span class="sxs-lookup"><span data-stu-id="0fd10-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="0fd10-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span><span class="sxs-lookup"><span data-stu-id="0fd10-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="0fd10-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="0fd10-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="0fd10-112">View rule groups and rules</span><span class="sxs-lookup"><span data-stu-id="0fd10-112">View rule groups and rules</span></span>

<span data-ttu-id="0fd10-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span><span class="sxs-lookup"><span data-stu-id="0fd10-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="0fd10-114">View rule groups</span><span class="sxs-lookup"><span data-stu-id="0fd10-114">View rule groups</span></span>

<span data-ttu-id="0fd10-115">The following example shows how to view rule groups:</span><span class="sxs-lookup"><span data-stu-id="0fd10-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="0fd10-116">The following output is a truncated response from the preceding example:</span><span class="sxs-lookup"><span data-stu-id="0fd10-116">The following output is a truncated response from the preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="0fd10-117">Disable rules</span><span class="sxs-lookup"><span data-stu-id="0fd10-117">Disable rules</span></span>

<span data-ttu-id="0fd10-118">The following example disables rules `910018` and `910017` on an application gateway:</span><span class="sxs-lookup"><span data-stu-id="0fd10-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```powershell
$disabledrules=New-AzureRmApplicationGatewayFirewallDisabledRuleGroupConfig -RuleGroupName REQUEST-910-IP-REPUTATION -Rules 910018,910017
Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -ApplicationGateway $gw -Enabled $true -FirewallMode Detection -RuleSetVersion 3.0 -RuleSetType OWASP -DisabledRuleGroups $disabledrules
```

## <a name="next-steps"></a><span data-ttu-id="0fd10-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fd10-119">Next steps</span></span>

<span data-ttu-id="0fd10-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span><span class="sxs-lookup"><span data-stu-id="0fd10-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="0fd10-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="0fd10-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
