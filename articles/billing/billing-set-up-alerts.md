---
title: Set up billing or credit alerts for Azure subscriptions | Microsoft Docs
description: Describes how you can set up alerts on your Azure bill so you can avoid billing surprises.
keywords: credit alert,billing alert
services: ''
documentationcenter: ''
author: vikdesai
manager: vikdesai
editor: ''
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 606a112b5d19b3dc3b7b7f0d5722994996275a2f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553117"
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="5d748-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span><span class="sxs-lookup"><span data-stu-id="5d748-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="5d748-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span><span class="sxs-lookup"><span data-stu-id="5d748-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="5d748-106">This service is in preview, so you need to enable it in the Preview Features page first.</span><span class="sxs-lookup"><span data-stu-id="5d748-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="5d748-107">Set the alert threshold and email recipients</span><span class="sxs-lookup"><span data-stu-id="5d748-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="5d748-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span><span class="sxs-lookup"><span data-stu-id="5d748-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="5d748-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span><span class="sxs-lookup"><span data-stu-id="5d748-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="5d748-110">Click the subscription you want to monitor, and then click **Alerts**.</span><span class="sxs-lookup"><span data-stu-id="5d748-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Screenshot of the subscriptions view of Azure Account center, with Alerts highlighted][Image1]

2. <span data-ttu-id="5d748-112">Next, click **Add Alert** to create your first one.</span><span class="sxs-lookup"><span data-stu-id="5d748-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="5d748-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span><span class="sxs-lookup"><span data-stu-id="5d748-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Screenshot of the Alerts view, where you can add alert][Image2]

3. <span data-ttu-id="5d748-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span><span class="sxs-lookup"><span data-stu-id="5d748-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="5d748-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span><span class="sxs-lookup"><span data-stu-id="5d748-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="5d748-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span><span class="sxs-lookup"><span data-stu-id="5d748-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="5d748-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span><span class="sxs-lookup"><span data-stu-id="5d748-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="5d748-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5d748-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Screenshot of the alert addition view, where you can configure recipients][Image3]

<span data-ttu-id="5d748-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span><span class="sxs-lookup"><span data-stu-id="5d748-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="5d748-122">Check on your alerts</span><span class="sxs-lookup"><span data-stu-id="5d748-122">Check on your alerts</span></span>
<span data-ttu-id="5d748-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span><span class="sxs-lookup"><span data-stu-id="5d748-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="5d748-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span><span class="sxs-lookup"><span data-stu-id="5d748-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="5d748-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span><span class="sxs-lookup"><span data-stu-id="5d748-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="5d748-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span><span class="sxs-lookup"><span data-stu-id="5d748-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="5d748-127">Billing alerts for Enterprise Agreement (EA) customers</span><span class="sxs-lookup"><span data-stu-id="5d748-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="5d748-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span><span class="sxs-lookup"><span data-stu-id="5d748-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="5d748-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span><span class="sxs-lookup"><span data-stu-id="5d748-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="5d748-130">Learn more about Azure cost management</span><span class="sxs-lookup"><span data-stu-id="5d748-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="5d748-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span><span class="sxs-lookup"><span data-stu-id="5d748-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="5d748-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="5d748-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="5d748-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="5d748-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="5d748-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5d748-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/azure-billing-set-up-alerts/billingalerts3.png 



