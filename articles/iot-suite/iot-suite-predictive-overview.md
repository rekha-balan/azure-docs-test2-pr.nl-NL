---
title: Predictive maintenance preconfigured solution | Microsoft Docs
description: A description of the Azure IoT Suite predictive maintenance preconfigured solution.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: dobett
ms.openlocfilehash: ddc3a0489fac70c2518000273a7a403a1d067aa4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556703"
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="6c95b-103">Predictive maintenance preconfigured solution overview</span><span class="sxs-lookup"><span data-stu-id="6c95b-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="6c95b-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span><span class="sxs-lookup"><span data-stu-id="6c95b-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="6c95b-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="6c95b-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="6c95b-106">With Azure IoT Suite, an enterprise can quickly and easily connect to and monitor assets, and analyze data in real time.</span><span class="sxs-lookup"><span data-stu-id="6c95b-106">With Azure IoT Suite, an enterprise can quickly and easily connect to and monitor assets, and analyze data in real time.</span></span> <span data-ttu-id="6c95b-107">The predictive maintenance preconfigured solution takes that data and uses rich dashboards and visualizations to provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span><span class="sxs-lookup"><span data-stu-id="6c95b-107">The predictive maintenance preconfigured solution takes that data and uses rich dashboards and visualizations to provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="6c95b-108">The Scenario</span><span class="sxs-lookup"><span data-stu-id="6c95b-108">The Scenario</span></span>
<span data-ttu-id="6c95b-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span><span class="sxs-lookup"><span data-stu-id="6c95b-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="6c95b-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span><span class="sxs-lookup"><span data-stu-id="6c95b-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="6c95b-111">Engine failure during flight must be avoided at all costs, so Fabrikam inspects its engines regularly and adheres to a scheduled maintenance program.</span><span class="sxs-lookup"><span data-stu-id="6c95b-111">Engine failure during flight must be avoided at all costs, so Fabrikam inspects its engines regularly and adheres to a scheduled maintenance program.</span></span> <span data-ttu-id="6c95b-112">However, aircraft engines don’t always wear the same.</span><span class="sxs-lookup"><span data-stu-id="6c95b-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="6c95b-113">Some unnecessary maintenance is performed on engines.</span><span class="sxs-lookup"><span data-stu-id="6c95b-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="6c95b-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span><span class="sxs-lookup"><span data-stu-id="6c95b-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="6c95b-115">These issues cause costly delays, especially if an aircraft is at a location where the right technicians or spare parts are not available.</span><span class="sxs-lookup"><span data-stu-id="6c95b-115">These issues cause costly delays, especially if an aircraft is at a location where the right technicians or spare parts are not available.</span></span>

<span data-ttu-id="6c95b-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span><span class="sxs-lookup"><span data-stu-id="6c95b-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="6c95b-117">Fabrikam uses the predictive maintenance preconfigured solution to collect the sensor data collected during the flight.</span><span class="sxs-lookup"><span data-stu-id="6c95b-117">Fabrikam uses the predictive maintenance preconfigured solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="6c95b-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="6c95b-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="6c95b-119">What they have identified is a correlation between the data from four of the engine sensors with the engine wear that leads to eventual failure.</span><span class="sxs-lookup"><span data-stu-id="6c95b-119">What they have identified is a correlation between the data from four of the engine sensors with the engine wear that leads to eventual failure.</span></span> <span data-ttu-id="6c95b-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span><span class="sxs-lookup"><span data-stu-id="6c95b-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="6c95b-121">The model uses the telemetry collected from the engines during the flight.</span><span class="sxs-lookup"><span data-stu-id="6c95b-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="6c95b-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span><span class="sxs-lookup"><span data-stu-id="6c95b-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="6c95b-123">The solution model uses actual engine wear data.</span><span class="sxs-lookup"><span data-stu-id="6c95b-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="6c95b-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span><span class="sxs-lookup"><span data-stu-id="6c95b-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span> <span data-ttu-id="6c95b-125">Maintenance coordinators work with schedulers:</span><span class="sxs-lookup"><span data-stu-id="6c95b-125">Maintenance coordinators work with schedulers:</span></span>

