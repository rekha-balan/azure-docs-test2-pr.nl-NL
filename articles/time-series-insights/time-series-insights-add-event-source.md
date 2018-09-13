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
# <a name="create-a-new-event-source-for-your-time-series-insights-environment-using-the-azure-portal"></a><span data-ttu-id="07682-103">Create a new event source for your Time Series Insights environment using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="07682-103">Create a new event source for your Time Series Insights environment using the Azure portal</span></span>

<span data-ttu-id="07682-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="07682-104">Time Series Insights Event Source is derived from an event broker, like Azure Event Hubs.</span></span> <span data-ttu-id="07682-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span><span class="sxs-lookup"><span data-stu-id="07682-105">Time Series Insights connects directly to Event Sources, ingesting the data stream without requiring users to write a single line of code.</span></span> <span data-ttu-id="07682-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs, and in the future, more Event Sources will be added.</span><span class="sxs-lookup"><span data-stu-id="07682-106">Currently, Time Series Insights supports Azure Event Hubs and Azure IoT Hubs, and in the future, more Event Sources will be added.</span></span>

## <a name="steps-to-add-an-event-source-to-your-environment"></a><span data-ttu-id="07682-107">Steps to add an event source to your environment</span><span class="sxs-lookup"><span data-stu-id="07682-107">Steps to add an event source to your environment</span></span>

1.  <span data-ttu-id="07682-108">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07682-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="07682-109">Click “All resources” in the menu on the left side of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="07682-109">Click “All resources” in the menu on the left side of the Azure portal.</span></span>
3.  <span data-ttu-id="07682-110">Select your Time Series Insights environment.</span><span class="sxs-lookup"><span data-stu-id="07682-110">Select your Time Series Insights environment.</span></span>
  
  ![Create the Time Series Insights source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/add-event-source/getstarted-create-eventsource1.png)
  
4.  <span data-ttu-id="07682-112">Select “Event Sources”, click “+ Add”.</span><span class="sxs-lookup"><span data-stu-id="07682-112">Select “Event Sources”, click “+ Add”.</span></span>
  
  ![Create the Time Series Insights source - details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/add-event-source/getstarted-create-eventsource2.png)
  
5.  <span data-ttu-id="07682-114">Specify the name of the event source.</span><span class="sxs-lookup"><span data-stu-id="07682-114">Specify the name of the event source.</span></span> <span data-ttu-id="07682-115">This name will be associated with all events coming from this event source and will be available at query time.</span><span class="sxs-lookup"><span data-stu-id="07682-115">This name will be associated with all events coming from this event source and will be available at query time.</span></span>
6.  <span data-ttu-id="07682-116">Select an event hub from the list of Event Hub resources in the current subscription or choose “Import option: Provide Event Hub settings manually” to specify an event hub located in another subscription.</span><span class="sxs-lookup"><span data-stu-id="07682-116">Select an event hub from the list of Event Hub resources in the current subscription or choose “Import option: Provide Event Hub settings manually” to specify an event hub located in another subscription.</span></span>
7.  <span data-ttu-id="07682-117">Select policy that has read permission in the event hub.</span><span class="sxs-lookup"><span data-stu-id="07682-117">Select policy that has read permission in the event hub.</span></span>
8.  <span data-ttu-id="07682-118">Specify event hub consumer group.</span><span class="sxs-lookup"><span data-stu-id="07682-118">Specify event hub consumer group.</span></span> <span data-ttu-id="07682-119">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment), otherwise read operation may be negatively affected for this environment and the other service.</span><span class="sxs-lookup"><span data-stu-id="07682-119">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment), otherwise read operation may be negatively affected for this environment and the other service.</span></span>
9.  <span data-ttu-id="07682-120">Click “Create”.</span><span class="sxs-lookup"><span data-stu-id="07682-120">Click “Create”.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07682-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="07682-121">Next steps</span></span>

<span data-ttu-id="07682-122">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span><span class="sxs-lookup"><span data-stu-id="07682-122">After creation of the event source, Time Series Insights will automatically start streaming data into your environment.</span></span> <span data-ttu-id="07682-123">To see your data, open https://insights.timeseries.azure.com and select the environment.</span><span class="sxs-lookup"><span data-stu-id="07682-123">To see your data, open https://insights.timeseries.azure.com and select the environment.</span></span>


