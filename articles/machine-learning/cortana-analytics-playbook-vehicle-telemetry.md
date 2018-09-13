---
title: Predict vehicle health and driving habits - Azure | Microsoft Docs
description: Use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 3dbc99a2c90f947d05ecc37d5eea1bb21cf982d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552588"
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="b23bc-103">Vehicle telemetry analytics solution playbook</span><span class="sxs-lookup"><span data-stu-id="b23bc-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="b23bc-104">This **menu** links to the chapters in this playbook.</span><span class="sxs-lookup"><span data-stu-id="b23bc-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="b23bc-105">Overview</span><span class="sxs-lookup"><span data-stu-id="b23bc-105">Overview</span></span>
<span data-ttu-id="b23bc-106">Super computers have moved out of the lab and are now parked in our garage!</span><span class="sxs-lookup"><span data-stu-id="b23bc-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="b23bc-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span><span class="sxs-lookup"><span data-stu-id="b23bc-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="b23bc-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="b23bc-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="b23bc-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span><span class="sxs-lookup"><span data-stu-id="b23bc-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="b23bc-110">Microsoft has made this dream a reality with Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="b23bc-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="b23bc-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span><span class="sxs-lookup"><span data-stu-id="b23bc-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="b23bc-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span><span class="sxs-lookup"><span data-stu-id="b23bc-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="b23bc-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="b23bc-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="b23bc-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span><span class="sxs-lookup"><span data-stu-id="b23bc-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="b23bc-115">The solution:</span><span class="sxs-lookup"><span data-stu-id="b23bc-115">The solution:</span></span> 

* <span data-ttu-id="b23bc-116">provides a Vehicle Telematics simulator</span><span class="sxs-lookup"><span data-stu-id="b23bc-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="b23bc-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span><span class="sxs-lookup"><span data-stu-id="b23bc-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="b23bc-118">uses Stream Analytics to gain real-time insights on vehicle health</span><span class="sxs-lookup"><span data-stu-id="b23bc-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="b23bc-119">persists the data into long-term storage for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="b23bc-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="b23bc-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span><span class="sxs-lookup"><span data-stu-id="b23bc-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="b23bc-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span><span class="sxs-lookup"><span data-stu-id="b23bc-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="b23bc-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span><span class="sxs-lookup"><span data-stu-id="b23bc-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="b23bc-123">Architecture</span><span class="sxs-lookup"><span data-stu-id="b23bc-123">Architecture</span></span>
<span data-ttu-id="b23bc-124">![Solution architecture diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span><span class="sxs-lookup"><span data-stu-id="b23bc-124">![Solution architecture diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="b23bc-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span><span class="sxs-lookup"><span data-stu-id="b23bc-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="b23bc-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span><span class="sxs-lookup"><span data-stu-id="b23bc-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="b23bc-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="b23bc-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="b23bc-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span><span class="sxs-lookup"><span data-stu-id="b23bc-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="b23bc-129">**HDInsight** is leveraged to transform data at scale</span><span class="sxs-lookup"><span data-stu-id="b23bc-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="b23bc-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="b23bc-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="b23bc-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="b23bc-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="b23bc-132">This solution accesses two different **data sources**:</span><span class="sxs-lookup"><span data-stu-id="b23bc-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="b23bc-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span><span class="sxs-lookup"><span data-stu-id="b23bc-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="b23bc-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span><span class="sxs-lookup"><span data-stu-id="b23bc-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>


