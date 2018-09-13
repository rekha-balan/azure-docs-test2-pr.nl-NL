---
title: Logic Apps B2B Integration Account Disaster Recovery - Azure Logic Apps | Microsoft Docs
description: Azure Logic Apps B2B Disaster Recovery
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: padmavc
ms.openlocfilehash: e48b79eca23bc8e7440fd70bc651c22f58ea520b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660853"
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Logic Apps B2B cross region disaster recovery
B2B workloads involve money transactions like orders, invoices.  For business, it is critical to quickly recover to meet business level SLAs as agreed with their partners during a disaster event.  This topic demonstrates building a business continuity plan for B2B workloads.  It covers

* Create an integration account in secondary region
* Establish a connection from primary region to secondary region 
* Fail over to secondary region during a disaster event
* Fall back to primary region post-disaster event

## <a name="create-an-integration-account-in-secondary-region"></a>Create an integration account in secondary region
1. Select a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).  

2. Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.

    > [!Tip]
    > Make sure consistency in integration account artifacts naming convention across regions 
    > 
    > 

3. The recommendation is to deploy all primary region resources (for example SQL Azure or DocumentDB databases, or Service Bus / Event Hubs used for messaging, APIM, Logic Apps) in the secondary region as well.  

## <a name="establish-a-connection-from-primary-to-secondary"></a>Establish a connection from primary to secondary 
To pull the run status from the primary region, create a Logic App in the secondary region.  It should have a **trigger** and an **action**.  The trigger should connect to primary region integration account and the action should connect to secondary region integration account.  Based on the time interval, the trigger polls the primary region run status table pulls the new records if any and action updates them to secondary region integration account. This helps to get incremental runtime status from primary region to secondary region.

Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.  To find detailed steps, select respective links.

* [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12)
* [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2)
* EDIFACT (coming soon)

## <a name="fail-over-to-secondary-region-during-a-disaster-event"></a>Fail over to secondary region during a disaster event
During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region. Secondary region helps recover business functions quickly to meet recovery time/point objectives (RPO/RTO) as agreed with their partners.  Also, minimizes efforts to fail over from one region to another region. 

There is an expected latency while copying control numbers from primary to secondary region.  To avoid sending duplicate generated control numbers to partners during a disaster event, it is recommended to bump up control numbers in the **secondary region agreements** using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-to-primary-region-post-disaster-event"></a>Fall back to primary region post-disaster event
When primary region is available, to fall back to primary region follow below steps     
* Stop accepting messages from partners in the **secondary region**   
* Bump up generated control numbers for all the **primary region agreements** using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)   
* Direct traffic from secondary to primary region   
* Check the Logic App created in the secondary region to pull run status from the primary is enabled    

## <a name="x12"></a>X12 
Business continuity for EDI X12 documents is designed based on control numbers   
* Control numbers received (Inbound messages) from partners  
* Control numbers generated (outbound messages) and send to partners  
    
    > [!Tip]
    > You can also use [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create Logic Apps.  Creating primary and secondary integration accounts are prerequisites to use the template.  The template helps create 2 Logic Apps, one for received control number and another for generated control number.  Respective triggers and actions are created in the Logic Apps, connects the trigger to primary integration account and action to secondary integration account.
    > 
    >

### <a name="control-numbers-received-from-the-partners"></a>Control numbers received from the partners
1. Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region   

2. Search **X12** and select **X12 - When a received control number is modified**    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN1.png)

3. Selecting the trigger prompts to establish a connection to integration account. Trigger to be connected to primary region integration account.  Give a connection name, select your **primary region integration account** from the list and click create.   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN2.png)

4. DateTime to start control number sync is optional.  Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN3.png)

5. Click **New step** and **Add an action**    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN4.png)

6. Search **X12** and select **X12 - Add or update a received control number**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN5.png)

7. Action to be connected to secondary integration account.  Select **Change connection** and **Add new connection** lists the available integration accounts.  Give a connection name, select your **secondary region integration account** from the list and click create.     
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN6.png)

8. Select the dynamic content and save the logic app   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN7.png)

9. Based on the time interval, the trigger polls the primary region received control number table, pulls the new records, and actions updates them to secondary region integration account.  If they are no updates, the trigger status shows as skipped.
    
    > [!Tip]
    > Enabling duplicate check on the agreement receive settings keeps received control numbers runtime state and helps fire the triggers at regular intervals
    > 
    >

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12recevicedCN8.png)


### <a name="control-numbers-generated-and-send-to-the-partners"></a>Control numbers generated and send to the partners
1. Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region  

2. Search **X12** and select **X12 - When a generated control number is modified**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN1.png)

3. Selecting the trigger prompts to establish a connection to integration account. Trigger to be connected to primary region integration account.  Give a connection name, select your **primary region integration account** from the list and click create.   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN2.png) 

4. DateTime to start control number sync is optional.  Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN3.png)  

5. Click **New step** and **Add an action**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN4.png)

6. Search **X12** and select **X12 - Add or update a generated control number**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN5.png)

7. Action to be connected to secondary integration account.  Select **Change connection** and **Add new connection** lists the available integration accounts.  Give a connection name, select your **secondary region integration account** from the list and click create.    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN6.png)

8. Select the dynamic content and save the logic app   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN7.png)

9. Based on the time interval, the trigger polls the primary region received control number table, pulls the new records, and actions updates them to secondary region integration account.  If they are no updates, the trigger status shows as skipped.  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/X12generatedCN8.png)

Based on the time interval, the incremental runtime status replicates from primary region to secondary region.  During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity. 

## <a name="as2"></a>AS2 
Business continuity for documents that use AS2 protocol is designed based on message id and MIC value

> [!Tip]
    > You can also use [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create Logic Apps.  Creating primary and secondary integration accounts are prerequisites to use the template.  The template helps create a Logic App, having a trigger and an action.  Creates a connection from trigger to primary integration account and action to secondary integration account.
    > 
    >

1. Create a [Logic App](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region  

2. Search **AS2** and select **AS2 - When a MIC value is created**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid1.png)

3. Selecting the trigger prompts to establish a connection to integration account. Trigger to be connected to primary region integration account.  Give a connection name, select your **primary region integration account** from the list and click create.   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid2.png)

4. DateTime to start MIC value sync is optional.  Frequency can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid3.png)

5. Click **New step** and **Add an action**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid4.png)

6. Search **AS2** and select **AS2 - Add or update a MIC**   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid5.png)

7. Action to be connected to secondary integration account.  Select **Change connection** and **Add new connection** lists the available integration accounts.  Give a connection name, select your **secondary region integration account** from the list and click create.    
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid6.png)

8. Select the dynamic content and save the logic app   
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid7.png)

9. Based on the time interval, the trigger polls the primary region table, pulls the new records, and actions updates them to secondary region integration account.  If they are no updates, the trigger status shows as skipped.  
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-b2b-business-continuity/AS2messageid8.png)

Based on the time interval, the incremental runtime status replicates from primary region to secondary region.  During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity. 

## <a name="next-steps"></a>Next Steps
* Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).   























