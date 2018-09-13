---
title: Monitor and track usage of Azure free services | Microsoft Docs
description: Learn to check usage of free services. Use Azure portal and usage csv.
services: ''
documentationcenter: ''
author: amberbhargava
manager: amberb
editor: ''
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/25/2017
ms.author: amberb
ms.openlocfilehash: 7fa0196b7a44ef20ecd63797869dffea55f92c3d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871096"
---
# <a name="check-usage-of-free-services-included-with-your-azure-free-account"></a><span data-ttu-id="69115-104">Check usage of free services included with your Azure free account</span><span class="sxs-lookup"><span data-stu-id="69115-104">Check usage of free services included with your Azure free account</span></span> 

<span data-ttu-id="69115-105">You are not charged for services included for free with Azure free account, unless you exceed the limits of these services.</span><span class="sxs-lookup"><span data-stu-id="69115-105">You are not charged for services included for free with Azure free account, unless you exceed the limits of these services.</span></span> <span data-ttu-id="69115-106">To remain with the limits, you can either use the Azure portal or your usage file to monitor and track the usage of free services.</span><span class="sxs-lookup"><span data-stu-id="69115-106">To remain with the limits, you can either use the Azure portal or your usage file to monitor and track the usage of free services.</span></span> 

## <a name="check-usage-on-the-azure-portal"></a><span data-ttu-id="69115-107">Check usage on the Azure portal</span><span class="sxs-lookup"><span data-stu-id="69115-107">Check usage on the Azure portal</span></span>

