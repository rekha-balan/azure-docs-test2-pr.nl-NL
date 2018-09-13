---
title: Try and run a device simulation solution on Azure | Microsoft Docs
description: In this quickstart, you deploy the Device Simulation Azure IoT solution accelerator. You sign use the solution dashboard to create a simulation.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: quickstart
ms.custom: mvc
ms.date: 07/05/2018
ms.author: dobett
ms.openlocfilehash: 549a1b867ad35c6de42969722ba5a2bd28c8f99a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969275"
---
# <a name="quickstart-deploy-and-run-a-cloud-based-device-simulation-solution"></a><span data-ttu-id="7dbf8-104">Quickstart: Deploy and run a cloud-based device simulation solution</span><span class="sxs-lookup"><span data-stu-id="7dbf8-104">Quickstart: Deploy and run a cloud-based device simulation solution</span></span>

<span data-ttu-id="7dbf8-105">This quickstart shows you how to deploy the Azure IoT Device Simulation solution accelerator to use to test your IoT solution.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-105">This quickstart shows you how to deploy the Azure IoT Device Simulation solution accelerator to use to test your IoT solution.</span></span> <span data-ttu-id="7dbf8-106">After you've deployed the solution accelerator, you use the **Simulation** page to create and run a simulation.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-106">After you've deployed the solution accelerator, you use the **Simulation** page to create and run a simulation.</span></span>

<span data-ttu-id="7dbf8-107">To complete this quickstart, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-107">To complete this quickstart, you need an active Azure subscription.</span></span>

<span data-ttu-id="7dbf8-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="7dbf8-109">Deploy the solution</span><span class="sxs-lookup"><span data-stu-id="7dbf8-109">Deploy the solution</span></span>

<span data-ttu-id="7dbf8-110">When you deploy the solution accelerator to your Azure subscription, you must set some configuration options.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-110">When you deploy the solution accelerator to your Azure subscription, you must set some configuration options.</span></span>

<span data-ttu-id="7dbf8-111">Sign in to [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) using your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-111">Sign in to [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) using your Azure account credentials.</span></span>

<span data-ttu-id="7dbf8-112">Click **Try Now** on the **Device Simulation** tile.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-112">Click **Try Now** on the **Device Simulation** tile.</span></span>

![Choose Device Simulation](./media/quickstart-device-simulation-deploy/devicesimulation.png)

<span data-ttu-id="7dbf8-114">On the **Create Device Simulation solution** page, enter a unique **Solution name**.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-114">On the **Create Device Simulation solution** page, enter a unique **Solution name**.</span></span> <span data-ttu-id="7dbf8-115">Make a note of your solution name, it's the name of the Azure resource group that contains all the solution's resources.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-115">Make a note of your solution name, it's the name of the Azure resource group that contains all the solution's resources.</span></span>

<span data-ttu-id="7dbf8-116">Select the **Subscription** and **Region** you want to use to deploy the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-116">Select the **Subscription** and **Region** you want to use to deploy the solution accelerator.</span></span> <span data-ttu-id="7dbf8-117">Typically, you choose the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-117">Typically, you choose the region closest to you.</span></span> <span data-ttu-id="7dbf8-118">You must be a [global administrator or user](iot-accelerators-permissions.md) in the subscription.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-118">You must be a [global administrator or user](iot-accelerators-permissions.md) in the subscription.</span></span>

<span data-ttu-id="7dbf8-119">Check the box to deploy an IoT hub to use with your Device Simulation solution.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-119">Check the box to deploy an IoT hub to use with your Device Simulation solution.</span></span> <span data-ttu-id="7dbf8-120">You can always change the IoT hub your simulation uses later.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-120">You can always change the IoT hub your simulation uses later.</span></span>

<span data-ttu-id="7dbf8-121">Click **Create Solution** to begin provisioning your solution.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-121">Click **Create Solution** to begin provisioning your solution.</span></span> <span data-ttu-id="7dbf8-122">This process takes at least five minutes to run:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-122">This process takes at least five minutes to run:</span></span>

