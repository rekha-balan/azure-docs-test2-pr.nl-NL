---
title: Connected Factory solution features - Azure | Microsoft Docs
description: An overview of the features of the Connected Factory preconfigured solution.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: dobett
ms.openlocfilehash: 3478217771418ab31772d6a42a7ed8d8a2e8069a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871668"
---
# <a name="what-is-connected-factory-iot-solution-accelerator"></a><span data-ttu-id="d26e9-103">What is Connected Factory IoT solution accelerator?</span><span class="sxs-lookup"><span data-stu-id="d26e9-103">What is Connected Factory IoT solution accelerator?</span></span>

<span data-ttu-id="d26e9-104">Connected Factory is an implementation of Microsoft's Azure Industrial IoT reference architecture, packaged as on open-source solution.</span><span class="sxs-lookup"><span data-stu-id="d26e9-104">Connected Factory is an implementation of Microsoft's Azure Industrial IoT reference architecture, packaged as on open-source solution.</span></span> <span data-ttu-id="d26e9-105">You can use it as a starting point for a commercial product.</span><span class="sxs-lookup"><span data-stu-id="d26e9-105">You can use it as a starting point for a commercial product.</span></span> <span data-ttu-id="d26e9-106">You can deploy a pre-built version of the Connected Factory solution into your Azure subscription from [Azure IoT solution accelerators](https://www.azureiotsolutions.com/#solutions/types/CF).</span><span class="sxs-lookup"><span data-stu-id="d26e9-106">You can deploy a pre-built version of the Connected Factory solution into your Azure subscription from [Azure IoT solution accelerators](https://www.azureiotsolutions.com/#solutions/types/CF).</span></span>

![Connected Factory solution dashboard](./media/iot-accelerators-connected-factory-features/dashboard.png)

<span data-ttu-id="d26e9-108">Connected Factory includes the following features:</span><span class="sxs-lookup"><span data-stu-id="d26e9-108">Connected Factory includes the following features:</span></span>

## <a name="industrial-device-interoperability"></a><span data-ttu-id="d26e9-109">Industrial device interoperability</span><span class="sxs-lookup"><span data-stu-id="d26e9-109">Industrial device interoperability</span></span>

- <span data-ttu-id="d26e9-110">Connect to industrial assets with an OPC UA interface.</span><span class="sxs-lookup"><span data-stu-id="d26e9-110">Connect to industrial assets with an OPC UA interface.</span></span>
- <span data-ttu-id="d26e9-111">Use the simulated production lines (running OPC UA servers in Docker containers) to see live telemetry from them.</span><span class="sxs-lookup"><span data-stu-id="d26e9-111">Use the simulated production lines (running OPC UA servers in Docker containers) to see live telemetry from them.</span></span>
- <span data-ttu-id="d26e9-112">Browse the OPC UA information model of the OPC UA servers from a cloud dashboard.</span><span class="sxs-lookup"><span data-stu-id="d26e9-112">Browse the OPC UA information model of the OPC UA servers from a cloud dashboard.</span></span>

## <a name="remote-management"></a><span data-ttu-id="d26e9-113">Remote management</span><span class="sxs-lookup"><span data-stu-id="d26e9-113">Remote management</span></span>

- <span data-ttu-id="d26e9-114">Configure your OPC UA assets from the cloud dashboard (call methods, read, and write data).</span><span class="sxs-lookup"><span data-stu-id="d26e9-114">Configure your OPC UA assets from the cloud dashboard (call methods, read, and write data).</span></span>
- <span data-ttu-id="d26e9-115">Publish and unpublish telemetry data from your OPC UA assets from a cloud dashboard.</span><span class="sxs-lookup"><span data-stu-id="d26e9-115">Publish and unpublish telemetry data from your OPC UA assets from a cloud dashboard.</span></span>

## <a name="cloud-dashboard"></a><span data-ttu-id="d26e9-116">Cloud dashboard</span><span class="sxs-lookup"><span data-stu-id="d26e9-116">Cloud dashboard</span></span>

- <span data-ttu-id="d26e9-117">View telemetry previews directly in a cloud dashboard.</span><span class="sxs-lookup"><span data-stu-id="d26e9-117">View telemetry previews directly in a cloud dashboard.</span></span>
- <span data-ttu-id="d26e9-118">View trends in telemetry data and create correlations using the Time Series Insights Explorer dashboard.</span><span class="sxs-lookup"><span data-stu-id="d26e9-118">View trends in telemetry data and create correlations using the Time Series Insights Explorer dashboard.</span></span>
- <span data-ttu-id="d26e9-119">See calculated Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) from a cloud dashboard.</span><span class="sxs-lookup"><span data-stu-id="d26e9-119">See calculated Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) from a cloud dashboard.</span></span>
- <span data-ttu-id="d26e9-120">View industrial asset hierarchies in a tree topology as well as on an interactive map.</span><span class="sxs-lookup"><span data-stu-id="d26e9-120">View industrial asset hierarchies in a tree topology as well as on an interactive map.</span></span>
- <span data-ttu-id="d26e9-121">View, acknowledge, and close alerts from a cloud dashboard.</span><span class="sxs-lookup"><span data-stu-id="d26e9-121">View, acknowledge, and close alerts from a cloud dashboard.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="d26e9-122">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="d26e9-122">Azure Time Series Insights</span></span>

