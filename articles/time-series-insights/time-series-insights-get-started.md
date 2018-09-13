---
title: Create an Azure Time Series Insights environment | Microsoft Docs
description: In this tutorial, you will learn how to create Time Series Environment, connect it to an event source and ready to analyze your event data in minutes.
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
ms.openlocfilehash: 0b33169c791c6c72cfdbf712223bf95487bacd38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555698"
---
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a>Create a new Time Series Insights environment in the Azure portal

Time Series Insights environment is an Azure resource with ingress and storage capacity. Customers provision environments via the Azure portal with the required capacity.

## <a name="steps-to-create-the-environment"></a>Steps to create the environment

Follow these steps to create your environment:

1.  Sign in to the [Azure portal](https://portal.azure.com).
2.  Click the plus sign (“+”) in the top left corner.
3.  Search for “Time Series Insights” in the search box.
  
  ![Create the Time Series Insights environment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment1.png)
  
4.  Select “Time Series Insights”, click “Create”.
   
  ![Create the Time Series Insights resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment2.png)
  
5.  Specify environment name. This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).
6.  Select a subscription. Choose one that contains your event source. Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.
7.  Select or create a resource group. A resource group is a collection of Azure resources used together.
8.  Select a hosting location. To void moving data across data centers, choose location that contains your event source.
9.  Select a pricing tier.
10. Select capacity. You can change capacity of an environment after creation.
11. Create your environment. Remember to pin your environment to the dashboard for easy access whenever you sign in.

![Create the Time Series Insights pin to dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Next steps

After creation of the environment, you are ready to create an event source and start streaming data into the environment.
To access environment in the time series explorer, use the Time Series Insights URL as shown below or simply open [time series explorer](https://insights.timeseries.azure.com).

![Create the Time Series Insights explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment4.png)