1.  <span data-ttu-id="69115-108">Log in to the [Azure portal]( http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="69115-108">Log in to the [Azure portal]( http://portal.azure.com).</span></span>

2.  <span data-ttu-id="69115-109">From left navigation area, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="69115-109">From left navigation area, select **All services**.</span></span>

3.  <span data-ttu-id="69115-110">Select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="69115-110">Select **Subscriptions**.</span></span>

4.  <span data-ttu-id="69115-111">Select the subscription that you created when you signed up for free account.</span><span class="sxs-lookup"><span data-stu-id="69115-111">Select the subscription that you created when you signed up for free account.</span></span>

    ![Screenshot that shows all the subscriptions](./media/billing-check-usage-of-free-services/select-free-account-subscription.png)

5.  <span data-ttu-id="69115-113">The overview section shows you essential information about your subscription such as subscription       ID,         offer type, and subscription name.</span><span class="sxs-lookup"><span data-stu-id="69115-113">The overview section shows you essential information about your subscription such as subscription       ID,         offer type, and subscription name.</span></span> <span data-ttu-id="69115-114">You can also find information on when your free account          credit          would expire.</span><span class="sxs-lookup"><span data-stu-id="69115-114">You can also find information on when your free account          credit          would expire.</span></span>

    ![Screenshot that shows subscription essential information](./media/billing-check-usage-of-free-services/subscription-essential-information.png)

6.  <span data-ttu-id="69115-116">Scroll down to find information on your current and forecasted cost.</span><span class="sxs-lookup"><span data-stu-id="69115-116">Scroll down to find information on your current and forecasted cost.</span></span> <span data-ttu-id="69115-117">The cost includes usage of                     services not included with your free account and usage exceeding the limits of free                                 services.</span><span class="sxs-lookup"><span data-stu-id="69115-117">The cost includes usage of                     services not included with your free account and usage exceeding the limits of free                                 services.</span></span> 

    ![Screenshot that shows subscription cost information](./media/billing-check-usage-of-free-services/subscription-cost-information.png)

7.  <span data-ttu-id="69115-119">The final part of the overview section has a table on usage of free services.</span><span class="sxs-lookup"><span data-stu-id="69115-119">The final part of the overview section has a table on usage of free services.</span></span> 

    ![Screenshot that shows usage of free services](./media/billing-check-usage-of-free-services/subscription-usage-free-services.png)

    <span data-ttu-id="69115-121">The table contains the following columns:</span><span class="sxs-lookup"><span data-stu-id="69115-121">The table contains the following columns:</span></span>

* <span data-ttu-id="69115-122">**Meter Name:** Identifies the unit of measure for the meter being consumed.</span><span class="sxs-lookup"><span data-stu-id="69115-122">**Meter Name:** Identifies the unit of measure for the meter being consumed.</span></span> <span data-ttu-id="69115-123">To learn about service to meter                        mapping, see [Understand free service to meter mapping](billing-understand-free-service-meter-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="69115-123">To learn about service to meter                        mapping, see [Understand free service to meter mapping](billing-understand-free-service-meter-mapping.md).</span></span> 
* <span data-ttu-id="69115-124">**Usage/Limit:** Current month's usage and limit for the meter.</span><span class="sxs-lookup"><span data-stu-id="69115-124">**Usage/Limit:** Current month's usage and limit for the meter.</span></span> <span data-ttu-id="69115-125">You can also find this information in the status bar.</span><span class="sxs-lookup"><span data-stu-id="69115-125">You can also find this information in the status bar.</span></span>
* <span data-ttu-id="69115-126">**Status:** Usage status of the meter.</span><span class="sxs-lookup"><span data-stu-id="69115-126">**Status:** Usage status of the meter.</span></span> <span data-ttu-id="69115-127">Based on your usage pattern, you can have one of these             statutes.</span><span class="sxs-lookup"><span data-stu-id="69115-127">Based on your usage pattern, you can have one of these             statutes.</span></span>
  * <span data-ttu-id="69115-128">**Not in use:** You have not used the meter or the usage for the meter has not reached the billing system.</span><span class="sxs-lookup"><span data-stu-id="69115-128">**Not in use:** You have not used the meter or the usage for the meter has not reached the billing system.</span></span>
  * <span data-ttu-id="69115-129">**Exceeded on \<Date>:** You have exceeded the limit for the meter on \<Date>.</span><span class="sxs-lookup"><span data-stu-id="69115-129">**Exceeded on \<Date>:** You have exceeded the limit for the meter on \<Date>.</span></span>
  * <span data-ttu-id="69115-130">**Unlikely to Exceed:** You are unlikely to exceed the limit for the meter.</span><span class="sxs-lookup"><span data-stu-id="69115-130">**Unlikely to Exceed:** You are unlikely to exceed the limit for the meter.</span></span>
  * <span data-ttu-id="69115-131">**Exceeds on \<Date>:** You are likely to exceed the limit for the meter on \<Date>.</span><span class="sxs-lookup"><span data-stu-id="69115-131">**Exceeds on \<Date>:** You are likely to exceed the limit for the meter on \<Date>.</span></span>


## <a name="check-usage-through-the-usage-file"></a><span data-ttu-id="69115-132">Check usage through the usage file</span><span class="sxs-lookup"><span data-stu-id="69115-132">Check usage through the usage file</span></span>

<span data-ttu-id="69115-133">Your usage file provides granular information for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="69115-133">Your usage file provides granular information for your Azure subscription.</span></span> <span data-ttu-id="69115-134">You can download your monthly and daily usage file from Azure Account Center.</span><span class="sxs-lookup"><span data-stu-id="69115-134">You can download your monthly and daily usage file from Azure Account Center.</span></span> <span data-ttu-id="69115-135">To learn how to download the usage file and understand the access required, see [Get Invoice and Usage](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="69115-135">To learn how to download the usage file and understand the access required, see [Get Invoice and Usage](billing-download-azure-invoice-daily-usage-date.md).</span></span> <span data-ttu-id="69115-136">To learn about columns in the usage file, see [Understand terms on your usage](billing-understand-your-usage.md).</span><span class="sxs-lookup"><span data-stu-id="69115-136">To learn about columns in the usage file, see [Understand terms on your usage](billing-understand-your-usage.md).</span></span> 

<span data-ttu-id="69115-137">The usage file contains usage information for both free and paid services.</span><span class="sxs-lookup"><span data-stu-id="69115-137">The usage file contains usage information for both free and paid services.</span></span> <span data-ttu-id="69115-138">Free service meters would have **Free** appended at the end of the meter name.</span><span class="sxs-lookup"><span data-stu-id="69115-138">Free service meters would have **Free** appended at the end of the meter name.</span></span> <span data-ttu-id="69115-139">To find free meters, open the file in excel and filter the **Meter Category column** for cells that contain text **- Free** (Use Text Filters &rarr; Contains filter) &nbsp;</span><span class="sxs-lookup"><span data-stu-id="69115-139">To find free meters, open the file in excel and filter the **Meter Category column** for cells that contain text **- Free** (Use Text Filters &rarr; Contains filter) &nbsp;</span></span>

![Screenshot that shows usage of free services](./media/billing-check-usage-of-free-services/free-services-usage-csv.png)


## <a name="need-help-contact-support"></a><span data-ttu-id="69115-141">Need help?</span><span class="sxs-lookup"><span data-stu-id="69115-141">Need help?</span></span> <span data-ttu-id="69115-142">Contact support</span><span class="sxs-lookup"><span data-stu-id="69115-142">Contact support</span></span>

<span data-ttu-id="69115-143">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="69115-143">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
