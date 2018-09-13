---
title: Add an event source to your Azure Time Series Insights environment | Microsoft Docs
description: In this tutorial, you connect an event source to your Time Series Insights environment
keywords: ''
services: time-series-insights
documentationcenter: ''
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: ''
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/20/2017
ms.author: omravi
ms.openlocfilehash: 082ed027a605827556d9dc5a01b464a0356a25e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552864"
---
# <a name="create-a-new-event-source-for-your-time-series-insights-environment-using-the-azure-portal"></a>Create a new event source for your Time Series Insights environment using the Azure portal

Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs. Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code. Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs, and in the future, more Event Sources will be added.

## <a name="steps-to-add-an-event-source-to-your-environment"></a>Steps to add an event source to your environment

1.  Sign in to the [Azure portal](https://portal.azure.com).
2.  Click “All resources” in the menu on the left side of the Azure portal.
3.  Select your Time Series Insights environment.
  
  ![Create the Time Series Insights source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/add-event-source/getstarted-create-eventsource1.png)
  
4.  Select “Event Sources”, click “+ Add”.
  
  ![Create the Time Series Insights source - details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/add-event-source/getstarted-create-eventsource2.png)
  
5.  Specify the name of the event source. This name will be associated with all events coming from this event source and will be available at query time.
6.  Select an event hub from the list of Event Hub resources in the current subscription or choose “Import option: Provide Event Hub settings manually” to specify an event hub located in another subscription.
7.  Select policy that has read permission in the event hub.
8.  Specify event hub consumer group. Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment), otherwise read operation may be negatively affected for this environment and the other service.
9.  Click “Create”.

## <a name="next-steps"></a>Next steps

After creation of the event source, Time Series Insights will automatically start streaming data into your environment. To see your data, open https://insights.timeseries.azure.com and select the environment.


