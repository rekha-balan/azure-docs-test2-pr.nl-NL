---
title: Set up cloud for Azure IoT Hub Device Provisioning Service in portal | Microsoft Docs
description: IoT Hub automatic device provisioning in Azure Portal
author: sethmanheim
ms.author: sethm
ms.date: 09/05/2017
ms.topic: tutorial
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: c2c80790fa3e7c20408346fbebf60c39879a94df
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867840"
---
# <a name="configure-cloud-resources-for-device-provisioning-with-the-iot-hub-device-provisioning-service"></a><span data-ttu-id="4285d-103">Configure cloud resources for device provisioning with the IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4285d-103">Configure cloud resources for device provisioning with the IoT Hub Device Provisioning Service</span></span>

<span data-ttu-id="4285d-104">This tutorial shows how to set up the cloud for automatic device provisioning using the IoT Hub Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="4285d-104">This tutorial shows how to set up the cloud for automatic device provisioning using the IoT Hub Device Provisioning Service.</span></span> <span data-ttu-id="4285d-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4285d-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4285d-106">Use the Azure portal to create an IoT Hub Device Provisioning Service and get the ID scope</span><span class="sxs-lookup"><span data-stu-id="4285d-106">Use the Azure portal to create an IoT Hub Device Provisioning Service and get the ID scope</span></span>
> * <span data-ttu-id="4285d-107">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4285d-107">Create an IoT hub</span></span>
> * <span data-ttu-id="4285d-108">Link the IoT hub to the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4285d-108">Link the IoT hub to the Device Provisioning Service</span></span>
> * <span data-ttu-id="4285d-109">Set the allocation policy on the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4285d-109">Set the allocation policy on the Device Provisioning Service</span></span>

<span data-ttu-id="4285d-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="4285d-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="4285d-111">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4285d-111">Sign in to the Azure portal</span></span>

<span data-ttu-id="4285d-112">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4285d-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-device-provisioning-service-instance-and-get-the-id-scope"></a><span data-ttu-id="4285d-113">Create a Device Provisioning Service instance and get the ID scope</span><span class="sxs-lookup"><span data-stu-id="4285d-113">Create a Device Provisioning Service instance and get the ID scope</span></span>

<span data-ttu-id="4285d-114">Follow these steps to create a new Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="4285d-114">Follow these steps to create a new Device Provisioning Service instance.</span></span>

1. <span data-ttu-id="4285d-115">In the upper left-hand corner of the Azure portal, click **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="4285d-115">In the upper left-hand corner of the Azure portal, click **Create a resource**.</span></span>
2. <span data-ttu-id="4285d-116">In the Search box, type **device provisioning**.</span><span class="sxs-lookup"><span data-stu-id="4285d-116">In the Search box, type **device provisioning**.</span></span> 
3. <span data-ttu-id="4285d-117">Click **IoT Hub Device Provisioning Service**.</span><span class="sxs-lookup"><span data-stu-id="4285d-117">Click **IoT Hub Device Provisioning Service**.</span></span>
4. <span data-ttu-id="4285d-118">Fill out the **IoT Hub Device Provisioning Service** form with the following information:</span><span class="sxs-lookup"><span data-stu-id="4285d-118">Fill out the **IoT Hub Device Provisioning Service** form with the following information:</span></span>
    
   | <span data-ttu-id="4285d-119">Setting</span><span class="sxs-lookup"><span data-stu-id="4285d-119">Setting</span></span>       | <span data-ttu-id="4285d-120">Suggested value</span><span class="sxs-lookup"><span data-stu-id="4285d-120">Suggested value</span></span> | <span data-ttu-id="4285d-121">Description</span><span class="sxs-lookup"><span data-stu-id="4285d-121">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="4285d-122">**Name**</span><span class="sxs-lookup"><span data-stu-id="4285d-122">**Name**</span></span> | <span data-ttu-id="4285d-123">Any unique name</span><span class="sxs-lookup"><span data-stu-id="4285d-123">Any unique name</span></span> | -- | 
   | <span data-ttu-id="4285d-124">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="4285d-124">**Subscription**</span></span> | <span data-ttu-id="4285d-125">Your subscription</span><span class="sxs-lookup"><span data-stu-id="4285d-125">Your subscription</span></span>  | <span data-ttu-id="4285d-126">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="4285d-126">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="4285d-127">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="4285d-127">**Resource group**</span></span> | <span data-ttu-id="4285d-128">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4285d-128">myResourceGroup</span></span> | <span data-ttu-id="4285d-129">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="4285d-129">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="4285d-130">**Location**</span><span class="sxs-lookup"><span data-stu-id="4285d-130">**Location**</span></span> | <span data-ttu-id="4285d-131">Any valid location</span><span class="sxs-lookup"><span data-stu-id="4285d-131">Any valid location</span></span> | <span data-ttu-id="4285d-132">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="4285d-132">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |   

   ![Enter basic information about your Device Provisioning service in the portal](./media/tutorial-set-up-cloud/create-iot-dps-portal.png)

