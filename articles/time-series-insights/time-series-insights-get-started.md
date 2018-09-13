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
# <a name="create-a-new-time-series-insights-environment-in-the-azure-portal"></a><span data-ttu-id="e5536-103">Create a new Time Series Insights environment in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e5536-103">Create a new Time Series Insights environment in the Azure portal</span></span>

<span data-ttu-id="e5536-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span><span class="sxs-lookup"><span data-stu-id="e5536-104">Time Series Insights environment is an Azure resource with ingress and storage capacity.</span></span> <span data-ttu-id="e5536-105">Customers provision environments via the Azure portal with the required capacity.</span><span class="sxs-lookup"><span data-stu-id="e5536-105">Customers provision environments via the Azure portal with the required capacity.</span></span>

## <a name="steps-to-create-the-environment"></a><span data-ttu-id="e5536-106">Steps to create the environment</span><span class="sxs-lookup"><span data-stu-id="e5536-106">Steps to create the environment</span></span>

<span data-ttu-id="e5536-107">Follow these steps to create your environment:</span><span class="sxs-lookup"><span data-stu-id="e5536-107">Follow these steps to create your environment:</span></span>

1.  <span data-ttu-id="e5536-108">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5536-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="e5536-109">Click the plus sign (“+”) in the top left corner.</span><span class="sxs-lookup"><span data-stu-id="e5536-109">Click the plus sign (“+”) in the top left corner.</span></span>
3.  <span data-ttu-id="e5536-110">Search for “Time Series Insights” in the search box.</span><span class="sxs-lookup"><span data-stu-id="e5536-110">Search for “Time Series Insights” in the search box.</span></span>
  
  ![Create the Time Series Insights environment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment1.png)
  
4.  <span data-ttu-id="e5536-112">Select “Time Series Insights”, click “Create”.</span><span class="sxs-lookup"><span data-stu-id="e5536-112">Select “Time Series Insights”, click “Create”.</span></span>
   
  ![Create the Time Series Insights resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment2.png)
  
5.  <span data-ttu-id="e5536-114">Specify environment name.</span><span class="sxs-lookup"><span data-stu-id="e5536-114">Specify environment name.</span></span> <span data-ttu-id="e5536-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5536-115">This name will represent the environment in [time series explorer](https://insights.timeseries.azure.com).</span></span>
6.  <span data-ttu-id="e5536-116">Select a subscription.</span><span class="sxs-lookup"><span data-stu-id="e5536-116">Select a subscription.</span></span> <span data-ttu-id="e5536-117">Choose one that contains your event source.</span><span class="sxs-lookup"><span data-stu-id="e5536-117">Choose one that contains your event source.</span></span> <span data-ttu-id="e5536-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="e5536-118">Time Series Insights can auto-detect Azure IoT Hub and Event Hub resources existing in the same subscription.</span></span>
7.  <span data-ttu-id="e5536-119">Select or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="e5536-119">Select or create a resource group.</span></span> <span data-ttu-id="e5536-120">A resource group is a collection of Azure resources used together.</span><span class="sxs-lookup"><span data-stu-id="e5536-120">A resource group is a collection of Azure resources used together.</span></span>
8.  <span data-ttu-id="e5536-121">Select a hosting location.</span><span class="sxs-lookup"><span data-stu-id="e5536-121">Select a hosting location.</span></span> <span data-ttu-id="e5536-122">To void moving data across data centers, choose location that contains your event source.</span><span class="sxs-lookup"><span data-stu-id="e5536-122">To void moving data across data centers, choose location that contains your event source.</span></span>
9.  <span data-ttu-id="e5536-123">Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="e5536-123">Select a pricing tier.</span></span>
10. <span data-ttu-id="e5536-124">Select capacity.</span><span class="sxs-lookup"><span data-stu-id="e5536-124">Select capacity.</span></span> <span data-ttu-id="e5536-125">You can change capacity of an environment after creation.</span><span class="sxs-lookup"><span data-stu-id="e5536-125">You can change capacity of an environment after creation.</span></span>
11. <span data-ttu-id="e5536-126">Create your environment.</span><span class="sxs-lookup"><span data-stu-id="e5536-126">Create your environment.</span></span> <span data-ttu-id="e5536-127">Remember to pin your environment to the dashboard for easy access whenever you sign in.</span><span class="sxs-lookup"><span data-stu-id="e5536-127">Remember to pin your environment to the dashboard for easy access whenever you sign in.</span></span>

![Create the Time Series Insights pin to dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a><span data-ttu-id="e5536-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5536-129">Next steps</span></span>

<span data-ttu-id="e5536-130">After creation of the environment, you are ready to create an event source and start streaming data into the environment.</span><span class="sxs-lookup"><span data-stu-id="e5536-130">After creation of the environment, you are ready to create an event source and start streaming data into the environment.</span></span>
<span data-ttu-id="e5536-131">To access environment in the time series explorer, use the Time Series Insights URL as shown below or simply open [time series explorer](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5536-131">To access environment in the time series explorer, use the Time Series Insights URL as shown below or simply open [time series explorer](https://insights.timeseries.azure.com).</span></span>

![Create the Time Series Insights explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/time-series-insights/media/get-started/getstarted-create-environment4.png)





