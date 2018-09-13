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
# <a name="start-or-enable-logging-of-as2-x12-and-edifact-messages-to-monitor-success-errors-and-message-properties"></a>Start or enable logging of AS2, X12, and EDIFACT messages to monitor success, errors, and message properties

B2B communication involves message exchanges between two running business processes or applications. The relationship defines an agreement between business processes. After communication is established, you can set up message monitoring to check that communication is working as expected. For richer details and debugging, you can set up diagnostics for your integration account.

Message tracking is available for these B2B protocols: AS2, X12, and EDIFACT. 

## <a name="prerequisites"></a>Prerequisites

* An Azure account; you can create a [free account](https://azure.microsoft.com/free).
* An Integration Account; you can create an [Integration Account](logic-apps-enterprise-integration-create-integration-account.md).
* A Logic App; you can create a [Logic App](logic-apps-create-a-logic-app.md) and [enable logging](logic-apps-monitor-your-logic-apps.md).

## <a name="enable-logging-for-an-integration-account"></a>Enable logging for an integration account

You can enable logging for an integration account either with the **Azure portal** or with **Monitor**.

### <a name="enable-logging-with-azure-portal"></a>Enable logging with Azure portal

1. Select your integration account, then select **Diagnostics logs**.

    ![Select your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic5.png)

2. Select your **Subscription** and **Resource Group**. From **Resource Type**, select **Integration Accounts**. From **Resource**, select your integration account. Click **Turn on Diagnostics** to enable diagnostics for your selected integration account.

    ![Set up diagnostics for your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic2.png)

3. Select status **ON**.

    ![Turn on diagnostics status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic3.png)

4. Select **Send to Log Analytics** and configure Log Analytics to emit data.

    ![Send diagnostics data to a log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic4.png)

### <a name="enable-logging-with-monitor"></a>Enable logging with Monitor

0. Select **Monitor**, **Diagnostics logs**.

    ![Select Monitor, Diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic1.png)

0. Select your **Subscription** and **Resource Group**. From **Resource Type**, select **Integration Accounts**. From **Resource**, select your integration account. Click **Turn on Diagnostics** to enable diagnostics for your selected integration account.

    ![Set up diagnostics for your integration account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic2.png)

0. Select status **ON**.

    ![Turn on diagnostics status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic3.png) 

0. Select **Send to Log Analytics** and configure **Log Analytics** to emit data.

    ![Send diagnostics data to a log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-b2b-message/pic4.png)

## <a name="extend-your-solutions"></a>Extend your solutions

In addition to the **Log Analytics**, you can configure your integration account and [Logic Apps](./logic-apps-monitor-your-logic-apps.md) to an Event Hub or Storage Account.

![Azure Diagnostics settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-monitor-your-logic-apps/diagnostics.png)

You can use this telemetry from the Event Hub or Storage into other services like [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/), and [Power BI](https://powerbi.com) to have real-time monitoring of your integration workflows.

## <a name="supported-tracking-schema"></a>Supported Tracking Schema

We support these tracking schema types, which all have fixed schemas except the Custom type.

* [Custom Tracking Schema](logic-apps-track-integration-account-custom-tracking-schema.md)
* [AS2 Tracking Schema](logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 Tracking Schema](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Next steps

[Tracking B2B messages in OMS Portal](logic-apps-track-b2b-messages-omsportal.md "Tracking B2B messages")

[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack")










