---
title: Managing connected partner solutions in Azure Security Center | Microsoft Docs
description: This document walks you through how Azure Security Center lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/20/2018
ms.author: terrylan
ms.openlocfilehash: 3174f2d6562030702b14ef1fa3708a1a4e8e373b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776849"
---
# <a name="managing-connected-partner-solutions-with-azure-security-center"></a><span data-ttu-id="030bf-103">Managing connected partner solutions with Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="030bf-103">Managing connected partner solutions with Azure Security Center</span></span>
<span data-ttu-id="030bf-104">This article walks you through how to manage and monitor connected security solutions in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="030bf-104">This article walks you through how to manage and monitor connected security solutions in Azure Security Center.</span></span>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="030bf-105">Monitoring partner solutions</span><span class="sxs-lookup"><span data-stu-id="030bf-105">Monitoring partner solutions</span></span>
<span data-ttu-id="030bf-106">To monitor the health status of connected security solutions and perform basic management:</span><span class="sxs-lookup"><span data-stu-id="030bf-106">To monitor the health status of connected security solutions and perform basic management:</span></span>

1. <span data-ttu-id="030bf-107">Under **Security Center - Overview**, select **Security solutions**.</span><span class="sxs-lookup"><span data-stu-id="030bf-107">Under **Security Center - Overview**, select **Security solutions**.</span></span>

  ![Select security solutions][1]

  <span data-ttu-id="030bf-109">The **Connected solutions** section includes security solutions that are connected to Security Center and information about the health status of each solution.</span><span class="sxs-lookup"><span data-stu-id="030bf-109">The **Connected solutions** section includes security solutions that are connected to Security Center and information about the health status of each solution.</span></span>

  ![Partner solutions][2]

   <span data-ttu-id="030bf-111">The status of a partner solution can be:</span><span class="sxs-lookup"><span data-stu-id="030bf-111">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="030bf-112">Healthy (green) - there is no health issue.</span><span class="sxs-lookup"><span data-stu-id="030bf-112">Healthy (green) - there is no health issue.</span></span>
   * <span data-ttu-id="030bf-113">Unhealthy (red) - there is a health issue that requires immediate attention.</span><span class="sxs-lookup"><span data-stu-id="030bf-113">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="030bf-114">Health issues (orange) - the solution has stopped reporting its health.</span><span class="sxs-lookup"><span data-stu-id="030bf-114">Health issues (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="030bf-115">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying, or no health data is available.</span><span class="sxs-lookup"><span data-stu-id="030bf-115">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying, or no health data is available.</span></span>

   > [!NOTE]
   > <span data-ttu-id="030bf-116">If health status data is not available, Security Center shows the date and time of the last event received to indicate whether the solution is reporting or not.</span><span class="sxs-lookup"><span data-stu-id="030bf-116">If health status data is not available, Security Center shows the date and time of the last event received to indicate whether the solution is reporting or not.</span></span> <span data-ttu-id="030bf-117">If no health data is available and no alerts are received within the last 14 days, Security Center indicates that the solution is unhealthy or not reporting.</span><span class="sxs-lookup"><span data-stu-id="030bf-117">If no health data is available and no alerts are received within the last 14 days, Security Center indicates that the solution is unhealthy or not reporting.</span></span>
   >
   >

2. <span data-ttu-id="030bf-118">Select **VIEW** for additional information and options, which includes:</span><span class="sxs-lookup"><span data-stu-id="030bf-118">Select **VIEW** for additional information and options, which includes:</span></span>

  - <span data-ttu-id="030bf-119">**Solution console**.</span><span class="sxs-lookup"><span data-stu-id="030bf-119">**Solution console**.</span></span> <span data-ttu-id="030bf-120">Opens the management experience for this solution.</span><span class="sxs-lookup"><span data-stu-id="030bf-120">Opens the management experience for this solution.</span></span>
  - <span data-ttu-id="030bf-121">**Link VM**.</span><span class="sxs-lookup"><span data-stu-id="030bf-121">**Link VM**.</span></span> <span data-ttu-id="030bf-122">Opens the Link Applications blade.</span><span class="sxs-lookup"><span data-stu-id="030bf-122">Opens the Link Applications blade.</span></span> <span data-ttu-id="030bf-123">Here you can connect resources to the partner solution.</span><span class="sxs-lookup"><span data-stu-id="030bf-123">Here you can connect resources to the partner solution.</span></span>
  - <span data-ttu-id="030bf-124">**Delete solution**.</span><span class="sxs-lookup"><span data-stu-id="030bf-124">**Delete solution**.</span></span>
  - <span data-ttu-id="030bf-125">**Configure**.</span><span class="sxs-lookup"><span data-stu-id="030bf-125">**Configure**.</span></span>

   ![Partner solution detail][3]

## <a name="next-steps"></a><span data-ttu-id="030bf-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="030bf-127">Next steps</span></span>
<span data-ttu-id="030bf-128">In this article, you learned how to manage and monitor connected security solutions in Security Center.</span><span class="sxs-lookup"><span data-stu-id="030bf-128">In this article, you learned how to manage and monitor connected security solutions in Security Center.</span></span> <span data-ttu-id="030bf-129">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="030bf-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="030bf-130">[Security solutions overview](security-center-partner-integration.md) — Learn how to connect and manage security solutions.</span><span class="sxs-lookup"><span data-stu-id="030bf-130">[Security solutions overview](security-center-partner-integration.md) — Learn how to connect and manage security solutions.</span></span>
* <span data-ttu-id="030bf-131">[Connecting Microsoft Advanced Threat Analytics (ATA)](security-center-ata-integration.md) — Learn how to connect alerts from ATA.</span><span class="sxs-lookup"><span data-stu-id="030bf-131">[Connecting Microsoft Advanced Threat Analytics (ATA)](security-center-ata-integration.md) — Learn how to connect alerts from ATA.</span></span>
* <span data-ttu-id="030bf-132">[Connecting Azure Active Directory (AD) Identity Protection ](security-center-aadip-integration.md) — Learn how to connect alerts from Azure AD Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="030bf-132">[Connecting Azure Active Directory (AD) Identity Protection ](security-center-aadip-integration.md) — Learn how to connect alerts from Azure AD Identity Protection.</span></span>
* <span data-ttu-id="030bf-133">[Partner and solutions integration](security-center-partner-integration.md) - Get an overview of integrating other security solutions.</span><span class="sxs-lookup"><span data-stu-id="030bf-133">[Partner and solutions integration](security-center-partner-integration.md) - Get an overview of integrating other security solutions.</span></span>
* <span data-ttu-id="030bf-134">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="030bf-134">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="030bf-135">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="030bf-135">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="030bf-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="030bf-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[2]: ./media/security-center-partner-solutions/partner-solutions.png
[3]: ./media/security-center-partner-solutions/partner-solutions-detail.png
