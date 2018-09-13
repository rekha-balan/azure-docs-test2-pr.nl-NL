---
title: Architectural concepts in Azure IoT Central | Microsoft Docs
description: This article introduces key concepts relating the architecture of Azure IoT Central
author: dominicbetts
ms.author: dobett
ms.date: 11/30/2017
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: timlt
ms.openlocfilehash: 44408e7b6ad1a068f265bf7b78d973e6aae3001b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967074"
---
# <a name="azure-iot-central-architecture"></a><span data-ttu-id="3b1c0-103">Azure IoT Central architecture</span><span class="sxs-lookup"><span data-stu-id="3b1c0-103">Azure IoT Central architecture</span></span>

<span data-ttu-id="3b1c0-104">This article provides an overview of the Microsoft Azure IoT Central architecture.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-104">This article provides an overview of the Microsoft Azure IoT Central architecture.</span></span>

![Top-level architecture](media/concepts-architecture/architecture.png)

## <a name="devices"></a><span data-ttu-id="3b1c0-106">Devices</span><span class="sxs-lookup"><span data-stu-id="3b1c0-106">Devices</span></span>

<span data-ttu-id="3b1c0-107">Devices exchange data with your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-107">Devices exchange data with your Azure IoT Central application.</span></span> <span data-ttu-id="3b1c0-108">A device can:</span><span class="sxs-lookup"><span data-stu-id="3b1c0-108">A device can:</span></span>

- <span data-ttu-id="3b1c0-109">Send measurements such as telemetry.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-109">Send measurements such as telemetry.</span></span>
- <span data-ttu-id="3b1c0-110">Synchronize settings with your application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-110">Synchronize settings with your application.</span></span>

<span data-ttu-id="3b1c0-111">In Azure IoT Central, the data that a device can exchange with your application is specified in a device template.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-111">In Azure IoT Central, the data that a device can exchange with your application is specified in a device template.</span></span> <span data-ttu-id="3b1c0-112">For more information about device templates, see [Metadata management](#metadata-management).</span><span class="sxs-lookup"><span data-stu-id="3b1c0-112">For more information about device templates, see [Metadata management](#metadata-management).</span></span>

<span data-ttu-id="3b1c0-113">To learn more about how devices connect to your Azure IoT Central application, see [Device connectivity](concepts-connectivity.md).</span><span class="sxs-lookup"><span data-stu-id="3b1c0-113">To learn more about how devices connect to your Azure IoT Central application, see [Device connectivity](concepts-connectivity.md).</span></span>

## <a name="cloud-gateway"></a><span data-ttu-id="3b1c0-114">Cloud gateway</span><span class="sxs-lookup"><span data-stu-id="3b1c0-114">Cloud gateway</span></span>

<span data-ttu-id="3b1c0-115">Azure IoT Central uses Azure IoT Hub as a cloud gateway that enables device connectivity.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-115">Azure IoT Central uses Azure IoT Hub as a cloud gateway that enables device connectivity.</span></span> <span data-ttu-id="3b1c0-116">IoT Hub enables:</span><span class="sxs-lookup"><span data-stu-id="3b1c0-116">IoT Hub enables:</span></span>

- <span data-ttu-id="3b1c0-117">Data ingestion at scale in the cloud.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-117">Data ingestion at scale in the cloud.</span></span>
- <span data-ttu-id="3b1c0-118">Device management.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-118">Device management.</span></span>
- <span data-ttu-id="3b1c0-119">Secure device connectivity.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-119">Secure device connectivity.</span></span>

