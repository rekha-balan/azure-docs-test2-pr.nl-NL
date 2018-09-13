---
title: Track AS2, X12, EDIFACT messages using a query - Azure logic apps  | Microsoft Docs
description: Use queries to track business-to-business messages in the Operations Management Suite portal
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
ms.openlocfilehash: a4c6ea3f43ba7ed2d4b3b0104b3ec7dd43b8b0fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670354"
---
# <a name="track-b2b-messages-in-the-operations-management-suite-portal-by-using-a-query"></a>Track B2B messages in the Operations Management Suite portal by using a query
To track business-to-business (B2B) messages in the Operations Management Suite portal, you can create a query that filters data for a specific interchange control number.

## <a name="prereqs"></a>Prereqs

For debugging and for more detailed diagnostics information, turn on diagnostics in your [integration account](logic-apps-monitor-b2b-message.md) for your [logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics-and-alerts) that have X12 connectors. Then, do the steps to [publish diagnostic data](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) to the Operations Management Suite portal.

## <a name="search-for-an-interchange-control-number"></a>Search for an interchange control number

1. On the start page, select **Log Search**.  
![Select log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

2. In the search box, type **Type="AzureDiagnostics"**. To filter data, select **Add**.  
![Select query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

3. Type **interchange**, select **event_record_messageProperties_interchangeControlNumber_s**, and then select **Add**.  
![Add filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query2.png)

4. Select the control number that you want to filter data for, and then select **Apply**.  
![Search on the control number](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query3.png)

5. Find the query that you created to filter data for the selected control number.   
![Find the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query4.png)

6. Type a name for the query, and then save it.   
![Save the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query5.png)

7. To view the query, and to use it in future searches, select **Favorites**.  
![View the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query7.png)

8. You can update the query to search for a new interchange control number.  
![Update the query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query6.png)


## <a name="next-steps"></a>Next steps
* Learn more about [custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Learn more about [AS2 tracking schemas](logic-apps-track-integration-account-as2-tracking-schemas.md).    
* Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).  
* Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).








