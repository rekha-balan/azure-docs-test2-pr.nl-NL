---
title: Set up Device Provisioning in the Azure portal | Microsoft Docs
description: Azure Quickstart - Set up the Azure IoT Hub Device Provisioning Service in the Azure Portal
author: wesmc7777
ms.author: wesmc
ms.date: 07/12/2018
ms.topic: quickstart
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: ce1586e472e1d1ea5ddd9ca5a426b1bea2b5b931
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966200"
---
# <a name="set-up-the-iot-hub-device-provisioning-service-with-the-azure-portal"></a><span data-ttu-id="2b913-103">Set up the IoT Hub Device Provisioning Service with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2b913-103">Set up the IoT Hub Device Provisioning Service with the Azure portal</span></span>

<span data-ttu-id="2b913-104">These steps show how to set up the Azure cloud resources in the portal for provisioning your devices.</span><span class="sxs-lookup"><span data-stu-id="2b913-104">These steps show how to set up the Azure cloud resources in the portal for provisioning your devices.</span></span> <span data-ttu-id="2b913-105">This article includes steps for: creating your IoT hub, creating a new IoT Hub Device Provisioning Service, and linking the two services together.</span><span class="sxs-lookup"><span data-stu-id="2b913-105">This article includes steps for: creating your IoT hub, creating a new IoT Hub Device Provisioning Service, and linking the two services together.</span></span> 

<span data-ttu-id="2b913-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="2b913-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="create-an-iot-hub"></a><span data-ttu-id="2b913-107">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="2b913-107">Create an IoT hub</span></span>

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]


## <a name="create-a-new-instance-for-the-iot-hub-device-provisioning-service"></a><span data-ttu-id="2b913-108">Create a new instance for the IoT Hub Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="2b913-108">Create a new instance for the IoT Hub Device Provisioning Service</span></span>

1. <span data-ttu-id="2b913-109">Click the **Create a resource** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b913-109">Click the **Create a resource** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="2b913-110">*Search the Marketplace* for the **Device provisioning service**.</span><span class="sxs-lookup"><span data-stu-id="2b913-110">*Search the Marketplace* for the **Device provisioning service**.</span></span> <span data-ttu-id="2b913-111">Select **IoT Hub Device Provisioning Service** and click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="2b913-111">Select **IoT Hub Device Provisioning Service** and click the **Create** button.</span></span> 

3. <span data-ttu-id="2b913-112">Provide the following information for your new Device Provisioning service instance and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b913-112">Provide the following information for your new Device Provisioning service instance and click **Create**.</span></span>

    * <span data-ttu-id="2b913-113">**Name:** Provide a unique name for your new Device Provisioning service instance.</span><span class="sxs-lookup"><span data-stu-id="2b913-113">**Name:** Provide a unique name for your new Device Provisioning service instance.</span></span> <span data-ttu-id="2b913-114">If the name you enter is available, a green check mark appears.</span><span class="sxs-lookup"><span data-stu-id="2b913-114">If the name you enter is available, a green check mark appears.</span></span>
    * <span data-ttu-id="2b913-115">**Subscription:** Choose the subscription that you want to use to create this Device Provisioning service instance.</span><span class="sxs-lookup"><span data-stu-id="2b913-115">**Subscription:** Choose the subscription that you want to use to create this Device Provisioning service instance.</span></span>
    * <span data-ttu-id="2b913-116">**Resource group:** This field allows you to create a new resource group, or choose an existing one to contain the new instance.</span><span class="sxs-lookup"><span data-stu-id="2b913-116">**Resource group:** This field allows you to create a new resource group, or choose an existing one to contain the new instance.</span></span> <span data-ttu-id="2b913-117">Choose the same resource group that contains the Iot hub you created above, for example, **TestResources**.</span><span class="sxs-lookup"><span data-stu-id="2b913-117">Choose the same resource group that contains the Iot hub you created above, for example, **TestResources**.</span></span> <span data-ttu-id="2b913-118">By putting all related resources in a group together, you can manage them together.</span><span class="sxs-lookup"><span data-stu-id="2b913-118">By putting all related resources in a group together, you can manage them together.</span></span> <span data-ttu-id="2b913-119">For example, deleting the resource group deletes all resources contained in that group.</span><span class="sxs-lookup"><span data-stu-id="2b913-119">For example, deleting the resource group deletes all resources contained in that group.</span></span> <span data-ttu-id="2b913-120">For more information, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2b913-120">For more information, see [Use resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>
    * <span data-ttu-id="2b913-121">**Location:** Select the closest location to your devices.</span><span class="sxs-lookup"><span data-stu-id="2b913-121">**Location:** Select the closest location to your devices.</span></span>
    * <span data-ttu-id="2b913-122">**Pin to dashboard:** Select this option to have the instance pinned to your dashboard making it easier to find.</span><span class="sxs-lookup"><span data-stu-id="2b913-122">**Pin to dashboard:** Select this option to have the instance pinned to your dashboard making it easier to find.</span></span>

    ![Enter basic information about your Device Provisioning service instance in the portal blade](./media/quick-setup-auto-provision/create-iot-dps-portal.png)  

4. <span data-ttu-id="2b913-124">Once the service is successfully deployed, its summary blade automatically opens.</span><span class="sxs-lookup"><span data-stu-id="2b913-124">Once the service is successfully deployed, its summary blade automatically opens.</span></span>


## <a name="link-the-iot-hub-and-your-device-provisioning-service"></a><span data-ttu-id="2b913-125">Link the IoT hub and your Device Provisioning service</span><span class="sxs-lookup"><span data-stu-id="2b913-125">Link the IoT hub and your Device Provisioning service</span></span>

