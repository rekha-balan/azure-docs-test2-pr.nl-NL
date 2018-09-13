---
title: Power BI Dashboard for vehicle health and driving habits - Azure | Microsoft Docs
description: Use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: ebc5d9cd02aeb2491c6b6692a0de069530d554fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549295"
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="6a4d1-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span><span class="sxs-lookup"><span data-stu-id="6a4d1-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="6a4d1-104">This **menu** links to the chapters in this playbook.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="6a4d1-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="6a4d1-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6a4d1-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6a4d1-107">Prerequisites</span></span>
1. <span data-ttu-id="6a4d1-108">Deploy the Vehicle Telemetry Analytics solution by navigating to [https://gallery.cortanaintelligence.com/Solution/Vehicle-Telemetry-Analytics-9](https://gallery.cortanaintelligence.com/Solution/Vehicle-Telemetry-Analytics-9)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-108">Deploy the Vehicle Telemetry Analytics solution by navigating to [https://gallery.cortanaintelligence.com/Solution/Vehicle-Telemetry-Analytics-9](https://gallery.cortanaintelligence.com/Solution/Vehicle-Telemetry-Analytics-9)</span></span>  
2. [<span data-ttu-id="6a4d1-109">Install Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="6a4d1-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="6a4d1-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a4d1-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="6a4d1-111">If you don't have an Azure subscription, get started with Azure free subscription</span><span class="sxs-lookup"><span data-stu-id="6a4d1-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="6a4d1-112">Microsoft Power BI account</span><span class="sxs-lookup"><span data-stu-id="6a4d1-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="6a4d1-113">Cortana Intelligence Suite Components</span><span class="sxs-lookup"><span data-stu-id="6a4d1-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="6a4d1-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="6a4d1-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="6a4d1-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="6a4d1-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="6a4d1-118">**HDInsight** is leveraged to transform data at scale</span><span class="sxs-lookup"><span data-stu-id="6a4d1-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="6a4d1-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="6a4d1-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="6a4d1-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="6a4d1-122">A vehicle telematics simulator is included as part of this solution.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="6a4d1-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="6a4d1-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span><span class="sxs-lookup"><span data-stu-id="6a4d1-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="6a4d1-125">Power BI Dashboard Preparation</span><span class="sxs-lookup"><span data-stu-id="6a4d1-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="6a4d1-126">Setup Power BI Real-Time Dashboard</span><span class="sxs-lookup"><span data-stu-id="6a4d1-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="6a4d1-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span><span class="sxs-lookup"><span data-stu-id="6a4d1-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="6a4d1-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="6a4d1-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="6a4d1-130">Run application RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="6a4d1-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="6a4d1-132">Then the app will start to run.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-132">Then the app will start to run.</span></span>

   ![Sign-in to Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI Dashboard permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="6a4d1-135">Login to PowerBI website, and create real-time dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="6a4d1-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="6a4d1-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="6a4d1-138">Configure Power BI reports</span><span class="sxs-lookup"><span data-stu-id="6a4d1-138">Configure Power BI reports</span></span>
<span data-ttu-id="6a4d1-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="6a4d1-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Sign-in to Power BI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="6a4d1-142">A new dataset is generated in Power BI.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="6a4d1-143">Click the **ConnectedCarsRealtime** dataset.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Selecte connected cars real-time dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="6a4d1-145">Save the blank report using **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-145">Save the blank report using **Ctrl + s**.</span></span>

![Save blank report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="6a4d1-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Provide report name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="6a4d1-149">Real-time reports</span><span class="sxs-lookup"><span data-stu-id="6a4d1-149">Real-time reports</span></span>
<span data-ttu-id="6a4d1-150">There are three real-time reports in this solution:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="6a4d1-151">Vehicles in operation</span><span class="sxs-lookup"><span data-stu-id="6a4d1-151">Vehicles in operation</span></span>
2. <span data-ttu-id="6a4d1-152">Vehicles Requiring Maintenance</span><span class="sxs-lookup"><span data-stu-id="6a4d1-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="6a4d1-153">Vehicles Health Statistics</span><span class="sxs-lookup"><span data-stu-id="6a4d1-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="6a4d1-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="6a4d1-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="6a4d1-156">1. Vehicles in operation</span><span class="sxs-lookup"><span data-stu-id="6a4d1-156">1. Vehicles in operation</span></span>
<span data-ttu-id="6a4d1-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span><span class="sxs-lookup"><span data-stu-id="6a4d1-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="6a4d1-158">![Connected Cars - Vehicles in operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-158">![Connected Cars - Vehicles in operation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="6a4d1-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="6a4d1-160">Card visualization is created as shown in figure.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-160">Card visualization is created as shown in figure.</span></span>  
    ![Connected Cars - Select vin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="6a4d1-162">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-163">Select **City** and **vin** from fields.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="6a4d1-164">Change visualization to **“Map”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="6a4d1-165">Drag **vin** in values area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-165">Drag **vin** in values area.</span></span> <span data-ttu-id="6a4d1-166">Drag **city** from fields to **Legend** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="6a4d1-167">![Connected Cars - Card Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-167">![Connected Cars - Card Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="6a4d1-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="6a4d1-169">![Connected Cars - Vehicles in operation by city](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-169">![Connected Cars - Vehicles in operation by city](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="6a4d1-170">Final visualization looks as shown in figure.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-170">Final visualization looks as shown in figure.</span></span>    
    ![Connected Cars - Final visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="6a4d1-172">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="6a4d1-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="6a4d1-175">Sort chart by **“Count of vin”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="6a4d1-176">![Connected Cars - Count of vin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-176">![Connected Cars - Count of vin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="6a4d1-177">Change chart **Title** to **“Vehicles in operation by city”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="6a4d1-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="6a4d1-179">![Connected Cars - Show all Data Colors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-179">![Connected Cars - Show all Data Colors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="6a4d1-180">Change the color of individual city by clicking on color icon.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Connected Cars - Change Colors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="6a4d1-182">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="6a4d1-184">![Connected Cars - Clustered Column Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-184">![Connected Cars - Clustered Column Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="6a4d1-185">![Connected Cars - Rendering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-185">![Connected Cars - Rendering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="6a4d1-186">Rearrange all visualization on this page as shown in figure.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Connected Cars - Visualizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="6a4d1-188">You have successfully configured the “Vehicles in operation” real-time report.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="6a4d1-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="6a4d1-190">2. Vehicles Requiring Maintenance</span><span class="sxs-lookup"><span data-stu-id="6a4d1-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="6a4d1-191">Click ![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-191">Click ![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Connected Cars - Vehicles Requiring Maintenance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="6a4d1-193">Select **vin** field and change visualization type to **Card**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="6a4d1-194">![Connected Cars - Vin Card Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-194">![Connected Cars - Vin Card Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="6a4d1-195">We have a field named “MaintenanceLabel” In the dataset.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="6a4d1-196">This field can have a value of “0” or “1”.”</span><span class="sxs-lookup"><span data-stu-id="6a4d1-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="6a4d1-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="6a4d1-198">The value “1” indicates a vehicle requires maintenance.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="6a4d1-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="6a4d1-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="6a4d1-201">![Connected Cars - Page Level Filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-201">![Connected Cars - Page Level Filters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="6a4d1-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="6a4d1-203">![Connected Cars - Basic Filtering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-203">![Connected Cars - Basic Filtering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="6a4d1-204">Set its filter value to **“1”**  </span><span class="sxs-lookup"><span data-stu-id="6a4d1-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="6a4d1-205">![Connected Cars - Filter Value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-205">![Connected Cars - Filter Value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="6a4d1-206">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-207">Select **Clustered Column Chart** from visualizations</span><span class="sxs-lookup"><span data-stu-id="6a4d1-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="6a4d1-208">![Connected Cars - Vind Card Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-208">![Connected Cars - Vind Card Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="6a4d1-209">![Connected Cars - Clustered Column Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-209">![Connected Cars - Clustered Column Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="6a4d1-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="6a4d1-211">Then sort visualization by **Count of vin**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="6a4d1-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="6a4d1-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span><span class="sxs-lookup"><span data-stu-id="6a4d1-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="6a4d1-214">![Connected Cars - Color Saturation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-214">![Connected Cars - Color Saturation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="6a4d1-215">Change **Data Colors** in visualizations from **Format** section</span><span class="sxs-lookup"><span data-stu-id="6a4d1-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="6a4d1-216">Change Minimum color to: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="6a4d1-217">Change Maximum color to: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="6a4d1-218">![Connected Cars - Color Changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-218">![Connected Cars - Color Changes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="6a4d1-219">![Connected Cars - New Visualization Colors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-219">![Connected Cars - New Visualization Colors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="6a4d1-220">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="6a4d1-222">Sort chart by **“Count of vin”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="6a4d1-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span><span class="sxs-lookup"><span data-stu-id="6a4d1-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="6a4d1-224">![Connected Cars - Vehicles requiring maintenance by city](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-224">![Connected Cars - Vehicles requiring maintenance by city](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="6a4d1-225">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="6a4d1-227">![Connected Cars - Multi-Row Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-227">![Connected Cars - Multi-Row Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="6a4d1-228">Rearranging all of the visualization, the final report looks as follows:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Connected Cars - Multi-Row Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="6a4d1-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="6a4d1-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="6a4d1-232">3. Vehicles Health Statistics</span><span class="sxs-lookup"><span data-stu-id="6a4d1-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="6a4d1-233">Click ![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-233">Click ![Add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="6a4d1-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="6a4d1-235">![Connected Cars - Multi-Row Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="6a4d1-235">![Connected Cars - Multi-Row Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="6a4d1-236">Change the default aggregation of **speed** in **Value area** to **Average**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="6a4d1-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="6a4d1-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Connected Cars - Multi-Row Card](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="6a4d1-240">Rename the **Gauge Title** to **“Average speed”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Connected Cars - Gauge](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="6a4d1-242">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="6a4d1-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="6a4d1-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Connected Cars - Gauges](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="6a4d1-246">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="6a4d1-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="6a4d1-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Connected Cars - Visualizations Fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="6a4d1-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Connected Cars - Visualizations Fields](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="6a4d1-252">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="6a4d1-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="6a4d1-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Connected Cars - Change Chart Title](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="6a4d1-256">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="6a4d1-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Connected Cars - Add New Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="6a4d1-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="6a4d1-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Connected Cars - Add New Visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="6a4d1-262">Click the blank area to add new visualization.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="6a4d1-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="6a4d1-264">Change their aggregation type to **“Average”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-264">Change their aggregation type to **“Average”**.</span></span> 

![Connected Cars - Change Aggregation Type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="6a4d1-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Connected Cars - Change Chart Title](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="6a4d1-268">Click the blank area to add new visualization:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="6a4d1-269">Select **Scatter Chart** visualization from visualizations.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="6a4d1-270">Drag the **Model** field into the **Details** and **Legend** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="6a4d1-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="6a4d1-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="6a4d1-273">Drag the **vin** field into the **Size** area.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-273">Drag the **vin** field into the **Size** area.</span></span>

![Connected Cars - Add new visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="6a4d1-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Connected Cars - Change Chart Title](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="6a4d1-277">The final report will look like as shown below.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-277">The final report will look like as shown below.</span></span>

![Connected Cars-Final Report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="6a4d1-279">Pin visualizations from the reports to the real-time dashboard</span><span class="sxs-lookup"><span data-stu-id="6a4d1-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="6a4d1-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="6a4d1-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span><span class="sxs-lookup"><span data-stu-id="6a4d1-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Connected Cars-Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="6a4d1-283">Pin the visualization from the above reports to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Connected Cars-Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="6a4d1-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="6a4d1-286">If you have not created all the reports, your dashboard could look different.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Connected Cars-Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="6a4d1-288">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6a4d1-288">Congratulations!</span></span> <span data-ttu-id="6a4d1-289">You have successfully created the real-time dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="6a4d1-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="6a4d1-291">It should take about 10 to 15 minutes to complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="6a4d1-292">Setup Power BI batch processing dashboard</span><span class="sxs-lookup"><span data-stu-id="6a4d1-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="6a4d1-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="6a4d1-294">So wait for the processing to finish before proceeding with the next steps.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="6a4d1-295">**Download the Power BI designer file**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="6a4d1-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span><span class="sxs-lookup"><span data-stu-id="6a4d1-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="6a4d1-297">Look for 2.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-297">Look for 2.</span></span> <span data-ttu-id="6a4d1-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="6a4d1-299">Save locally</span><span class="sxs-lookup"><span data-stu-id="6a4d1-299">Save locally</span></span>

<span data-ttu-id="6a4d1-300">**Configure Power BI reports**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="6a4d1-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="6a4d1-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="6a4d1-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="6a4d1-303">Click the **Edit Queries**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-303">Click the **Edit Queries**.</span></span>

![Edit Power BI query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="6a4d1-305">Double-click the **Source**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-305">Double-click the **Source**.</span></span>

![Set Power BI source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="6a4d1-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="6a4d1-308">Look in the Manual Operation Instructions under</span><span class="sxs-lookup"><span data-stu-id="6a4d1-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="6a4d1-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6a4d1-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="6a4d1-310">Server: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="6a4d1-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="6a4d1-311">Database: connectedcar</span><span class="sxs-lookup"><span data-stu-id="6a4d1-311">Database: connectedcar</span></span>
    * <span data-ttu-id="6a4d1-312">Username: username</span><span class="sxs-lookup"><span data-stu-id="6a4d1-312">Username: username</span></span>
    * <span data-ttu-id="6a4d1-313">Password: You can manage your SQL server password from Azure portal</span><span class="sxs-lookup"><span data-stu-id="6a4d1-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="6a4d1-314">Leave **Database** as *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-314">Leave **Database** as *connectedcar*.</span></span>

![Set Power BI database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="6a4d1-316">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-316">Click **OK**.</span></span>
* <span data-ttu-id="6a4d1-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="6a4d1-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Provide database credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="6a4d1-320">Click **Connect**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-320">Click **Connect**</span></span>
* <span data-ttu-id="6a4d1-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="6a4d1-322">Click **Close and Load**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-322">Click **Close and Load**.</span></span> <span data-ttu-id="6a4d1-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="6a4d1-324">**Close** Power BI Desktop file.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-324">**Close** Power BI Desktop file.</span></span>

![Close Power BI desktop](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="6a4d1-326">Click **Save** button to save the changes.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="6a4d1-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="6a4d1-328">Upload to *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="6a4d1-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="6a4d1-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="6a4d1-330">Click **Get Data**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="6a4d1-331">Upload the Power BI Desktop File.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="6a4d1-332">To upload, click **Get Data -> Files Get -> Local file**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="6a4d1-333">Navigate to the **“** ConnectedCarsPbiReport.pbix **”**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-333">Navigate to the **“** ConnectedCarsPbiReport.pbix **”**</span></span>  
6. <span data-ttu-id="6a4d1-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="6a4d1-335">A dataset, report and a blank dashboard will be created for you.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="6a4d1-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="6a4d1-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Vehicle Telemetry Power BI.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="6a4d1-339">**Note the report has six pages:**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="6a4d1-340">Page 1: Vehicle density</span><span class="sxs-lookup"><span data-stu-id="6a4d1-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="6a4d1-341">Page 2: Real-time vehicle health</span><span class="sxs-lookup"><span data-stu-id="6a4d1-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="6a4d1-342">Page 3: Aggressively Driven Vehicles</span><span class="sxs-lookup"><span data-stu-id="6a4d1-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="6a4d1-343">Page 4: Recalled vehicles</span><span class="sxs-lookup"><span data-stu-id="6a4d1-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="6a4d1-344">Page 5: Fuel Efficiently Driven Vehicles</span><span class="sxs-lookup"><span data-stu-id="6a4d1-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="6a4d1-345">Page 6: Contoso Logo</span><span class="sxs-lookup"><span data-stu-id="6a4d1-345">Page 6: Contoso Logo</span></span>  

![Connected Cars Power BI.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="6a4d1-347">**From Page 3**, pin the following:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="6a4d1-348">Count of VIN</span><span class="sxs-lookup"><span data-stu-id="6a4d1-348">Count of VIN</span></span>  
   ![Connected Cars Power BI.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="6a4d1-350">Aggressively driven vehicles by model – Waterfall chart</span><span class="sxs-lookup"><span data-stu-id="6a4d1-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Vehicle Telemetry - Pin Charts 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="6a4d1-352">**From Page 5**, pin the following:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="6a4d1-353">Count of vin</span><span class="sxs-lookup"><span data-stu-id="6a4d1-353">Count of vin</span></span>    
   ![Vehicle Telemetry - Pin Charts 5](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="6a4d1-355">Fuel efficient vehicles by model: Clustered column chart</span><span class="sxs-lookup"><span data-stu-id="6a4d1-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Vehicle Telemetry - Pin Charts 6](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="6a4d1-357">**From Page 4**, pin the following:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="6a4d1-358">Count of vin</span><span class="sxs-lookup"><span data-stu-id="6a4d1-358">Count of vin</span></span>  
   ![Vehicle Telemetry - Pin Charts 7](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="6a4d1-360">Recalled vehicles by city, model: Treemap</span><span class="sxs-lookup"><span data-stu-id="6a4d1-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Vehicle Telemetry - Pin Charts 8](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="6a4d1-362">**From Page 6**, pin the following:</span><span class="sxs-lookup"><span data-stu-id="6a4d1-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="6a4d1-363">Contoso Motors logo</span><span class="sxs-lookup"><span data-stu-id="6a4d1-363">Contoso Motors logo</span></span>  
   ![Vehicle Telemetry - Pin Charts 9](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="6a4d1-365">**Organize the dashboard**</span><span class="sxs-lookup"><span data-stu-id="6a4d1-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="6a4d1-366">Navigate to the dashboard</span><span class="sxs-lookup"><span data-stu-id="6a4d1-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="6a4d1-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="6a4d1-368">Also move the charts around to look like the dashboard below.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Vehicle Telemetry - Organize Dashboard 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="6a4d1-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Vehicle Telemetry - Organize Dashboard 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="6a4d1-373">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6a4d1-373">Congratulations!</span></span> <span data-ttu-id="6a4d1-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="6a4d1-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  



































































