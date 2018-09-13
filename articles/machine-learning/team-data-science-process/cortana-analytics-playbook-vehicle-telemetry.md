---
title: Predict vehicle health and driving habits - Azure | Microsoft Docs
description: Use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2018
ms.author: deguhath
ms.openlocfilehash: fc8dfbbfc40db33f19d2b183546ed9c6df0159fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856469"
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="21763-103">Vehicle Telemetry Analytics Solution playbook</span><span class="sxs-lookup"><span data-stu-id="21763-103">Vehicle Telemetry Analytics Solution playbook</span></span>
<span data-ttu-id="21763-104">This menu links to the chapters in this playbook:</span><span class="sxs-lookup"><span data-stu-id="21763-104">This menu links to the chapters in this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="21763-105">Overview</span><span class="sxs-lookup"><span data-stu-id="21763-105">Overview</span></span>
<span data-ttu-id="21763-106">Super computers have moved out of the lab and are now parked in garages.</span><span class="sxs-lookup"><span data-stu-id="21763-106">Super computers have moved out of the lab and are now parked in garages.</span></span> <span data-ttu-id="21763-107">These are now being placed in cutting-edge automobiles that contain myriad sensors.</span><span class="sxs-lookup"><span data-stu-id="21763-107">These are now being placed in cutting-edge automobiles that contain myriad sensors.</span></span> <span data-ttu-id="21763-108">These sensors give them the ability to track and monitor millions of events every second.</span><span class="sxs-lookup"><span data-stu-id="21763-108">These sensors give them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="21763-109">By 2020, most of these vehicles will be connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="21763-109">By 2020, most of these vehicles will be connected to the Internet.</span></span> <span data-ttu-id="21763-110">Tapping into this wealth of data provides greater safety, reliability, and so a better driving experience.</span><span class="sxs-lookup"><span data-stu-id="21763-110">Tapping into this wealth of data provides greater safety, reliability, and so a better driving experience.</span></span> <span data-ttu-id="21763-111">Microsoft makes this dream a reality with Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="21763-111">Microsoft makes this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="21763-112">Cortana Intelligence is a fully managed big data and advanced analytics suite that you can use to transform your data into intelligent action.</span><span class="sxs-lookup"><span data-stu-id="21763-112">Cortana Intelligence is a fully managed big data and advanced analytics suite that you can use to transform your data into intelligent action.</span></span> <span data-ttu-id="21763-113">The Cortana Intelligence Vehicle Telemetry Analytics Solution Template demonstrates how car dealerships, automobile manufacturers, and insurance companies are able to obtain real-time and predictive insights on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="21763-113">The Cortana Intelligence Vehicle Telemetry Analytics Solution Template demonstrates how car dealerships, automobile manufacturers, and insurance companies are able to obtain real-time and predictive insights on vehicle health and driving habits.</span></span>

<span data-ttu-id="21763-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture), which shows the full potential of the Cortana Intelligence platform for real-time and batch processing.</span><span class="sxs-lookup"><span data-stu-id="21763-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture), which shows the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span>

## <a name="architecture"></a><span data-ttu-id="21763-115">Architecture</span><span class="sxs-lookup"><span data-stu-id="21763-115">Architecture</span></span>
<span data-ttu-id="21763-116">The Vehicle Telemetry Analytics Solution architecture is illustrated in this diagram:</span><span class="sxs-lookup"><span data-stu-id="21763-116">The Vehicle Telemetry Analytics Solution architecture is illustrated in this diagram:</span></span>

![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)


<span data-ttu-id="21763-118">This solution includes the following Cortana Intelligence components and showcases their integration:</span><span class="sxs-lookup"><span data-stu-id="21763-118">This solution includes the following Cortana Intelligence components and showcases their integration:</span></span>

* <span data-ttu-id="21763-119">**Azure Event Hubs** ingests millions of vehicle telemetry events into Azure.</span><span class="sxs-lookup"><span data-stu-id="21763-119">**Azure Event Hubs** ingests millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="21763-120">**Azure Stream Analytics** provides real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="21763-120">**Azure Stream Analytics** provides real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="21763-121">**Azure Machine Learning** detects anomalies in real time and uses batch processing to provide predictive insights.</span><span class="sxs-lookup"><span data-stu-id="21763-121">**Azure Machine Learning** detects anomalies in real time and uses batch processing to provide predictive insights.</span></span>
* <span data-ttu-id="21763-122">**Azure HDInsight** transforms data at scale.</span><span class="sxs-lookup"><span data-stu-id="21763-122">**Azure HDInsight** transforms data at scale.</span></span>
* <span data-ttu-id="21763-123">**Azure Data Factory** handles orchestration, scheduling, resource management, and monitoring of the batch processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="21763-123">**Azure Data Factory** handles orchestration, scheduling, resource management, and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="21763-124">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="21763-124">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="21763-125">This solution accesses two different data sources:</span><span class="sxs-lookup"><span data-stu-id="21763-125">This solution accesses two different data sources:</span></span> 

* <span data-ttu-id="21763-126">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span><span class="sxs-lookup"><span data-stu-id="21763-126">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="21763-127">**Vehicle catalog**: This reference data set maps VIN numbers to models.</span><span class="sxs-lookup"><span data-stu-id="21763-127">**Vehicle catalog**: This reference data set maps VIN numbers to models.</span></span>