![Device Simulation solution details](./media/quickstart-device-simulation-deploy/createform.png)

## <a name="sign-in-to-the-solution"></a><span data-ttu-id="7dbf8-124">Sign in to the solution</span><span class="sxs-lookup"><span data-stu-id="7dbf8-124">Sign in to the solution</span></span>

<span data-ttu-id="7dbf8-125">When the provisioning process is complete, you can sign in to your Device Simulation solution accelerator dashboard.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-125">When the provisioning process is complete, you can sign in to your Device Simulation solution accelerator dashboard.</span></span>

<span data-ttu-id="7dbf8-126">On the **Provisioned solutions** page, click your new Device Simulation solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-126">On the **Provisioned solutions** page, click your new Device Simulation solution accelerator:</span></span>

![Choose new solution](./media/quickstart-device-simulation-deploy/choosenew.png)

<span data-ttu-id="7dbf8-128">You can view information about your Device Simulation solution accelerator in the panel that appears.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-128">You can view information about your Device Simulation solution accelerator in the panel that appears.</span></span> <span data-ttu-id="7dbf8-129">Choose **Solution dashboard** to view your Device Simulation solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-129">Choose **Solution dashboard** to view your Device Simulation solution accelerator:</span></span>

![Solution panel](./media/quickstart-device-simulation-deploy/solutionpanel.png)

<span data-ttu-id="7dbf8-131">Click **Accept** to accept the permissions request, the Device Simulation solution dashboard displays in your browser:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-131">Click **Accept** to accept the permissions request, the Device Simulation solution dashboard displays in your browser:</span></span>

