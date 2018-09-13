---
title: Azure Government Internet of Things | Microsoft Docs
description: This provides a comparision of features and guidance on developing IoT Hub applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: gsacavdm
manager: pathuff
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 03/30/2018
ms.author: gsacavdm
ms.openlocfilehash: 77ab2382d29537d81868bd0064ef4178cc0fa65d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856802"
---
# <a name="azure-government-internet-of-things"></a><span data-ttu-id="85913-103">Azure Government Internet of Things</span><span class="sxs-lookup"><span data-stu-id="85913-103">Azure Government Internet of Things</span></span>

## <a name="azure-iot-hub"></a><span data-ttu-id="85913-104">Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="85913-104">Azure IoT Hub</span></span>

<span data-ttu-id="85913-105">Azure IoT Hub is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="85913-105">Azure IoT Hub is generally available in Azure Government.</span></span>

<span data-ttu-id="85913-106">For more information, see [Azure IoT Hub commercial documentation](../iot-hub/index.yml).</span><span class="sxs-lookup"><span data-stu-id="85913-106">For more information, see [Azure IoT Hub commercial documentation](../iot-hub/index.yml).</span></span>

### <a name="variations"></a><span data-ttu-id="85913-107">Variations</span><span class="sxs-lookup"><span data-stu-id="85913-107">Variations</span></span>

<span data-ttu-id="85913-108">The following URL for Azure IoT Hub is different in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="85913-108">The following URL for Azure IoT Hub is different in Azure Government:</span></span>

| <span data-ttu-id="85913-109">Azure Public</span><span class="sxs-lookup"><span data-stu-id="85913-109">Azure Public</span></span>        | <span data-ttu-id="85913-110">Azure Government</span><span class="sxs-lookup"><span data-stu-id="85913-110">Azure Government</span></span>   |
| ------------------- | ------------------ |
| <span data-ttu-id="85913-111">\*.azure-devices.net</span><span class="sxs-lookup"><span data-stu-id="85913-111">\*.azure-devices.net</span></span> | <span data-ttu-id="85913-112">\*.azure-devices.us</span><span class="sxs-lookup"><span data-stu-id="85913-112">\*.azure-devices.us</span></span> |

<span data-ttu-id="85913-113">If you are using the IoT Hub connection string (instead of the Event Hub-compatible settings) with the Microsoft Azure Service Bus .NET client library to receive telemetry or operations monitoring events, then be sure to use WindowsAzure.ServiceBus NuGet package version 4.1.2 or higher.</span><span class="sxs-lookup"><span data-stu-id="85913-113">If you are using the IoT Hub connection string (instead of the Event Hub-compatible settings) with the Microsoft Azure Service Bus .NET client library to receive telemetry or operations monitoring events, then be sure to use WindowsAzure.ServiceBus NuGet package version 4.1.2 or higher.</span></span>

## <a name="azure-event-hubs"></a><span data-ttu-id="85913-114">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="85913-114">Azure Event Hubs</span></span>
<span data-ttu-id="85913-115">For details on this service and how to use it, see [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="85913-115">For details on this service and how to use it, see [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

### <a name="variations"></a><span data-ttu-id="85913-116">Variations</span><span class="sxs-lookup"><span data-stu-id="85913-116">Variations</span></span>

<span data-ttu-id="85913-117">The following URL for Azure Event Hubs is different in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="85913-117">The following URL for Azure Event Hubs is different in Azure Government:</span></span>

| <span data-ttu-id="85913-118">Azure Public</span><span class="sxs-lookup"><span data-stu-id="85913-118">Azure Public</span></span>        | <span data-ttu-id="85913-119">Azure Government</span><span class="sxs-lookup"><span data-stu-id="85913-119">Azure Government</span></span>   | 
| ------------------- | ------------------ | 
| <span data-ttu-id="85913-120">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="85913-120">\*.servicebus.windows.net</span></span> | <span data-ttu-id="85913-121">\*.servicebus.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="85913-121">\*.servicebus.usgovcloudapi.net</span></span> |

## <a name="azure-notification-hubs"></a><span data-ttu-id="85913-122">Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="85913-122">Azure Notification Hubs</span></span>
 <span data-ttu-id="85913-123">Azure Notification Hubs is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="85913-123">Azure Notification Hubs is generally available in Azure Government.</span></span>
 
 <span data-ttu-id="85913-124">For details on this service and how to use it, see [Azure Notification Hubs documentation](../notification-hubs/index.yml).</span><span class="sxs-lookup"><span data-stu-id="85913-124">For details on this service and how to use it, see [Azure Notification Hubs documentation](../notification-hubs/index.yml).</span></span>

### <a name="variations"></a><span data-ttu-id="85913-125">Variations</span><span class="sxs-lookup"><span data-stu-id="85913-125">Variations</span></span>

<span data-ttu-id="85913-126">The URLs for accessing and managing Azure Notification Hub in Azure Government are different:</span><span class="sxs-lookup"><span data-stu-id="85913-126">The URLs for accessing and managing Azure Notification Hub in Azure Government are different:</span></span>

| <span data-ttu-id="85913-127">Azure Public</span><span class="sxs-lookup"><span data-stu-id="85913-127">Azure Public</span></span>        | <span data-ttu-id="85913-128">Azure Government</span><span class="sxs-lookup"><span data-stu-id="85913-128">Azure Government</span></span>   | 
| ------------------- | ------------------ | 
| <span data-ttu-id="85913-129">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="85913-129">\*.servicebus.windows.net</span></span> | <span data-ttu-id="85913-130">\*.servicebus.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="85913-130">\*.servicebus.usgovcloudapi.net</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85913-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="85913-131">Next steps</span></span>

<span data-ttu-id="85913-132">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov).</span><span class="sxs-lookup"><span data-stu-id="85913-132">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov).</span></span>