<span data-ttu-id="2b913-126">In this section, you will add a configuration to the Device Provisioning service instance.</span><span class="sxs-lookup"><span data-stu-id="2b913-126">In this section, you will add a configuration to the Device Provisioning service instance.</span></span> <span data-ttu-id="2b913-127">This configuration sets the IoT hub for which devices will be provisioned.</span><span class="sxs-lookup"><span data-stu-id="2b913-127">This configuration sets the IoT hub for which devices will be provisioned.</span></span>

1. <span data-ttu-id="2b913-128">Click the **All resources** button from the left-hand menu of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b913-128">Click the **All resources** button from the left-hand menu of the Azure portal.</span></span> <span data-ttu-id="2b913-129">Select the Device Provisioning service instance that you created in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="2b913-129">Select the Device Provisioning service instance that you created in the preceding section.</span></span>  

2. <span data-ttu-id="2b913-130">On the Device Provisioning Service summary blade, select **Linked IoT hubs**.</span><span class="sxs-lookup"><span data-stu-id="2b913-130">On the Device Provisioning Service summary blade, select **Linked IoT hubs**.</span></span> <span data-ttu-id="2b913-131">Click the **+ Add** button seen at the top.</span><span class="sxs-lookup"><span data-stu-id="2b913-131">Click the **+ Add** button seen at the top.</span></span> 

3. <span data-ttu-id="2b913-132">On the **Add link to IoT hub** page, provide the following information to link your new Device Provisioning service instance to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b913-132">On the **Add link to IoT hub** page, provide the following information to link your new Device Provisioning service instance to an IoT hub.</span></span> <span data-ttu-id="2b913-133">Then click  **Save**.</span><span class="sxs-lookup"><span data-stu-id="2b913-133">Then click  **Save**.</span></span> 

    * <span data-ttu-id="2b913-134">**Subscription:** Select the subscription containing the IoT hub that you want to link with your new Device Provisioning service instance.</span><span class="sxs-lookup"><span data-stu-id="2b913-134">**Subscription:** Select the subscription containing the IoT hub that you want to link with your new Device Provisioning service instance.</span></span>
    * <span data-ttu-id="2b913-135">**Iot hub:** Select the IoT hub to link with your new Device Provisioning service instance.</span><span class="sxs-lookup"><span data-stu-id="2b913-135">**Iot hub:** Select the IoT hub to link with your new Device Provisioning service instance.</span></span>
    * <span data-ttu-id="2b913-136">**Access Policy:** Select **iothubowner** as the credentials for establishing the link with the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b913-136">**Access Policy:** Select **iothubowner** as the credentials for establishing the link with the IoT hub.</span></span>  

    ![Link the hub name to link to the Device Provisioning service instance in the portal blade](./media/quick-setup-auto-provision/link-iot-hub-to-dps-portal.png)  

3. <span data-ttu-id="2b913-138">Now you should see the selected hub under the **Linked IoT hubs** blade.</span><span class="sxs-lookup"><span data-stu-id="2b913-138">Now you should see the selected hub under the **Linked IoT hubs** blade.</span></span> <span data-ttu-id="2b913-139">You might need to click **Refresh** to show **Linked IoT hubs**.</span><span class="sxs-lookup"><span data-stu-id="2b913-139">You might need to click **Refresh** to show **Linked IoT hubs**.</span></span>



## <a name="clean-up-resources"></a><span data-ttu-id="2b913-140">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2b913-140">Clean up resources</span></span>

<span data-ttu-id="2b913-141">Other Quickstarts in this collection build upon this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="2b913-141">Other Quickstarts in this collection build upon this Quickstart.</span></span> <span data-ttu-id="2b913-142">If you plan to continue on to work with subsequent Quickstarts or with the tutorials, do not clean up the resources created in this Quickstart.</span><span class="sxs-lookup"><span data-stu-id="2b913-142">If you plan to continue on to work with subsequent Quickstarts or with the tutorials, do not clean up the resources created in this Quickstart.</span></span> <span data-ttu-id="2b913-143">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b913-143">If you do not plan to continue, use the following steps to delete all resources created by this Quickstart in the Azure portal.</span></span>

1. <span data-ttu-id="2b913-144">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span><span class="sxs-lookup"><span data-stu-id="2b913-144">From the left-hand menu in the Azure portal, click **All resources** and then select your Device Provisioning service.</span></span> <span data-ttu-id="2b913-145">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2b913-145">At the top of the **All resources** blade, click **Delete**.</span></span>  
2. <span data-ttu-id="2b913-146">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2b913-146">From the left-hand menu in the Azure portal, click **All resources** and then select your IoT hub.</span></span> <span data-ttu-id="2b913-147">At the top of the **All resources** blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2b913-147">At the top of the **All resources** blade, click **Delete**.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2b913-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b913-148">Next steps</span></span>

<span data-ttu-id="2b913-149">In this Quickstart, you’ve deployed an IoT hub and a Device Provisioning service instance, and linked the two resources.</span><span class="sxs-lookup"><span data-stu-id="2b913-149">In this Quickstart, you’ve deployed an IoT hub and a Device Provisioning service instance, and linked the two resources.</span></span> <span data-ttu-id="2b913-150">To learn how to use this set up to provision a simulated device, continue to the Quickstart for creating simulated device.</span><span class="sxs-lookup"><span data-stu-id="2b913-150">To learn how to use this set up to provision a simulated device, continue to the Quickstart for creating simulated device.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b913-151">Quickstart to create simulated device</span><span class="sxs-lookup"><span data-stu-id="2b913-151">Quickstart to create simulated device</span></span>](./quick-create-simulated-device.md)
