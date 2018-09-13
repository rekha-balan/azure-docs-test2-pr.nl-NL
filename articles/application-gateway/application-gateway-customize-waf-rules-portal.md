---
title: Customize web application firewall rules in Azure Application Gateway - Azure portal | Microsoft Docs
description: This article provides information on how to customize web application firewall rules in Application Gateway with the Azure portal.
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: ''
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: victorh
ms.openlocfilehash: ae61e3a8308e95c16ccde71de37fb10666ef0df9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776912"
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="dbeb8-103">Customize web application firewall rules through the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dbeb8-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="dbeb8-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="dbeb8-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span><span class="sxs-lookup"><span data-stu-id="dbeb8-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="dbeb8-109">Some rules can cause false positives and block real traffic.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="dbeb8-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="dbeb8-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="dbeb8-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane. 

![Enable WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="dbeb8-114">View rule groups and rules</span><span class="sxs-lookup"><span data-stu-id="dbeb8-114">View rule groups and rules</span></span>

<span data-ttu-id="dbeb8-115">**To view rule groups and rules**</span><span class="sxs-lookup"><span data-stu-id="dbeb8-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="dbeb8-116">Browse to the application gateway, and then select **Web application firewall**.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="dbeb8-117">Select **Advanced rule configuration**.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="dbeb8-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="dbeb8-119">All of the rule's check boxes are selected.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-119">All of the rule's check boxes are selected.</span></span>

![Configure disabled rules][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="dbeb8-121">Search for rules to disable</span><span class="sxs-lookup"><span data-stu-id="dbeb8-121">Search for rules to disable</span></span>

<span data-ttu-id="dbeb8-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="dbeb8-123">The result displays only the rule groups and rules that contain the text you searched for.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Search for rules][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="dbeb8-125">Disable rule groups and rules</span><span class="sxs-lookup"><span data-stu-id="dbeb8-125">Disable rule groups and rules</span></span>

<span data-ttu-id="dbeb8-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="dbeb8-127">**To disable rule groups or specific rules**</span><span class="sxs-lookup"><span data-stu-id="dbeb8-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="dbeb8-128">Search for the rules or rule groups that you want to disable.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="dbeb8-129">Clear the check boxes for the rules that you want to disable.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="dbeb8-130">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-130">Select **Save**.</span></span> 

![Save changes][3]

## <a name="next-steps"></a><span data-ttu-id="dbeb8-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbeb8-132">Next steps</span></span>

<span data-ttu-id="dbeb8-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span><span class="sxs-lookup"><span data-stu-id="dbeb8-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="dbeb8-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="dbeb8-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