<span data-ttu-id="7dbf8-132">[![Solution dashboard](./media/quickstart-device-simulation-deploy/solutiondashboard-inline.png)](./media/quickstart-device-simulation-deploy/solutiondashboard-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="7dbf8-132">[![Solution dashboard](./media/quickstart-device-simulation-deploy/solutiondashboard-inline.png)](./media/quickstart-device-simulation-deploy/solutiondashboard-expanded.png#lightbox)</span></span>

## <a name="configure-the-simulation"></a><span data-ttu-id="7dbf8-133">Configure the simulation</span><span class="sxs-lookup"><span data-stu-id="7dbf8-133">Configure the simulation</span></span>

<span data-ttu-id="7dbf8-134">You configure and run a simulation from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-134">You configure and run a simulation from the dashboard.</span></span> <span data-ttu-id="7dbf8-135">Use the values in the following table to configure your simulation:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-135">Use the values in the following table to configure your simulation:</span></span>

| <span data-ttu-id="7dbf8-136">Setting</span><span class="sxs-lookup"><span data-stu-id="7dbf8-136">Setting</span></span>             | <span data-ttu-id="7dbf8-137">Value</span><span class="sxs-lookup"><span data-stu-id="7dbf8-137">Value</span></span>                       |
| ------------------- | --------------------------- |
| <span data-ttu-id="7dbf8-138">Target IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7dbf8-138">Target IoT Hub</span></span>      | <span data-ttu-id="7dbf8-139">Use pre-provisioned IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7dbf8-139">Use pre-provisioned IoT Hub</span></span> |
| <span data-ttu-id="7dbf8-140">Device model</span><span class="sxs-lookup"><span data-stu-id="7dbf8-140">Device model</span></span>        | <span data-ttu-id="7dbf8-141">Chiller</span><span class="sxs-lookup"><span data-stu-id="7dbf8-141">Chiller</span></span>                     |
| <span data-ttu-id="7dbf8-142">Number of devices</span><span class="sxs-lookup"><span data-stu-id="7dbf8-142">Number of devices</span></span>   | <span data-ttu-id="7dbf8-143">10</span><span class="sxs-lookup"><span data-stu-id="7dbf8-143">10</span></span>                          |
| <span data-ttu-id="7dbf8-144">Telemetry frequency</span><span class="sxs-lookup"><span data-stu-id="7dbf8-144">Telemetry frequency</span></span> | <span data-ttu-id="7dbf8-145">10 seconds</span><span class="sxs-lookup"><span data-stu-id="7dbf8-145">10 seconds</span></span>                  |
| <span data-ttu-id="7dbf8-146">Simulation duration</span><span class="sxs-lookup"><span data-stu-id="7dbf8-146">Simulation duration</span></span> | <span data-ttu-id="7dbf8-147">5 minutes</span><span class="sxs-lookup"><span data-stu-id="7dbf8-147">5 minutes</span></span>                   |

<span data-ttu-id="7dbf8-148">[![Simulation configuration](./media/quickstart-device-simulation-deploy/simulationconfig-inline.png)](./media/quickstart-device-simulation-deploy/simulationconfig-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="7dbf8-148">[![Simulation configuration](./media/quickstart-device-simulation-deploy/simulationconfig-inline.png)](./media/quickstart-device-simulation-deploy/simulationconfig-expanded.png#lightbox)</span></span>

## <a name="run-the-simulation"></a><span data-ttu-id="7dbf8-149">Run the simulation</span><span class="sxs-lookup"><span data-stu-id="7dbf8-149">Run the simulation</span></span>

<span data-ttu-id="7dbf8-150">Click **Start Simulation**.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-150">Click **Start Simulation**.</span></span> <span data-ttu-id="7dbf8-151">The simulation runs for the duration you chose.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-151">The simulation runs for the duration you chose.</span></span> <span data-ttu-id="7dbf8-152">You can stop the simulation at any time by clicking **Stop Simulation**.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-152">You can stop the simulation at any time by clicking **Stop Simulation**.</span></span> <span data-ttu-id="7dbf8-153">The simulation shows statistics for the current run.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-153">The simulation shows statistics for the current run.</span></span> <span data-ttu-id="7dbf8-154">Click on **View IoT Hub metrics in the Azure portal** to see the metrics reported by the IoT hub:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-154">Click on **View IoT Hub metrics in the Azure portal** to see the metrics reported by the IoT hub:</span></span>

<span data-ttu-id="7dbf8-155">[![Simulation run](./media/quickstart-device-simulation-deploy/simulationrun-inline.png)](./media/quickstart-device-simulation-deploy/simulationrun-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="7dbf8-155">[![Simulation run](./media/quickstart-device-simulation-deploy/simulationrun-inline.png)](./media/quickstart-device-simulation-deploy/simulationrun-expanded.png#lightbox)</span></span>

<span data-ttu-id="7dbf8-156">You can only run one simulation at a time from a provisioned instance of the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-156">You can only run one simulation at a time from a provisioned instance of the solution accelerator.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7dbf8-157">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7dbf8-157">Clean up resources</span></span>

<span data-ttu-id="7dbf8-158">If you plan to explore further, leave the Device Simulation solution accelerator deployed.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-158">If you plan to explore further, leave the Device Simulation solution accelerator deployed.</span></span>

<span data-ttu-id="7dbf8-159">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-159">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**:</span></span>

![Delete solution](media/quickstart-device-simulation-deploy/deletesolution.png)

## <a name="next-steps"></a><span data-ttu-id="7dbf8-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="7dbf8-161">Next steps</span></span>

<span data-ttu-id="7dbf8-162">In this quickstart, you've deployed the Device Simulation solution accelerator and run an IoT device simulation.</span><span class="sxs-lookup"><span data-stu-id="7dbf8-162">In this quickstart, you've deployed the Device Simulation solution accelerator and run an IoT device simulation.</span></span>

<span data-ttu-id="7dbf8-163">To learn how to use an existing IoT Hub in a simulation, see the following How-to guide:</span><span class="sxs-lookup"><span data-stu-id="7dbf8-163">To learn how to use an existing IoT Hub in a simulation, see the following How-to guide:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dbf8-164">Use an existing IoT hub with the Device Simulation solution accelerator</span><span class="sxs-lookup"><span data-stu-id="7dbf8-164">Use an existing IoT hub with the Device Simulation solution accelerator</span></span>](iot-accelerators-device-simulation-choose-hub.md)
