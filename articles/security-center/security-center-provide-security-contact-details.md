---
title: Provide security contact details in Azure Security Center | Microsoft Docs
description: This document shows you how to provide security contact details in Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 624fbda7bd8b83eb53e2147eaea2c51326d36cff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554592"
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="95daf-103">Provide security contact details in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="95daf-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="95daf-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span><span class="sxs-lookup"><span data-stu-id="95daf-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="95daf-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span><span class="sxs-lookup"><span data-stu-id="95daf-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="95daf-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span><span class="sxs-lookup"><span data-stu-id="95daf-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="95daf-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span><span class="sxs-lookup"><span data-stu-id="95daf-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="95daf-108">Email preferences can only be configured for subscription policies.</span><span class="sxs-lookup"><span data-stu-id="95daf-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="95daf-109">Resource groups within a subscription will inherit these settings.</span><span class="sxs-lookup"><span data-stu-id="95daf-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="95daf-110">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="95daf-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="95daf-111">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="95daf-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="95daf-112">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="95daf-112">Implement the recommendation</span></span>
1. <span data-ttu-id="95daf-113">In the **Recommendations** blade, select **Provide security contact details**.</span><span class="sxs-lookup"><span data-stu-id="95daf-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="95daf-114">![Provide security contact][1]</span><span class="sxs-lookup"><span data-stu-id="95daf-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="95daf-115">This opens the blade **Provide security contact details**.</span><span class="sxs-lookup"><span data-stu-id="95daf-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="95daf-116">Select the Azure subscription to provide contact information on.</span><span class="sxs-lookup"><span data-stu-id="95daf-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="95daf-117">![Provide security contact details][2]</span><span class="sxs-lookup"><span data-stu-id="95daf-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="95daf-118">A second **Provide security contact details** blade opens.</span><span class="sxs-lookup"><span data-stu-id="95daf-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="95daf-119">Enter the security contact email address or addresses separated by commas.</span><span class="sxs-lookup"><span data-stu-id="95daf-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="95daf-120">There is not a limit to the number of email addresses that you can enter.</span><span class="sxs-lookup"><span data-stu-id="95daf-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="95daf-121">Enter one security contact international phone number.</span><span class="sxs-lookup"><span data-stu-id="95daf-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="95daf-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span><span class="sxs-lookup"><span data-stu-id="95daf-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="95daf-123">In the future, you will have the option to send email notifications to subscription owners.</span><span class="sxs-lookup"><span data-stu-id="95daf-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="95daf-124">This option is currently grayed out.</span><span class="sxs-lookup"><span data-stu-id="95daf-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="95daf-125">Select **OK** to apply the security contact information to your subscription.</span><span class="sxs-lookup"><span data-stu-id="95daf-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="95daf-126">See also</span><span class="sxs-lookup"><span data-stu-id="95daf-126">See also</span></span>
<span data-ttu-id="95daf-127">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="95daf-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="95daf-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="95daf-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="95daf-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="95daf-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="95daf-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="95daf-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="95daf-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="95daf-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="95daf-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="95daf-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="95daf-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="95daf-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="95daf-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="95daf-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-provide-security-contacts/provide-contacts.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-provide-security-contacts/provide-contact-details.png