5. <span data-ttu-id="4285d-134">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4285d-134">Click **Create**.</span></span> <span data-ttu-id="4285d-135">After a few moments, the Device Provisioning Service instance is created and the **Overview** page is displayed.</span><span class="sxs-lookup"><span data-stu-id="4285d-135">After a few moments, the Device Provisioning Service instance is created and the **Overview** page is displayed.</span></span>
6. <span data-ttu-id="4285d-136">On the **Overview** page for the new service instance, copy the value for the **ID scope** for use later.</span><span class="sxs-lookup"><span data-stu-id="4285d-136">On the **Overview** page for the new service instance, copy the value for the **ID scope** for use later.</span></span> <span data-ttu-id="4285d-137">That value is used to identify registration IDs, and provides a guarantee that the registration ID is unique.</span><span class="sxs-lookup"><span data-stu-id="4285d-137">That value is used to identify registration IDs, and provides a guarantee that the registration ID is unique.</span></span>
7. <span data-ttu-id="4285d-138">Also, copy the **Service endpoint** value for later use.</span><span class="sxs-lookup"><span data-stu-id="4285d-138">Also, copy the **Service endpoint** value for later use.</span></span> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="4285d-139">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4285d-139">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="link-the-device-provisioning-service-to-an-iot-hub"></a><span data-ttu-id="4285d-140">Link the Device Provisioning Service to an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4285d-140">Link the Device Provisioning Service to an IoT hub</span></span>

<span data-ttu-id="4285d-141">The next step is to link the Device Provisioning Service and IoT hub so that the IoT Hub Device Provisioning Service can register devices to that hub.</span><span class="sxs-lookup"><span data-stu-id="4285d-141">The next step is to link the Device Provisioning Service and IoT hub so that the IoT Hub Device Provisioning Service can register devices to that hub.</span></span> <span data-ttu-id="4285d-142">The service can only provision devices to IoT hubs that have been linked to the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="4285d-142">The service can only provision devices to IoT hubs that have been linked to the Device Provisioning Service.</span></span> <span data-ttu-id="4285d-143">Follow these steps.</span><span class="sxs-lookup"><span data-stu-id="4285d-143">Follow these steps.</span></span>

1. <span data-ttu-id="4285d-144">In the **All resources** page, click the Device Provisioning Service instance you created previously.</span><span class="sxs-lookup"><span data-stu-id="4285d-144">In the **All resources** page, click the Device Provisioning Service instance you created previously.</span></span>
2. <span data-ttu-id="4285d-145">In the Device Provisioning Service page, click **Linked IoT hubs**.</span><span class="sxs-lookup"><span data-stu-id="4285d-145">In the Device Provisioning Service page, click **Linked IoT hubs**.</span></span>
3. <span data-ttu-id="4285d-146">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="4285d-146">Click **Add**.</span></span>
4. <span data-ttu-id="4285d-147">In the **Add link to IoT hub** page, provide the following information, and click **Save**:</span><span class="sxs-lookup"><span data-stu-id="4285d-147">In the **Add link to IoT hub** page, provide the following information, and click **Save**:</span></span>

    * <span data-ttu-id="4285d-148">**Subscription:** Make sure the subscription that contains the IoT hub is selected.</span><span class="sxs-lookup"><span data-stu-id="4285d-148">**Subscription:** Make sure the subscription that contains the IoT hub is selected.</span></span> <span data-ttu-id="4285d-149">You can link to IoT hub that resides in a different subscription.</span><span class="sxs-lookup"><span data-stu-id="4285d-149">You can link to IoT hub that resides in a different subscription.</span></span>
    * <span data-ttu-id="4285d-150">**IoT hub:** Choose the name of the IoT hub that you want to link with this Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="4285d-150">**IoT hub:** Choose the name of the IoT hub that you want to link with this Device Provisioning Service instance.</span></span>
    * <span data-ttu-id="4285d-151">**Access Policy:** Select **iothubowner** as the credentials to use for establishing the link to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4285d-151">**Access Policy:** Select **iothubowner** as the credentials to use for establishing the link to the IoT hub.</span></span>

   ![Link the hub name to link to the Device Provisioning Service in the portal](./media/tutorial-set-up-cloud/link-iot-hub-to-dps-portal.png)

## <a name="set-the-allocation-policy-on-the-device-provisioning-service"></a><span data-ttu-id="4285d-153">Set the allocation policy on the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4285d-153">Set the allocation policy on the Device Provisioning Service</span></span>

<span data-ttu-id="4285d-154">The allocation policy is a IoT Hub Device Provisioning Service setting that determines how devices are assigned to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4285d-154">The allocation policy is a IoT Hub Device Provisioning Service setting that determines how devices are assigned to an IoT hub.</span></span> <span data-ttu-id="4285d-155">There are three supported allocation policies:</span><span class="sxs-lookup"><span data-stu-id="4285d-155">There are three supported allocation policies:</span></span> 

