---
title: Try a cloud-based IoT remote monitoring solution on Azure | Microsoft Docs
description: In this quickstart, you deploy the Remote Monitoring Azure IoT solution accelerator, and sign in to and use the solution dashboard.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: quickstart
ms.custom: mvc
ms.date: 07/12/2018
ms.author: dobett
ms.openlocfilehash: 50005e38214bf22aa664c2d2b0cc4f86da412818
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867794"
---
# <a name="quickstart-try-a-cloud-based-remote-monitoring-solution"></a><span data-ttu-id="c9aa7-103">Quickstart: Try a cloud-based remote monitoring solution</span><span class="sxs-lookup"><span data-stu-id="c9aa7-103">Quickstart: Try a cloud-based remote monitoring solution</span></span>

<span data-ttu-id="c9aa7-104">This quickstart shows you how to deploy the Azure IoT Remote Monitoring solution accelerator to run a cloud-based remote monitoring simulation.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-104">This quickstart shows you how to deploy the Azure IoT Remote Monitoring solution accelerator to run a cloud-based remote monitoring simulation.</span></span> <span data-ttu-id="c9aa7-105">After you've deployed the solution accelerator, you use the solution **Dashboard** page to visualize simulated devices on a map, and the **Maintenance** page respond to a pressure alert from a simulated chiller device.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-105">After you've deployed the solution accelerator, you use the solution **Dashboard** page to visualize simulated devices on a map, and the **Maintenance** page respond to a pressure alert from a simulated chiller device.</span></span> <span data-ttu-id="c9aa7-106">You can use this solution accelerator as the starting point for your own implementation or as a learning tool.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-106">You can use this solution accelerator as the starting point for your own implementation or as a learning tool.</span></span>

<span data-ttu-id="c9aa7-107">The initial deployment configures the Remote Monitoring solution accelerator for a company called Contoso.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-107">The initial deployment configures the Remote Monitoring solution accelerator for a company called Contoso.</span></span> <span data-ttu-id="c9aa7-108">Contoso manages a selection of different device types, such as chillers, deployed in different physical environments.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-108">Contoso manages a selection of different device types, such as chillers, deployed in different physical environments.</span></span> <span data-ttu-id="c9aa7-109">A chiller device sends temperature, humidity, and pressure telemetry to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-109">A chiller device sends temperature, humidity, and pressure telemetry to the Remote Monitoring solution accelerator.</span></span>

<span data-ttu-id="c9aa7-110">To complete this quickstart, you need an active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-110">To complete this quickstart, you need an active Azure subscription.</span></span>

<span data-ttu-id="c9aa7-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="c9aa7-112">Deploy the solution</span><span class="sxs-lookup"><span data-stu-id="c9aa7-112">Deploy the solution</span></span>

<span data-ttu-id="c9aa7-113">When you deploy the solution accelerator to your Azure subscription, you must set some configuration options.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-113">When you deploy the solution accelerator to your Azure subscription, you must set some configuration options.</span></span>

<span data-ttu-id="c9aa7-114">Sign in to [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) using your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-114">Sign in to [azureiotsolutions.com](https://www.azureiotsolutions.com/Accelerators) using your Azure account credentials.</span></span>

<span data-ttu-id="c9aa7-115">Click **Try Now** on the **Remote Monitoring** tile.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-115">Click **Try Now** on the **Remote Monitoring** tile.</span></span>

![Choose Remote Monitoring](./media/quickstart-remote-monitoring-deploy/remotemonitoring.png)

<span data-ttu-id="c9aa7-117">On the **Create Remote Monitoring solution** page, select a **Basic** deployment.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-117">On the **Create Remote Monitoring solution** page, select a **Basic** deployment.</span></span> <span data-ttu-id="c9aa7-118">If you're deploying the solution accelerator to learn how it works or to run a demonstration, choose the **Basic** option to minimize costs.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-118">If you're deploying the solution accelerator to learn how it works or to run a demonstration, choose the **Basic** option to minimize costs.</span></span>

