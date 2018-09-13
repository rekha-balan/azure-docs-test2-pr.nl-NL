---
title: Protecting Azure SQL service and data in Azure Security Center  | Microsoft Docs
description: This document addresses recommendations in Azure Security Center that help you protect your data and Azure SQL service and stay in compliance with security policies.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 0b3b8082412b12a0fffbaea04409a8bbb3f4ac15
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782202"
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="2a23a-103">Protecting Azure SQL service and data in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="2a23a-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="2a23a-104">Azure Security Center analyzes the security state of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="2a23a-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="2a23a-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span><span class="sxs-lookup"><span data-stu-id="2a23a-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="2a23a-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span><span class="sxs-lookup"><span data-stu-id="2a23a-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="2a23a-107">This article addresses recommendations that apply to Azure SQL service and data.</span><span class="sxs-lookup"><span data-stu-id="2a23a-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="2a23a-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="2a23a-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="2a23a-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span><span class="sxs-lookup"><span data-stu-id="2a23a-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="2a23a-110">Available SQL service and data recommendations</span><span class="sxs-lookup"><span data-stu-id="2a23a-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="2a23a-111">Recommendation</span><span class="sxs-lookup"><span data-stu-id="2a23a-111">Recommendation</span></span> | <span data-ttu-id="2a23a-112">Description</span><span class="sxs-lookup"><span data-stu-id="2a23a-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="2a23a-113">Enable auditing and threat detection on SQL servers</span><span class="sxs-lookup"><span data-stu-id="2a23a-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="2a23a-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span><span class="sxs-lookup"><span data-stu-id="2a23a-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="2a23a-115">Enable auditing and threat detection on SQL databases</span><span class="sxs-lookup"><span data-stu-id="2a23a-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="2a23a-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span><span class="sxs-lookup"><span data-stu-id="2a23a-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="2a23a-117">Enable Transparent Data Encryption on SQL databases</span><span class="sxs-lookup"><span data-stu-id="2a23a-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="2a23a-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span><span class="sxs-lookup"><span data-stu-id="2a23a-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="2a23a-119">See also</span><span class="sxs-lookup"><span data-stu-id="2a23a-119">See also</span></span>
<span data-ttu-id="2a23a-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span><span class="sxs-lookup"><span data-stu-id="2a23a-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="2a23a-121">Protecting your virtual machines in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="2a23a-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="2a23a-122">Protecting your applications in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="2a23a-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="2a23a-123">Protecting your network in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="2a23a-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="2a23a-124">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="2a23a-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="2a23a-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="2a23a-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2a23a-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="2a23a-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="2a23a-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="2a23a-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
