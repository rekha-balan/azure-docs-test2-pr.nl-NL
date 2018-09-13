---
title: Analyze data usage in Log Analytics | Microsoft Docs
description: You can use the Usage dashboard in Log Analytics to view how much data is being sent to the OMS service.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 13ae96979e51dc62a8712837edf03b7b13ee30a7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563405"
---
# <a name="analyze-data-usage-in-log-analytics"></a>Analyze data usage in Log Analytics
Log Analytics collects data and sends it to the OMS service periodically.  You can use the **Log Analytics Usage** dashboard to view how much data is being sent to the OMS service. The dashboard also shows you how much data is being sent by solutions and how often your servers are sending data.

> [!NOTE]
> If you have a free account, you're limited to sending 500 MB of data to the OMS service daily. If you reach the daily limit, data analysis stops and resumes at the start of the next day. In that case, you need to resend any data that wasn't accepted or processed by OMS.

If you have exceeded or are near your daily usage limit, you can optionally remove a solution to reduce the amount of data to send to the OMS service. For more information about removing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).

![usage dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/usage-dashboard01.png)

The **Log Analytics usage** dashboard displays the following information:

- Data volume
    - Data volume over time (based on your current time scope)
    - Data volume by solution
    - Data not associated with a computer
- Computers
    - Computers sending data
    - Computers with no data in last 24 hours
- Offerings
    - Insight and Analytics nodes
    - Automation and Control nodes
    - Security nodes
- Performance
    - Time taken to collect and index data
- List of queries

## <a name="understanding-nodes-for-oms-offers"></a>Understanding nodes for OMS offers

If you are on the *per node (OMS)* pricing tier, then you are charged based on the number of nodes and solutions you have enabled. You can see how many nodes of each offer are being used in the *offerings* section of the usage dashboard.

![usage dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/log-analytics-usage-offerings.png)

## <a name="to-work-with-usage-data"></a>To work with usage data
1. If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com) using your Azure subscription.
2. On the **Hub** menu, click **More services** and in the list of resources, type **Log Analytics**. As you begin typing, the list filters based on your input. Click **Log Analytics**.  
    ![Azure hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/hub.png)
3. The **Log Analytics** dashboard shows a list of your workspaces. Select a workspace.
4. In the *workspace* dashboard, click **Log Analytics usage**.
5. On the **Log Analytics Usage** dashboard, click **Time: Last 24 hours** to change the time interval.  
    ![time interval](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/time.png)
6. View the usage category blades that show areas you’re interested in. Choose a blade and then click an item in it to view more details in [Log Search](log-analytics-log-searches.md).  
    ![example data usage blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/blade.png)
7. On the Log Search dashboard, review the results that are returned from the search.  
    ![example usage log search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-usage/usage-log-search.png)


## <a name="next-steps"></a>Next steps
* See [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed information that is gathered and sent to OMS by features and solutions.






