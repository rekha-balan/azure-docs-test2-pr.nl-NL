---
title: Get started with Azure Advisor | Microsoft Docs
description: Get started with Azure Advisor.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: 8e2718b4144b5e77806a65b10fd623ec2594ee49
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671647"
---
# <a name="get-started-with-azure-advisor"></a>Get started with Azure Advisor

Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.

## <a name="get-advisor-recommendations"></a>Get Advisor recommendations

1. Sign in to the [Azure portal](https://portal.azure.com).

2. In the left pane, click **More services**.

3. In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.  
 The Advisor dashboard is displayed.

   ![Access Azure Advisor using the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-azure-portal-menu.png) 

4. On the Advisor dashboard, select the subscription for which you want to receive recommendations.  
The Advisor dashboard displays personalized recommendations for a selected subscription. 

5. To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.
 
> [!NOTE]
> To access Advisor recommendations, you must first *register your subscription* with Advisor. A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button. This is a *one-time operation*. After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.

  ![Azure Advisor dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a>Get Advisor recommendation details, and implement a solution

The **Recommendation** blade in Advisor offers additional information about the recommendation. 

1. Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).

2. On the **Advisor recommendations** dashboard, click **Get recommendations**.

3. In the list of recommendations, click a recommendation that you want to review in detail.  
The **Recommendation** blade is displayed.

4. On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity. 
  
  ![The Advisor Recommendation blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a>Search for Advisor recommendations

You can search for recommendations for a particular subscription or resource group. You can also search for recommendations by status.

1. Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).

2. Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).

3. To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.

  ![Advisor search-filter criteria](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a>Snooze or dismiss Advisor recommendations

1. Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).

2. Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.

3. On the **Recommendation** blade, click **Snooze**.  

   ![Advisor recommendation action example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/advisor/media/advisor-get-started/advisor-snooze.png)

4. Specify a snooze time period, or select **Never** to dismiss the recommendation.


## <a name="next-steps"></a>Next steps

To learn more about Advisor, see:
* [Introduction to Azure Advisor](advisor-overview.md)
* [Advisor High Availability recommendations](advisor-high-availability-recommendations.md)
* [Advisor Security recommendations](advisor-security-recommendations.md)
-  [Advisor Performance recommendations](advisor-performance-recommendations.md)
* [Advisor Cost recommendations](advisor-performance-recommendations.md)





