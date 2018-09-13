---
title: Upgrade Azure IoT Hub | Microsoft Docs
description: Change the pricing and scale tier for IoT Hub to get more messaging and device management capabilities.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 04/02/2018
ms.author: kgremban
ms.openlocfilehash: e1342ed574d84ed5b4edd5060c2d6d3ec8bca1a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856417"
---
# <a name="how-to-upgrade-your-iot-hub"></a><span data-ttu-id="21f13-103">How to upgrade your IoT hub</span><span class="sxs-lookup"><span data-stu-id="21f13-103">How to upgrade your IoT hub</span></span>

<span data-ttu-id="21f13-104">As your IoT solution grows, Azure IoT Hub is ready to help you scale up.</span><span class="sxs-lookup"><span data-stu-id="21f13-104">As your IoT solution grows, Azure IoT Hub is ready to help you scale up.</span></span> <span data-ttu-id="21f13-105">Azure IoT Hub offers two tiers, basic (B) and standard (S), to accommodate customers that want to use different features.</span><span class="sxs-lookup"><span data-stu-id="21f13-105">Azure IoT Hub offers two tiers, basic (B) and standard (S), to accommodate customers that want to use different features.</span></span> <span data-ttu-id="21f13-106">Within each tier are three sizes (1, 2, and 3) that determine the number of messages that can be sent each day.</span><span class="sxs-lookup"><span data-stu-id="21f13-106">Within each tier are three sizes (1, 2, and 3) that determine the number of messages that can be sent each day.</span></span> 

<span data-ttu-id="21f13-107">When you have more devices and need more capabilities, there are three ways to adjust your IoT hub to suit your needs:</span><span class="sxs-lookup"><span data-stu-id="21f13-107">When you have more devices and need more capabilities, there are three ways to adjust your IoT hub to suit your needs:</span></span>

* <span data-ttu-id="21f13-108">Add units within the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="21f13-108">Add units within the IoT hub.</span></span> <span data-ttu-id="21f13-109">For example, each additional unit in a B1 IoT hub allows for an additional 400,000 messages per day.</span><span class="sxs-lookup"><span data-stu-id="21f13-109">For example, each additional unit in a B1 IoT hub allows for an additional 400,000 messages per day.</span></span> 
* <span data-ttu-id="21f13-110">Change the size of the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="21f13-110">Change the size of the IoT hub.</span></span> <span data-ttu-id="21f13-111">For example, migrate from the B1 tier to the B2 tier to increase the amount of messages that each unit can support per day.</span><span class="sxs-lookup"><span data-stu-id="21f13-111">For example, migrate from the B1 tier to the B2 tier to increase the amount of messages that each unit can support per day.</span></span>
* <span data-ttu-id="21f13-112">Upgrade to a higher tier.</span><span class="sxs-lookup"><span data-stu-id="21f13-112">Upgrade to a higher tier.</span></span> <span data-ttu-id="21f13-113">For example, upgrade from the B1 tier to the S1 tier for the same messaging capacity but with the advanced features that come in the standard tier.</span><span class="sxs-lookup"><span data-stu-id="21f13-113">For example, upgrade from the B1 tier to the S1 tier for the same messaging capacity but with the advanced features that come in the standard tier.</span></span>

<span data-ttu-id="21f13-114">These changes can all occur without interrupting existing operations.</span><span class="sxs-lookup"><span data-stu-id="21f13-114">These changes can all occur without interrupting existing operations.</span></span>