- <span data-ttu-id="d26e9-123">[Azure Time Series Insights](../time-series-insights/time-series-insights-overview.md) is built for storing, visualizing, and querying large amounts of time-series data.</span><span class="sxs-lookup"><span data-stu-id="d26e9-123">[Azure Time Series Insights](../time-series-insights/time-series-insights-overview.md) is built for storing, visualizing, and querying large amounts of time-series data.</span></span> <span data-ttu-id="d26e9-124">Connected Factory leverages this service.</span><span class="sxs-lookup"><span data-stu-id="d26e9-124">Connected Factory leverages this service.</span></span>
- <span data-ttu-id="d26e9-125">Connected Factory integrates with this service enabling you perform deep, real-time analysis of your device data.</span><span class="sxs-lookup"><span data-stu-id="d26e9-125">Connected Factory integrates with this service enabling you perform deep, real-time analysis of your device data.</span></span>

## <a name="rules-and-alerts"></a><span data-ttu-id="d26e9-126">Rules and alerts</span><span class="sxs-lookup"><span data-stu-id="d26e9-126">Rules and alerts</span></span>

<span data-ttu-id="d26e9-127">[Configure threshold-based rules for alerts](iot-accelerators-connected-factory-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d26e9-127">[Configure threshold-based rules for alerts](iot-accelerators-connected-factory-configure.md).</span></span>

## <a name="end-to-end-security"></a><span data-ttu-id="d26e9-128">End-to-end security</span><span class="sxs-lookup"><span data-stu-id="d26e9-128">End-to-end security</span></span>

- <span data-ttu-id="d26e9-129">Configure security permissions for users using Role-Based Access Control (RBAC).</span><span class="sxs-lookup"><span data-stu-id="d26e9-129">Configure security permissions for users using Role-Based Access Control (RBAC).</span></span>
- <span data-ttu-id="d26e9-130">End-to-end encryption is implemented using OPC UA authentication (using X.509 certificates) as well as security tokens.</span><span class="sxs-lookup"><span data-stu-id="d26e9-130">End-to-end encryption is implemented using OPC UA authentication (using X.509 certificates) as well as security tokens.</span></span>

## <a name="customizability"></a><span data-ttu-id="d26e9-131">Customizability</span><span class="sxs-lookup"><span data-stu-id="d26e9-131">Customizability</span></span>

- <span data-ttu-id="d26e9-132">Customize the solution to meet specific business requirements.</span><span class="sxs-lookup"><span data-stu-id="d26e9-132">Customize the solution to meet specific business requirements.</span></span>
- <span data-ttu-id="d26e9-133">Full solution source-code available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d26e9-133">Full solution source-code available on GitHub.</span></span> <span data-ttu-id="d26e9-134">See the [Connected Factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory) repository.</span><span class="sxs-lookup"><span data-stu-id="d26e9-134">See the [Connected Factory preconfigured solution](https://github.com/Azure/azure-iot-connected-factory) repository.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d26e9-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="d26e9-135">Next steps</span></span>

<span data-ttu-id="d26e9-136">Learn more about the Connected Factory preconfigured solution by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="d26e9-136">Learn more about the Connected Factory preconfigured solution by reading the following articles:</span></span>

* [<span data-ttu-id="d26e9-137">Connected Factory preconfigured solution walkthrough</span><span class="sxs-lookup"><span data-stu-id="d26e9-137">Connected Factory preconfigured solution walkthrough</span></span>](iot-accelerators-connected-factory-sample-walkthrough.md)
* [<span data-ttu-id="d26e9-138">Deploy a gateway for Connected Factory</span><span class="sxs-lookup"><span data-stu-id="d26e9-138">Deploy a gateway for Connected Factory</span></span>]( iot-accelerators-connected-factory-gateway-deployment.md)
