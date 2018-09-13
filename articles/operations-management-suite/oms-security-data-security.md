---
title: Operations Management Suite Security and Audit Solution Data Security | Microsoft Docs
description: This document explains how data is managed and safeguarded in Operations Management Suite Security and Audit Solution.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 3b6327b1f5150f32afd71639f32c55d823f1d1f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555888"
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="82721-103">Operations Management Suite Security and Audit solution data security</span><span class="sxs-lookup"><span data-stu-id="82721-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="82721-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span><span class="sxs-lookup"><span data-stu-id="82721-104">To help customers prevent, detect, and respond to threats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="82721-105">Security event log</span><span class="sxs-lookup"><span data-stu-id="82721-105">Security event log</span></span>
* <span data-ttu-id="82721-106">Event Tracing for Windows (ETW) events</span><span class="sxs-lookup"><span data-stu-id="82721-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="82721-107">AppLocker auditing events</span><span class="sxs-lookup"><span data-stu-id="82721-107">AppLocker auditing events</span></span>
* <span data-ttu-id="82721-108">Windows Firewall log</span><span class="sxs-lookup"><span data-stu-id="82721-108">Windows Firewall log</span></span>
* <span data-ttu-id="82721-109">Advanced Threat Analytics events</span><span class="sxs-lookup"><span data-stu-id="82721-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="82721-110">Results of baseline assessment</span><span class="sxs-lookup"><span data-stu-id="82721-110">Results of baseline assessment</span></span>
* <span data-ttu-id="82721-111">Results of antimalware assessment</span><span class="sxs-lookup"><span data-stu-id="82721-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="82721-112">Results of update/patch assessment</span><span class="sxs-lookup"><span data-stu-id="82721-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="82721-113">Syslogs streams that are explicitly enabled on the agent</span><span class="sxs-lookup"><span data-stu-id="82721-113">Syslogs streams that are explicitly enabled on the agent</span></span>

<span data-ttu-id="82721-114">We make strong commitments to protect the privacy and security of this data.</span><span class="sxs-lookup"><span data-stu-id="82721-114">We make strong commitments to protect the privacy and security of this data.</span></span> <span data-ttu-id="82721-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span><span class="sxs-lookup"><span data-stu-id="82721-115">Microsoft adheres to strict compliance and security guidelines—from coding to operating a service.</span></span>
<span data-ttu-id="82721-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span><span class="sxs-lookup"><span data-stu-id="82721-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="82721-117">Data sources</span><span class="sxs-lookup"><span data-stu-id="82721-117">Data sources</span></span>
<span data-ttu-id="82721-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span><span class="sxs-lookup"><span data-stu-id="82721-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where the OMS Agent is installed.</span></span> <span data-ttu-id="82721-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span><span class="sxs-lookup"><span data-stu-id="82721-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="82721-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span><span class="sxs-lookup"><span data-stu-id="82721-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="82721-121">Data protection</span><span class="sxs-lookup"><span data-stu-id="82721-121">Data protection</span></span>
<span data-ttu-id="82721-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span><span class="sxs-lookup"><span data-stu-id="82721-122">**Data segregation**: Data is kept logically separate on each component throughout the service.</span></span> <span data-ttu-id="82721-123">All data is tagged per organization.</span><span class="sxs-lookup"><span data-stu-id="82721-123">All data is tagged per organization.</span></span> <span data-ttu-id="82721-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span><span class="sxs-lookup"><span data-stu-id="82721-124">This tagging persists throughout the data lifecycle, and it is enforced at each layer of the service.</span></span> 

<span data-ttu-id="82721-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span><span class="sxs-lookup"><span data-stu-id="82721-125">**Data access**: To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="82721-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span><span class="sxs-lookup"><span data-stu-id="82721-126">We adhere to the [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="82721-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span><span class="sxs-lookup"><span data-stu-id="82721-127">To provide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="82721-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span><span class="sxs-lookup"><span data-stu-id="82721-128">We only use Customer Data as needed to provide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="82721-129">You retain all rights to your own data.</span><span class="sxs-lookup"><span data-stu-id="82721-129">You retain all rights to your own data.</span></span>

<span data-ttu-id="82721-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="82721-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants to enhance our prevention and detection capabilities; we do so in accordance with the privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="82721-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span><span class="sxs-lookup"><span data-stu-id="82721-131">Data location is configured at the OMS workspace level, during the workspace creation, which is part of the initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="82721-132">See also</span><span class="sxs-lookup"><span data-stu-id="82721-132">See also</span></span>
<span data-ttu-id="82721-133">In this document, you learned how data is managed and safeguarded in OMS.</span><span class="sxs-lookup"><span data-stu-id="82721-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="82721-134">To learn more about OMS Security and Audit solution, see:</span><span class="sxs-lookup"><span data-stu-id="82721-134">To learn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="82721-135">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="82721-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="82721-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="82721-136">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="82721-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="82721-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

