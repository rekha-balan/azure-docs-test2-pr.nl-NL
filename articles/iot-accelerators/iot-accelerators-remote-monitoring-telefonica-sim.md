---
title: Integrate SIM data in the Remote Monitoring Solution - Azure| Microsoft Docs
description: This article describes how to integrate Telefónica SIM data into the Remote Monitoring solution.
author: hegate
manager: ''
ms.author: hegate
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 05/15/2018
ms.topic: conceptual
ms.openlocfilehash: c453998eea2a747b2cb608482f0ef9c1ee197ee0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858024"
---
# <a name="integrate-sim-data-in-the-remote-monitoring-solution"></a><span data-ttu-id="99cf5-103">Integrate SIM data in the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="99cf5-103">Integrate SIM data in the Remote Monitoring solution</span></span>

<span data-ttu-id="99cf5-104">IoT devices often connect to the cloud using a SIM card that allows them to send data streams from anywhere.</span><span class="sxs-lookup"><span data-stu-id="99cf5-104">IoT devices often connect to the cloud using a SIM card that allows them to send data streams from anywhere.</span></span> <span data-ttu-id="99cf5-105">The Azure IoT Remote Monitoring solution allows the integration of IoT Managed Connectivity data, so that operators can also track the health of the device through the data provided by the IoT SIM.</span><span class="sxs-lookup"><span data-stu-id="99cf5-105">The Azure IoT Remote Monitoring solution allows the integration of IoT Managed Connectivity data, so that operators can also track the health of the device through the data provided by the IoT SIM.</span></span>

