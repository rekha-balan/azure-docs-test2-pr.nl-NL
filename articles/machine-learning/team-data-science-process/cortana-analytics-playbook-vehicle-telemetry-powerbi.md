---
title: Power BI dashboard for vehicle health and driving habits - Azure | Microsoft Docs
description: Use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.
services: machine-learning
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2018
ms.author: deguhath
ms.openlocfilehash: e6601093577eb9e3dfba4ed27e1e0510cad17de7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857005"
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="74753-103">Vehicle Telemetry Analytics Solution Template Power BI dashboard setup instructions</span><span class="sxs-lookup"><span data-stu-id="74753-103">Vehicle Telemetry Analytics Solution Template Power BI dashboard setup instructions</span></span>
<span data-ttu-id="74753-104">This menu links to the chapters in this playbook:</span><span class="sxs-lookup"><span data-stu-id="74753-104">This menu links to the chapters in this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="74753-105">The Vehicle Telemetry Analytics Solution showcases how car dealerships, automobile manufacturers, and insurance companies are able use the capabilities of Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="74753-105">The Vehicle Telemetry Analytics Solution showcases how car dealerships, automobile manufacturers, and insurance companies are able use the capabilities of Cortana Intelligence.</span></span> <span data-ttu-id="74753-106">They can obtain real-time and predictive insights on vehicle health and driving habits to improve customer experience, research and development, and marketing campaigns.</span><span class="sxs-lookup"><span data-stu-id="74753-106">They can obtain real-time and predictive insights on vehicle health and driving habits to improve customer experience, research and development, and marketing campaigns.</span></span> <span data-ttu-id="74753-107">These step-by-step instructions show how to configure the Power BI reports and dashboard after you deploy the solution in your subscription.</span><span class="sxs-lookup"><span data-stu-id="74753-107">These step-by-step instructions show how to configure the Power BI reports and dashboard after you deploy the solution in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="74753-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="74753-108">Prerequisites</span></span>
* <span data-ttu-id="74753-109">Deploy the [Vehicle Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) Solution.</span><span class="sxs-lookup"><span data-stu-id="74753-109">Deploy the [Vehicle Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) Solution.</span></span> 
* <span data-ttu-id="74753-110">[Install Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="74753-110">[Install Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span></span>
* <span data-ttu-id="74753-111">Obtain an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74753-111">Obtain an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="74753-112">If you don't have an Azure subscription, get started with the Azure free subscription.</span><span class="sxs-lookup"><span data-stu-id="74753-112">If you don't have an Azure subscription, get started with the Azure free subscription.</span></span>
* <span data-ttu-id="74753-113">Open a Power BI account.</span><span class="sxs-lookup"><span data-stu-id="74753-113">Open a Power BI account.</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="74753-114">Cortana Intelligence suite components</span><span class="sxs-lookup"><span data-stu-id="74753-114">Cortana Intelligence suite components</span></span>
<span data-ttu-id="74753-115">As part of the Vehicle Telemetry Analytics Solution Template, the following Cortana Intelligence services are deployed in your subscription:</span><span class="sxs-lookup"><span data-stu-id="74753-115">As part of the Vehicle Telemetry Analytics Solution Template, the following Cortana Intelligence services are deployed in your subscription:</span></span>

* <span data-ttu-id="74753-116">**Azure Event Hubs** ingests millions of vehicle telemetry events into Azure.</span><span class="sxs-lookup"><span data-stu-id="74753-116">**Azure Event Hubs** ingests millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="74753-117">**Azure Stream Analytics** provides real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span><span class="sxs-lookup"><span data-stu-id="74753-117">**Azure Stream Analytics** provides real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="74753-118">**Azure Machine Learning** detects anomalies in real time, and uses batch processing to provide predictive insights.</span><span class="sxs-lookup"><span data-stu-id="74753-118">**Azure Machine Learning** detects anomalies in real time, and uses batch processing to provide predictive insights.</span></span>
* <span data-ttu-id="74753-119">**Azure HDInsight** transforms data at scale.</span><span class="sxs-lookup"><span data-stu-id="74753-119">**Azure HDInsight** transforms data at scale.</span></span>
* <span data-ttu-id="74753-120">**Azure Data Factory** handles orchestration, scheduling, resource management, and monitoring of the batch processing pipeline.</span><span class="sxs-lookup"><span data-stu-id="74753-120">**Azure Data Factory** handles orchestration, scheduling, resource management, and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="74753-121">**Power BI** gives this solution a rich dashboard for data and predictive analytics visualizations.</span><span class="sxs-lookup"><span data-stu-id="74753-121">**Power BI** gives this solution a rich dashboard for data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="74753-122">The solution uses two different data sources:</span><span class="sxs-lookup"><span data-stu-id="74753-122">The solution uses two different data sources:</span></span>

* <span data-ttu-id="74753-123">Simulated vehicle signals and diagnostic data sets</span><span class="sxs-lookup"><span data-stu-id="74753-123">Simulated vehicle signals and diagnostic data sets</span></span>
* <span data-ttu-id="74753-124">Vehicle catalog</span><span class="sxs-lookup"><span data-stu-id="74753-124">Vehicle catalog</span></span>

<span data-ttu-id="74753-125">A vehicle telematics simulator is included as part of this solution.</span><span class="sxs-lookup"><span data-stu-id="74753-125">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="74753-126">It emits diagnostic information and signals that correspond to the state of the vehicle and driving patterns at a given point in time.</span><span class="sxs-lookup"><span data-stu-id="74753-126">It emits diagnostic information and signals that correspond to the state of the vehicle and driving patterns at a given point in time.</span></span> 

<span data-ttu-id="74753-127">The vehicle catalog is a reference data set that maps VINs to models.</span><span class="sxs-lookup"><span data-stu-id="74753-127">The vehicle catalog is a reference data set that maps VINs to models.</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="74753-128">Power BI dashboard preparation</span><span class="sxs-lookup"><span data-stu-id="74753-128">Power BI dashboard preparation</span></span>
### <a name="set-up-the-power-bi-real-time-dashboard"></a><span data-ttu-id="74753-129">Set up the Power BI real-time dashboard</span><span class="sxs-lookup"><span data-stu-id="74753-129">Set up the Power BI real-time dashboard</span></span>

#### <a name="start-the-real-time-dashboard-application"></a><span data-ttu-id="74753-130">Start the real-time dashboard application</span><span class="sxs-lookup"><span data-stu-id="74753-130">Start the real-time dashboard application</span></span>
<span data-ttu-id="74753-131">After the deployment is finished, follow the manual operation instructions.</span><span class="sxs-lookup"><span data-stu-id="74753-131">After the deployment is finished, follow the manual operation instructions.</span></span>

1. <span data-ttu-id="74753-132">Download the real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span><span class="sxs-lookup"><span data-stu-id="74753-132">Download the real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>

1.  <span data-ttu-id="74753-133">In the unzipped folder, open the app config file RealtimeDashboardApp.exe.config. Replace appSettings for Event Hubs, Azure Blob storage, and Azure Machine Learning service connections with the values in the manual operation instructions.</span><span class="sxs-lookup"><span data-stu-id="74753-133">In the unzipped folder, open the app config file RealtimeDashboardApp.exe.config. Replace appSettings for Event Hubs, Azure Blob storage, and Azure Machine Learning service connections with the values in the manual operation instructions.</span></span> <span data-ttu-id="74753-134">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="74753-134">Save your changes.</span></span>

1. <span data-ttu-id="74753-135">Run the application RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="74753-135">Run the application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="74753-136">On the sign-in window, enter your valid Power BI credentials.</span><span class="sxs-lookup"><span data-stu-id="74753-136">On the sign-in window, enter your valid Power BI credentials.</span></span> 

   ![Power BI sign-in window](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
1. <span data-ttu-id="74753-138">Select **Accept**.</span><span class="sxs-lookup"><span data-stu-id="74753-138">Select **Accept**.</span></span> <span data-ttu-id="74753-139">The app starts to run.</span><span class="sxs-lookup"><span data-stu-id="74753-139">The app starts to run.</span></span>

   ![Power BI dashboard permissions](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

1. <span data-ttu-id="74753-141">Sign in to the Power BI website, and create a real-time dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-141">Sign in to the Power BI website, and create a real-time dashboard.</span></span>

<span data-ttu-id="74753-142">Now you're ready to configure the Power BI dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-142">Now you're ready to configure the Power BI dashboard.</span></span>  

### <a name="configure-power-bi-reports"></a><span data-ttu-id="74753-143">Configure Power BI reports</span><span class="sxs-lookup"><span data-stu-id="74753-143">Configure Power BI reports</span></span>
<span data-ttu-id="74753-144">The real-time reports and the dashboard take about 30 to 45 minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="74753-144">The real-time reports and the dashboard take about 30 to 45 minutes to finish.</span></span> 

1. <span data-ttu-id="74753-145">Browse to the [Power BI](http://powerbi.com) webpage, and sign in.</span><span class="sxs-lookup"><span data-stu-id="74753-145">Browse to the [Power BI](http://powerbi.com) webpage, and sign in.</span></span>

    ![Power BI sign-in page](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

1. <span data-ttu-id="74753-147">A new data set is generated in Power BI.</span><span class="sxs-lookup"><span data-stu-id="74753-147">A new data set is generated in Power BI.</span></span> <span data-ttu-id="74753-148">Select the **ConnectedCarsRealtime** data set.</span><span class="sxs-lookup"><span data-stu-id="74753-148">Select the **ConnectedCarsRealtime** data set.</span></span>

    ![ConnectedCarsRealtime data set](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

1. <span data-ttu-id="74753-150">To save the blank report, press Ctrl+S.</span><span class="sxs-lookup"><span data-stu-id="74753-150">To save the blank report, press Ctrl+S.</span></span>

    ![Blank report](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

1. <span data-ttu-id="74753-152">Enter the report name **Vehicle Telemetry Analytics Real-time - Reports**.</span><span class="sxs-lookup"><span data-stu-id="74753-152">Enter the report name **Vehicle Telemetry Analytics Real-time - Reports**.</span></span>

    ![Report name](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="74753-154">Real-time reports</span><span class="sxs-lookup"><span data-stu-id="74753-154">Real-time reports</span></span>
<span data-ttu-id="74753-155">Three real-time reports are in this solution:</span><span class="sxs-lookup"><span data-stu-id="74753-155">Three real-time reports are in this solution:</span></span>

* <span data-ttu-id="74753-156">Vehicles in Operation</span><span class="sxs-lookup"><span data-stu-id="74753-156">Vehicles in Operation</span></span>
* <span data-ttu-id="74753-157">Vehicles Requiring Maintenance</span><span class="sxs-lookup"><span data-stu-id="74753-157">Vehicles Requiring Maintenance</span></span>
* <span data-ttu-id="74753-158">Vehicle Health Statistics</span><span class="sxs-lookup"><span data-stu-id="74753-158">Vehicle Health Statistics</span></span>

<span data-ttu-id="74753-159">You can configure all three of the reports, or you can stop after any stage.</span><span class="sxs-lookup"><span data-stu-id="74753-159">You can configure all three of the reports, or you can stop after any stage.</span></span> <span data-ttu-id="74753-160">You then can proceed to the next section on how to configure batch reports.</span><span class="sxs-lookup"><span data-stu-id="74753-160">You then can proceed to the next section on how to configure batch reports.</span></span> <span data-ttu-id="74753-161">We recommend that you create all three reports to visualize the full insights of the real-time path of the solution.</span><span class="sxs-lookup"><span data-stu-id="74753-161">We recommend that you create all three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="vehicles-in-operation-report"></a><span data-ttu-id="74753-162">Vehicles in Operation report</span><span class="sxs-lookup"><span data-stu-id="74753-162">Vehicles in Operation report</span></span>
1. <span data-ttu-id="74753-163">Double-click **Page 1**, and rename it **Vehicles in Operation**.</span><span class="sxs-lookup"><span data-stu-id="74753-163">Double-click **Page 1**, and rename it **Vehicles in Operation**.</span></span>

    ![Vehicles in Operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

1. <span data-ttu-id="74753-165">On the **Fields** tab, select **vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-165">On the **Fields** tab, select **vin**.</span></span> <span data-ttu-id="74753-166">On the **Visualizations** tab, select the **Card** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-166">On the **Visualizations** tab, select the **Card** visualization.</span></span>  

    <span data-ttu-id="74753-167">The **Card** visualization is created as shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="74753-167">The **Card** visualization is created as shown in the following figure:</span></span>

    ![Select vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

1. <span data-ttu-id="74753-169">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-169">Select the blank area to add a new visualization.</span></span>  

1. <span data-ttu-id="74753-170">On the **Fields** tab, select **city** and **vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-170">On the **Fields** tab, select **city** and **vin**.</span></span> <span data-ttu-id="74753-171">On the **Visualizations** tab, select the **Map** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-171">On the **Visualizations** tab, select the **Map** visualization.</span></span> <span data-ttu-id="74753-172">Drag **vin** to the **Values** area.</span><span class="sxs-lookup"><span data-stu-id="74753-172">Drag **vin** to the **Values** area.</span></span> <span data-ttu-id="74753-173">Drag **city** to the **Legend** area.</span><span class="sxs-lookup"><span data-stu-id="74753-173">Drag **city** to the **Legend** area.</span></span> 

    ![Card visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

1. <span data-ttu-id="74753-175">On the **Visualizations** tab, select the **Format** section.</span><span class="sxs-lookup"><span data-stu-id="74753-175">On the **Visualizations** tab, select the **Format** section.</span></span> <span data-ttu-id="74753-176">Select **Title**, and change **Text** to **Vehicles in operation by city**.</span><span class="sxs-lookup"><span data-stu-id="74753-176">Select **Title**, and change **Text** to **Vehicles in operation by city**.</span></span>

    ![Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

    <span data-ttu-id="74753-178">The final visualization looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="74753-178">The final visualization looks like the following example:</span></span>

    ![Final visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

1. <span data-ttu-id="74753-180">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-180">Select the blank area to add a new visualization.</span></span>  

1. <span data-ttu-id="74753-181">On the **Fields** tab, select **city** and **vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-181">On the **Fields** tab, select **city** and **vin**.</span></span> <span data-ttu-id="74753-182">On the **Visualizations** tab, select the **Clustered Column Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-182">On the **Visualizations** tab, select the **Clustered Column Chart** visualization.</span></span> <span data-ttu-id="74753-183">Drag **city** to the **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-183">Drag **city** to the **Axis** area.</span></span> <span data-ttu-id="74753-184">Drag **vin** to the **Value** area.</span><span class="sxs-lookup"><span data-stu-id="74753-184">Drag **vin** to the **Value** area.</span></span>

1. <span data-ttu-id="74753-185">Sort the chart by **Count of vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-185">Sort the chart by **Count of vin**.</span></span>

    ![Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

1. <span data-ttu-id="74753-187">Change the chart **Title** to **Vehicles in operation by city**.</span><span class="sxs-lookup"><span data-stu-id="74753-187">Change the chart **Title** to **Vehicles in operation by city**.</span></span> 

1. <span data-ttu-id="74753-188">Select the **Format** section, and then select **Data Colors**.</span><span class="sxs-lookup"><span data-stu-id="74753-188">Select the **Format** section, and then select **Data Colors**.</span></span> <span data-ttu-id="74753-189">Change **Show All** to **On**.</span><span class="sxs-lookup"><span data-stu-id="74753-189">Change **Show All** to **On**.</span></span>

    ![Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

1. <span data-ttu-id="74753-191">Change the color of an individual city by selecting the color symbol.</span><span class="sxs-lookup"><span data-stu-id="74753-191">Change the color of an individual city by selecting the color symbol.</span></span>

    ![Color change](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

1. <span data-ttu-id="74753-193">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-193">Select the blank area to add a new visualization.</span></span>  

1. <span data-ttu-id="74753-194">On the **Visualizations** tab, select the **Clustered Column Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-194">On the **Visualizations** tab, select the **Clustered Column Chart** visualization.</span></span> <span data-ttu-id="74753-195">On the **Fields** tab, drag **city** to the **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-195">On the **Fields** tab, drag **city** to the **Axis** area.</span></span> <span data-ttu-id="74753-196">Drag **Model** to the **Legend** area.</span><span class="sxs-lookup"><span data-stu-id="74753-196">Drag **Model** to the **Legend** area.</span></span> <span data-ttu-id="74753-197">Drag **vin** to the **Value** area.</span><span class="sxs-lookup"><span data-stu-id="74753-197">Drag **vin** to the **Value** area.</span></span>

    ![Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)

    <span data-ttu-id="74753-199">The chart looks like the following image:</span><span class="sxs-lookup"><span data-stu-id="74753-199">The chart looks like the following image:</span></span>

    ![Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

1. <span data-ttu-id="74753-201">Rearrange all the visualizations so that the page looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="74753-201">Rearrange all the visualizations so that the page looks like the following example:</span></span>

    ![Dashboard with visualizations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="74753-203">You successfully configured the "Vehicles in Operation" report.</span><span class="sxs-lookup"><span data-stu-id="74753-203">You successfully configured the "Vehicles in Operation" report.</span></span> <span data-ttu-id="74753-204">You can create the next real-time report, or you can stop here and configure the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-204">You can create the next real-time report, or you can stop here and configure the dashboard.</span></span> 

### <a name="vehicles-requiring-maintenance-report"></a><span data-ttu-id="74753-205">Vehicles Requiring Maintenance report</span><span class="sxs-lookup"><span data-stu-id="74753-205">Vehicles Requiring Maintenance report</span></span>

1. <span data-ttu-id="74753-206">Select ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report.</span><span class="sxs-lookup"><span data-stu-id="74753-206">Select ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report.</span></span> <span data-ttu-id="74753-207">Rename it **Vehicles Requiring Maintenance**.</span><span class="sxs-lookup"><span data-stu-id="74753-207">Rename it **Vehicles Requiring Maintenance**.</span></span>

    ![Vehicles Requiring Maintenance](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

1. <span data-ttu-id="74753-209">On the **Fields** tab, select **vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-209">On the **Fields** tab, select **vin**.</span></span> <span data-ttu-id="74753-210">On the **Visualizations** tab, select the **Card** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-210">On the **Visualizations** tab, select the **Card** visualization.</span></span>

    ![Vin Card visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

    <span data-ttu-id="74753-212">The data set contains a field named **MaintenanceLabel**.</span><span class="sxs-lookup"><span data-stu-id="74753-212">The data set contains a field named **MaintenanceLabel**.</span></span> <span data-ttu-id="74753-213">This field can have a value of "0" or "1."</span><span class="sxs-lookup"><span data-stu-id="74753-213">This field can have a value of "0" or "1."</span></span> <span data-ttu-id="74753-214">The value is set by the machine learning model that's provisioned as part of the solution.</span><span class="sxs-lookup"><span data-stu-id="74753-214">The value is set by the machine learning model that's provisioned as part of the solution.</span></span> <span data-ttu-id="74753-215">It's integrated with the real-time path.</span><span class="sxs-lookup"><span data-stu-id="74753-215">It's integrated with the real-time path.</span></span> <span data-ttu-id="74753-216">The value "1" indicates that a vehicle requires maintenance.</span><span class="sxs-lookup"><span data-stu-id="74753-216">The value "1" indicates that a vehicle requires maintenance.</span></span> 

1. <span data-ttu-id="74753-217">To add a **Page Level Filter** to show data for the vehicles that require maintenance:</span><span class="sxs-lookup"><span data-stu-id="74753-217">To add a **Page Level Filter** to show data for the vehicles that require maintenance:</span></span> 

   <span data-ttu-id="74753-218">a.</span><span class="sxs-lookup"><span data-stu-id="74753-218">a.</span></span> <span data-ttu-id="74753-219">Drag the **MaintenanceLabel** field to **Page Level Filters**.</span><span class="sxs-lookup"><span data-stu-id="74753-219">Drag the **MaintenanceLabel** field to **Page Level Filters**.</span></span>
  
      ![Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)

    <span data-ttu-id="74753-221">b.</span><span class="sxs-lookup"><span data-stu-id="74753-221">b.</span></span> <span data-ttu-id="74753-222">At the bottom of **Page Level Filters MaintenanceLabel**, select **Basic Filtering**.</span><span class="sxs-lookup"><span data-stu-id="74753-222">At the bottom of **Page Level Filters MaintenanceLabel**, select **Basic Filtering**.</span></span>

      ![Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png) 

    <span data-ttu-id="74753-224">c.</span><span class="sxs-lookup"><span data-stu-id="74753-224">c.</span></span> <span data-ttu-id="74753-225">Set the filter value to **1**.</span><span class="sxs-lookup"><span data-stu-id="74753-225">Set the filter value to **1**.</span></span>

      ![Filter value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

1. <span data-ttu-id="74753-227">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-227">Select the blank area to add a new visualization.</span></span>  

1. <span data-ttu-id="74753-228">On the **Visualizations** tab, select the **Clustered Column Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-228">On the **Visualizations** tab, select the **Clustered Column Chart** visualization.</span></span> 

    ![Vin Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)

    ![Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

1. <span data-ttu-id="74753-231">On the **Fields** tab, drag **Model** to the **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-231">On the **Fields** tab, drag **Model** to the **Axis** area.</span></span> <span data-ttu-id="74753-232">Drag **vin** to the **Value** area.</span><span class="sxs-lookup"><span data-stu-id="74753-232">Drag **vin** to the **Value** area.</span></span> <span data-ttu-id="74753-233">Then sort the visualization by **Count of vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-233">Then sort the visualization by **Count of vin**.</span></span> <span data-ttu-id="74753-234">Change the chart **Title** to **Vehicles requiring maintenance by model**.</span><span class="sxs-lookup"><span data-stu-id="74753-234">Change the chart **Title** to **Vehicles requiring maintenance by model**.</span></span> 

1. <span data-ttu-id="74753-235">On the **Fields** ![Fields-image](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of the **Visualizations** tab, drag **vin** to **Color Saturation**.</span><span class="sxs-lookup"><span data-stu-id="74753-235">On the **Fields** ![Fields-image](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of the **Visualizations** tab, drag **vin** to **Color Saturation**.</span></span>

    ![Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

1. <span data-ttu-id="74753-237">On the **Format** section, change **Data Colors** in the visualization:</span><span class="sxs-lookup"><span data-stu-id="74753-237">On the **Format** section, change **Data Colors** in the visualization:</span></span> 

    <span data-ttu-id="74753-238">a.</span><span class="sxs-lookup"><span data-stu-id="74753-238">a.</span></span> <span data-ttu-id="74753-239">Change the **Minimum** color to **F2C812**.</span><span class="sxs-lookup"><span data-stu-id="74753-239">Change the **Minimum** color to **F2C812**.</span></span>

    <span data-ttu-id="74753-240">b.</span><span class="sxs-lookup"><span data-stu-id="74753-240">b.</span></span> <span data-ttu-id="74753-241">Change the **Maximum** color to **FF6300**.</span><span class="sxs-lookup"><span data-stu-id="74753-241">Change the **Maximum** color to **FF6300**.</span></span>

    ![New data colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)

    <span data-ttu-id="74753-243">The new visualization colors look like the following example:</span><span class="sxs-lookup"><span data-stu-id="74753-243">The new visualization colors look like the following example:</span></span>

    ![New visualization colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

1. <span data-ttu-id="74753-245">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-245">Select the blank area to add a new visualization.</span></span>  

1. <span data-ttu-id="74753-246">On the **Visualizations** tab, select **Clustered Column Chart**.</span><span class="sxs-lookup"><span data-stu-id="74753-246">On the **Visualizations** tab, select **Clustered Column Chart**.</span></span> <span data-ttu-id="74753-247">Drag **vin** to the **Value** area.</span><span class="sxs-lookup"><span data-stu-id="74753-247">Drag **vin** to the **Value** area.</span></span> <span data-ttu-id="74753-248">Drag **city** to the **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-248">Drag **city** to the **Axis** area.</span></span> <span data-ttu-id="74753-249">Sort the chart by **Count of vin**.</span><span class="sxs-lookup"><span data-stu-id="74753-249">Sort the chart by **Count of vin**.</span></span> <span data-ttu-id="74753-250">Change the chart **Title** to **Vehicles requiring maintenance by city**.</span><span class="sxs-lookup"><span data-stu-id="74753-250">Change the chart **Title** to **Vehicles requiring maintenance by city**.</span></span>

    ![Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

1. <span data-ttu-id="74753-252">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-252">Select the blank area to add a new visualization.</span></span>  

1. <span data-ttu-id="74753-253">On the **Visualizations** tab, select the **Multi-Row Card** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-253">On the **Visualizations** tab, select the **Multi-Row Card** visualization.</span></span> <span data-ttu-id="74753-254">Drag **Model** and **vin** to the **Fields** area.</span><span class="sxs-lookup"><span data-stu-id="74753-254">Drag **Model** and **vin** to the **Fields** area.</span></span>

    ![Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

1. <span data-ttu-id="74753-256">Rearrange all the visualizations so that the final report looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="74753-256">Rearrange all the visualizations so that the final report looks like the following example:</span></span> 

    ![Rearranged final report](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="74753-258">You successfully configured the "Vehicles Requiring Maintenance" real-time report.</span><span class="sxs-lookup"><span data-stu-id="74753-258">You successfully configured the "Vehicles Requiring Maintenance" real-time report.</span></span> <span data-ttu-id="74753-259">You can create the next real-time report, or you can stop here and configure the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-259">You can create the next real-time report, or you can stop here and configure the dashboard.</span></span> 

### <a name="vehicle-health-statistics-report"></a><span data-ttu-id="74753-260">Vehicle Health Statistics report</span><span class="sxs-lookup"><span data-stu-id="74753-260">Vehicle Health Statistics report</span></span>

1. <span data-ttu-id="74753-261">Select ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report.</span><span class="sxs-lookup"><span data-stu-id="74753-261">Select ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report.</span></span> <span data-ttu-id="74753-262">Rename it **Vehicles Health Statistics**.</span><span class="sxs-lookup"><span data-stu-id="74753-262">Rename it **Vehicles Health Statistics**.</span></span> 

1. <span data-ttu-id="74753-263">On the **Visualizations** tab, select the **Gauge** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-263">On the **Visualizations** tab, select the **Gauge** visualization.</span></span> <span data-ttu-id="74753-264">Drag **speed** to the **Value**, **Minimum Value**, and **Maximum Value** areas.</span><span class="sxs-lookup"><span data-stu-id="74753-264">Drag **speed** to the **Value**, **Minimum Value**, and **Maximum Value** areas.</span></span>

   ![Vehicles Health Statistics](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

1. <span data-ttu-id="74753-266">In the **Value** area, change the default aggregation of **speed** to **Average**.</span><span class="sxs-lookup"><span data-stu-id="74753-266">In the **Value** area, change the default aggregation of **speed** to **Average**.</span></span>

1. <span data-ttu-id="74753-267">In the **Minimum Value** area, change the default aggregation of **speed** to **Minimum**.</span><span class="sxs-lookup"><span data-stu-id="74753-267">In the **Minimum Value** area, change the default aggregation of **speed** to **Minimum**.</span></span>

1. <span data-ttu-id="74753-268">In the **Maximum Value** area, change the default aggregation of **speed** to **Maximum**.</span><span class="sxs-lookup"><span data-stu-id="74753-268">In the **Maximum Value** area, change the default aggregation of **speed** to **Maximum**.</span></span>

   ![Speed values](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

1. <span data-ttu-id="74753-270">Rename the **Gauge Title** to **Average speed**.</span><span class="sxs-lookup"><span data-stu-id="74753-270">Rename the **Gauge Title** to **Average speed**.</span></span>

   ![Gauge](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

1. <span data-ttu-id="74753-272">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-272">Select the blank area to add a new visualization.</span></span>  

    <span data-ttu-id="74753-273">Similarly, add a **Gauge** for **Average engine oil**, **Average fuel**, and **Average engine temperature**.</span><span class="sxs-lookup"><span data-stu-id="74753-273">Similarly, add a **Gauge** for **Average engine oil**, **Average fuel**, and **Average engine temperature**.</span></span>  

1. <span data-ttu-id="74753-274">Change the default aggregation of fields in each gauge like you did in the previous steps in the **Average speed** gauge.</span><span class="sxs-lookup"><span data-stu-id="74753-274">Change the default aggregation of fields in each gauge like you did in the previous steps in the **Average speed** gauge.</span></span>

    ![Additional gauges](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

1. <span data-ttu-id="74753-276">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-276">Select the blank area to add a new visualization.</span></span>

1. <span data-ttu-id="74753-277">On the **Visualizations** tab, select the **Line and Clustered Column Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-277">On the **Visualizations** tab, select the **Line and Clustered Column Chart** visualization.</span></span> <span data-ttu-id="74753-278">Drag **city** to **Shared Axis**.</span><span class="sxs-lookup"><span data-stu-id="74753-278">Drag **city** to **Shared Axis**.</span></span> <span data-ttu-id="74753-279">Drag **tirepressure**, **engineoil**, and **speed** to the **Column Values** area.</span><span class="sxs-lookup"><span data-stu-id="74753-279">Drag **tirepressure**, **engineoil**, and **speed** to the **Column Values** area.</span></span> <span data-ttu-id="74753-280">Change their aggregation type to **Average**.</span><span class="sxs-lookup"><span data-stu-id="74753-280">Change their aggregation type to **Average**.</span></span> 

1. <span data-ttu-id="74753-281">Drag **engineTemperature** to the **Line Values** area.</span><span class="sxs-lookup"><span data-stu-id="74753-281">Drag **engineTemperature** to the **Line Values** area.</span></span> <span data-ttu-id="74753-282">Change the aggregation type to **Average**.</span><span class="sxs-lookup"><span data-stu-id="74753-282">Change the aggregation type to **Average**.</span></span> 

    ![Column and Line Values](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

1. <span data-ttu-id="74753-284">Change the chart **Title** to **Average speed, tire pressure, engine oil, and engine temperature**.</span><span class="sxs-lookup"><span data-stu-id="74753-284">Change the chart **Title** to **Average speed, tire pressure, engine oil, and engine temperature**.</span></span>  

    ![Line and Clustered Column Chart title](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

1. <span data-ttu-id="74753-286">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-286">Select the blank area to add a new visualization.</span></span>

1. <span data-ttu-id="74753-287">On the **Visualizations** tab, select the **Treemap** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-287">On the **Visualizations** tab, select the **Treemap** visualization.</span></span> <span data-ttu-id="74753-288">Drag **Model** to the **Group** area.</span><span class="sxs-lookup"><span data-stu-id="74753-288">Drag **Model** to the **Group** area.</span></span> <span data-ttu-id="74753-289">Drag **MaintenanceProbability** to the **Values** area.</span><span class="sxs-lookup"><span data-stu-id="74753-289">Drag **MaintenanceProbability** to the **Values** area.</span></span>

1. <span data-ttu-id="74753-290">Change the chart **Title** to **Vehicle models requiring maintenance**.</span><span class="sxs-lookup"><span data-stu-id="74753-290">Change the chart **Title** to **Vehicle models requiring maintenance**.</span></span>

    ![Treemap title](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

1. <span data-ttu-id="74753-292">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-292">Select the blank area to add a new visualization.</span></span>

1. <span data-ttu-id="74753-293">On the **Visualizations** tab, select the **100% Stacked Bar Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-293">On the **Visualizations** tab, select the **100% Stacked Bar Chart** visualization.</span></span> <span data-ttu-id="74753-294">Drag **city** to the **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-294">Drag **city** to the **Axis** area.</span></span> <span data-ttu-id="74753-295">Drag **MaintenanceProbability** and **RecallProbability** to the **Value** area.</span><span class="sxs-lookup"><span data-stu-id="74753-295">Drag **MaintenanceProbability** and **RecallProbability** to the **Value** area.</span></span>

    ![Axis and Value areas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

1. <span data-ttu-id="74753-297">On the **Format** section, select **Data Colors**.</span><span class="sxs-lookup"><span data-stu-id="74753-297">On the **Format** section, select **Data Colors**.</span></span> <span data-ttu-id="74753-298">Set the **MaintenanceProbability** color to the value **F2C80F**.</span><span class="sxs-lookup"><span data-stu-id="74753-298">Set the **MaintenanceProbability** color to the value **F2C80F**.</span></span>

1. <span data-ttu-id="74753-299">Change the chart **Title** to **Probability of Vehicle Maintenance & Recall by City**.</span><span class="sxs-lookup"><span data-stu-id="74753-299">Change the chart **Title** to **Probability of Vehicle Maintenance & Recall by City**.</span></span>

    ![100% Stacked Bar Chart title](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

1. <span data-ttu-id="74753-301">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-301">Select the blank area to add a new visualization.</span></span>

1. <span data-ttu-id="74753-302">On the **Visualizations** tab, select the **Area Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-302">On the **Visualizations** tab, select the **Area Chart** visualization.</span></span> <span data-ttu-id="74753-303">Drag **Model** to the **Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-303">Drag **Model** to the **Axis** area.</span></span> <span data-ttu-id="74753-304">Drag **engineOil**, **tirepressure**, **speed**, and **MaintenanceProbability** to the **Values** area.</span><span class="sxs-lookup"><span data-stu-id="74753-304">Drag **engineOil**, **tirepressure**, **speed**, and **MaintenanceProbability** to the **Values** area.</span></span> <span data-ttu-id="74753-305">Change their aggregation type to **Average**.</span><span class="sxs-lookup"><span data-stu-id="74753-305">Change their aggregation type to **Average**.</span></span> 

    ![Aggregation type](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

1. <span data-ttu-id="74753-307">Change the chart **Title** to **Average engine oil, tire pressure, speed, and maintenance probability by model**.</span><span class="sxs-lookup"><span data-stu-id="74753-307">Change the chart **Title** to **Average engine oil, tire pressure, speed, and maintenance probability by model**.</span></span>

    ![Area Chart title](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

1. <span data-ttu-id="74753-309">Select the blank area to add a new visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-309">Select the blank area to add a new visualization.</span></span>

1. <span data-ttu-id="74753-310">On the **Visualizations** tab, select the **Scatter Chart** visualization.</span><span class="sxs-lookup"><span data-stu-id="74753-310">On the **Visualizations** tab, select the **Scatter Chart** visualization.</span></span> <span data-ttu-id="74753-311">Drag **Model** to the **Details** and **Legend** areas.</span><span class="sxs-lookup"><span data-stu-id="74753-311">Drag **Model** to the **Details** and **Legend** areas.</span></span> <span data-ttu-id="74753-312">Drag **fuel** to the **X-Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-312">Drag **fuel** to the **X-Axis** area.</span></span> <span data-ttu-id="74753-313">Change the aggregation to **Average**.</span><span class="sxs-lookup"><span data-stu-id="74753-313">Change the aggregation to **Average**.</span></span> <span data-ttu-id="74753-314">Drag **engineTemperature** to the **Y-Axis** area.</span><span class="sxs-lookup"><span data-stu-id="74753-314">Drag **engineTemperature** to the **Y-Axis** area.</span></span> <span data-ttu-id="74753-315">Change the aggregation to **Average**.</span><span class="sxs-lookup"><span data-stu-id="74753-315">Change the aggregation to **Average**.</span></span> <span data-ttu-id="74753-316">Drag **vin** to the **Size** area.</span><span class="sxs-lookup"><span data-stu-id="74753-316">Drag **vin** to the **Size** area.</span></span>

    ![Details, Legend, Axis, and Size areas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

1. <span data-ttu-id="74753-318">Change the chart **Title** to **Average of fuel, Average of engineTemperature, and Count of vin by Model**.</span><span class="sxs-lookup"><span data-stu-id="74753-318">Change the chart **Title** to **Average of fuel, Average of engineTemperature, and Count of vin by Model**.</span></span>

    ![Scatter Chart title](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

    <span data-ttu-id="74753-320">The final report looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="74753-320">The final report looks like the following example:</span></span>

    ![Final report](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="74753-322">Pin visualizations from the reports to the real-time dashboard</span><span class="sxs-lookup"><span data-stu-id="74753-322">Pin visualizations from the reports to the real-time dashboard</span></span>
1. <span data-ttu-id="74753-323">Create a blank dashboard by selecting the plus symbol next to **Dashboards**.</span><span class="sxs-lookup"><span data-stu-id="74753-323">Create a blank dashboard by selecting the plus symbol next to **Dashboards**.</span></span> <span data-ttu-id="74753-324">Enter the name **Vehicle Telemetry Analytics Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="74753-324">Enter the name **Vehicle Telemetry Analytics Dashboard**.</span></span>

    ![Dashboard plus symbol](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

1. <span data-ttu-id="74753-326">Pin the visualizations from the previous reports to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-326">Pin the visualizations from the previous reports to the dashboard.</span></span> 

    ![Dashboard pin symbol](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

    <span data-ttu-id="74753-328">When all three reports are pinned to the dashboard, it should look like the following example.</span><span class="sxs-lookup"><span data-stu-id="74753-328">When all three reports are pinned to the dashboard, it should look like the following example.</span></span> <span data-ttu-id="74753-329">If you didn't create all the reports, your dashboard might look different.</span><span class="sxs-lookup"><span data-stu-id="74753-329">If you didn't create all the reports, your dashboard might look different.</span></span> 

    ![Dashboard with reports](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="74753-331">You successfully created the real-time dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-331">You successfully created the real-time dashboard.</span></span> <span data-ttu-id="74753-332">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you see live updates on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-332">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you see live updates on the dashboard.</span></span> <span data-ttu-id="74753-333">The following steps take about 10 to 15 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="74753-333">The following steps take about 10 to 15 minutes to complete.</span></span>

## <a name="set-up-the-power-bi-batch-processing-dashboard"></a><span data-ttu-id="74753-334">Set up the Power BI batch processing dashboard</span><span class="sxs-lookup"><span data-stu-id="74753-334">Set up the Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="74753-335">It takes about two hours (from the successful completion of the deployment) for the end-to-end batch processing pipeline to finish execution and process a year's worth of generated data.</span><span class="sxs-lookup"><span data-stu-id="74753-335">It takes about two hours (from the successful completion of the deployment) for the end-to-end batch processing pipeline to finish execution and process a year's worth of generated data.</span></span> <span data-ttu-id="74753-336">Wait for the processing to finish before you proceed with the following steps:</span><span class="sxs-lookup"><span data-stu-id="74753-336">Wait for the processing to finish before you proceed with the following steps:</span></span>
> 
> 

### <a name="download-the-power-bi-designer-file"></a><span data-ttu-id="74753-337">Download the Power BI designer file</span><span class="sxs-lookup"><span data-stu-id="74753-337">Download the Power BI designer file</span></span>

1. <span data-ttu-id="74753-338">A preconfigured Power BI designer file is included as part of the deployment manual operation instructions.</span><span class="sxs-lookup"><span data-stu-id="74753-338">A preconfigured Power BI designer file is included as part of the deployment manual operation instructions.</span></span> <span data-ttu-id="74753-339">Look for "2.</span><span class="sxs-lookup"><span data-stu-id="74753-339">Look for "2.</span></span> <span data-ttu-id="74753-340">Set up the PowerBI batch processing dashboard."</span><span class="sxs-lookup"><span data-stu-id="74753-340">Set up the PowerBI batch processing dashboard."</span></span>

1. <span data-ttu-id="74753-341">Download the Power BI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="74753-341">Download the Power BI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>

1. <span data-ttu-id="74753-342">Save it locally.</span><span class="sxs-lookup"><span data-stu-id="74753-342">Save it locally.</span></span>

### <a name="configure-power-bi-reports"></a><span data-ttu-id="74753-343">Configure Power BI reports</span><span class="sxs-lookup"><span data-stu-id="74753-343">Configure Power BI reports</span></span>

1. <span data-ttu-id="74753-344">Open the designer file **ConnectedCarsPbiReport.pbix** by using the Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="74753-344">Open the designer file **ConnectedCarsPbiReport.pbix** by using the Power BI Desktop.</span></span> <span data-ttu-id="74753-345">If you don't already have it, install the Power BI Desktop from the [Power BI Desktop installation](http://www.microsoft.com/download/details.aspx?id=45331) website.</span><span class="sxs-lookup"><span data-stu-id="74753-345">If you don't already have it, install the Power BI Desktop from the [Power BI Desktop installation](http://www.microsoft.com/download/details.aspx?id=45331) website.</span></span>

1. <span data-ttu-id="74753-346">Select **Edit Queries**.</span><span class="sxs-lookup"><span data-stu-id="74753-346">Select **Edit Queries**.</span></span>

    ![Edit Queries](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

1. <span data-ttu-id="74753-348">Double-click **Source**.</span><span class="sxs-lookup"><span data-stu-id="74753-348">Double-click **Source**.</span></span>

    ![Source](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

1. <span data-ttu-id="74753-350">Update the server connection string with the Azure SQL server that got provisioned as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="74753-350">Update the server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span> <span data-ttu-id="74753-351">Look in the manual operation instructions under Azure SQL database:</span><span class="sxs-lookup"><span data-stu-id="74753-351">Look in the manual operation instructions under Azure SQL database:</span></span>

    * <span data-ttu-id="74753-352">Server: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="74753-352">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="74753-353">Database: connectedcar</span><span class="sxs-lookup"><span data-stu-id="74753-353">Database: connectedcar</span></span>
    * <span data-ttu-id="74753-354">Username: username</span><span class="sxs-lookup"><span data-stu-id="74753-354">Username: username</span></span>
    * <span data-ttu-id="74753-355">Password: You can manage your SQL Server password from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="74753-355">Password: You can manage your SQL Server password from the Azure portal.</span></span>

1. <span data-ttu-id="74753-356">Leave **Database** as **connectedcar**.</span><span class="sxs-lookup"><span data-stu-id="74753-356">Leave **Database** as **connectedcar**.</span></span>

    ![Database](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

1. <span data-ttu-id="74753-358">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="74753-358">Select **OK**.</span></span>

1. <span data-ttu-id="74753-359">The **Windows credential** tab is selected by default.</span><span class="sxs-lookup"><span data-stu-id="74753-359">The **Windows credential** tab is selected by default.</span></span> <span data-ttu-id="74753-360">Change it to **Database credentials** by selecting the **Database** tab at the right.</span><span class="sxs-lookup"><span data-stu-id="74753-360">Change it to **Database credentials** by selecting the **Database** tab at the right.</span></span>

1. <span data-ttu-id="74753-361">Enter the **Username** and **Password** of your Azure SQL database that was specified during its deployment setup.</span><span class="sxs-lookup"><span data-stu-id="74753-361">Enter the **Username** and **Password** of your Azure SQL database that was specified during its deployment setup.</span></span>

    ![Database credentials](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

1. <span data-ttu-id="74753-363">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="74753-363">Select **Connect**.</span></span>

1. <span data-ttu-id="74753-364">Repeat the previous steps for each of the three remaining queries present in the right pane.</span><span class="sxs-lookup"><span data-stu-id="74753-364">Repeat the previous steps for each of the three remaining queries present in the right pane.</span></span> <span data-ttu-id="74753-365">Then update the data source connection details.</span><span class="sxs-lookup"><span data-stu-id="74753-365">Then update the data source connection details.</span></span>

1. <span data-ttu-id="74753-366">Select **Close and Load**.</span><span class="sxs-lookup"><span data-stu-id="74753-366">Select **Close and Load**.</span></span> <span data-ttu-id="74753-367">Power BI Desktop file data sets are connected to SQL database tables.</span><span class="sxs-lookup"><span data-stu-id="74753-367">Power BI Desktop file data sets are connected to SQL database tables.</span></span>

1. <span data-ttu-id="74753-368">Select **Close** to close the Power BI Desktop file.</span><span class="sxs-lookup"><span data-stu-id="74753-368">Select **Close** to close the Power BI Desktop file.</span></span>

    ![Close](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

1. <span data-ttu-id="74753-370">Select **Save** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="74753-370">Select **Save** to save the changes.</span></span> 

<span data-ttu-id="74753-371">You have now configured all the reports that correspond to the batch processing path in the solution.</span><span class="sxs-lookup"><span data-stu-id="74753-371">You have now configured all the reports that correspond to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="74753-372">Upload to powerbi.com</span><span class="sxs-lookup"><span data-stu-id="74753-372">Upload to powerbi.com</span></span>
1. <span data-ttu-id="74753-373">Go to the [Power BI web portal](http://powerbi.com), and sign in.</span><span class="sxs-lookup"><span data-stu-id="74753-373">Go to the [Power BI web portal](http://powerbi.com), and sign in.</span></span>

1. <span data-ttu-id="74753-374">Select **Get Data**.</span><span class="sxs-lookup"><span data-stu-id="74753-374">Select **Get Data**.</span></span>

1. <span data-ttu-id="74753-375">Upload the Power BI Desktop file.</span><span class="sxs-lookup"><span data-stu-id="74753-375">Upload the Power BI Desktop file.</span></span> <span data-ttu-id="74753-376">Select **Get Data** > **Files Get** > **Local file**.</span><span class="sxs-lookup"><span data-stu-id="74753-376">Select **Get Data** > **Files Get** > **Local file**.</span></span>

1. <span data-ttu-id="74753-377">Go to **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="74753-377">Go to **ConnectedCarsPbiReport.pbix**.</span></span>

1. <span data-ttu-id="74753-378">After the file is uploaded, go back to your Power BI work space.</span><span class="sxs-lookup"><span data-stu-id="74753-378">After the file is uploaded, go back to your Power BI work space.</span></span> <span data-ttu-id="74753-379">A dataset, a report, and a blank dashboard are created for you.</span><span class="sxs-lookup"><span data-stu-id="74753-379">A dataset, a report, and a blank dashboard are created for you.</span></span>  

1. <span data-ttu-id="74753-380">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in Power BI.</span><span class="sxs-lookup"><span data-stu-id="74753-380">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in Power BI.</span></span> <span data-ttu-id="74753-381">Select the blank dashboard that was previously created, and then go to the **Reports** section.</span><span class="sxs-lookup"><span data-stu-id="74753-381">Select the blank dashboard that was previously created, and then go to the **Reports** section.</span></span> <span data-ttu-id="74753-382">Select the newly uploaded report.</span><span class="sxs-lookup"><span data-stu-id="74753-382">Select the newly uploaded report.</span></span>  

    ![New Power BI dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

    <span data-ttu-id="74753-384">The report has six pages:</span><span class="sxs-lookup"><span data-stu-id="74753-384">The report has six pages:</span></span>

    <span data-ttu-id="74753-385">Page 1: Vehicle density</span><span class="sxs-lookup"><span data-stu-id="74753-385">Page 1: Vehicle density</span></span>  
    <span data-ttu-id="74753-386">Page 2: Real-time vehicle health</span><span class="sxs-lookup"><span data-stu-id="74753-386">Page 2: Real-time vehicle health</span></span>  
    <span data-ttu-id="74753-387">Page 3: Aggressively driven vehicles</span><span class="sxs-lookup"><span data-stu-id="74753-387">Page 3: Aggressively driven vehicles</span></span>   
    <span data-ttu-id="74753-388">Page 4: Recalled vehicles</span><span class="sxs-lookup"><span data-stu-id="74753-388">Page 4: Recalled vehicles</span></span>  
    <span data-ttu-id="74753-389">Page 5: Fuel efficiently driven vehicles</span><span class="sxs-lookup"><span data-stu-id="74753-389">Page 5: Fuel efficiently driven vehicles</span></span>  
    <span data-ttu-id="74753-390">Page 6: Contoso Motors logo</span><span class="sxs-lookup"><span data-stu-id="74753-390">Page 6: Contoso Motors logo</span></span>  

    ![Power BI report with six pages](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

1. <span data-ttu-id="74753-392">From **Page 3**, pin the following content:</span><span class="sxs-lookup"><span data-stu-id="74753-392">From **Page 3**, pin the following content:</span></span>  

    <span data-ttu-id="74753-393">a.</span><span class="sxs-lookup"><span data-stu-id="74753-393">a.</span></span> <span data-ttu-id="74753-394">**Count of vin**</span><span class="sxs-lookup"><span data-stu-id="74753-394">**Count of vin**</span></span>  

   ![Page 3 Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png)

    <span data-ttu-id="74753-396">b.</span><span class="sxs-lookup"><span data-stu-id="74753-396">b.</span></span> <span data-ttu-id="74753-397">**Aggressively driven vehicles by model – Waterfall chart**</span><span class="sxs-lookup"><span data-stu-id="74753-397">**Aggressively driven vehicles by model – Waterfall chart**</span></span> 

   ![Page 3 chart 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

1. <span data-ttu-id="74753-399">From **Page 5**, pin the following content:</span><span class="sxs-lookup"><span data-stu-id="74753-399">From **Page 5**, pin the following content:</span></span> 

    <span data-ttu-id="74753-400">a.</span><span class="sxs-lookup"><span data-stu-id="74753-400">a.</span></span> <span data-ttu-id="74753-401">**Count of vin**</span><span class="sxs-lookup"><span data-stu-id="74753-401">**Count of vin**</span></span>

   ![Page 5 chart 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)

    <span data-ttu-id="74753-403">b.</span><span class="sxs-lookup"><span data-stu-id="74753-403">b.</span></span> <span data-ttu-id="74753-404">**Fuel-efficient vehicles by model: Clustered column chart**</span><span class="sxs-lookup"><span data-stu-id="74753-404">**Fuel-efficient vehicles by model: Clustered column chart**</span></span>

   ![Page 5 chart 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

1. <span data-ttu-id="74753-406">From **Page 4**, pin the following content:</span><span class="sxs-lookup"><span data-stu-id="74753-406">From **Page 4**, pin the following content:</span></span>  

    <span data-ttu-id="74753-407">a.</span><span class="sxs-lookup"><span data-stu-id="74753-407">a.</span></span> <span data-ttu-id="74753-408">**Count of vin**</span><span class="sxs-lookup"><span data-stu-id="74753-408">**Count of vin**</span></span> 

   ![Page 4 chart 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 

    <span data-ttu-id="74753-410">b.</span><span class="sxs-lookup"><span data-stu-id="74753-410">b.</span></span> <span data-ttu-id="74753-411">**Recalled vehicles by city, model: Treemap**</span><span class="sxs-lookup"><span data-stu-id="74753-411">**Recalled vehicles by city, model: Treemap**</span></span>

   ![Page 4 chart 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

1. <span data-ttu-id="74753-413">From **Page 6**, pin the following content:</span><span class="sxs-lookup"><span data-stu-id="74753-413">From **Page 6**, pin the following content:</span></span>  

    * <span data-ttu-id="74753-414">**Contoso Motors logo**</span><span class="sxs-lookup"><span data-stu-id="74753-414">**Contoso Motors logo**</span></span>

    ![Contoso Motors logo](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

### <a name="organize-the-dashboard"></a><span data-ttu-id="74753-416">Organize the dashboard</span><span class="sxs-lookup"><span data-stu-id="74753-416">Organize the dashboard</span></span>  

1. <span data-ttu-id="74753-417">Go to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74753-417">Go to the dashboard.</span></span>

1. <span data-ttu-id="74753-418">Hover over each chart.</span><span class="sxs-lookup"><span data-stu-id="74753-418">Hover over each chart.</span></span> <span data-ttu-id="74753-419">Rename each chart based on the naming provided in the following finished dashboard example:</span><span class="sxs-lookup"><span data-stu-id="74753-419">Rename each chart based on the naming provided in the following finished dashboard example:</span></span>

   ![Dashboard organization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png) 
   
1. <span data-ttu-id="74753-421">Move the charts around to look like the following dashboard example:</span><span class="sxs-lookup"><span data-stu-id="74753-421">Move the charts around to look like the following dashboard example:</span></span>

    ![Rearranged dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)

1. <span data-ttu-id="74753-423">After you create all the reports mentioned in this document, the final finished dashboard looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="74753-423">After you create all the reports mentioned in this document, the final finished dashboard looks like the following example:</span></span> 

   ![Final dashboard](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="74753-425">You have successfully created the reports and the dashboard to gain real-time, predictive, and batch insights on vehicle health and driving habits.</span><span class="sxs-lookup"><span data-stu-id="74753-425">You have successfully created the reports and the dashboard to gain real-time, predictive, and batch insights on vehicle health and driving habits.</span></span>  
