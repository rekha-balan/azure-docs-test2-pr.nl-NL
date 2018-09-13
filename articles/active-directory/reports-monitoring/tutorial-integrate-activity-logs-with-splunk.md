---
title: How to integrate Azure Active Directory logs with Splunk by using Azure Monitor (preview)  | Microsoft Docs
description: Learn how to integrate Azure Active Directory logs with Splunk by using Azure Monitor (preview)
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: c4b605b6-6fc0-40dc-bd49-101d03f34665
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 07/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: bafd130b2fbd22f85407590ff2e86ecf5c6dfe67
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867700"
---
# <a name="integrate-azure-ad-logs-with-splunk-by-using-azure-monitor-preview"></a><span data-ttu-id="33bdc-103">Integrate Azure AD logs with Splunk by using Azure Monitor (preview)</span><span class="sxs-lookup"><span data-stu-id="33bdc-103">Integrate Azure AD logs with Splunk by using Azure Monitor (preview)</span></span>

<span data-ttu-id="33bdc-104">In this article, you learn how to integrate Azure Active Directory (Azure AD) logs with Splunk by using Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="33bdc-104">In this article, you learn how to integrate Azure Active Directory (Azure AD) logs with Splunk by using Azure Monitor.</span></span> <span data-ttu-id="33bdc-105">You first route the logs to an Azure event hub, and then you integrate the event hub with Splunk.</span><span class="sxs-lookup"><span data-stu-id="33bdc-105">You first route the logs to an Azure event hub, and then you integrate the event hub with Splunk.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33bdc-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33bdc-106">Prerequisites</span></span>

<span data-ttu-id="33bdc-107">To use this feature, you need:</span><span class="sxs-lookup"><span data-stu-id="33bdc-107">To use this feature, you need:</span></span>
* <span data-ttu-id="33bdc-108">An Azure event hub that contains Azure AD activity logs.</span><span class="sxs-lookup"><span data-stu-id="33bdc-108">An Azure event hub that contains Azure AD activity logs.</span></span> <span data-ttu-id="33bdc-109">Learn how to [stream your activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="33bdc-109">Learn how to [stream your activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md).</span></span> 
* <span data-ttu-id="33bdc-110">The Azure Monitor Add-on for Splunk.</span><span class="sxs-lookup"><span data-stu-id="33bdc-110">The Azure Monitor Add-on for Splunk.</span></span> <span data-ttu-id="33bdc-111">[Download and configure your Splunk instance](https://github.com/Microsoft/AzureMonitorAddonForSplunk/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="33bdc-111">[Download and configure your Splunk instance](https://github.com/Microsoft/AzureMonitorAddonForSplunk/blob/master/README.md).</span></span>

## <a name="tutorial"></a><span data-ttu-id="33bdc-112">Tutorial</span><span class="sxs-lookup"><span data-stu-id="33bdc-112">Tutorial</span></span> 

1. <span data-ttu-id="33bdc-113">Open your Splunk instance, and select **Data Summary**.</span><span class="sxs-lookup"><span data-stu-id="33bdc-113">Open your Splunk instance, and select **Data Summary**.</span></span>

    ![The "Data Summary" button](./media/tutorial-integrate-activity-logs-with-splunk/DataSummary.png)

2. <span data-ttu-id="33bdc-115">Select the **Sourcetypes** tab, and then select **amal: aadal:audit**</span><span class="sxs-lookup"><span data-stu-id="33bdc-115">Select the **Sourcetypes** tab, and then select **amal: aadal:audit**</span></span>

    ![The Data Summary Sourcetypes tab](./media/tutorial-integrate-activity-logs-with-splunk/sourcetypeaadal.png)

    <span data-ttu-id="33bdc-117">The Azure AD activity logs are shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="33bdc-117">The Azure AD activity logs are shown in the following figure:</span></span>

    ![Activity logs](./media/tutorial-integrate-activity-logs-with-splunk/activitylogs.png)

> [!NOTE]
> <span data-ttu-id="33bdc-119">If you cannot install an add-on in your Splunk instance (for example, if you're using a proxy or running on Splunk Cloud), you can forward these events to the Splunk HTTP Event Collector.</span><span class="sxs-lookup"><span data-stu-id="33bdc-119">If you cannot install an add-on in your Splunk instance (for example, if you're using a proxy or running on Splunk Cloud), you can forward these events to the Splunk HTTP Event Collector.</span></span> <span data-ttu-id="33bdc-120">To do so, use this [Azure function](https://github.com/Microsoft/AzureFunctionforSplunkVS), which is triggered by new messages in the event hub.</span><span class="sxs-lookup"><span data-stu-id="33bdc-120">To do so, use this [Azure function](https://github.com/Microsoft/AzureFunctionforSplunkVS), which is triggered by new messages in the event hub.</span></span> 
>

## <a name="next-steps"></a><span data-ttu-id="33bdc-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="33bdc-121">Next steps</span></span>

* [<span data-ttu-id="33bdc-122">Interpret audit logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="33bdc-122">Interpret audit logs schema in Azure Monitor</span></span>](reference-azure-monitor-audit-log-schema.md)
* [<span data-ttu-id="33bdc-123">Interpret sign-in logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="33bdc-123">Interpret sign-in logs schema in Azure Monitor</span></span>](reference-azure-monitor-sign-ins-log-schema.md)
* [<span data-ttu-id="33bdc-124">Frequently asked questions and known issues</span><span class="sxs-lookup"><span data-stu-id="33bdc-124">Frequently asked questions and known issues</span></span>](overview-activity-logs-in-azure-monitor.md#frequently-asked-questions)