<span data-ttu-id="99cf5-106">Remote Monitoring provides out of the box integration with Telefónica IoT Connectivity, allowing customers using its IoT Connectivity Platform synchronize their device SIMs connectivity data to their solutions.</span><span class="sxs-lookup"><span data-stu-id="99cf5-106">Remote Monitoring provides out of the box integration with Telefónica IoT Connectivity, allowing customers using its IoT Connectivity Platform synchronize their device SIMs connectivity data to their solutions.</span></span> <span data-ttu-id="99cf5-107">This solution can be extended to support other IoT Connectivity providers through GitHub [repository](http://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet).</span><span class="sxs-lookup"><span data-stu-id="99cf5-107">This solution can be extended to support other IoT Connectivity providers through GitHub [repository](http://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet).</span></span>

<span data-ttu-id="99cf5-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="99cf5-108">In this tutorial, you learn how to:</span></span>

* <span data-ttu-id="99cf5-109">Integrate Telefónica IoT SIM data into the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="99cf5-109">Integrate Telefónica IoT SIM data into the Remote Monitoring solution</span></span>
* <span data-ttu-id="99cf5-110">View real-time telemetry</span><span class="sxs-lookup"><span data-stu-id="99cf5-110">View real-time telemetry</span></span>
* <span data-ttu-id="99cf5-111">View SIM data</span><span class="sxs-lookup"><span data-stu-id="99cf5-111">View SIM data</span></span>

## <a name="telefnica-iot-integration-setup"></a><span data-ttu-id="99cf5-112">Telefónica IoT integration setup</span><span class="sxs-lookup"><span data-stu-id="99cf5-112">Telefónica IoT integration setup</span></span>

### <a name="prerequisites"></a><span data-ttu-id="99cf5-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99cf5-113">Prerequisites</span></span>

<span data-ttu-id="99cf5-114">This additional Remote Monitoring feature is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="99cf5-114">This additional Remote Monitoring feature is currently in preview.</span></span> <span data-ttu-id="99cf5-115">To sync your connectivity data into Azure Remote Monitoring Solution, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="99cf5-115">To sync your connectivity data into Azure Remote Monitoring Solution, follow these steps:</span></span>

1. <span data-ttu-id="99cf5-116">Fill a request at [Telefónica's site](https://iot.telefonica.com/contact), select the option **Azure Remote Monitoring**, including your contact data.</span><span class="sxs-lookup"><span data-stu-id="99cf5-116">Fill a request at [Telefónica's site](https://iot.telefonica.com/contact), select the option **Azure Remote Monitoring**, including your contact data.</span></span>
2. <span data-ttu-id="99cf5-117">Telefónica activates your account.</span><span class="sxs-lookup"><span data-stu-id="99cf5-117">Telefónica activates your account.</span></span>
3. <span data-ttu-id="99cf5-118">If you are not a Telefónica client yet and you want to enjoy this or other IoT Connectivity Cloud Ready services, visit [Telefónica's site](https://iot.telefonica.com/) and select the option **Connectivity**.</span><span class="sxs-lookup"><span data-stu-id="99cf5-118">If you are not a Telefónica client yet and you want to enjoy this or other IoT Connectivity Cloud Ready services, visit [Telefónica's site](https://iot.telefonica.com/) and select the option **Connectivity**.</span></span>

### <a name="telefnica-sim-setup"></a><span data-ttu-id="99cf5-119">Telefónica SIM setup</span><span class="sxs-lookup"><span data-stu-id="99cf5-119">Telefónica SIM setup</span></span>
<span data-ttu-id="99cf5-120">Telefónica SIM & Azure Twin device ID association is based on Telefónica IoT SIM "alias" property.</span><span class="sxs-lookup"><span data-stu-id="99cf5-120">Telefónica SIM & Azure Twin device ID association is based on Telefónica IoT SIM "alias" property.</span></span> 

<span data-ttu-id="99cf5-121">Navigate to [Telefónica IoT Connectivity Platform Portal](https://m2m-movistar-es.telefonica.com/) > SIM Inventory > Select your SIM, and update each SIM "alias" with your desired Twin deviceID.</span><span class="sxs-lookup"><span data-stu-id="99cf5-121">Navigate to [Telefónica IoT Connectivity Platform Portal](https://m2m-movistar-es.telefonica.com/) > SIM Inventory > Select your SIM, and update each SIM "alias" with your desired Twin deviceID.</span></span> <span data-ttu-id="99cf5-122">This task can also be done in bulk mode (refer to Telefónica IoT Connectivity Platform user manuals).</span><span class="sxs-lookup"><span data-stu-id="99cf5-122">This task can also be done in bulk mode (refer to Telefónica IoT Connectivity Platform user manuals).</span></span>

<span data-ttu-id="99cf5-123">This task can also be done in bulk mode (refer to Telefónica IoT Connectivity Platform user manuals)</span><span class="sxs-lookup"><span data-stu-id="99cf5-123">This task can also be done in bulk mode (refer to Telefónica IoT Connectivity Platform user manuals)</span></span>

![Telefónica Update](./media/iot-accelerators-remote-monitoring-telefonica-sim/telefonica_site.png)

<span data-ttu-id="99cf5-125">To connect your device to the Remote Monitoring, you can follow these tutorials using [C](iot-accelerators-connecting-devices-linux.md) or [Node](iot-accelerators-connecting-devices-node.md).</span><span class="sxs-lookup"><span data-stu-id="99cf5-125">To connect your device to the Remote Monitoring, you can follow these tutorials using [C](iot-accelerators-connecting-devices-linux.md) or [Node](iot-accelerators-connecting-devices-node.md).</span></span> 

## <a name="view-device-telemetry-and-sim-properties"></a><span data-ttu-id="99cf5-126">View device telemetry and SIM Properties</span><span class="sxs-lookup"><span data-stu-id="99cf5-126">View device telemetry and SIM Properties</span></span>

<span data-ttu-id="99cf5-127">Once your Telefónica account is properly configured and your device is connected, you can view device details and SIM data.</span><span class="sxs-lookup"><span data-stu-id="99cf5-127">Once your Telefónica account is properly configured and your device is connected, you can view device details and SIM data.</span></span>

<span data-ttu-id="99cf5-128">The following connectivity parameters are published:</span><span class="sxs-lookup"><span data-stu-id="99cf5-128">The following connectivity parameters are published:</span></span>

* <span data-ttu-id="99cf5-129">ICCID</span><span class="sxs-lookup"><span data-stu-id="99cf5-129">ICCID</span></span>
* <span data-ttu-id="99cf5-130">IP</span><span class="sxs-lookup"><span data-stu-id="99cf5-130">IP</span></span>
* <span data-ttu-id="99cf5-131">Network presence</span><span class="sxs-lookup"><span data-stu-id="99cf5-131">Network presence</span></span>
* <span data-ttu-id="99cf5-132">SIM Status</span><span class="sxs-lookup"><span data-stu-id="99cf5-132">SIM Status</span></span>
* <span data-ttu-id="99cf5-133">Network-based location</span><span class="sxs-lookup"><span data-stu-id="99cf5-133">Network-based location</span></span>
* <span data-ttu-id="99cf5-134">Consumed data traffic</span><span class="sxs-lookup"><span data-stu-id="99cf5-134">Consumed data traffic</span></span>

![Dashboard](./media/iot-accelerators-remote-monitoring-telefonica-sim/dashboard.png)

## <a name="next-steps"></a><span data-ttu-id="99cf5-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="99cf5-136">Next steps</span></span>

<span data-ttu-id="99cf5-137">Now that you have an overview of how to integrate SIM Data into Azure IoT Remote Monitoring, here are suggested next steps for solutions accelerators:</span><span class="sxs-lookup"><span data-stu-id="99cf5-137">Now that you have an overview of how to integrate SIM Data into Azure IoT Remote Monitoring, here are suggested next steps for solutions accelerators:</span></span>

* [<span data-ttu-id="99cf5-138">Operate the Azure IoT Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="99cf5-138">Operate the Azure IoT Remote Monitoring solution</span></span>](quickstart-remote-monitoring-deploy.md)
* [<span data-ttu-id="99cf5-139">Perform advanced monitoring</span><span class="sxs-lookup"><span data-stu-id="99cf5-139">Perform advanced monitoring</span></span>](iot-accelerators-remote-monitoring-monitor.md)
* [<span data-ttu-id="99cf5-140">Manage your devices</span><span class="sxs-lookup"><span data-stu-id="99cf5-140">Manage your devices</span></span>](iot-accelerators-remote-monitoring-manage.md)
* [<span data-ttu-id="99cf5-141">Troubleshoot device issues</span><span class="sxs-lookup"><span data-stu-id="99cf5-141">Troubleshoot device issues</span></span>](iot-accelerators-remote-monitoring-maintain.md)