<span data-ttu-id="c9aa7-119">Choose **.NET** as the language.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-119">Choose **.NET** as the language.</span></span> <span data-ttu-id="c9aa7-120">The Java and .NET implementations have identical features.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-120">The Java and .NET implementations have identical features.</span></span>

<span data-ttu-id="c9aa7-121">Enter a unique **Solution name** for your Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-121">Enter a unique **Solution name** for your Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="c9aa7-122">For this quickstart, we're calling ours **contoso-rm2**.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-122">For this quickstart, we're calling ours **contoso-rm2**.</span></span>

<span data-ttu-id="c9aa7-123">Select the **Subscription** and **Region** you want to use to deploy the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-123">Select the **Subscription** and **Region** you want to use to deploy the solution accelerator.</span></span> <span data-ttu-id="c9aa7-124">Typically, you choose the region closest to you.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-124">Typically, you choose the region closest to you.</span></span> <span data-ttu-id="c9aa7-125">For this quickstart, we're using **Visual Studio Enterprise** and **West Europe**.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-125">For this quickstart, we're using **Visual Studio Enterprise** and **West Europe**.</span></span> <span data-ttu-id="c9aa7-126">You must be a [global administrator or user](iot-accelerators-permissions.md) in the subscription.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-126">You must be a [global administrator or user](iot-accelerators-permissions.md) in the subscription.</span></span>

<span data-ttu-id="c9aa7-127">Click **Create Solution** to begin the deployment.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-127">Click **Create Solution** to begin the deployment.</span></span> <span data-ttu-id="c9aa7-128">This process takes at least five minutes to run:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-128">This process takes at least five minutes to run:</span></span>

![Remote Monitoring solution details](./media/quickstart-remote-monitoring-deploy/createform.png)

## <a name="sign-in-to-the-solution"></a><span data-ttu-id="c9aa7-130">Sign in to the solution</span><span class="sxs-lookup"><span data-stu-id="c9aa7-130">Sign in to the solution</span></span>

<span data-ttu-id="c9aa7-131">When the deployment to your Azure subscription is complete, you see a green checkmark and **Ready** on the solution tile.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-131">When the deployment to your Azure subscription is complete, you see a green checkmark and **Ready** on the solution tile.</span></span> <span data-ttu-id="c9aa7-132">You can now sign in to your Remote Monitoring solution accelerator dashboard.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-132">You can now sign in to your Remote Monitoring solution accelerator dashboard.</span></span>

<span data-ttu-id="c9aa7-133">On the **Provisioned solutions** page, click your new Remote Monitoring solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-133">On the **Provisioned solutions** page, click your new Remote Monitoring solution accelerator:</span></span>

![Choose new solution](./media/quickstart-remote-monitoring-deploy/choosenew.png)

<span data-ttu-id="c9aa7-135">You can view information about your Remote Monitoring solution accelerator in the panel that appears.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-135">You can view information about your Remote Monitoring solution accelerator in the panel that appears.</span></span> <span data-ttu-id="c9aa7-136">Choose **Solution dashboard** to view your Remote Monitoring solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-136">Choose **Solution dashboard** to view your Remote Monitoring solution accelerator:</span></span>

![Solution panel](./media/quickstart-remote-monitoring-deploy/solutionpanel.png)

<span data-ttu-id="c9aa7-138">Click **Accept** to accept the permissions request, the Remote Monitoring solution dashboard displays in your browser:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-138">Click **Accept** to accept the permissions request, the Remote Monitoring solution dashboard displays in your browser:</span></span>

