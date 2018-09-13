---
title: Manage security alerts in Azure Security Center | Microsoft Docs
description: This document helps you to use Azure Security Center capabilities to manage and respond to security alerts.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: ''
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: yurid
ms.openlocfilehash: 6b2636446cff87e722d0e09253916ee4953663f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671838"
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="9f88d-103">Managing and responding to security alerts in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9f88d-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="9f88d-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="9f88d-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="9f88d-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="9f88d-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="9f88d-106">A free 60-day trial is available.</span><span class="sxs-lookup"><span data-stu-id="9f88d-106">A free 60-day trial is available.</span></span> <span data-ttu-id="9f88d-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="9f88d-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="9f88d-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span><span class="sxs-lookup"><span data-stu-id="9f88d-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="9f88d-109">What are security alerts?</span><span class="sxs-lookup"><span data-stu-id="9f88d-109">What are security alerts?</span></span>
<span data-ttu-id="9f88d-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span><span class="sxs-lookup"><span data-stu-id="9f88d-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="9f88d-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span><span class="sxs-lookup"><span data-stu-id="9f88d-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="9f88d-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="9f88d-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="9f88d-113">Managing security alerts</span><span class="sxs-lookup"><span data-stu-id="9f88d-113">Managing security alerts</span></span>
<span data-ttu-id="9f88d-114">You can review your current alerts by looking at the **Security alerts** tile.</span><span class="sxs-lookup"><span data-stu-id="9f88d-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="9f88d-115">Open Azure Portal and follow the steps below to see more details about each alert:</span><span class="sxs-lookup"><span data-stu-id="9f88d-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="9f88d-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span><span class="sxs-lookup"><span data-stu-id="9f88d-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Security alerts tile in Security Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="9f88d-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span><span class="sxs-lookup"><span data-stu-id="9f88d-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![The Security alerts blade in Security Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="9f88d-120">In the bottom part of this blade are the details for each alert.</span><span class="sxs-lookup"><span data-stu-id="9f88d-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="9f88d-121">To sort, click the column that you want to sort by.</span><span class="sxs-lookup"><span data-stu-id="9f88d-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="9f88d-122">The definition for each column is given below:</span><span class="sxs-lookup"><span data-stu-id="9f88d-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="9f88d-123">**Description**: A brief explanation of the alert.</span><span class="sxs-lookup"><span data-stu-id="9f88d-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="9f88d-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span><span class="sxs-lookup"><span data-stu-id="9f88d-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="9f88d-125">**Detected by**: The service that was responsible for triggering the alert.</span><span class="sxs-lookup"><span data-stu-id="9f88d-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="9f88d-126">**Date**: The date that the event occurred.</span><span class="sxs-lookup"><span data-stu-id="9f88d-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="9f88d-127">**State**: The current state for that alert.</span><span class="sxs-lookup"><span data-stu-id="9f88d-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="9f88d-128">There are two types of states:</span><span class="sxs-lookup"><span data-stu-id="9f88d-128">There are two types of states:</span></span>
  * <span data-ttu-id="9f88d-129">**Active**: The security alert has been detected.</span><span class="sxs-lookup"><span data-stu-id="9f88d-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="9f88d-130">**Severity**: The severity level, which can be high, medium or low.</span><span class="sxs-lookup"><span data-stu-id="9f88d-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="9f88d-131">Filtering alerts</span><span class="sxs-lookup"><span data-stu-id="9f88d-131">Filtering alerts</span></span>
<span data-ttu-id="9f88d-132">You can filter alerts based on date, state, and severity.</span><span class="sxs-lookup"><span data-stu-id="9f88d-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="9f88d-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span><span class="sxs-lookup"><span data-stu-id="9f88d-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="9f88d-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span><span class="sxs-lookup"><span data-stu-id="9f88d-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="9f88d-135">Click **Filter** on the **Security Alerts** blade.</span><span class="sxs-lookup"><span data-stu-id="9f88d-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="9f88d-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span><span class="sxs-lookup"><span data-stu-id="9f88d-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Filtering alerts in Security Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="9f88d-138">Respond to security alerts</span><span class="sxs-lookup"><span data-stu-id="9f88d-138">Respond to security alerts</span></span>
<span data-ttu-id="9f88d-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span><span class="sxs-lookup"><span data-stu-id="9f88d-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="9f88d-140">Security alerts are grouped by type and date.</span><span class="sxs-lookup"><span data-stu-id="9f88d-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="9f88d-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span><span class="sxs-lookup"><span data-stu-id="9f88d-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Respond to security alerts in Azure Security Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="9f88d-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span><span class="sxs-lookup"><span data-stu-id="9f88d-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="9f88d-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span><span class="sxs-lookup"><span data-stu-id="9f88d-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="9f88d-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span><span class="sxs-lookup"><span data-stu-id="9f88d-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Suggestions for what to do about security alerts in Azure Security Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="9f88d-147">In the **Description** field of this blade you will find more details about this event.</span><span class="sxs-lookup"><span data-stu-id="9f88d-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="9f88d-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span><span class="sxs-lookup"><span data-stu-id="9f88d-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="9f88d-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span><span class="sxs-lookup"><span data-stu-id="9f88d-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="9f88d-150">The remediation suggested by Security Center will vary according to the security alert.</span><span class="sxs-lookup"><span data-stu-id="9f88d-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="9f88d-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span><span class="sxs-lookup"><span data-stu-id="9f88d-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="9f88d-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span><span class="sxs-lookup"><span data-stu-id="9f88d-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="9f88d-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="9f88d-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="9f88d-154">See also</span><span class="sxs-lookup"><span data-stu-id="9f88d-154">See also</span></span>
<span data-ttu-id="9f88d-155">In this document, you learned how to configure security policies in Security Center.</span><span class="sxs-lookup"><span data-stu-id="9f88d-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="9f88d-156">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="9f88d-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="9f88d-157">Handling Security Incident in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9f88d-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="9f88d-158">Azure Security Center Detection Capabilities</span><span class="sxs-lookup"><span data-stu-id="9f88d-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="9f88d-159">Azure Security Center Planning and Operations Guide</span><span class="sxs-lookup"><span data-stu-id="9f88d-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="9f88d-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="9f88d-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9f88d-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="9f88d-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>





