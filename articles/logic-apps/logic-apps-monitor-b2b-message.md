---
title: Monitor messages in B2B transactions - Azure Logic Apps | Microsoft Docs
description: Monitor and track messages during B2B communication between processes and apps using Logic Apps in your Integration Account.
author: padmavc
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0eff434155667b5148d0c0b47356fb60e346df68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555739"
---
# <a name="start-or-enable-logging-of-as2-x12-and-edifact-messages-to-monitor-success-errors-and-message-properties"></a><span data-ttu-id="9a5a4-103">Start or enable logging of AS2, X12, and EDIFACT messages to monitor success, errors, and message properties</span><span class="sxs-lookup"><span data-stu-id="9a5a4-103">Start or enable logging of AS2, X12, and EDIFACT messages to monitor success, errors, and message properties</span></span>

<span data-ttu-id="9a5a4-104">B2B communication involves message exchanges between two running business processes or applications.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-104">B2B communication involves message exchanges between two running business processes or applications.</span></span> <span data-ttu-id="9a5a4-105">The relationship defines an agreement between business processes.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-105">The relationship defines an agreement between business processes.</span></span> <span data-ttu-id="9a5a4-106">After communication is established, you can set up message monitoring to check that communication is working as expected.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-106">After communication is established, you can set up message monitoring to check that communication is working as expected.</span></span> <span data-ttu-id="9a5a4-107">For richer details and debugging, you can set up diagnostics for your integration account.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-107">For richer details and debugging, you can set up diagnostics for your integration account.</span></span>

<span data-ttu-id="9a5a4-108">Message tracking is available for these B2B protocols: AS2, X12, and EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-108">Message tracking is available for these B2B protocols: AS2, X12, and EDIFACT.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9a5a4-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9a5a4-109">Prerequisites</span></span>