<span data-ttu-id="c9aa7-139">[![Solution dashboard](./media/quickstart-remote-monitoring-deploy/solutiondashboard-inline.png)](./media/quickstart-remote-monitoring-deploy/solutiondashboard-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-139">[![Solution dashboard](./media/quickstart-remote-monitoring-deploy/solutiondashboard-inline.png)](./media/quickstart-remote-monitoring-deploy/solutiondashboard-expanded.png#lightbox)</span></span>

## <a name="view-your-devices"></a><span data-ttu-id="c9aa7-140">View your devices</span><span class="sxs-lookup"><span data-stu-id="c9aa7-140">View your devices</span></span>

<span data-ttu-id="c9aa7-141">The solution dashboard shows the following information about Contoso's simulated devices:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-141">The solution dashboard shows the following information about Contoso's simulated devices:</span></span>

* <span data-ttu-id="c9aa7-142">**Device statistics** shows summary information about alerts and the total number of devices.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-142">**Device statistics** shows summary information about alerts and the total number of devices.</span></span> <span data-ttu-id="c9aa7-143">In the default deployment, Contoso has 10 simulated devices of different types.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-143">In the default deployment, Contoso has 10 simulated devices of different types.</span></span>

* <span data-ttu-id="c9aa7-144">**Device locations** shows where your devices are physically located.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-144">**Device locations** shows where your devices are physically located.</span></span> <span data-ttu-id="c9aa7-145">The color of the pin shows when there are alerts from the device.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-145">The color of the pin shows when there are alerts from the device.</span></span>

* <span data-ttu-id="c9aa7-146">**Alerts** shows details of alerts from your devices.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-146">**Alerts** shows details of alerts from your devices.</span></span>

* <span data-ttu-id="c9aa7-147">**Telemetry** shows telemetry from your devices.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-147">**Telemetry** shows telemetry from your devices.</span></span> <span data-ttu-id="c9aa7-148">You can view different telemetry streams by clicking the telemetry types at the top.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-148">You can view different telemetry streams by clicking the telemetry types at the top.</span></span>

* <span data-ttu-id="c9aa7-149">**Analytics** shows combined information about the alerts from your devices.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-149">**Analytics** shows combined information about the alerts from your devices.</span></span>

## <a name="respond-to-an-alert"></a><span data-ttu-id="c9aa7-150">Respond to an alert</span><span class="sxs-lookup"><span data-stu-id="c9aa7-150">Respond to an alert</span></span>

<span data-ttu-id="c9aa7-151">As an operator at Contoso, you can monitor your devices from the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-151">As an operator at Contoso, you can monitor your devices from the solution dashboard.</span></span> <span data-ttu-id="c9aa7-152">The **Device statistics** panel shows there have been a number of critical alerts, and the **Alerts** panel shows most of them are coming from a chiller device.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-152">The **Device statistics** panel shows there have been a number of critical alerts, and the **Alerts** panel shows most of them are coming from a chiller device.</span></span> <span data-ttu-id="c9aa7-153">For Contoso's chiller devices, an internal pressure over 250 PSI indicates the device isn't working correctly.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-153">For Contoso's chiller devices, an internal pressure over 250 PSI indicates the device isn't working correctly.</span></span>

### <a name="identify-the-issue"></a><span data-ttu-id="c9aa7-154">Identify the issue</span><span class="sxs-lookup"><span data-stu-id="c9aa7-154">Identify the issue</span></span>

<span data-ttu-id="c9aa7-155">On the **Dashboard** page, in the **Alerts** panel, you can see the **Chiller pressure too high** alert.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-155">On the **Dashboard** page, in the **Alerts** panel, you can see the **Chiller pressure too high** alert.</span></span> <span data-ttu-id="c9aa7-156">The chiller has a red pin on the map (you may need to pan and zoom on the map):</span><span class="sxs-lookup"><span data-stu-id="c9aa7-156">The chiller has a red pin on the map (you may need to pan and zoom on the map):</span></span>

<span data-ttu-id="c9aa7-157">[![Dashboard shows pressure alert and device on map](./media/quickstart-remote-monitoring-deploy/dashboardalarm-inline.png)](./media/quickstart-remote-monitoring-deploy/dashboardalarm-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-157">[![Dashboard shows pressure alert and device on map](./media/quickstart-remote-monitoring-deploy/dashboardalarm-inline.png)](./media/quickstart-remote-monitoring-deploy/dashboardalarm-expanded.png#lightbox)</span></span>

<span data-ttu-id="c9aa7-158">In the **Alerts** panel, click **...** in the **Explore** column next to the **Chiller pressure too high** rule.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-158">In the **Alerts** panel, click **...** in the **Explore** column next to the **Chiller pressure too high** rule.</span></span> <span data-ttu-id="c9aa7-159">This action takes you to the **Maintenance** page where you can view the details of the rule that triggered the alert.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-159">This action takes you to the **Maintenance** page where you can view the details of the rule that triggered the alert.</span></span>

<span data-ttu-id="c9aa7-160">The **Chiller pressure too high** maintenance page shows details of the rule that triggered the alerts.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-160">The **Chiller pressure too high** maintenance page shows details of the rule that triggered the alerts.</span></span> <span data-ttu-id="c9aa7-161">The page also lists when the alerts occurred and which device triggered them:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-161">The page also lists when the alerts occurred and which device triggered them:</span></span>

<span data-ttu-id="c9aa7-162">[![Maintenance page shows list of alerts that have triggered](./media/quickstart-remote-monitoring-deploy/maintenancealarmlist-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenancealarmlist-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-162">[![Maintenance page shows list of alerts that have triggered](./media/quickstart-remote-monitoring-deploy/maintenancealarmlist-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenancealarmlist-expanded.png#lightbox)</span></span>

<span data-ttu-id="c9aa7-163">You've now identified the issue that triggered the alert and the associated device.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-163">You've now identified the issue that triggered the alert and the associated device.</span></span> <span data-ttu-id="c9aa7-164">As an operator, the next steps are to acknowledge the alert and fix the issue.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-164">As an operator, the next steps are to acknowledge the alert and fix the issue.</span></span>

### <a name="fix-the-issue"></a><span data-ttu-id="c9aa7-165">Fix the issue</span><span class="sxs-lookup"><span data-stu-id="c9aa7-165">Fix the issue</span></span>

<span data-ttu-id="c9aa7-166">To indicate to other operators that you're now working on the alert, select it, and change the **Alert status** to **Acknowledged**:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-166">To indicate to other operators that you're now working on the alert, select it, and change the **Alert status** to **Acknowledged**:</span></span>

<span data-ttu-id="c9aa7-167">[![Select and acknowledge the alert](./media/quickstart-remote-monitoring-deploy/maintenanceacknowledge-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenanceacknowledge-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-167">[![Select and acknowledge the alert](./media/quickstart-remote-monitoring-deploy/maintenanceacknowledge-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenanceacknowledge-expanded.png#lightbox)</span></span>

<span data-ttu-id="c9aa7-168">The value in the status column changes to **Acknowledged**.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-168">The value in the status column changes to **Acknowledged**.</span></span>

<span data-ttu-id="c9aa7-169">To act on the chiller, scroll-down to **Related information**, select the chiller device in the **Alerted devices** list, and then choose **Jobs**:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-169">To act on the chiller, scroll-down to **Related information**, select the chiller device in the **Alerted devices** list, and then choose **Jobs**:</span></span>

<span data-ttu-id="c9aa7-170">[![Select the device and schedule an action](./media/quickstart-remote-monitoring-deploy/maintenanceschedule-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenanceschedule-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-170">[![Select the device and schedule an action](./media/quickstart-remote-monitoring-deploy/maintenanceschedule-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenanceschedule-expanded.png#lightbox)</span></span>

<span data-ttu-id="c9aa7-171">In the **Jobs** panel, choose **Run method** and then the **EmergencyValveRelease** method.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-171">In the **Jobs** panel, choose **Run method** and then the **EmergencyValveRelease** method.</span></span> <span data-ttu-id="c9aa7-172">Add the job name **ChillerPressureRelease**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-172">Add the job name **ChillerPressureRelease**, and click **Apply**.</span></span> <span data-ttu-id="c9aa7-173">These settings create a job that executes immediately.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-173">These settings create a job that executes immediately.</span></span>

<span data-ttu-id="c9aa7-174">To view the job status, return to the **Maintenance** page and view the list of jobs in the **Jobs** view.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-174">To view the job status, return to the **Maintenance** page and view the list of jobs in the **Jobs** view.</span></span> <span data-ttu-id="c9aa7-175">You may need to wait a few seconds before you can see the job has run to release the valve pressure on the chiller:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-175">You may need to wait a few seconds before you can see the job has run to release the valve pressure on the chiller:</span></span>

<span data-ttu-id="c9aa7-176">[![The status of the jobs in the Jobs view](./media/quickstart-remote-monitoring-deploy/maintenancerunningjob-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenancerunningjob-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-176">[![The status of the jobs in the Jobs view](./media/quickstart-remote-monitoring-deploy/maintenancerunningjob-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenancerunningjob-expanded.png#lightbox)</span></span>

### <a name="check-the-pressure-is-back-to-normal"></a><span data-ttu-id="c9aa7-177">Check the pressure is back to normal</span><span class="sxs-lookup"><span data-stu-id="c9aa7-177">Check the pressure is back to normal</span></span>

<span data-ttu-id="c9aa7-178">To view the pressure telemetry for the chiller, navigate to the **Dashboard** page, select **Pressure** in the telemetry panel, and confirm that the pressure for **chiller-02.0** is back to normal:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-178">To view the pressure telemetry for the chiller, navigate to the **Dashboard** page, select **Pressure** in the telemetry panel, and confirm that the pressure for **chiller-02.0** is back to normal:</span></span>

<span data-ttu-id="c9aa7-179">[![Pressure back to normal](./media/quickstart-remote-monitoring-deploy/pressurenormal-inline.png)](./media/quickstart-remote-monitoring-deploy/pressurenormal-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-179">[![Pressure back to normal](./media/quickstart-remote-monitoring-deploy/pressurenormal-inline.png)](./media/quickstart-remote-monitoring-deploy/pressurenormal-expanded.png#lightbox)</span></span>

<span data-ttu-id="c9aa7-180">To close the incident, navigate to the **Maintenance** page, select the alert, and set the status to **Closed**:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-180">To close the incident, navigate to the **Maintenance** page, select the alert, and set the status to **Closed**:</span></span>

<span data-ttu-id="c9aa7-181">[![Select and close the alert](./media/quickstart-remote-monitoring-deploy/maintenanceclose-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenanceclose-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="c9aa7-181">[![Select and close the alert](./media/quickstart-remote-monitoring-deploy/maintenanceclose-inline.png)](./media/quickstart-remote-monitoring-deploy/maintenanceclose-expanded.png#lightbox)</span></span>

<span data-ttu-id="c9aa7-182">The value in the status column changes to **Closed**.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-182">The value in the status column changes to **Closed**.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="c9aa7-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c9aa7-183">Clean up resources</span></span>

<span data-ttu-id="c9aa7-184">If you plan to move on to the tutorials, leave the Remote Monitoring solution accelerator deployed.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-184">If you plan to move on to the tutorials, leave the Remote Monitoring solution accelerator deployed.</span></span>

<span data-ttu-id="c9aa7-185">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**:</span><span class="sxs-lookup"><span data-stu-id="c9aa7-185">If you no longer need the solution accelerator, delete it from the [Provisioned solutions](https://www.azureiotsolutions.com/Accelerators#dashboard) page, by selecting it, and then clicking **Delete Solution**:</span></span>

![Delete solution](media/quickstart-remote-monitoring-deploy/deletesolution.png)

## <a name="next-steps"></a><span data-ttu-id="c9aa7-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9aa7-187">Next steps</span></span>

<span data-ttu-id="c9aa7-188">In this quickstart, you've deployed the Remote Monitoring solution accelerator and completed a monitoring task using the simulated devices in the default Contoso deployment.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-188">In this quickstart, you've deployed the Remote Monitoring solution accelerator and completed a monitoring task using the simulated devices in the default Contoso deployment.</span></span>

<span data-ttu-id="c9aa7-189">To learn more about the solution accelerator using simulated devices, continue to the following tutorial.</span><span class="sxs-lookup"><span data-stu-id="c9aa7-189">To learn more about the solution accelerator using simulated devices, continue to the following tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c9aa7-190">Tutorial: Monitor your IoT devices</span><span class="sxs-lookup"><span data-stu-id="c9aa7-190">Tutorial: Monitor your IoT devices</span></span>](iot-accelerators-remote-monitoring-monitor.md)