---
title: Use Azure IoT Hub Device Provisioning Service to provision devices across load balanced IoT hubs | Microsoft Docs
description: Device Provisioning Service automatic device provisioning across load balanced IoT hubs in Azure Portal
author: sethmanheim
ms.author: sethm
ms.date: 09/05/2017
ms.topic: tutorial
ms.service: iot-dps
services: iot-dps
manager: timlt
ms.custom: mvc
ms.openlocfilehash: 784fb99fc2cd721a43c9ca7c767b449a9d0d6cb3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867139"
---
# <a name="provision-devices-across-load-balanced-iot-hubs"></a><span data-ttu-id="fc635-103">Provision devices across load-balanced IoT hubs</span><span class="sxs-lookup"><span data-stu-id="fc635-103">Provision devices across load-balanced IoT hubs</span></span>

<span data-ttu-id="fc635-104">This tutorial shows how to provision devices for multiple, load-balanced IoT hubs using the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="fc635-104">This tutorial shows how to provision devices for multiple, load-balanced IoT hubs using the Device Provisioning Service.</span></span> <span data-ttu-id="fc635-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="fc635-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc635-106">Use the Azure portal to provision a second device to a second IoT hub</span><span class="sxs-lookup"><span data-stu-id="fc635-106">Use the Azure portal to provision a second device to a second IoT hub</span></span> 
> * <span data-ttu-id="fc635-107">Add an enrollment list entry to the second device</span><span class="sxs-lookup"><span data-stu-id="fc635-107">Add an enrollment list entry to the second device</span></span>
> * <span data-ttu-id="fc635-108">Set the Device Provisioning Service allocation policy to **even distribution**</span><span class="sxs-lookup"><span data-stu-id="fc635-108">Set the Device Provisioning Service allocation policy to **even distribution**</span></span>
> * <span data-ttu-id="fc635-109">Link the new IoT hub to the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="fc635-109">Link the new IoT hub to the Device Provisioning Service</span></span>

<span data-ttu-id="fc635-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="fc635-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc635-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fc635-111">Prerequisites</span></span>

