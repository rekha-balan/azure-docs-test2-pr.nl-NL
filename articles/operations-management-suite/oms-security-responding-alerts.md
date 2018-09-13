---
title: Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution | Microsoft Docs
description: This document helps you to use the threat intelligence option available in OMS Security and Audit to monitor and respond to security alerts.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: b5c04a21f40f43038059631cdc2b0f91393cfbef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552538"
---
# <a name="monitoring-and-responding-to-security-alerts-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="60d71-103">Monitoring and responding to security alerts in Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="60d71-103">Monitoring and responding to security alerts in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="60d71-104">This document helps you use the threat intelligence option available in OMS Security and Audit to monitor and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="60d71-104">This document helps you use the threat intelligence option available in OMS Security and Audit to monitor and respond to security alerts.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="60d71-105">What is OMS?</span><span class="sxs-lookup"><span data-stu-id="60d71-105">What is OMS?</span></span>
<span data-ttu-id="60d71-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span><span class="sxs-lookup"><span data-stu-id="60d71-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="60d71-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span><span class="sxs-lookup"><span data-stu-id="60d71-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="threat-intelligence"></a><span data-ttu-id="60d71-108">Threat intelligence</span><span class="sxs-lookup"><span data-stu-id="60d71-108">Threat intelligence</span></span>
<span data-ttu-id="60d71-109">In an enterprise environment where users have broad access to the network and use a variety of devices to connect to corporate data, it is imperative that you can actively monitor your resources and quickly respond to security incidents.</span><span class="sxs-lookup"><span data-stu-id="60d71-109">In an enterprise environment where users have broad access to the network and use a variety of devices to connect to corporate data, it is imperative that you can actively monitor your resources and quickly respond to security incidents.</span></span> <span data-ttu-id="60d71-110">This is particular important from the security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span><span class="sxs-lookup"><span data-stu-id="60d71-110">This is particular important from the security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span></span> 

<span data-ttu-id="60d71-111">By using the **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against the environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span><span class="sxs-lookup"><span data-stu-id="60d71-111">By using the **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against the environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span></span> <span data-ttu-id="60d71-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer to the command and control.</span><span class="sxs-lookup"><span data-stu-id="60d71-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer to the command and control.</span></span> <span data-ttu-id="60d71-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span><span class="sxs-lookup"><span data-stu-id="60d71-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span></span> 

<span data-ttu-id="60d71-114">In order to build this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60d71-114">In order to build this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span></span> <span data-ttu-id="60d71-115">OMS Security and Audit will leverage this data to identify potential threats against your environment.</span><span class="sxs-lookup"><span data-stu-id="60d71-115">OMS Security and Audit will leverage this data to identify potential threats against your environment.</span></span>

<span data-ttu-id="60d71-116">The Threat Intelligence pane is composed by three major options:</span><span class="sxs-lookup"><span data-stu-id="60d71-116">The Threat Intelligence pane is composed by three major options:</span></span>

* <span data-ttu-id="60d71-117">Servers with outbound malicious traffic</span><span class="sxs-lookup"><span data-stu-id="60d71-117">Servers with outbound malicious traffic</span></span>
* <span data-ttu-id="60d71-118">Detected threats types</span><span class="sxs-lookup"><span data-stu-id="60d71-118">Detected threats types</span></span>
* <span data-ttu-id="60d71-119">Threat intelligence map</span><span class="sxs-lookup"><span data-stu-id="60d71-119">Threat intelligence map</span></span>

> [!NOTE]
> <span data-ttu-id="60d71-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="60d71-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="responding-to-security-alerts"></a><span data-ttu-id="60d71-121">Responding to security alerts</span><span class="sxs-lookup"><span data-stu-id="60d71-121">Responding to security alerts</span></span>
<span data-ttu-id="60d71-122">One of the steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is to identify the severity of the compromise system(s).</span><span class="sxs-lookup"><span data-stu-id="60d71-122">One of the steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is to identify the severity of the compromise system(s).</span></span> <span data-ttu-id="60d71-123">In this phase you should perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="60d71-123">In this phase you should perform the following tasks:</span></span>

* <span data-ttu-id="60d71-124">Determine the nature of the attack</span><span class="sxs-lookup"><span data-stu-id="60d71-124">Determine the nature of the attack</span></span>
* <span data-ttu-id="60d71-125">Determine the attack point of origin</span><span class="sxs-lookup"><span data-stu-id="60d71-125">Determine the attack point of origin</span></span>
* <span data-ttu-id="60d71-126">Determine the intent of the attack.</span><span class="sxs-lookup"><span data-stu-id="60d71-126">Determine the intent of the attack.</span></span> <span data-ttu-id="60d71-127">Was the attack specifically directed at your organization to acquire specific information, or was it random?</span><span class="sxs-lookup"><span data-stu-id="60d71-127">Was the attack specifically directed at your organization to acquire specific information, or was it random?</span></span>
* <span data-ttu-id="60d71-128">Identify the systems that have been compromised</span><span class="sxs-lookup"><span data-stu-id="60d71-128">Identify the systems that have been compromised</span></span>
* <span data-ttu-id="60d71-129">Identify the files that have been accessed and determine the sensitivity of those files</span><span class="sxs-lookup"><span data-stu-id="60d71-129">Identify the files that have been accessed and determine the sensitivity of those files</span></span>