<span data-ttu-id="3b1c0-120">To learn more about IoT Hub, see [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="3b1c0-120">To learn more about IoT Hub, see [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/).</span></span>

<span data-ttu-id="3b1c0-121">To learn more about device connectivity in Azure IoT Central, see [Device connectivity](concepts-connectivity.md).</span><span class="sxs-lookup"><span data-stu-id="3b1c0-121">To learn more about device connectivity in Azure IoT Central, see [Device connectivity](concepts-connectivity.md).</span></span>

## <a name="data-stores"></a><span data-ttu-id="3b1c0-122">Data stores</span><span class="sxs-lookup"><span data-stu-id="3b1c0-122">Data stores</span></span>

<span data-ttu-id="3b1c0-123">Azure IoT Central stores application data in the cloud.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-123">Azure IoT Central stores application data in the cloud.</span></span> <span data-ttu-id="3b1c0-124">Application data stored includes:</span><span class="sxs-lookup"><span data-stu-id="3b1c0-124">Application data stored includes:</span></span>

- <span data-ttu-id="3b1c0-125">Device templates.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-125">Device templates.</span></span>
- <span data-ttu-id="3b1c0-126">Device identities.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-126">Device identities.</span></span>
- <span data-ttu-id="3b1c0-127">Device metadata.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-127">Device metadata.</span></span>
- <span data-ttu-id="3b1c0-128">User and role data.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-128">User and role data.</span></span>

<span data-ttu-id="3b1c0-129">Azure IoT Central uses a time series store for the measurement data sent from your devices.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-129">Azure IoT Central uses a time series store for the measurement data sent from your devices.</span></span> <span data-ttu-id="3b1c0-130">Time series data from devices used by the analytics service.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-130">Time series data from devices used by the analytics service.</span></span>

## <a name="analytics"></a><span data-ttu-id="3b1c0-131">Analytics</span><span class="sxs-lookup"><span data-stu-id="3b1c0-131">Analytics</span></span>

<span data-ttu-id="3b1c0-132">The analytics service is responsible for generating the custom reporting data that the application displays.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-132">The analytics service is responsible for generating the custom reporting data that the application displays.</span></span> <span data-ttu-id="3b1c0-133">An operator can [customize the analytics](howto-create-analytics.md) displayed in the application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-133">An operator can [customize the analytics](howto-create-analytics.md) displayed in the application.</span></span> <span data-ttu-id="3b1c0-134">The analytics service is built on top of [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/) and processes the measurement data sent from your devices.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-134">The analytics service is built on top of [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/) and processes the measurement data sent from your devices.</span></span>

## <a name="rules-and-actions"></a><span data-ttu-id="3b1c0-135">Rules and actions</span><span class="sxs-lookup"><span data-stu-id="3b1c0-135">Rules and actions</span></span>

<span data-ttu-id="3b1c0-136">[Rules and actions](howto-create-telemetry-rules.md) work closely together to automate tasks within the application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-136">[Rules and actions](howto-create-telemetry-rules.md) work closely together to automate tasks within the application.</span></span> <span data-ttu-id="3b1c0-137">A builder can define rules based on device telemetry such as the temperature exceeding a defined threshold.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-137">A builder can define rules based on device telemetry such as the temperature exceeding a defined threshold.</span></span> <span data-ttu-id="3b1c0-138">Azure IoT Central uses a stream processor to determine when the rule conditions are met.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-138">Azure IoT Central uses a stream processor to determine when the rule conditions are met.</span></span> <span data-ttu-id="3b1c0-139">When a rule condition is met, it triggers an action defined by the builder.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-139">When a rule condition is met, it triggers an action defined by the builder.</span></span> <span data-ttu-id="3b1c0-140">For example, an action can send an email to notify an engineer that the temperature in a device is too high.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-140">For example, an action can send an email to notify an engineer that the temperature in a device is too high.</span></span>

## <a name="metadata-management"></a><span data-ttu-id="3b1c0-141">Metadata management</span><span class="sxs-lookup"><span data-stu-id="3b1c0-141">Metadata management</span></span>

<span data-ttu-id="3b1c0-142">In an Azure IoT Central application, device templates define the behavior and capability of types of device.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-142">In an Azure IoT Central application, device templates define the behavior and capability of types of device.</span></span> <span data-ttu-id="3b1c0-143">For example, a refrigerator device template specifies the telemetry a refrigerator sends to your application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-143">For example, a refrigerator device template specifies the telemetry a refrigerator sends to your application.</span></span>

![Template architecture](media/concepts-architecture/template_architecture.png)

<span data-ttu-id="3b1c0-145">In a device template:</span><span class="sxs-lookup"><span data-stu-id="3b1c0-145">In a device template:</span></span>

- <span data-ttu-id="3b1c0-146">**Measurements** specify the telemetry the device sends to the application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-146">**Measurements** specify the telemetry the device sends to the application.</span></span>
- <span data-ttu-id="3b1c0-147">**Settings** specify the configurations that an operator can set.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-147">**Settings** specify the configurations that an operator can set.</span></span>
- <span data-ttu-id="3b1c0-148">**Properties** specify metadata that an operator can set.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-148">**Properties** specify metadata that an operator can set.</span></span>
- <span data-ttu-id="3b1c0-149">**Rules** automate behavior in the application based on data sent from a device.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-149">**Rules** automate behavior in the application based on data sent from a device.</span></span>
- <span data-ttu-id="3b1c0-150">**Dashboards** are customizable views of a device in the application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-150">**Dashboards** are customizable views of a device in the application.</span></span>

<span data-ttu-id="3b1c0-151">An application can have one or more simulated and real devices based on each device template.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-151">An application can have one or more simulated and real devices based on each device template.</span></span>

## <a name="rbac"></a><span data-ttu-id="3b1c0-152">RBAC</span><span class="sxs-lookup"><span data-stu-id="3b1c0-152">RBAC</span></span>

<span data-ttu-id="3b1c0-153">An [administrator can define access rules](howto-administer.md) for an Azure IoT Central application using the predefined roles.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-153">An [administrator can define access rules](howto-administer.md) for an Azure IoT Central application using the predefined roles.</span></span> <span data-ttu-id="3b1c0-154">An administrator can assign users to roles that determine what areas of the application the user has access to.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-154">An administrator can assign users to roles that determine what areas of the application the user has access to.</span></span>

## <a name="security"></a><span data-ttu-id="3b1c0-155">Security</span><span class="sxs-lookup"><span data-stu-id="3b1c0-155">Security</span></span>

<span data-ttu-id="3b1c0-156">Security features within Azure IoT Central include:</span><span class="sxs-lookup"><span data-stu-id="3b1c0-156">Security features within Azure IoT Central include:</span></span>

- <span data-ttu-id="3b1c0-157">Data is encrypted in transit and at rest.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-157">Data is encrypted in transit and at rest.</span></span>
- <span data-ttu-id="3b1c0-158">Authentication is provided either by Azure Active Directory or Microsoft Account.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-158">Authentication is provided either by Azure Active Directory or Microsoft Account.</span></span> <span data-ttu-id="3b1c0-159">Two-factor authentication is supported.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-159">Two-factor authentication is supported.</span></span>
- <span data-ttu-id="3b1c0-160">Full tenant isolation.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-160">Full tenant isolation.</span></span>
- <span data-ttu-id="3b1c0-161">Device level security.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-161">Device level security.</span></span>

## <a name="ui-shell"></a><span data-ttu-id="3b1c0-162">UI shell</span><span class="sxs-lookup"><span data-stu-id="3b1c0-162">UI shell</span></span>

<span data-ttu-id="3b1c0-163">The UI shell is a modern, responsive, HTML5 browser-based application.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-163">The UI shell is a modern, responsive, HTML5 browser-based application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b1c0-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b1c0-164">Next steps</span></span>

<span data-ttu-id="3b1c0-165">Now that you have learned about the architecture of Azure IoT Central, the suggested next step is to learn about [device connectivity](concepts-connectivity.md) in Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="3b1c0-165">Now that you have learned about the architecture of Azure IoT Central, the suggested next step is to learn about [device connectivity](concepts-connectivity.md) in Azure IoT Central.</span></span>