---
title: Try a cloud-based IoT predictive maintenance solution on Azure | Microsoft Docs
description: In this quickstart, you deploy the Predictive Maintenance Azure IoT solution accelerator, and sign in to and use the solution dashboard.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: quickstart
ms.custom: mvc
ms.date: 07/12/2018
ms.author: dobett
ms.openlocfilehash: 10ff6565ed8997a5cb87394aa0d743a0d94b67e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866562"
---
# <a name="quickstart-try-a-cloud-based-solution-to-run-a-predictive-maintenance-analysis-on-my-connected-devices"></a><span data-ttu-id="dbfa3-103">Quickstart: Try a cloud-based solution to run a predictive maintenance analysis on my connected devices</span><span class="sxs-lookup"><span data-stu-id="dbfa3-103">Quickstart: Try a cloud-based solution to run a predictive maintenance analysis on my connected devices</span></span>

<span data-ttu-id="dbfa3-104">This quickstart shows you how to deploy the Azure IoT Predictive Maintenance solution accelerator to run a cloud-based predictive maintenance simulation.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-104">This quickstart shows you how to deploy the Azure IoT Predictive Maintenance solution accelerator to run a cloud-based predictive maintenance simulation.</span></span> <span data-ttu-id="dbfa3-105">After you've deployed the solution accelerator, you use the solution **Dashboard** page to run a predictive maintenance analysis on data from a simulated aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-105">After you've deployed the solution accelerator, you use the solution **Dashboard** page to run a predictive maintenance analysis on data from a simulated aircraft engine.</span></span> <span data-ttu-id="dbfa3-106">You can use this solution accelerator as the starting point for your own implementation or as a learning tool.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-106">You can use this solution accelerator as the starting point for your own implementation or as a learning tool.</span></span>

<span data-ttu-id="dbfa3-107">In the simulation, Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-107">In the simulation, Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="dbfa3-108">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-108">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="dbfa3-109">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-109">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="dbfa3-110">However, aircraft engines don't always wear the same.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-110">However, aircraft engines don't always wear the same.</span></span> <span data-ttu-id="dbfa3-111">Some unnecessary maintenance is done on engines.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-111">Some unnecessary maintenance is done on engines.</span></span> <span data-ttu-id="dbfa3-112">More importantly, issues arise which can ground an aircraft until maintenance is done.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-112">More importantly, issues arise which can ground an aircraft until maintenance is done.</span></span> <span data-ttu-id="dbfa3-113">These issues can be especially costly if an aircraft is at a location where the right technicians or spare parts aren't available.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-113">These issues can be especially costly if an aircraft is at a location where the right technicians or spare parts aren't available.</span></span>

<span data-ttu-id="dbfa3-114">The engines of Fabrikam's aircraft are instrumented with sensors that monitor engine conditions during flight.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-114">The engines of Fabrikam's aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="dbfa3-115">After accumulating years of engine operational and failure data, Fabrikam's data scientists have developed a model to predict the Remaining Useful Life (RUL) of an aircraft engine.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-115">After accumulating years of engine operational and failure data, Fabrikam's data scientists have developed a model to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="dbfa3-116">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-116">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="dbfa3-117">While Fabrikam continues regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-117">While Fabrikam continues regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="dbfa3-118">Fabrikam can now predict future points of failure and plan for maintenance to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-118">Fabrikam can now predict future points of failure and plan for maintenance to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="dbfa3-119">To complete this quickstart, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-119">To complete this quickstart, you need an active Azure subscription.</span></span>

<span data-ttu-id="dbfa3-120">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-120">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="dbfa3-121">Deploy the solution</span><span class="sxs-lookup"><span data-stu-id="dbfa3-121">Deploy the solution</span></span>

<span data-ttu-id="dbfa3-122">When you deploy the solution accelerator to your Azure subscription, you must set some configuration options.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-122">When you deploy the solution accelerator to your Azure subscription, you must set some configuration options.</span></span>

<span data-ttu-id="dbfa3-123">Sign in to [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) using your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-123">Sign in to [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) using your Azure account credentials.</span></span>

<span data-ttu-id="dbfa3-124">Click **Try Now** on the **Predictive Maintenance** tile.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-124">Click **Try Now** on the **Predictive Maintenance** tile.</span></span>

![Choose Predictive Maintenance](./media/quickstart-predictive-maintenance-deploy/predictivemaintenance.png)

<span data-ttu-id="dbfa3-126">On the **Create Predictive Maintenance solution** page, enter a unique **Solution name** for your Predictive Maintenance solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-126">On the **Create Predictive Maintenance solution** page, enter a unique **Solution name** for your Predictive Maintenance solution accelerator.</span></span> <span data-ttu-id="dbfa3-127">For this quickstart, we're using **MyPredictiveMaintenance**.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-127">For this quickstart, we're using **MyPredictiveMaintenance**.</span></span>