<span data-ttu-id="60d71-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution to help with these tasks.</span><span class="sxs-lookup"><span data-stu-id="60d71-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution to help with these tasks.</span></span> <span data-ttu-id="60d71-131">Follow the steps below to access this **Threat Intelligence** options:</span><span class="sxs-lookup"><span data-stu-id="60d71-131">Follow the steps below to access this **Threat Intelligence** options:</span></span>

1. <span data-ttu-id="60d71-132">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span><span class="sxs-lookup"><span data-stu-id="60d71-132">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![Security and Audit](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="60d71-134">In the **Security and Audit** dashboard, you will see the **Threat Intelligence** options in the right, as shown below:</span><span class="sxs-lookup"><span data-stu-id="60d71-134">In the **Security and Audit** dashboard, you will see the **Threat Intelligence** options in the right, as shown below:</span></span>
   
    ![Threat intel](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

<span data-ttu-id="60d71-136">These three tiles will give you an overview of the current threats.</span><span class="sxs-lookup"><span data-stu-id="60d71-136">These three tiles will give you an overview of the current threats.</span></span> <span data-ttu-id="60d71-137">In the **Server with outbound malicious traffic** you will be able to identify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic to the Internet.</span><span class="sxs-lookup"><span data-stu-id="60d71-137">In the **Server with outbound malicious traffic** you will be able to identify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic to the Internet.</span></span> 

<span data-ttu-id="60d71-138">The **Detected threat types** tile shows a summary of the threats that are current “in the wild”, if you click on this tile you will see more details about these threats as show below:</span><span class="sxs-lookup"><span data-stu-id="60d71-138">The **Detected threat types** tile shows a summary of the threats that are current “in the wild”, if you click on this tile you will see more details about these threats as show below:</span></span>

![Detected threat types](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

<span data-ttu-id="60d71-140">You can extract more information about each threat by clicking on it.</span><span class="sxs-lookup"><span data-stu-id="60d71-140">You can extract more information about each threat by clicking on it.</span></span> <span data-ttu-id="60d71-141">The example below shows more details about Botnet:</span><span class="sxs-lookup"><span data-stu-id="60d71-141">The example below shows more details about Botnet:</span></span>

![more details about a threat](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

<span data-ttu-id="60d71-143">As described in the beginning of this section, this information can be very useful during an incident response case.</span><span class="sxs-lookup"><span data-stu-id="60d71-143">As described in the beginning of this section, this information can be very useful during an incident response case.</span></span> <span data-ttu-id="60d71-144">It can also be important during a forensic investigation, where you need to find the source of the attack, which system was compromised and the timeline.</span><span class="sxs-lookup"><span data-stu-id="60d71-144">It can also be important during a forensic investigation, where you need to find the source of the attack, which system was compromised and the timeline.</span></span> <span data-ttu-id="60d71-145">In this report you can easily identify some key details about the attack, such as: the source of the attack, the local IP that was compromised and the current session state of the connection.</span><span class="sxs-lookup"><span data-stu-id="60d71-145">In this report you can easily identify some key details about the attack, such as: the source of the attack, the local IP that was compromised and the current session state of the connection.</span></span> 

<span data-ttu-id="60d71-146">The **threat intelligence map** will help you to identify the current locations around the globe that have malicious traffic.</span><span class="sxs-lookup"><span data-stu-id="60d71-146">The **threat intelligence map** will help you to identify the current locations around the globe that have malicious traffic.</span></span> <span data-ttu-id="60d71-147">There are orange (incoming) and red (outgoing) arrows in this map that identify the traffic direction, if you click in one of these arrows, it will show the type of threat and the traffic direction as shown below:</span><span class="sxs-lookup"><span data-stu-id="60d71-147">There are orange (incoming) and red (outgoing) arrows in this map that identify the traffic direction, if you click in one of these arrows, it will show the type of threat and the traffic direction as shown below:</span></span>

![threat intel map](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> <span data-ttu-id="60d71-149">You can see a demonstration on how to use this capability during an incident response process by watching the presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span><span class="sxs-lookup"><span data-stu-id="60d71-149">You can see a demonstration on how to use this capability during an incident response process by watching the presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="60d71-150">See also</span><span class="sxs-lookup"><span data-stu-id="60d71-150">See also</span></span>
<span data-ttu-id="60d71-151">In this document, you learned how to use the **Threat Intelligence** option in OMS Security and Audit solution to respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="60d71-151">In this document, you learned how to use the **Threat Intelligence** option in OMS Security and Audit solution to respond to security alerts.</span></span> <span data-ttu-id="60d71-152">To learn more about OMS Security, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="60d71-152">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="60d71-153">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="60d71-153">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="60d71-154">Getting started with Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="60d71-154">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="60d71-155">Monitoring Resources in Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="60d71-155">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)






