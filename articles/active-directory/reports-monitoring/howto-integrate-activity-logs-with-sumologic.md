---
title: How to integrate Azure Active Directory logs with SumoLogic by using Azure Monitor (preview)  | Microsoft Docs
description: Learn how to integrate Azure Active Directory logs with SumoLogic by using Azure Monitor (preview)
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 2c3db9a8-50fa-475a-97d8-f31082af6593
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 07/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: c805416b71e7cdb7ce3cdef84baf1167694eda12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866830"
---
# <a name="integrate-azure-ad-logs-with-sumologic-by-using-azure-monitor-preview"></a><span data-ttu-id="74fb4-103">Integrate Azure AD logs with SumoLogic by using Azure Monitor (preview)</span><span class="sxs-lookup"><span data-stu-id="74fb4-103">Integrate Azure AD logs with SumoLogic by using Azure Monitor (preview)</span></span>

<span data-ttu-id="74fb4-104">In this article, you learn how to integrate Azure Active Directory (Azure AD) logs with SumoLogic by using Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="74fb4-104">In this article, you learn how to integrate Azure Active Directory (Azure AD) logs with SumoLogic by using Azure Monitor.</span></span> <span data-ttu-id="74fb4-105">You first route the logs to an Azure event hub, and then you integrate the event hub with SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="74fb4-105">You first route the logs to an Azure event hub, and then you integrate the event hub with SumoLogic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74fb4-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74fb4-106">Prerequisites</span></span>

<span data-ttu-id="74fb4-107">To use this feature, you need:</span><span class="sxs-lookup"><span data-stu-id="74fb4-107">To use this feature, you need:</span></span>
* <span data-ttu-id="74fb4-108">An Azure event hub that contains Azure AD activity logs.</span><span class="sxs-lookup"><span data-stu-id="74fb4-108">An Azure event hub that contains Azure AD activity logs.</span></span> <span data-ttu-id="74fb4-109">Learn how to [stream your activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="74fb4-109">Learn how to [stream your activity logs to an event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md).</span></span> 
* <span data-ttu-id="74fb4-110">A SumoLogic single sign-on enabled subscription.</span><span class="sxs-lookup"><span data-stu-id="74fb4-110">A SumoLogic single sign-on enabled subscription.</span></span>

## <a name="steps-to-integrate-azure-ad-logs-with-sumologic"></a><span data-ttu-id="74fb4-111">Steps to integrate Azure AD logs with SumoLogic</span><span class="sxs-lookup"><span data-stu-id="74fb4-111">Steps to integrate Azure AD logs with SumoLogic</span></span> 

1. <span data-ttu-id="74fb4-112">First, [stream the Azure AD logs to an Azure event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="74fb4-112">First, [stream the Azure AD logs to an Azure event hub](quickstart-azure-monitor-stream-logs-to-event-hub.md).</span></span>
2. <span data-ttu-id="74fb4-113">Configure your SumoLogic instance to [collect logs for Azure Active Directory](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Collect_Logs_for_Azure_Active_Directory).</span><span class="sxs-lookup"><span data-stu-id="74fb4-113">Configure your SumoLogic instance to [collect logs for Azure Active Directory](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Collect_Logs_for_Azure_Active_Directory).</span></span>
3. <span data-ttu-id="74fb4-114">[Install the Azure AD SumoLogic app](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards) to use the pre-configured dashboards that provide real-time analysis of your environment.</span><span class="sxs-lookup"><span data-stu-id="74fb4-114">[Install the Azure AD SumoLogic app](https://help.sumologic.com/Send-Data/Applications-and-Other-Data-Sources/Azure_Active_Directory/Install_the_Azure_Active_Directory_App_and_View_the_Dashboards) to use the pre-configured dashboards that provide real-time analysis of your environment.</span></span>

 ![Dashboard](./media/howto-integrate-activity-logs-with-sumologic/overview-dashboard.png)

## <a name="next-steps"></a><span data-ttu-id="74fb4-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="74fb4-116">Next steps</span></span>

* [<span data-ttu-id="74fb4-117">Interpret audit logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="74fb4-117">Interpret audit logs schema in Azure Monitor</span></span>](reference-azure-monitor-audit-log-schema.md)
* [<span data-ttu-id="74fb4-118">Interpret sign-in logs schema in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="74fb4-118">Interpret sign-in logs schema in Azure Monitor</span></span>](reference-azure-monitor-sign-ins-log-schema.md)
* [<span data-ttu-id="74fb4-119">Frequently asked questions and known issues</span><span class="sxs-lookup"><span data-stu-id="74fb4-119">Frequently asked questions and known issues</span></span>](overview-activity-logs-in-azure-monitor.md#frequently-asked-questions)