1. <span data-ttu-id="4285d-156">**Lowest latency**: Devices are provisioned to an IoT hub based on the hub with the lowest latency to the device.</span><span class="sxs-lookup"><span data-stu-id="4285d-156">**Lowest latency**: Devices are provisioned to an IoT hub based on the hub with the lowest latency to the device.</span></span>
2. <span data-ttu-id="4285d-157">**Evenly weighted distribution** (default): Linked IoT hubs are equally likely to have devices provisioned to them.</span><span class="sxs-lookup"><span data-stu-id="4285d-157">**Evenly weighted distribution** (default): Linked IoT hubs are equally likely to have devices provisioned to them.</span></span> <span data-ttu-id="4285d-158">This setting is the default.</span><span class="sxs-lookup"><span data-stu-id="4285d-158">This setting is the default.</span></span> <span data-ttu-id="4285d-159">If you are provisioning devices to only one IoT hub, you can keep this setting.</span><span class="sxs-lookup"><span data-stu-id="4285d-159">If you are provisioning devices to only one IoT hub, you can keep this setting.</span></span> 
3. <span data-ttu-id="4285d-160">**Static configuration via the enrollment list**: Specification of the desired IoT hub in the enrollment list takes priority over the Device Provisioning Service-level allocation policy.</span><span class="sxs-lookup"><span data-stu-id="4285d-160">**Static configuration via the enrollment list**: Specification of the desired IoT hub in the enrollment list takes priority over the Device Provisioning Service-level allocation policy.</span></span>

<span data-ttu-id="4285d-161">To set the allocation policy, in the Device Provisioning Service page click **Manage allocation policy**.</span><span class="sxs-lookup"><span data-stu-id="4285d-161">To set the allocation policy, in the Device Provisioning Service page click **Manage allocation policy**.</span></span> <span data-ttu-id="4285d-162">Make sure the allocation policy is set to **Evenly weighted distribution** (the default).</span><span class="sxs-lookup"><span data-stu-id="4285d-162">Make sure the allocation policy is set to **Evenly weighted distribution** (the default).</span></span> <span data-ttu-id="4285d-163">If you make any changes, click **Save** when you are done.</span><span class="sxs-lookup"><span data-stu-id="4285d-163">If you make any changes, click **Save** when you are done.</span></span>

![Manage allocation policy](./media/tutorial-set-up-cloud/iot-dps-manage-allocation.png)

## <a name="clean-up-resources"></a><span data-ttu-id="4285d-165">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="4285d-165">Clean up resources</span></span>

<span data-ttu-id="4285d-166">Other tutorials in this collection build upon this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4285d-166">Other tutorials in this collection build upon this tutorial.</span></span> <span data-ttu-id="4285d-167">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4285d-167">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this tutorial.</span></span> <span data-ttu-id="4285d-168">If you do not plan to continue, use the following steps to delete all resources created by this tutorial in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4285d-168">If you do not plan to continue, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>

1. <span data-ttu-id="4285d-169">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT Hub Device Provisioning Service instance.</span><span class="sxs-lookup"><span data-stu-id="4285d-169">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT Hub Device Provisioning Service instance.</span></span> <span data-ttu-id="4285d-170">At the top of the **All resources** page, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="4285d-170">At the top of the **All resources** page, click **Delete**.</span></span>  
2. <span data-ttu-id="4285d-171">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4285d-171">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="4285d-172">At the top of the **All resources** page, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="4285d-172">At the top of the **All resources** page, click **Delete**.</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="4285d-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="4285d-173">Next steps</span></span>

<span data-ttu-id="4285d-174">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="4285d-174">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4285d-175">Use the Azure portal to create an IoT Hub Device Provisioning Service and get the ID scope</span><span class="sxs-lookup"><span data-stu-id="4285d-175">Use the Azure portal to create an IoT Hub Device Provisioning Service and get the ID scope</span></span>
> * <span data-ttu-id="4285d-176">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="4285d-176">Create an IoT hub</span></span>
> * <span data-ttu-id="4285d-177">Link the IoT hub to the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4285d-177">Link the IoT hub to the Device Provisioning Service</span></span>
> * <span data-ttu-id="4285d-178">Set the allocation policy on the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="4285d-178">Set the allocation policy on the Device Provisioning Service</span></span>

<span data-ttu-id="4285d-179">Advance to the next tutorial to learn how to set up your device for provisioning.</span><span class="sxs-lookup"><span data-stu-id="4285d-179">Advance to the next tutorial to learn how to set up your device for provisioning.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4285d-180">Set up device for provisioning</span><span class="sxs-lookup"><span data-stu-id="4285d-180">Set up device for provisioning</span></span>](tutorial-set-up-device.md)