- <span data-ttu-id="6c95b-126">To plan maintenance to coincide with an aircraft stopping at a particular location.</span><span class="sxs-lookup"><span data-stu-id="6c95b-126">To plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="6c95b-127">To ensure there is sufficient time for the aircraft to be out of service without causing schedule disruption.</span><span class="sxs-lookup"><span data-stu-id="6c95b-127">To ensure there is sufficient time for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="6c95b-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span><span class="sxs-lookup"><span data-stu-id="6c95b-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="6c95b-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span><span class="sxs-lookup"><span data-stu-id="6c95b-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span> <span data-ttu-id="6c95b-130">All these factors enable Fabrikam to minimize aircraft ground time and to reduce operating costs while ensuring the safety of passengers and crew.</span><span class="sxs-lookup"><span data-stu-id="6c95b-130">All these factors enable Fabrikam to minimize aircraft ground time and to reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="6c95b-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="6c95b-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="6c95b-132">How the predictive maintenance solution is built</span><span class="sxs-lookup"><span data-stu-id="6c95b-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="6c95b-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span><span class="sxs-lookup"><span data-stu-id="6c95b-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="6c95b-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span><span class="sxs-lookup"><span data-stu-id="6c95b-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="6c95b-135">The Azure IoT predictive maintenance preconfigured solution uses the regression model created from this template.</span><span class="sxs-lookup"><span data-stu-id="6c95b-135">The Azure IoT predictive maintenance preconfigured solution uses the regression model created from this template.</span></span> <span data-ttu-id="6c95b-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span><span class="sxs-lookup"><span data-stu-id="6c95b-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="6c95b-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span><span class="sxs-lookup"><span data-stu-id="6c95b-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="6c95b-138">This data is sufficient to provide an accurate result from the trained model.</span><span class="sxs-lookup"><span data-stu-id="6c95b-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="6c95b-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="6c95b-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="6c95b-140">Get started with predictive maintenance</span><span class="sxs-lookup"><span data-stu-id="6c95b-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="6c95b-141">This tutorial shows you how to provision the predictive maintenance solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="6c95b-142">It also walks you through the basic features of the predictive maintenance solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="6c95b-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="6c95b-144">To complete this tutorial, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6c95b-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6c95b-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="6c95b-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6c95b-146">For details, see [Azure Free Trial][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="6c95b-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="6c95b-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="6c95b-148">Click **Select** the **Predictive maintenance** tile.</span><span class="sxs-lookup"><span data-stu-id="6c95b-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="6c95b-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="6c95b-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="6c95b-151">Click **Create Solution** to begin the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="6c95b-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="6c95b-152">This process typically takes several minutes to run.</span><span class="sxs-lookup"><span data-stu-id="6c95b-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="6c95b-153">Wait for the provisioning process to complete</span><span class="sxs-lookup"><span data-stu-id="6c95b-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="6c95b-154">Click the tile for your solution with **Provisioning** status.</span><span class="sxs-lookup"><span data-stu-id="6c95b-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="6c95b-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6c95b-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="6c95b-156">Once provisioning completes, the status changes to **Ready**.</span><span class="sxs-lookup"><span data-stu-id="6c95b-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="6c95b-157">Click the tile to see the details of your solution in the right-hand pane.</span><span class="sxs-lookup"><span data-stu-id="6c95b-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="6c95b-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="6c95b-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="6c95b-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="6c95b-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="6c95b-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="6c95b-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="6c95b-161">Are there details you'd expect to see that aren't listed for your solution?</span><span class="sxs-lookup"><span data-stu-id="6c95b-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="6c95b-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="6c95b-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="6c95b-163">View the solution</span><span class="sxs-lookup"><span data-stu-id="6c95b-163">View the solution</span></span>

<span data-ttu-id="6c95b-164">This section guides you through the solution UI.</span><span class="sxs-lookup"><span data-stu-id="6c95b-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="6c95b-165">Predictive Maintenance Dashboard</span><span class="sxs-lookup"><span data-stu-id="6c95b-165">Predictive Maintenance Dashboard</span></span>
<span data-ttu-id="6c95b-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span><span class="sxs-lookup"><span data-stu-id="6c95b-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="6c95b-167">The output data from the Stream Analytics jobs in blob storage.</span><span class="sxs-lookup"><span data-stu-id="6c95b-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="6c95b-168">The RUL and cycle count per aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="6c95b-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="6c95b-169">Observing the behavior of the cloud solution</span><span class="sxs-lookup"><span data-stu-id="6c95b-169">Observing the behavior of the cloud solution</span></span>
<span data-ttu-id="6c95b-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span><span class="sxs-lookup"><span data-stu-id="6c95b-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="6c95b-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="6c95b-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="6c95b-172">You can also navigate to the Machine Learning workspace from the tile on the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution when it’s in the **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="6c95b-172">You can also navigate to the Machine Learning workspace from the tile on the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution when it’s in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="6c95b-173">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span><span class="sxs-lookup"><span data-stu-id="6c95b-173">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="6c95b-174">When you first navigate to the solution portal, the simulation is stopped.</span><span class="sxs-lookup"><span data-stu-id="6c95b-174">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="6c95b-175">Click **Start simulation** to begin the simulation in which you see the sensor history, RUL, Cycles, and RUL history populate the dashboard.</span><span class="sxs-lookup"><span data-stu-id="6c95b-175">Click **Start simulation** to begin the simulation in which you see the sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="6c95b-176">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display and highlights the aircraft engine in yellow.</span><span class="sxs-lookup"><span data-stu-id="6c95b-176">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display and highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="6c95b-177">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span><span class="sxs-lookup"><span data-stu-id="6c95b-177">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="6c95b-178">This behavior results from the varying cycle lengths and the model accuracy.</span><span class="sxs-lookup"><span data-stu-id="6c95b-178">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="6c95b-179">The full simulation takes around 35 minutes to complete 148 cycles.</span><span class="sxs-lookup"><span data-stu-id="6c95b-179">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="6c95b-180">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span><span class="sxs-lookup"><span data-stu-id="6c95b-180">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="6c95b-181">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span><span class="sxs-lookup"><span data-stu-id="6c95b-181">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="6c95b-182">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span><span class="sxs-lookup"><span data-stu-id="6c95b-182">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c95b-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c95b-183">Next steps</span></span>

<span data-ttu-id="6c95b-184">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="6c95b-184">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="6c95b-185">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="6c95b-185">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance preconfigured solution.</span></span>

<span data-ttu-id="6c95b-186">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="6c95b-186">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="6c95b-187">[Frequently asked questions for IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="6c95b-187">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="6c95b-188">[IoT security from the ground up][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="6c95b-188">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-resource-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-suite/media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/



