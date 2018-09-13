---
title: Use the Azure portal to create an IoT Hub | Microsoft Docs
description: How to create, manage, and delete Azure IoT hubs through the Azure portal. Includes information about pricing tiers, scaling, security, and messaging configuration.
services: iot-hub
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/31/2017
ms.author: dobett
ms.openlocfilehash: 14091289c157038e4c349f7fd8fc5af67f43400d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564135"
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="150d8-104">Create an IoT hub using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="150d8-104">Create an IoT hub using the Azure portal</span></span>
[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="150d8-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="150d8-105">Introduction</span></span>
<span data-ttu-id="150d8-106">This article describes how to find the IoT Hub service in the Azure portal, and how to create and manage IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="150d8-106">This article describes how to find the IoT Hub service in the Azure portal, and how to create and manage IoT hubs.</span></span>

## <a name="where-to-find-iot-hubs"></a><span data-ttu-id="150d8-107">Where to find IoT hubs</span><span class="sxs-lookup"><span data-stu-id="150d8-107">Where to find IoT hubs</span></span>
<span data-ttu-id="150d8-108">There are various places where you can find IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="150d8-108">There are various places where you can find IoT hubs.</span></span>

1. <span data-ttu-id="150d8-109">**+ New**: **Azure IoT Hub** is an IoT service, and can be found in the category **Internet of Things**, under **+ New**, similar to other services.</span><span class="sxs-lookup"><span data-stu-id="150d8-109">**+ New**: **Azure IoT Hub** is an IoT service, and can be found in the category **Internet of Things**, under **+ New**, similar to other services.</span></span>
2. <span data-ttu-id="150d8-110">IoT hubs can also be accessed through the Marketplace as the hero service under **Internet of Things**.</span><span class="sxs-lookup"><span data-stu-id="150d8-110">IoT hubs can also be accessed through the Marketplace as the hero service under **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="150d8-111">Create an IoT hub</span><span class="sxs-lookup"><span data-stu-id="150d8-111">Create an IoT hub</span></span>
<span data-ttu-id="150d8-112">You can create an IoT hub using the following methods:</span><span class="sxs-lookup"><span data-stu-id="150d8-112">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="150d8-113">Creating an IoT hub through the **+ New** option leads to the blade shown in the next screen shot.</span><span class="sxs-lookup"><span data-stu-id="150d8-113">Creating an IoT hub through the **+ New** option leads to the blade shown in the next screen shot.</span></span> <span data-ttu-id="150d8-114">The steps for creating the IoT hub through this method and through the marketplace are identical.</span><span class="sxs-lookup"><span data-stu-id="150d8-114">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="150d8-115">Creating an IoT hub through the Marketplace: Clicking **Create** opens a blade that is identical to the previous blade for the **+New** experience.</span><span class="sxs-lookup"><span data-stu-id="150d8-115">Creating an IoT hub through the Marketplace: Clicking **Create** opens a blade that is identical to the previous blade for the **+New** experience.</span></span> <span data-ttu-id="150d8-116">The next sections list the several steps involved in creating an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-116">The next sections list the several steps involved in creating an IoT hub.</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="150d8-117">Choose the name of the IoT hub</span><span class="sxs-lookup"><span data-stu-id="150d8-117">Choose the name of the IoT hub</span></span>
<span data-ttu-id="150d8-118">To create an IoT hub, you must name the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-118">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="150d8-119">This name must be unique across the IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="150d8-119">This name must be unique across the IoT hubs.</span></span> <span data-ttu-id="150d8-120">No duplication of hubs is allowed on the solution back end, so it is recommended that this hub is named as uniquely as possible.</span><span class="sxs-lookup"><span data-stu-id="150d8-120">No duplication of hubs is allowed on the solution back end, so it is recommended that this hub is named as uniquely as possible.</span></span>

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="150d8-121">Choose the pricing tier</span><span class="sxs-lookup"><span data-stu-id="150d8-121">Choose the pricing tier</span></span>
<span data-ttu-id="150d8-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span><span class="sxs-lookup"><span data-stu-id="150d8-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="150d8-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span><span class="sxs-lookup"><span data-stu-id="150d8-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="150d8-124">**Standard S1**: IoT Hubs S1 edition is designed for IoT solutions that have a large number of devices generating relatively small amounts of data per device.</span><span class="sxs-lookup"><span data-stu-id="150d8-124">**Standard S1**: IoT Hubs S1 edition is designed for IoT solutions that have a large number of devices generating relatively small amounts of data per device.</span></span> <span data-ttu-id="150d8-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span><span class="sxs-lookup"><span data-stu-id="150d8-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="150d8-126">**Standard S2**: IoT Hub S2 edition is designed for IoT solutions in which devices generate large amounts of data.</span><span class="sxs-lookup"><span data-stu-id="150d8-126">**Standard S2**: IoT Hub S2 edition is designed for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="150d8-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span><span class="sxs-lookup"><span data-stu-id="150d8-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="150d8-128">**Standard S3**: IoT Hub S3 edition is designed for IoT solutions that generate large amounts of data.</span><span class="sxs-lookup"><span data-stu-id="150d8-128">**Standard S3**: IoT Hub S3 edition is designed for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="150d8-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span><span class="sxs-lookup"><span data-stu-id="150d8-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="150d8-130">IoT Hub only allows one free hub per Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="150d8-130">IoT Hub only allows one free hub per Azure subscription.</span></span>
> 
> 

### <a name="iot-hub-units"></a><span data-ttu-id="150d8-131">IoT hub units</span><span class="sxs-lookup"><span data-stu-id="150d8-131">IoT hub units</span></span>
<span data-ttu-id="150d8-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span><span class="sxs-lookup"><span data-stu-id="150d8-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="150d8-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span><span class="sxs-lookup"><span data-stu-id="150d8-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="150d8-134">Device to cloud partitions and resource group</span><span class="sxs-lookup"><span data-stu-id="150d8-134">Device to cloud partitions and resource group</span></span>
<span data-ttu-id="150d8-135">You can change the number of partitions for an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="150d8-136">Default partitions are set to 4; however, you can choose a different number of partitions from a drop-down list.</span><span class="sxs-lookup"><span data-stu-id="150d8-136">Default partitions are set to 4; however, you can choose a different number of partitions from a drop-down list.</span></span>

<span data-ttu-id="150d8-137">For resource groups, you do not need to explicitly create an empty resource group.</span><span class="sxs-lookup"><span data-stu-id="150d8-137">For resource groups, you do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="150d8-138">When creating a resource, you can choose to either create a new resource group or use an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="150d8-138">When creating a resource, you can choose to either create a new resource group or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscriptions"></a><span data-ttu-id="150d8-139">Choose subscriptions</span><span class="sxs-lookup"><span data-stu-id="150d8-139">Choose subscriptions</span></span>
<span data-ttu-id="150d8-140">Azure IoT Hub automatically shows the list of Azure subscriptions to which the user account is linked.</span><span class="sxs-lookup"><span data-stu-id="150d8-140">Azure IoT Hub automatically shows the list of Azure subscriptions to which the user account is linked.</span></span> <span data-ttu-id="150d8-141">You can choose one of the options here to associate the IoT hub with that Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="150d8-141">You can choose one of the options here to associate the IoT hub with that Azure subscription.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="150d8-142">Choose the location</span><span class="sxs-lookup"><span data-stu-id="150d8-142">Choose the location</span></span>
<span data-ttu-id="150d8-143">The location option provides a list of the regions in which IoT Hub is offered.</span><span class="sxs-lookup"><span data-stu-id="150d8-143">The location option provides a list of the regions in which IoT Hub is offered.</span></span> <span data-ttu-id="150d8-144">IoT Hub is available to deploy in the following locations: Australia East, Australia Southeast, Asia East, Asia Southeast, Europe North, Europe West, Japan East, Japan West, US East, US West.</span><span class="sxs-lookup"><span data-stu-id="150d8-144">IoT Hub is available to deploy in the following locations: Australia East, Australia Southeast, Asia East, Asia Southeast, Europe North, Europe West, Japan East, Japan West, US East, US West.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="150d8-145">Create the IoT hub</span><span class="sxs-lookup"><span data-stu-id="150d8-145">Create the IoT hub</span></span>
<span data-ttu-id="150d8-146">When all previous steps are complete, the IoT hub is ready to be created.</span><span class="sxs-lookup"><span data-stu-id="150d8-146">When all previous steps are complete, the IoT hub is ready to be created.</span></span> <span data-ttu-id="150d8-147">Click **Create** to start the back-end process of creating this IoT hub with the specific options, and to deploy it to the location specified.</span><span class="sxs-lookup"><span data-stu-id="150d8-147">Click **Create** to start the back-end process of creating this IoT hub with the specific options, and to deploy it to the location specified.</span></span>

<span data-ttu-id="150d8-148">It can take a few minutes for the IoT hub to be created as it takes time for the back-end deployment to occur in the appropriate location servers.</span><span class="sxs-lookup"><span data-stu-id="150d8-148">It can take a few minutes for the IoT hub to be created as it takes time for the back-end deployment to occur in the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="150d8-149">Change the settings of the IoT hub</span><span class="sxs-lookup"><span data-stu-id="150d8-149">Change the settings of the IoT hub</span></span>
<span data-ttu-id="150d8-150">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span><span class="sxs-lookup"><span data-stu-id="150d8-150">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="150d8-151">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-151">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="150d8-152">You can access these policies by clicking **Shared access policies** under **General**.</span><span class="sxs-lookup"><span data-stu-id="150d8-152">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="150d8-153">In this blade, you can either modify existing policies or add a new policy.</span><span class="sxs-lookup"><span data-stu-id="150d8-153">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="150d8-154">Create a policy</span><span class="sxs-lookup"><span data-stu-id="150d8-154">Create a policy</span></span>
* <span data-ttu-id="150d8-155">Click **Add** to open a blade.</span><span class="sxs-lookup"><span data-stu-id="150d8-155">Click **Add** to open a blade.</span></span> <span data-ttu-id="150d8-156">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="150d8-156">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>
  
    <span data-ttu-id="150d8-157">There are several permissions that can be associated with these shared policies.</span><span class="sxs-lookup"><span data-stu-id="150d8-157">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="150d8-158">The first two policies, **Registry read** and **Registry write**, grant read and write access rights to the device identity store or the identity registry.</span><span class="sxs-lookup"><span data-stu-id="150d8-158">The first two policies, **Registry read** and **Registry write**, grant read and write access rights to the device identity store or the identity registry.</span></span> <span data-ttu-id="150d8-159">Choosing the write option automatically chooses the read option as well.</span><span class="sxs-lookup"><span data-stu-id="150d8-159">Choosing the write option automatically chooses the read option as well.</span></span>
  
     <span data-ttu-id="150d8-160">The **Service connect** policy grants permission to access the cloud-side endpoints such as the consumer group for services connecting to the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-160">The **Service connect** policy grants permission to access the cloud-side endpoints such as the consumer group for services connecting to the IoT hub.</span></span> <span data-ttu-id="150d8-161">The **Device connect** policy grants permissions for sending and receiving messages on the device-side endpoints of the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-161">The **Device connect** policy grants permissions for sending and receiving messages on the device-side endpoints of the IoT hub.</span></span>
* <span data-ttu-id="150d8-162">Click **Create** to add this newly created policy to the existing list.</span><span class="sxs-lookup"><span data-stu-id="150d8-162">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="150d8-163">Endpoints</span><span class="sxs-lookup"><span data-stu-id="150d8-163">Endpoints</span></span>
<span data-ttu-id="150d8-164">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span><span class="sxs-lookup"><span data-stu-id="150d8-164">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="150d8-165">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span><span class="sxs-lookup"><span data-stu-id="150d8-165">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="150d8-166">Built-in endpoints</span><span class="sxs-lookup"><span data-stu-id="150d8-166">Built-in endpoints</span></span>
<span data-ttu-id="150d8-167">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span><span class="sxs-lookup"><span data-stu-id="150d8-167">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="150d8-168">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span><span class="sxs-lookup"><span data-stu-id="150d8-168">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="150d8-169">When your first create an IoT hub, both these settings have the default value of one hour.</span><span class="sxs-lookup"><span data-stu-id="150d8-169">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="150d8-170">To adjust these settings, use the sliders or type the values.</span><span class="sxs-lookup"><span data-stu-id="150d8-170">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="150d8-171">**Events** settings: This setting has several subsettings, some of which are read-only.</span><span class="sxs-lookup"><span data-stu-id="150d8-171">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="150d8-172">The following list describes these settings:</span><span class="sxs-lookup"><span data-stu-id="150d8-172">The following list describes these settings:</span></span>

    * <span data-ttu-id="150d8-173">**Partitions**: A default value is set when the IoT hub is created.</span><span class="sxs-lookup"><span data-stu-id="150d8-173">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="150d8-174">You can change the number of partitions through this setting.</span><span class="sxs-lookup"><span data-stu-id="150d8-174">You can change the number of partitions through this setting.</span></span>

    * <span data-ttu-id="150d8-175">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span><span class="sxs-lookup"><span data-stu-id="150d8-175">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="150d8-176">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span><span class="sxs-lookup"><span data-stu-id="150d8-176">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

    * <span data-ttu-id="150d8-177">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="150d8-177">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="150d8-178">This value is in days for the device-to-cloud setting.</span><span class="sxs-lookup"><span data-stu-id="150d8-178">This value is in days for the device-to-cloud setting.</span></span>

    * <span data-ttu-id="150d8-179">**Consumer Groups**: Consumer groups are a setting similar to other messaging systems that can be used to pull data in specific ways to connect other applications or services to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-179">**Consumer Groups**: Consumer groups are a setting similar to other messaging systems that can be used to pull data in specific ways to connect other applications or services to IoT Hub.</span></span> <span data-ttu-id="150d8-180">Every IoT hub is created with a default consumer group.</span><span class="sxs-lookup"><span data-stu-id="150d8-180">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="150d8-181">However, you can add or delete consumer groups to your IoT hubs using this setting.</span><span class="sxs-lookup"><span data-stu-id="150d8-181">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

    > [!NOTE]
    > <span data-ttu-id="150d8-182">The default consumer group cannot be edited or deleted.</span><span class="sxs-lookup"><span data-stu-id="150d8-182">The default consumer group cannot be edited or deleted.</span></span>
    > 
    > 

### <a name="custom-endpoints"></a><span data-ttu-id="150d8-183">Custom endpoints</span><span class="sxs-lookup"><span data-stu-id="150d8-183">Custom endpoints</span></span>
<span data-ttu-id="150d8-184">You can add custom endpoints on your IoT hub using the portal.</span><span class="sxs-lookup"><span data-stu-id="150d8-184">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="150d8-185">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span><span class="sxs-lookup"><span data-stu-id="150d8-185">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="150d8-186">Enter the required information, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="150d8-186">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="150d8-187">Your custom endpoint is now listed in the main **Endpoints** blade.</span><span class="sxs-lookup"><span data-stu-id="150d8-187">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="150d8-188">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="150d8-188">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="150d8-189">Routes</span><span class="sxs-lookup"><span data-stu-id="150d8-189">Routes</span></span>
<span data-ttu-id="150d8-190">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span><span class="sxs-lookup"><span data-stu-id="150d8-190">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="150d8-191">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes**\* blade, entering the required information, and clicking **OK**.</span><span class="sxs-lookup"><span data-stu-id="150d8-191">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes**\* blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="150d8-192">Your route is then listed in the main **Routes** blade.</span><span class="sxs-lookup"><span data-stu-id="150d8-192">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="150d8-193">You can edit a route by clicking it in the list of routes.</span><span class="sxs-lookup"><span data-stu-id="150d8-193">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="150d8-194">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span><span class="sxs-lookup"><span data-stu-id="150d8-194">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="150d8-195">Click **OK** at the bottom of the blade to save the change.</span><span class="sxs-lookup"><span data-stu-id="150d8-195">Click **OK** at the bottom of the blade to save the change.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="150d8-196">Pricing and scale</span><span class="sxs-lookup"><span data-stu-id="150d8-196">Pricing and scale</span></span>
<span data-ttu-id="150d8-197">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span><span class="sxs-lookup"><span data-stu-id="150d8-197">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="150d8-198">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span><span class="sxs-lookup"><span data-stu-id="150d8-198">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="150d8-199">There can only be one free tier IoT hub in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="150d8-199">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="150d8-200">Moving from a higher tier (S2 or S3) to lower tier (S1 or S2) is allowed only when the number of messages sent for that day are not in conflict.</span><span class="sxs-lookup"><span data-stu-id="150d8-200">Moving from a higher tier (S2 or S3) to lower tier (S1 or S2) is allowed only when the number of messages sent for that day are not in conflict.</span></span> <span data-ttu-id="150d8-201">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span><span class="sxs-lookup"><span data-stu-id="150d8-201">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="150d8-202">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span><span class="sxs-lookup"><span data-stu-id="150d8-202">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="150d8-203">Delete the IoT hub</span><span class="sxs-lookup"><span data-stu-id="150d8-203">Delete the IoT hub</span></span>
<span data-ttu-id="150d8-204">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span><span class="sxs-lookup"><span data-stu-id="150d8-204">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="150d8-205">Click the **Delete** button below the IoT hub name to delete the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="150d8-205">Click the **Delete** button below the IoT hub name to delete the IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="150d8-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="150d8-206">Next steps</span></span>
<span data-ttu-id="150d8-207">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="150d8-207">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="150d8-208">[Bulk manage IoT devices][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="150d8-208">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="150d8-209">[IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="150d8-209">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="150d8-210">[Operations monitoring][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="150d8-210">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="150d8-211">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="150d8-211">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="150d8-212">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="150d8-212">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="150d8-213">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="150d8-213">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>
* <span data-ttu-id="150d8-214">[Secure your IoT solution from the ground up][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="150d8-214">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/create-iothub.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/location1.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/portal-settings.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/shared-access-policies.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/messaging-settings.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/pricing-error.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/endpoint-creation.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/routes-list.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/iot-hub/media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md