* <span data-ttu-id="9a5a4-110">An Azure account; you can create a [free account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9a5a4-110">An Azure account; you can create a [free account](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="9a5a4-111">An Integration Account; you can create an [Integration Account](logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="9a5a4-111">An Integration Account; you can create an [Integration Account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>
* <span data-ttu-id="9a5a4-112">A Logic App; you can create a [Logic App](logic-apps-create-a-logic-app.md) and [enable logging](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9a5a4-112">A Logic App; you can create a [Logic App](logic-apps-create-a-logic-app.md) and [enable logging](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="enable-logging-for-an-integration-account"></a><span data-ttu-id="9a5a4-113">Enable logging for an integration account</span><span class="sxs-lookup"><span data-stu-id="9a5a4-113">Enable logging for an integration account</span></span>

<span data-ttu-id="9a5a4-114">You can enable logging for an integration account either with the **Azure portal** or with **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-114">You can enable logging for an integration account either with the **Azure portal** or with **Monitor**.</span></span>

### <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="9a5a4-115">Enable logging with Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a5a4-115">Enable logging with Azure portal</span></span>

1. <span data-ttu-id="9a5a4-116">Select your integration account, then select **Diagnostics logs**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-116">Select your integration account, then select **Diagnostics logs**.</span></span>

    ![Select your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic5.png)

2. <span data-ttu-id="9a5a4-118">Select your **Subscription** and **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-118">Select your **Subscription** and **Resource Group**.</span></span> <span data-ttu-id="9a5a4-119">From **Resource Type**, select **Integration Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-119">From **Resource Type**, select **Integration Accounts**.</span></span> <span data-ttu-id="9a5a4-120">From **Resource**, select your integration account.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-120">From **Resource**, select your integration account.</span></span> <span data-ttu-id="9a5a4-121">Click **Turn on Diagnostics** to enable diagnostics for your selected integration account.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-121">Click **Turn on Diagnostics** to enable diagnostics for your selected integration account.</span></span>

    ![Set up diagnostics for your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic2.png)

3. <span data-ttu-id="9a5a4-123">Select status **ON**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-123">Select status **ON**.</span></span>

    ![Turn on diagnostics status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic3.png)

4. <span data-ttu-id="9a5a4-125">Select **Send to Log Analytics** and configure Log Analytics to emit data.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-125">Select **Send to Log Analytics** and configure Log Analytics to emit data.</span></span>

    ![Send diagnostics data to a log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic4.png)

### <a name="enable-logging-with-monitor"></a><span data-ttu-id="9a5a4-127">Enable logging with Monitor</span><span class="sxs-lookup"><span data-stu-id="9a5a4-127">Enable logging with Monitor</span></span>

0. <span data-ttu-id="9a5a4-128">Select **Monitor**, **Diagnostics logs**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-128">Select **Monitor**, **Diagnostics logs**.</span></span>

    ![Select Monitor, Diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic1.png)

0. <span data-ttu-id="9a5a4-130">Select your **Subscription** and **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-130">Select your **Subscription** and **Resource Group**.</span></span> <span data-ttu-id="9a5a4-131">From **Resource Type**, select **Integration Accounts**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-131">From **Resource Type**, select **Integration Accounts**.</span></span> <span data-ttu-id="9a5a4-132">From **Resource**, select your integration account.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-132">From **Resource**, select your integration account.</span></span> <span data-ttu-id="9a5a4-133">Click **Turn on Diagnostics** to enable diagnostics for your selected integration account.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-133">Click **Turn on Diagnostics** to enable diagnostics for your selected integration account.</span></span>

    ![Set up diagnostics for your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic2.png)

0. <span data-ttu-id="9a5a4-135">Select status **ON**.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-135">Select status **ON**.</span></span>

    ![Turn on diagnostics status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic3.png) 

0. <span data-ttu-id="9a5a4-137">Select **Send to Log Analytics** and configure **Log Analytics** to emit data.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-137">Select **Send to Log Analytics** and configure **Log Analytics** to emit data.</span></span>

    ![Send diagnostics data to a log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic4.png)

## <a name="extend-your-solutions"></a><span data-ttu-id="9a5a4-139">Extend your solutions</span><span class="sxs-lookup"><span data-stu-id="9a5a4-139">Extend your solutions</span></span>

<span data-ttu-id="9a5a4-140">In addition to the **Log Analytics**, you can configure your integration account and [Logic Apps](./logic-apps-monitor-your-logic-apps.md) to an Event Hub or Storage Account.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-140">In addition to the **Log Analytics**, you can configure your integration account and [Logic Apps](./logic-apps-monitor-your-logic-apps.md) to an Event Hub or Storage Account.</span></span>

![Azure Diagnostics settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-your-logic-apps/diagnostics.png)

<span data-ttu-id="9a5a4-142">You can use this telemetry from the Event Hub or Storage into other services like [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/), and [Power BI](https://powerbi.com) to have real-time monitoring of your integration workflows.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-142">You can use this telemetry from the Event Hub or Storage into other services like [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/), and [Power BI](https://powerbi.com) to have real-time monitoring of your integration workflows.</span></span>

## <a name="supported-tracking-schema"></a><span data-ttu-id="9a5a4-143">Supported Tracking Schema</span><span class="sxs-lookup"><span data-stu-id="9a5a4-143">Supported Tracking Schema</span></span>

<span data-ttu-id="9a5a4-144">We support these tracking schema types, which all have fixed schemas except the Custom type.</span><span class="sxs-lookup"><span data-stu-id="9a5a4-144">We support these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="9a5a4-145">Custom Tracking Schema</span><span class="sxs-lookup"><span data-stu-id="9a5a4-145">Custom Tracking Schema</span></span>](logic-apps-track-integration-account-custom-tracking-schema.md)
* [<span data-ttu-id="9a5a4-146">AS2 Tracking Schema</span><span class="sxs-lookup"><span data-stu-id="9a5a4-146">AS2 Tracking Schema</span></span>](logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="9a5a4-147">X12 Tracking Schema</span><span class="sxs-lookup"><span data-stu-id="9a5a4-147">X12 Tracking Schema</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="9a5a4-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a5a4-148">Next steps</span></span>

[<span data-ttu-id="9a5a4-149">Tracking B2B messages in OMS Portal</span><span class="sxs-lookup"><span data-stu-id="9a5a4-149">Tracking B2B messages in OMS Portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Tracking B2B messages")

[<span data-ttu-id="9a5a4-150">Learn more about the Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="9a5a4-150">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")