<span data-ttu-id="21f13-115">If you want to downgrade your IoT hub, you can remove units and reduce the size of the IoT hub.</span><span class="sxs-lookup"><span data-stu-id="21f13-115">If you want to downgrade your IoT hub, you can remove units and reduce the size of the IoT hub.</span></span> <span data-ttu-id="21f13-116">However, you cannot downgrade to a lower tier.</span><span class="sxs-lookup"><span data-stu-id="21f13-116">However, you cannot downgrade to a lower tier.</span></span> <span data-ttu-id="21f13-117">For example, you can move from the S2 tier to the S1 tier, but not from the S2 tier to the B1 tier.</span><span class="sxs-lookup"><span data-stu-id="21f13-117">For example, you can move from the S2 tier to the S1 tier, but not from the S2 tier to the B1 tier.</span></span> <span data-ttu-id="21f13-118">Also note that only one type of [edition](https://azure.microsoft.com/pricing/details/iot-hub/) within a tier can be chosen per IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="21f13-118">Also note that only one type of [edition](https://azure.microsoft.com/pricing/details/iot-hub/) within a tier can be chosen per IoT Hub.</span></span> <span data-ttu-id="21f13-119">For example, you can create an IoT Hub with multiple units of S1, but not with a mix of units from different editions, such as S1 and B3, or S1 and S2.</span><span class="sxs-lookup"><span data-stu-id="21f13-119">For example, you can create an IoT Hub with multiple units of S1, but not with a mix of units from different editions, such as S1 and B3, or S1 and S2.</span></span>

<span data-ttu-id="21f13-120">These examples are meant to help you understand how to adjust your IoT hub as your solution changes.</span><span class="sxs-lookup"><span data-stu-id="21f13-120">These examples are meant to help you understand how to adjust your IoT hub as your solution changes.</span></span> <span data-ttu-id="21f13-121">For specific information about each tier's capabilities you should always refer to [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="21f13-121">For specific information about each tier's capabilities you should always refer to [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span> 

## <a name="upgrade-your-existing-iot-hub"></a><span data-ttu-id="21f13-122">Upgrade your existing IoT hub</span><span class="sxs-lookup"><span data-stu-id="21f13-122">Upgrade your existing IoT hub</span></span> 

1. <span data-ttu-id="21f13-123">Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="21f13-123">Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your IoT hub.</span></span> 
2. <span data-ttu-id="21f13-124">Select **Pricing and scale**.</span><span class="sxs-lookup"><span data-stu-id="21f13-124">Select **Pricing and scale**.</span></span> 

   ![Pricing and scale](./media/iot-hub-upgrade/pricing-scale.png)

3. <span data-ttu-id="21f13-126">To change the tier for your hub, select **Pricing and scale tier**.</span><span class="sxs-lookup"><span data-stu-id="21f13-126">To change the tier for your hub, select **Pricing and scale tier**.</span></span> <span data-ttu-id="21f13-127">Choose the new tier, then click **select**.</span><span class="sxs-lookup"><span data-stu-id="21f13-127">Choose the new tier, then click **select**.</span></span>

   ![Pricing and scale](./media/iot-hub-upgrade/select-tier.png)

4. <span data-ttu-id="21f13-129">To change the number of units in your hub, enter a new value under **IoT Hub units**.</span><span class="sxs-lookup"><span data-stu-id="21f13-129">To change the number of units in your hub, enter a new value under **IoT Hub units**.</span></span> 
5. <span data-ttu-id="21f13-130">Select **Save** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="21f13-130">Select **Save** to save your changes.</span></span> 

<span data-ttu-id="21f13-131">Your IoT hub is now adjusted, and your configurations are unchanged.</span><span class="sxs-lookup"><span data-stu-id="21f13-131">Your IoT hub is now adjusted, and your configurations are unchanged.</span></span> <span data-ttu-id="21f13-132">Note that the maximum partition limit for basic tier IoT Hub is 8 and for standard tier is 32.</span><span class="sxs-lookup"><span data-stu-id="21f13-132">Note that the maximum partition limit for basic tier IoT Hub is 8 and for standard tier is 32.</span></span> <span data-ttu-id="21f13-133">Most IoT Hubs only need 4 partitions.</span><span class="sxs-lookup"><span data-stu-id="21f13-133">Most IoT Hubs only need 4 partitions.</span></span> <span data-ttu-id="21f13-134">The partition limit is chosen when IoT Hub is created, and relates the device-to-cloud messages to the number of simultaneous readers of these messages.</span><span class="sxs-lookup"><span data-stu-id="21f13-134">The partition limit is chosen when IoT Hub is created, and relates the device-to-cloud messages to the number of simultaneous readers of these messages.</span></span> <span data-ttu-id="21f13-135">This value remains unchanged when you migrate from basic tier to standard tier.</span><span class="sxs-lookup"><span data-stu-id="21f13-135">This value remains unchanged when you migrate from basic tier to standard tier.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="21f13-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="21f13-136">Next steps</span></span>

<span data-ttu-id="21f13-137">Get more details about [How to choose the right IoT Hub tier](iot-hub-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="21f13-137">Get more details about [How to choose the right IoT Hub tier](iot-hub-scaling.md).</span></span> 