<span data-ttu-id="dbfa3-128">Select the **Subscription** and **Region** you want to use to deploy the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-128">Select the **Subscription** and **Region** you want to use to deploy the solution accelerator.</span></span> <span data-ttu-id="dbfa3-129">Typically, you choose the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-129">Typically, you choose the region closest to you.</span></span> <span data-ttu-id="dbfa3-130">For this quickstart, we're using **Visual Studio Enterprise** and **East US**.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-130">For this quickstart, we're using **Visual Studio Enterprise** and **East US**.</span></span> <span data-ttu-id="dbfa3-131">You must be a [global administrator or user](iot-accelerators-permissions.md) in the subscription.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-131">You must be a [global administrator or user](iot-accelerators-permissions.md) in the subscription.</span></span>

<span data-ttu-id="dbfa3-132">Click **Create Solution** to begin the deployment.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-132">Click **Create Solution** to begin the deployment.</span></span> <span data-ttu-id="dbfa3-133">This process takes at least five minutes to run:</span><span class="sxs-lookup"><span data-stu-id="dbfa3-133">This process takes at least five minutes to run:</span></span>

![Predictive Maintenance solution details](./media/quickstart-predictive-maintenance-deploy/createform.png)

## <a name="sign-in-to-the-solution"></a><span data-ttu-id="dbfa3-135">Sign in to the solution</span><span class="sxs-lookup"><span data-stu-id="dbfa3-135">Sign in to the solution</span></span>

<span data-ttu-id="dbfa3-136">When the deployment to your Azure subscription is complete, you see a green checkmark and **Ready** on the solution tile.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-136">When the deployment to your Azure subscription is complete, you see a green checkmark and **Ready** on the solution tile.</span></span> <span data-ttu-id="dbfa3-137">You can now sign in to your Predictive Maintenance solution accelerator dashboard.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-137">You can now sign in to your Predictive Maintenance solution accelerator dashboard.</span></span>

<span data-ttu-id="dbfa3-138">On the **Provisioned solutions** page, click your new Predictive Maintenance solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-138">On the **Provisioned solutions** page, click your new Predictive Maintenance solution accelerator.</span></span> <span data-ttu-id="dbfa3-139">You can view information about the solution accelerator in the panel that appears.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-139">You can view information about the solution accelerator in the panel that appears.</span></span> <span data-ttu-id="dbfa3-140">Choose **Solution dashboard** to view your Predictive Maintenance solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="dbfa3-140">Choose **Solution dashboard** to view your Predictive Maintenance solution accelerator:</span></span>

![Solution panel](./media/quickstart-predictive-maintenance-deploy/solutionpanel.png)

<span data-ttu-id="dbfa3-142">Click **Accept** to accept the permissions request, the Predictive Maintenance solution dashboard displays in your browser:</span><span class="sxs-lookup"><span data-stu-id="dbfa3-142">Click **Accept** to accept the permissions request, the Predictive Maintenance solution dashboard displays in your browser:</span></span>

![Solution dashboard](./media/quickstart-predictive-maintenance-deploy/solutiondashboard.png)

<span data-ttu-id="dbfa3-144">Click **Start simulation** to begin the simulation.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-144">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="dbfa3-145">The sensor history, RUL, Cycles, and RUL history populate the dashboard:</span><span class="sxs-lookup"><span data-stu-id="dbfa3-145">The sensor history, RUL, Cycles, and RUL history populate the dashboard:</span></span>

![Simulation running](./media/quickstart-predictive-maintenance-deploy/simulationrunning.png)

<span data-ttu-id="dbfa3-147">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-147">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="dbfa3-148">The solution portal also highlights the aircraft engine in yellow.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-148">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="dbfa3-149">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-149">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="dbfa3-150">This behavior results from the varying cycle lengths and the model accuracy.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-150">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![Simulation warning](./media/quickstart-predictive-maintenance-deploy/simulationwarning.png)

<span data-ttu-id="dbfa3-152">The full simulation takes around 35 minutes to complete 148 cycles.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-152">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="dbfa3-153">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-153">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="dbfa3-154">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-154">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="dbfa3-155">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-155">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="dbfa3-156">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="dbfa3-156">Clean up resources</span></span>

<span data-ttu-id="dbfa3-157">If you plan to explore further, leave the Predictive Maintenance solution accelerator deployed.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-157">If you plan to explore further, leave the Predictive Maintenance solution accelerator deployed.</span></span>

<span data-ttu-id="dbfa3-158">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**:</span><span class="sxs-lookup"><span data-stu-id="dbfa3-158">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**:</span></span>

![Delete solution](media/quickstart-predictive-maintenance-deploy/deletesolution.png)

## <a name="next-steps"></a><span data-ttu-id="dbfa3-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbfa3-160">Next steps</span></span>

<span data-ttu-id="dbfa3-161">In this quickstart, you've deployed the Predictive Maintenance solution accelerator and run a simulation.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-161">In this quickstart, you've deployed the Predictive Maintenance solution accelerator and run a simulation.</span></span>

<span data-ttu-id="dbfa3-162">To learn more about the solution accelerator and the simulated aircraft engines, continue to the following article.</span><span class="sxs-lookup"><span data-stu-id="dbfa3-162">To learn more about the solution accelerator and the simulated aircraft engines, continue to the following article.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dbfa3-163">Predictive Maintenance solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="dbfa3-163">Predictive Maintenance solution accelerator overview</span></span>](iot-accelerators-predictive-walkthrough.md)