<span data-ttu-id="fc635-112">This tutorial builds on the previous [Provision device to a hub](tutorial-provision-device-to-hub.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc635-112">This tutorial builds on the previous [Provision device to a hub](tutorial-provision-device-to-hub.md) tutorial.</span></span>

## <a name="use-the-azure-portal-to-provision-a-second-device-to-a-second-iot-hub"></a><span data-ttu-id="fc635-113">Use the Azure portal to provision a second device to a second IoT hub</span><span class="sxs-lookup"><span data-stu-id="fc635-113">Use the Azure portal to provision a second device to a second IoT hub</span></span>

<span data-ttu-id="fc635-114">Follow the steps in the [Provision device to a hub](tutorial-provision-device-to-hub.md) tutorial to provision a second device to another IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fc635-114">Follow the steps in the [Provision device to a hub](tutorial-provision-device-to-hub.md) tutorial to provision a second device to another IoT hub.</span></span>

## <a name="add-an-enrollment-list-entry-to-the-second-device"></a><span data-ttu-id="fc635-115">Add an enrollment list entry to the second device</span><span class="sxs-lookup"><span data-stu-id="fc635-115">Add an enrollment list entry to the second device</span></span>

<span data-ttu-id="fc635-116">The enrollment list tells the Device Provisioning Service which method of attestation (the method for confirming a device identity) it is using with the device.</span><span class="sxs-lookup"><span data-stu-id="fc635-116">The enrollment list tells the Device Provisioning Service which method of attestation (the method for confirming a device identity) it is using with the device.</span></span> <span data-ttu-id="fc635-117">The next step is to add an enrollment list entry for the second device.</span><span class="sxs-lookup"><span data-stu-id="fc635-117">The next step is to add an enrollment list entry for the second device.</span></span> 

1. <span data-ttu-id="fc635-118">In the page for your Device Provisioning Service, click **Manage enrollments**.</span><span class="sxs-lookup"><span data-stu-id="fc635-118">In the page for your Device Provisioning Service, click **Manage enrollments**.</span></span> <span data-ttu-id="fc635-119">The **Add enrollment list entry** page appears.</span><span class="sxs-lookup"><span data-stu-id="fc635-119">The **Add enrollment list entry** page appears.</span></span> 
2. <span data-ttu-id="fc635-120">At the top of the page, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="fc635-120">At the top of the page, click **Add**.</span></span>
2. <span data-ttu-id="fc635-121">Complete the fields and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fc635-121">Complete the fields and then click **Save**.</span></span>

## <a name="set-the-device-provisioning-service-allocation-policy"></a><span data-ttu-id="fc635-122">Set the Device Provisioning Service allocation policy</span><span class="sxs-lookup"><span data-stu-id="fc635-122">Set the Device Provisioning Service allocation policy</span></span>

<span data-ttu-id="fc635-123">The allocation policy is a Device Provisioning Service setting that determines how devices are assigned to an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fc635-123">The allocation policy is a Device Provisioning Service setting that determines how devices are assigned to an IoT hub.</span></span> <span data-ttu-id="fc635-124">There are three supported allocation policies:</span><span class="sxs-lookup"><span data-stu-id="fc635-124">There are three supported allocation policies:</span></span> 

1. <span data-ttu-id="fc635-125">**Lowest latency**: Devices are provisioned to an IoT hub based on the hub with the lowest latency to the device.</span><span class="sxs-lookup"><span data-stu-id="fc635-125">**Lowest latency**: Devices are provisioned to an IoT hub based on the hub with the lowest latency to the device.</span></span>
2. <span data-ttu-id="fc635-126">**Evenly weighted distribution** (default): Linked IoT hubs are equally likely to have devices provisioned to them.</span><span class="sxs-lookup"><span data-stu-id="fc635-126">**Evenly weighted distribution** (default): Linked IoT hubs are equally likely to have devices provisioned to them.</span></span> <span data-ttu-id="fc635-127">This is the default setting.</span><span class="sxs-lookup"><span data-stu-id="fc635-127">This is the default setting.</span></span> <span data-ttu-id="fc635-128">If you are provisioning devices to only one IoT hub, you can keep this setting.</span><span class="sxs-lookup"><span data-stu-id="fc635-128">If you are provisioning devices to only one IoT hub, you can keep this setting.</span></span> 
3. <span data-ttu-id="fc635-129">**Static configuration via the enrollment list**: Specification of the desired IoT hub in the enrollment list takes priority over the Device Provisioning Service-level allocation policy.</span><span class="sxs-lookup"><span data-stu-id="fc635-129">**Static configuration via the enrollment list**: Specification of the desired IoT hub in the enrollment list takes priority over the Device Provisioning Service-level allocation policy.</span></span>

<span data-ttu-id="fc635-130">Follow these steps to set the allocation policy:</span><span class="sxs-lookup"><span data-stu-id="fc635-130">Follow these steps to set the allocation policy:</span></span>

1. <span data-ttu-id="fc635-131">To set the allocation policy, in the Device Provisioning Service page click **Manage allocation policy**.</span><span class="sxs-lookup"><span data-stu-id="fc635-131">To set the allocation policy, in the Device Provisioning Service page click **Manage allocation policy**.</span></span>
2. <span data-ttu-id="fc635-132">Set the allocation policy to **Evenly weighted distribution**.</span><span class="sxs-lookup"><span data-stu-id="fc635-132">Set the allocation policy to **Evenly weighted distribution**.</span></span>
3. <span data-ttu-id="fc635-133">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fc635-133">Click **Save**.</span></span>

## <a name="link-the-new-iot-hub-to-the-device-provisioning-service"></a><span data-ttu-id="fc635-134">Link the new IoT hub to the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="fc635-134">Link the new IoT hub to the Device Provisioning Service</span></span>

<span data-ttu-id="fc635-135">Link the Device Provisioning Service and IoT hub so that the Device Provisioning Service can register devices to that hub.</span><span class="sxs-lookup"><span data-stu-id="fc635-135">Link the Device Provisioning Service and IoT hub so that the Device Provisioning Service can register devices to that hub.</span></span>

1. <span data-ttu-id="fc635-136">In the **All resources** page, click the Device Provisioning service you created previously.</span><span class="sxs-lookup"><span data-stu-id="fc635-136">In the **All resources** page, click the Device Provisioning service you created previously.</span></span>
2. <span data-ttu-id="fc635-137">In the Device Provisioning Service page, click **Linked IoT hubs**.</span><span class="sxs-lookup"><span data-stu-id="fc635-137">In the Device Provisioning Service page, click **Linked IoT hubs**.</span></span>
3. <span data-ttu-id="fc635-138">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="fc635-138">Click **Add**.</span></span>
4. <span data-ttu-id="fc635-139">In the **Add link to IoT hub** page, use the radio buttons to specify whether the linked IoT hub is located in the current subscription, or in a different subscription.</span><span class="sxs-lookup"><span data-stu-id="fc635-139">In the **Add link to IoT hub** page, use the radio buttons to specify whether the linked IoT hub is located in the current subscription, or in a different subscription.</span></span> <span data-ttu-id="fc635-140">Then, choose the name of the IoT hub from the **IoT hub** box.</span><span class="sxs-lookup"><span data-stu-id="fc635-140">Then, choose the name of the IoT hub from the **IoT hub** box.</span></span>
5. <span data-ttu-id="fc635-141">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fc635-141">Click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc635-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc635-142">Next steps</span></span>

<span data-ttu-id="fc635-143">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="fc635-143">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fc635-144">Use the Azure portal to provision a second device to a second IoT hub</span><span class="sxs-lookup"><span data-stu-id="fc635-144">Use the Azure portal to provision a second device to a second IoT hub</span></span> 
> * <span data-ttu-id="fc635-145">Add an enrollment list entry to the second device</span><span class="sxs-lookup"><span data-stu-id="fc635-145">Add an enrollment list entry to the second device</span></span>
> * <span data-ttu-id="fc635-146">Set the Device Provisioning Service allocation policy to **even distribution**</span><span class="sxs-lookup"><span data-stu-id="fc635-146">Set the Device Provisioning Service allocation policy to **even distribution**</span></span>
> * <span data-ttu-id="fc635-147">Link the new IoT hub to the Device Provisioning Service</span><span class="sxs-lookup"><span data-stu-id="fc635-147">Link the new IoT hub to the Device Provisioning Service</span></span>

<!-- Advance to the next tutorial to learn how to 
 Replace this .md
> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md)
-->
