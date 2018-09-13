---
title: Manual failover of an Azure IoT hub | Microsoft Docs
description: Show how to perform a manual failover for an Azure IoT hub
author: robinsh
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: robinsh
ms.custom: mvc
ms.openlocfilehash: f0e8bf922f142b795dd1a2ded4b3ec265c43481a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865995"
---
# <a name="tutorial-perform-manual-failover-for-an-iot-hub-public-preview"></a><span data-ttu-id="422dc-103">Tutorial: Perform manual failover for an IoT hub (public preview)</span><span class="sxs-lookup"><span data-stu-id="422dc-103">Tutorial: Perform manual failover for an IoT hub (public preview)</span></span>

<span data-ttu-id="422dc-104">Manual failover is a feature of the IoT Hub service that allows customers to [failover](https://en.wikipedia.org/wiki/Failover) their hub's operations from a primary region to the corresponding Azure geo-paired region.</span><span class="sxs-lookup"><span data-stu-id="422dc-104">Manual failover is a feature of the IoT Hub service that allows customers to [failover](https://en.wikipedia.org/wiki/Failover) their hub's operations from a primary region to the corresponding Azure geo-paired region.</span></span> <span data-ttu-id="422dc-105">Manual failover can be done in the event of a regional disaster or an extended service outage.</span><span class="sxs-lookup"><span data-stu-id="422dc-105">Manual failover can be done in the event of a regional disaster or an extended service outage.</span></span> <span data-ttu-id="422dc-106">You can also perform a planned failover to test your disaster recovery capabilities, although we recommend using a test IoT hub rather than one running in production.</span><span class="sxs-lookup"><span data-stu-id="422dc-106">You can also perform a planned failover to test your disaster recovery capabilities, although we recommend using a test IoT hub rather than one running in production.</span></span> <span data-ttu-id="422dc-107">The manual failover feature is offered to customers at no additional cost.</span><span class="sxs-lookup"><span data-stu-id="422dc-107">The manual failover feature is offered to customers at no additional cost.</span></span>

<span data-ttu-id="422dc-108">In this tutorial, you perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="422dc-108">In this tutorial, you perform the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="422dc-109">Using the Azure portal, create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-109">Using the Azure portal, create an IoT hub.</span></span> 
> * <span data-ttu-id="422dc-110">Perform a failover.</span><span class="sxs-lookup"><span data-stu-id="422dc-110">Perform a failover.</span></span> 
> * <span data-ttu-id="422dc-111">See the hub running in the secondary location.</span><span class="sxs-lookup"><span data-stu-id="422dc-111">See the hub running in the secondary location.</span></span>
> * <span data-ttu-id="422dc-112">Perform a failback to return the IoT hub's operations to the primary location.</span><span class="sxs-lookup"><span data-stu-id="422dc-112">Perform a failback to return the IoT hub's operations to the primary location.</span></span> 
> * <span data-ttu-id="422dc-113">Confirm the hub is running correctly in the right location.</span><span class="sxs-lookup"><span data-stu-id="422dc-113">Confirm the hub is running correctly in the right location.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="422dc-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="422dc-114">Prerequisites</span></span>

- <span data-ttu-id="422dc-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="422dc-115">An Azure subscription.</span></span> <span data-ttu-id="422dc-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="422dc-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="422dc-117">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="422dc-117">Create an IoT hub</span></span>

1. <span data-ttu-id="422dc-118">Log into the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="422dc-118">Log into the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="422dc-119">Click **+ Create a resource** and select **Internet of Things**, then **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="422dc-119">Click **+ Create a resource** and select **Internet of Things**, then **IoT Hub**.</span></span>

   ![Screenshot showing creating an IoT hub](./media/tutorial-manual-failover/create-hub-01.png)

3. <span data-ttu-id="422dc-121">Select the **Basics** tab. Fill in the following fields.</span><span class="sxs-lookup"><span data-stu-id="422dc-121">Select the **Basics** tab. Fill in the following fields.</span></span>

    <span data-ttu-id="422dc-122">**Subscription**: select the Azure subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="422dc-122">**Subscription**: select the Azure subscription you want to use.</span></span>

    <span data-ttu-id="422dc-123">**Resource Group**: click **Create new** and specify **ManlFailRG** for the resource group name.</span><span class="sxs-lookup"><span data-stu-id="422dc-123">**Resource Group**: click **Create new** and specify **ManlFailRG** for the resource group name.</span></span>

    <span data-ttu-id="422dc-124">**Region**: select a region close to you that is part of the preview.</span><span class="sxs-lookup"><span data-stu-id="422dc-124">**Region**: select a region close to you that is part of the preview.</span></span> <span data-ttu-id="422dc-125">This tutorial uses `westus2`.</span><span class="sxs-lookup"><span data-stu-id="422dc-125">This tutorial uses `westus2`.</span></span> <span data-ttu-id="422dc-126">A failover can only be performed between Azure geo-paired regions.</span><span class="sxs-lookup"><span data-stu-id="422dc-126">A failover can only be performed between Azure geo-paired regions.</span></span> <span data-ttu-id="422dc-127">The region geo-paired with westus2 is WestCentralUS.</span><span class="sxs-lookup"><span data-stu-id="422dc-127">The region geo-paired with westus2 is WestCentralUS.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="422dc-128">Manual failover is currently in public preview and is *not* available in the following Azure regions: East US, West US, North Europe, West Europe, Brazil South, and South Central US.</span><span class="sxs-lookup"><span data-stu-id="422dc-128">Manual failover is currently in public preview and is *not* available in the following Azure regions: East US, West US, North Europe, West Europe, Brazil South, and South Central US.</span></span>

   <span data-ttu-id="422dc-129">**IoT Hub Name**: specify a name for your Iot hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-129">**IoT Hub Name**: specify a name for your Iot hub.</span></span> <span data-ttu-id="422dc-130">The hub name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="422dc-130">The hub name must be globally unique.</span></span> 

   ![Screenshot showing Basics pane for creating an IoT hub](./media/tutorial-manual-failover/create-hub-02-basics.png)

   <span data-ttu-id="422dc-132">Click **Review + create**.</span><span class="sxs-lookup"><span data-stu-id="422dc-132">Click **Review + create**.</span></span> <span data-ttu-id="422dc-133">(It uses the defaults for size and scale.)</span><span class="sxs-lookup"><span data-stu-id="422dc-133">(It uses the defaults for size and scale.)</span></span> 

4. <span data-ttu-id="422dc-134">Review the information, then click **Create** to create the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-134">Review the information, then click **Create** to create the IoT hub.</span></span> 

   ![Screenshot showing final step for creating an IoT hub](./media/tutorial-manual-failover/create-hub-03-create.png)

## <a name="perform-a-manual-failover"></a><span data-ttu-id="422dc-136">Perform a manual failover</span><span class="sxs-lookup"><span data-stu-id="422dc-136">Perform a manual failover</span></span>

<span data-ttu-id="422dc-137">Note that there is a limit of two failovers and two failbacks per day for an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-137">Note that there is a limit of two failovers and two failbacks per day for an IoT hub.</span></span>

1. <span data-ttu-id="422dc-138">Click **Resource groups** and then select the resource group **ManlFailRG**.</span><span class="sxs-lookup"><span data-stu-id="422dc-138">Click **Resource groups** and then select the resource group **ManlFailRG**.</span></span> <span data-ttu-id="422dc-139">Click on your hub in the list of resources.</span><span class="sxs-lookup"><span data-stu-id="422dc-139">Click on your hub in the list of resources.</span></span> 

2. <span data-ttu-id="422dc-140">Under **Resiliency** on the IoT Hub pane, click **Manual failover (preview)**.</span><span class="sxs-lookup"><span data-stu-id="422dc-140">Under **Resiliency** on the IoT Hub pane, click **Manual failover (preview)**.</span></span> <span data-ttu-id="422dc-141">Note that if your hub is not set up in a valid region, the manual failover option will be disabled.</span><span class="sxs-lookup"><span data-stu-id="422dc-141">Note that if your hub is not set up in a valid region, the manual failover option will be disabled.</span></span>

   ![Screenshot showing IoT Hub properties pane](./media/tutorial-manual-failover/trigger-failover-01.png)

3. <span data-ttu-id="422dc-143">On the Manual failover pane, you see the **IoT Hub Primary Location** and the **IoT Hub Secondary Location**.</span><span class="sxs-lookup"><span data-stu-id="422dc-143">On the Manual failover pane, you see the **IoT Hub Primary Location** and the **IoT Hub Secondary Location**.</span></span> <span data-ttu-id="422dc-144">The primary location is initially set to the location you specified when you created the IoT hub, and always indicates the location in which the hub is currently active.</span><span class="sxs-lookup"><span data-stu-id="422dc-144">The primary location is initially set to the location you specified when you created the IoT hub, and always indicates the location in which the hub is currently active.</span></span> <span data-ttu-id="422dc-145">The secondary location is the standard [Azure geo-paired region](../best-practices-availability-paired-regions.md) that is paired to the primary location.</span><span class="sxs-lookup"><span data-stu-id="422dc-145">The secondary location is the standard [Azure geo-paired region](../best-practices-availability-paired-regions.md) that is paired to the primary location.</span></span> <span data-ttu-id="422dc-146">You cannot change the location values.</span><span class="sxs-lookup"><span data-stu-id="422dc-146">You cannot change the location values.</span></span> <span data-ttu-id="422dc-147">For this tutorial, the primary location is `westus2` and the secondary location is `WestCentralUS`.</span><span class="sxs-lookup"><span data-stu-id="422dc-147">For this tutorial, the primary location is `westus2` and the secondary location is `WestCentralUS`.</span></span>

   ![Screenshot showing Manual Failover pane](./media/tutorial-manual-failover/trigger-failover-02.png)

3. <span data-ttu-id="422dc-149">At the top of the Manual failover pane, click **Initiate failover**.</span><span class="sxs-lookup"><span data-stu-id="422dc-149">At the top of the Manual failover pane, click **Initiate failover**.</span></span> <span data-ttu-id="422dc-150">You see the **Confirm manual failover** pane.</span><span class="sxs-lookup"><span data-stu-id="422dc-150">You see the **Confirm manual failover** pane.</span></span> <span data-ttu-id="422dc-151">Fill in the name of your IoT hub to confirm it's the one you want to failover.</span><span class="sxs-lookup"><span data-stu-id="422dc-151">Fill in the name of your IoT hub to confirm it's the one you want to failover.</span></span> <span data-ttu-id="422dc-152">Then, to initiate the failover, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="422dc-152">Then, to initiate the failover, click **OK**.</span></span>

   <span data-ttu-id="422dc-153">The amount of time it takes to perform the manual failover is proportional to the number of devices that are registered for your hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-153">The amount of time it takes to perform the manual failover is proportional to the number of devices that are registered for your hub.</span></span> <span data-ttu-id="422dc-154">For example, if you have 100,000 devices, it might take 15 minutes, but if you have five million devices, it might take an hour or longer.</span><span class="sxs-lookup"><span data-stu-id="422dc-154">For example, if you have 100,000 devices, it might take 15 minutes, but if you have five million devices, it might take an hour or longer.</span></span>

4. <span data-ttu-id="422dc-155">In the **Confirm manual failover** pane, fill in the name of your IoT hub to confirm it's the one you want to failover.</span><span class="sxs-lookup"><span data-stu-id="422dc-155">In the **Confirm manual failover** pane, fill in the name of your IoT hub to confirm it's the one you want to failover.</span></span> <span data-ttu-id="422dc-156">Then, to initiate the failover, click OK.</span><span class="sxs-lookup"><span data-stu-id="422dc-156">Then, to initiate the failover, click OK.</span></span> 

   ![Screenshot showing Manual Failover pane](./media/tutorial-manual-failover/trigger-failover-03-confirm.png)

   <span data-ttu-id="422dc-158">While the manual failover process is running, there is a banner on the Manual Failover pane that tells you a manual failover is in progress.</span><span class="sxs-lookup"><span data-stu-id="422dc-158">While the manual failover process is running, there is a banner on the Manual Failover pane that tells you a manual failover is in progress.</span></span> 

   ![Screenshot showing Manual Failover in progress](./media/tutorial-manual-failover/trigger-failover-04-in-progress.png)

   <span data-ttu-id="422dc-160">If you close the IoT Hub pane and open it again by clicking it on the Resource Group pane, you see a banner that tells you the hub is not active.</span><span class="sxs-lookup"><span data-stu-id="422dc-160">If you close the IoT Hub pane and open it again by clicking it on the Resource Group pane, you see a banner that tells you the hub is not active.</span></span> 

   ![Screenshot showing IoT Hub inactive](./media/tutorial-manual-failover/trigger-failover-05-hub-inactive.png)

   <span data-ttu-id="422dc-162">After it's finished, the primary and secondary regions on the Manual Failover page are flipped and the hub is active again.</span><span class="sxs-lookup"><span data-stu-id="422dc-162">After it's finished, the primary and secondary regions on the Manual Failover page are flipped and the hub is active again.</span></span> <span data-ttu-id="422dc-163">In this example, the primary location is now `WestCentralUS` and the secondary location is now `westus2`.</span><span class="sxs-lookup"><span data-stu-id="422dc-163">In this example, the primary location is now `WestCentralUS` and the secondary location is now `westus2`.</span></span> 

   ![Screenshot showing failover is complete](./media/tutorial-manual-failover/trigger-failover-06-finished.png)

## <a name="perform-a-failback"></a><span data-ttu-id="422dc-165">Perform a failback</span><span class="sxs-lookup"><span data-stu-id="422dc-165">Perform a failback</span></span> 

<span data-ttu-id="422dc-166">After you have performed a manual failover, you can switch the hub's operations back to the original primary region -- this is called a failback.</span><span class="sxs-lookup"><span data-stu-id="422dc-166">After you have performed a manual failover, you can switch the hub's operations back to the original primary region -- this is called a failback.</span></span> <span data-ttu-id="422dc-167">If you have just performed a failover, you have to wait about an hour before you can request a failback.</span><span class="sxs-lookup"><span data-stu-id="422dc-167">If you have just performed a failover, you have to wait about an hour before you can request a failback.</span></span> <span data-ttu-id="422dc-168">If you try to perform the failback in a shorter amount of time, an error message is displayed.</span><span class="sxs-lookup"><span data-stu-id="422dc-168">If you try to perform the failback in a shorter amount of time, an error message is displayed.</span></span>

<span data-ttu-id="422dc-169">A failback is performed just like a manual failover.</span><span class="sxs-lookup"><span data-stu-id="422dc-169">A failback is performed just like a manual failover.</span></span> <span data-ttu-id="422dc-170">These are the steps:</span><span class="sxs-lookup"><span data-stu-id="422dc-170">These are the steps:</span></span> 

1. <span data-ttu-id="422dc-171">To perform a failback, return to the Iot Hub pane for your Iot hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-171">To perform a failback, return to the Iot Hub pane for your Iot hub.</span></span>

2. <span data-ttu-id="422dc-172">Under **Resiliency** on the IoT Hub pane, click **Manual failover (preview)**.</span><span class="sxs-lookup"><span data-stu-id="422dc-172">Under **Resiliency** on the IoT Hub pane, click **Manual failover (preview)**.</span></span> 

3. <span data-ttu-id="422dc-173">At the top of the Manual failover pane, click **Initiate failover**.</span><span class="sxs-lookup"><span data-stu-id="422dc-173">At the top of the Manual failover pane, click **Initiate failover**.</span></span> <span data-ttu-id="422dc-174">You see the **Confirm manual failover** pane.</span><span class="sxs-lookup"><span data-stu-id="422dc-174">You see the **Confirm manual failover** pane.</span></span> 

4. <span data-ttu-id="422dc-175">In the **Confirm manual failover** pane, fill in the name of your IoT hub to confirm it's the one you want to failback.</span><span class="sxs-lookup"><span data-stu-id="422dc-175">In the **Confirm manual failover** pane, fill in the name of your IoT hub to confirm it's the one you want to failback.</span></span> <span data-ttu-id="422dc-176">To then initiate the failback, click OK.</span><span class="sxs-lookup"><span data-stu-id="422dc-176">To then initiate the failback, click OK.</span></span> 

   ![Screenshot of manual failback request](./media/tutorial-manual-failover/trigger-failback-01-regions.png)

   <span data-ttu-id="422dc-178">The banners are displayed as explained in the [perform a failover](#perform-a-failover) section.</span><span class="sxs-lookup"><span data-stu-id="422dc-178">The banners are displayed as explained in the [perform a failover](#perform-a-failover) section.</span></span> <span data-ttu-id="422dc-179">After the failback is complete, it again shows `westus2` as the primary location and `WestCentralUS` as the secondary location, as set originally.</span><span class="sxs-lookup"><span data-stu-id="422dc-179">After the failback is complete, it again shows `westus2` as the primary location and `WestCentralUS` as the secondary location, as set originally.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="422dc-180">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="422dc-180">Clean up resources</span></span> 

<span data-ttu-id="422dc-181">To remove the resources you've created for this tutorial, delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="422dc-181">To remove the resources you've created for this tutorial, delete the resource group.</span></span> <span data-ttu-id="422dc-182">This action deletes all resources contained within the group.</span><span class="sxs-lookup"><span data-stu-id="422dc-182">This action deletes all resources contained within the group.</span></span> <span data-ttu-id="422dc-183">In this case, it removes the IoT hub and the resource group itself.</span><span class="sxs-lookup"><span data-stu-id="422dc-183">In this case, it removes the IoT hub and the resource group itself.</span></span> 

1. <span data-ttu-id="422dc-184">Click **Resource Groups**.</span><span class="sxs-lookup"><span data-stu-id="422dc-184">Click **Resource Groups**.</span></span> 

2. <span data-ttu-id="422dc-185">Locate and select the resource group **ManlFailRG**.</span><span class="sxs-lookup"><span data-stu-id="422dc-185">Locate and select the resource group **ManlFailRG**.</span></span> <span data-ttu-id="422dc-186">Click on it to open it.</span><span class="sxs-lookup"><span data-stu-id="422dc-186">Click on it to open it.</span></span> 

3. <span data-ttu-id="422dc-187">Click **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="422dc-187">Click **Delete resource group**.</span></span> <span data-ttu-id="422dc-188">When prompted, enter the name of the resource group and click **Delete** to confirm.</span><span class="sxs-lookup"><span data-stu-id="422dc-188">When prompted, enter the name of the resource group and click **Delete** to confirm.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="422dc-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="422dc-189">Next steps</span></span>

<span data-ttu-id="422dc-190">In this tutorial, you learned how to configure and perform a manual failover, and how to request a failback by performing the following tasks:</span><span class="sxs-lookup"><span data-stu-id="422dc-190">In this tutorial, you learned how to configure and perform a manual failover, and how to request a failback by performing the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="422dc-191">Using the Azure portal, create an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="422dc-191">Using the Azure portal, create an IoT hub.</span></span> 
> * <span data-ttu-id="422dc-192">Perform a failover.</span><span class="sxs-lookup"><span data-stu-id="422dc-192">Perform a failover.</span></span> 
> * <span data-ttu-id="422dc-193">See the hub running in the secondary location.</span><span class="sxs-lookup"><span data-stu-id="422dc-193">See the hub running in the secondary location.</span></span>
> * <span data-ttu-id="422dc-194">Perform a failback to return the IoT hub's operations to the primary location.</span><span class="sxs-lookup"><span data-stu-id="422dc-194">Perform a failback to return the IoT hub's operations to the primary location.</span></span> 
> * <span data-ttu-id="422dc-195">Confirm the hub is running correctly in the right location.</span><span class="sxs-lookup"><span data-stu-id="422dc-195">Confirm the hub is running correctly in the right location.</span></span>

<span data-ttu-id="422dc-196">Advance to the next tutorial to learn how to manage the state of an IoT device.</span><span class="sxs-lookup"><span data-stu-id="422dc-196">Advance to the next tutorial to learn how to manage the state of an IoT device.</span></span> 

> [!div class="nextstepaction"]
[<span data-ttu-id="422dc-197">Manage the state of an IoT device</span><span class="sxs-lookup"><span data-stu-id="422dc-197">Manage the state of an IoT device</span></span>](tutorial-device-twins.md)