---
title: Connected Factory solution walkthrough - Azure | Microsoft Docs
description: A description of the Azure IoT solution accelerator Connected Factory and its architecture.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 12/12/2017
ms.author: dobett
ms.openlocfilehash: ae5218bae12b9489d67b0264f0e5fdb6d833cb9e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856886"
---
# <a name="connected-factory-solution-accelerator-walkthrough"></a><span data-ttu-id="9e0a7-103">Connected Factory solution accelerator walkthrough</span><span class="sxs-lookup"><span data-stu-id="9e0a7-103">Connected Factory solution accelerator walkthrough</span></span>

<span data-ttu-id="9e0a7-104">The Connected Factory [solution accelerator][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span><span class="sxs-lookup"><span data-stu-id="9e0a7-104">The Connected Factory [solution accelerator][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="9e0a7-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-105">Connects to both simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="9e0a7-106">For more information about OPC UA, see the [Connected Factory FAQ](iot-accelerators-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-106">For more information about OPC UA, see the [Connected Factory FAQ](iot-accelerators-faq-cf.md).</span></span>
* <span data-ttu-id="9e0a7-107">Shows operational KPIs and OEE of those devices and production lines.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="9e0a7-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-108">Demonstrates how a cloud-based application could be used to interact with OPC UA server systems.</span></span>
* <span data-ttu-id="9e0a7-109">Enables you to connect your own OPC UA server devices.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-109">Enables you to connect your own OPC UA server devices.</span></span>
* <span data-ttu-id="9e0a7-110">Enables you to browse and modify the OPC UA server data.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-110">Enables you to browse and modify the OPC UA server data.</span></span>
* <span data-ttu-id="9e0a7-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-111">Integrates with the Azure Time Series Insights (TSI) service to provide customized views of the data from your OPC UA servers.</span></span>

<span data-ttu-id="9e0a7-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-112">You can use the solution as a starting point for your own implementation and [customize][lnk-customize] it to meet your own specific business requirements.</span></span>

<span data-ttu-id="9e0a7-113">This article walks you through some of the key elements of the Connected Factory solution to enable you to understand how it works.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-113">This article walks you through some of the key elements of the Connected Factory solution to enable you to understand how it works.</span></span> <span data-ttu-id="9e0a7-114">The article also describes how data flows through the solution.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-114">The article also describes how data flows through the solution.</span></span> <span data-ttu-id="9e0a7-115">This knowledge helps you to:</span><span class="sxs-lookup"><span data-stu-id="9e0a7-115">This knowledge helps you to:</span></span>

* <span data-ttu-id="9e0a7-116">Troubleshoot issues in the solution.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-116">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="9e0a7-117">Plan how to customize to the solution to meet your own specific requirements.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-117">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="9e0a7-118">Design your own IoT solution that uses Azure services.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-118">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="9e0a7-119">For more information, see the [Connected Factory FAQ](iot-accelerators-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-119">For more information, see the [Connected Factory FAQ](iot-accelerators-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="9e0a7-120">Logical architecture</span><span class="sxs-lookup"><span data-stu-id="9e0a7-120">Logical architecture</span></span>

<span data-ttu-id="9e0a7-121">The following diagram outlines the logical components of the solution accelerator:</span><span class="sxs-lookup"><span data-stu-id="9e0a7-121">The following diagram outlines the logical components of the solution accelerator:</span></span>

![Connected Factory logical architecture][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="9e0a7-123">Communication patterns</span><span class="sxs-lookup"><span data-stu-id="9e0a7-123">Communication patterns</span></span>

<span data-ttu-id="9e0a7-124">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-124">The solution uses the [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) to send OPC UA telemetry data to IoT Hub in JSON format.</span></span> <span data-ttu-id="9e0a7-125">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-125">The solution uses the [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="9e0a7-126">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-126">The solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="9e0a7-127">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-127">The client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub to make the connection without requiring open ports in the on-premises firewall.</span></span> <span data-ttu-id="9e0a7-128">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-128">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="9e0a7-129">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-129">The solution uses the [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="9e0a7-130">Simulation</span><span class="sxs-lookup"><span data-stu-id="9e0a7-130">Simulation</span></span>

<span data-ttu-id="9e0a7-131">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-131">The simulated stations and the simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="9e0a7-132">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-132">The simulated devices and the OPC Publisher Module are based on the [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by the OPC Foundation.</span></span>

<span data-ttu-id="9e0a7-133">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="9e0a7-133">The OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="9e0a7-134">Each simulated production line has a designated gateway attached.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-134">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="9e0a7-135">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-135">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="9e0a7-136">The simulation is configured to run eight simulated production lines by default.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-136">The simulation is configured to run eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="9e0a7-137">Simulated production line</span><span class="sxs-lookup"><span data-stu-id="9e0a7-137">Simulated production line</span></span>

<span data-ttu-id="9e0a7-138">A production line manufactures parts.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-138">A production line manufactures parts.</span></span> <span data-ttu-id="9e0a7-139">It is composed of different stations: an assembly station, a test station, and a packaging station.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-139">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="9e0a7-140">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-140">The simulation runs and updates the data that is exposed through the OPC UA nodes.</span></span> <span data-ttu-id="9e0a7-141">All simulated production line stations are orchestrated by the MES through OPC UA.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-141">All simulated production line stations are orchestrated by the MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="9e0a7-142">Simulated manufacturing execution system</span><span class="sxs-lookup"><span data-stu-id="9e0a7-142">Simulated manufacturing execution system</span></span>

<span data-ttu-id="9e0a7-143">The MES monitors each station in the production line through OPC UA to detect station status changes.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-143">The MES monitors each station in the production line through OPC UA to detect station status changes.</span></span> <span data-ttu-id="9e0a7-144">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-144">It calls OPC UA methods to control the stations and passes a product from one station to the next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="9e0a7-145">Gateway OPC publisher module</span><span class="sxs-lookup"><span data-stu-id="9e0a7-145">Gateway OPC publisher module</span></span>

<span data-ttu-id="9e0a7-146">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-146">OPC Publisher Module connects to the station OPC UA servers and subscribes to the OPC nodes to be published.</span></span> <span data-ttu-id="9e0a7-147">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-147">The module converts the node data into JSON format, encrypts it, and sends it to IoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="9e0a7-148">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-148">The OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="9e0a7-149">Gateway OPC proxy module</span><span class="sxs-lookup"><span data-stu-id="9e0a7-149">Gateway OPC proxy module</span></span>

<span data-ttu-id="9e0a7-150">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-150">The Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="9e0a7-151">It can work with existing enterprise infrastructure, including Web Proxies.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-151">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="9e0a7-152">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-152">It uses IoT Hub Device methods to transfer packetized TCP/IP data at the application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="9e0a7-153">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-153">The OPC UA binary protocol relayed through the proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="9e0a7-154">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="9e0a7-154">Azure Time Series Insights</span></span>

<span data-ttu-id="9e0a7-155">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-155">The Gateway OPC Publisher Module subscribes to OPC UA server nodes to detect change in the data values.</span></span> <span data-ttu-id="9e0a7-156">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-156">If a data change is detected in one of the nodes, this module then sends messages to Azure IoT Hub.</span></span>

<span data-ttu-id="9e0a7-157">IoT Hub provides an event source to Azure TSI.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-157">IoT Hub provides an event source to Azure TSI.</span></span> <span data-ttu-id="9e0a7-158">TSI stores data for 30 days based on timestamps attached to the messages.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-158">TSI stores data for 30 days based on timestamps attached to the messages.</span></span> <span data-ttu-id="9e0a7-159">This data includes:</span><span class="sxs-lookup"><span data-stu-id="9e0a7-159">This data includes:</span></span>

* <span data-ttu-id="9e0a7-160">OPC UA ApplicationUri</span><span class="sxs-lookup"><span data-stu-id="9e0a7-160">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="9e0a7-161">OPC UA NodeId</span><span class="sxs-lookup"><span data-stu-id="9e0a7-161">OPC UA NodeId</span></span>
* <span data-ttu-id="9e0a7-162">Value of the node</span><span class="sxs-lookup"><span data-stu-id="9e0a7-162">Value of the node</span></span>
* <span data-ttu-id="9e0a7-163">Source timestamp</span><span class="sxs-lookup"><span data-stu-id="9e0a7-163">Source timestamp</span></span>
* <span data-ttu-id="9e0a7-164">OPC UA DisplayName</span><span class="sxs-lookup"><span data-stu-id="9e0a7-164">OPC UA DisplayName</span></span>

<span data-ttu-id="9e0a7-165">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-165">Currently, TSI does not allow customers to customize how long they wish to keep the data for.</span></span>

<span data-ttu-id="9e0a7-166">TSI queries against node data using a **SearchSpan** (**Time.From**, **Time.To**) and aggregates by **OPC UA ApplicationUri** or **OPC UA NodeId** or **OPC UA DisplayName**.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-166">TSI queries against node data using a **SearchSpan** (**Time.From**, **Time.To**) and aggregates by **OPC UA ApplicationUri** or **OPC UA NodeId** or **OPC UA DisplayName**.</span></span>

<span data-ttu-id="9e0a7-167">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-167">To retrieve the data for the OEE and KPI gauges, and the time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="9e0a7-168">The time series are built using a different process.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-168">The time series are built using a different process.</span></span> <span data-ttu-id="9e0a7-169">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-169">OEE and KPIs are calculated from station base data and bubbled up for the topology (production lines, factories, enterprise) in the application.</span></span>

<span data-ttu-id="9e0a7-170">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-170">Additionally, time series for OEE and KPI topology is calculated in the app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="9e0a7-171">For example, the day view is updated every full hour.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-171">For example, the day view is updated every full hour.</span></span>

<span data-ttu-id="9e0a7-172">The time series view of node data comes directly from TSI using an aggregation for timespan.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-172">The time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="9e0a7-173">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9e0a7-173">IoT Hub</span></span>
<span data-ttu-id="9e0a7-174">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-174">The [IoT hub][lnk-IoT Hub] receives data sent from the OPC Publisher Module into the cloud and makes it available to the Azure TSI service.</span></span> 

<span data-ttu-id="9e0a7-175">The IoT Hub in the solution also:</span><span class="sxs-lookup"><span data-stu-id="9e0a7-175">The IoT Hub in the solution also:</span></span>
- <span data-ttu-id="9e0a7-176">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-176">Maintains an identity registry that stores the IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="9e0a7-177">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-177">Is used as transport channel for bidirectional communication of the OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="9e0a7-178">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9e0a7-178">Azure Storage</span></span>
<span data-ttu-id="9e0a7-179">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-179">The solution uses Azure blob storage as disk storage for the VM and to store deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="9e0a7-180">Web app</span><span class="sxs-lookup"><span data-stu-id="9e0a7-180">Web app</span></span>
<span data-ttu-id="9e0a7-181">The web app deployed as part of the solution accelerator comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-181">The web app deployed as part of the solution accelerator comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="telemetry-data-flow"></a><span data-ttu-id="9e0a7-182">Telemetry data flow</span><span class="sxs-lookup"><span data-stu-id="9e0a7-182">Telemetry data flow</span></span>

![Telemetry data flow](./media/iot-accelerators-connected-factory-sample-walkthrough/telemetry_dataflow.png)

### <a name="flow-steps"></a><span data-ttu-id="9e0a7-184">Flow steps</span><span class="sxs-lookup"><span data-stu-id="9e0a7-184">Flow steps</span></span>

1. <span data-ttu-id="9e0a7-185">OPC Publisher reads the required OPC UA X509 certificates and IoT Hub security credentials from the local certificate store.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-185">OPC Publisher reads the required OPC UA X509 certificates and IoT Hub security credentials from the local certificate store.</span></span>
    - <span data-ttu-id="9e0a7-186">If necessary, OPC Publisher creates and stores any missing certificates or credentials in the certificate store.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-186">If necessary, OPC Publisher creates and stores any missing certificates or credentials in the certificate store.</span></span>

2. <span data-ttu-id="9e0a7-187">OPC Publisher registers itself with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-187">OPC Publisher registers itself with IoT Hub.</span></span>
    - <span data-ttu-id="9e0a7-188">Uses the configured protocol.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-188">Uses the configured protocol.</span></span> <span data-ttu-id="9e0a7-189">Can use any IoT Hub client SDK supported protocol.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-189">Can use any IoT Hub client SDK supported protocol.</span></span> <span data-ttu-id="9e0a7-190">The default is MQTT.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-190">The default is MQTT.</span></span>
    - <span data-ttu-id="9e0a7-191">Protocol communication is secured by TLS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-191">Protocol communication is secured by TLS.</span></span>

3. <span data-ttu-id="9e0a7-192">OPC Publisher reads configuration file.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-192">OPC Publisher reads configuration file.</span></span>

4. <span data-ttu-id="9e0a7-193">OPC Publisher creates an OPC Session with each configured OPC UA Server.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-193">OPC Publisher creates an OPC Session with each configured OPC UA Server.</span></span>
    - <span data-ttu-id="9e0a7-194">Uses TCP connection.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-194">Uses TCP connection.</span></span>
    - <span data-ttu-id="9e0a7-195">OPC Publisher and OPC UA Server authenticate each other using X509 certificates.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-195">OPC Publisher and OPC UA Server authenticate each other using X509 certificates.</span></span>
    - <span data-ttu-id="9e0a7-196">All further OPC UA traffic is encrypted by the configured OPC UA encryption mechanism.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-196">All further OPC UA traffic is encrypted by the configured OPC UA encryption mechanism.</span></span>
    - <span data-ttu-id="9e0a7-197">OPC Publisher creates, in the OPC Session for each configured publishing interval, an OPC Subscription.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-197">OPC Publisher creates, in the OPC Session for each configured publishing interval, an OPC Subscription.</span></span>
    - <span data-ttu-id="9e0a7-198">Creates OPC Monitored items for the OPC Nodes to publish in the OPC Subscription.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-198">Creates OPC Monitored items for the OPC Nodes to publish in the OPC Subscription.</span></span>

5. <span data-ttu-id="9e0a7-199">If a monitored OPC Node value changes, OPC UA Server sends updates to OPC Publisher.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-199">If a monitored OPC Node value changes, OPC UA Server sends updates to OPC Publisher.</span></span>

6. <span data-ttu-id="9e0a7-200">OPC Publisher transcodes the new value.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-200">OPC Publisher transcodes the new value.</span></span>
    - <span data-ttu-id="9e0a7-201">Batches multiple changes if batching is enabled.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-201">Batches multiple changes if batching is enabled.</span></span>
    - <span data-ttu-id="9e0a7-202">Creates an IoT Hub message.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-202">Creates an IoT Hub message.</span></span>

7. <span data-ttu-id="9e0a7-203">OPC Publisher sends a message to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-203">OPC Publisher sends a message to IoT Hub.</span></span>
    - <span data-ttu-id="9e0a7-204">Use the configured protocol.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-204">Use the configured protocol.</span></span>
    - <span data-ttu-id="9e0a7-205">Communication is secured by TLS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-205">Communication is secured by TLS.</span></span>

8. <span data-ttu-id="9e0a7-206">Time Series Insights (TSI) reads the messages from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-206">Time Series Insights (TSI) reads the messages from IoT Hub.</span></span>
    - <span data-ttu-id="9e0a7-207">Uses AMQP over TCP/TLS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-207">Uses AMQP over TCP/TLS.</span></span>
    - <span data-ttu-id="9e0a7-208">This step is internal to the datacenter.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-208">This step is internal to the datacenter.</span></span>

9. <span data-ttu-id="9e0a7-209">Data at rest in TSI.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-209">Data at rest in TSI.</span></span>

10. <span data-ttu-id="9e0a7-210">Connected Factory WebApp in Azure AppService queries required data from TSI.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-210">Connected Factory WebApp in Azure AppService queries required data from TSI.</span></span>
    - <span data-ttu-id="9e0a7-211">Uses TCP/TLS secured communication.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-211">Uses TCP/TLS secured communication.</span></span>
    - <span data-ttu-id="9e0a7-212">This step is internal to the datacenter.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-212">This step is internal to the datacenter.</span></span>

11. <span data-ttu-id="9e0a7-213">Web browser connects to the Connected Factory WebApp.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-213">Web browser connects to the Connected Factory WebApp.</span></span>
    - <span data-ttu-id="9e0a7-214">Renders the Connected Factory dashboard.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-214">Renders the Connected Factory dashboard.</span></span>
    - <span data-ttu-id="9e0a7-215">Connects over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-215">Connects over HTTPS.</span></span>
    - <span data-ttu-id="9e0a7-216">Access to the Connected Factory App requires authentication of the user via Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-216">Access to the Connected Factory App requires authentication of the user via Azure Active Directory.</span></span>
    - <span data-ttu-id="9e0a7-217">Any WebApi calls into Connected Factory app are secured by Anti-Forgery-Tokens.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-217">Any WebApi calls into Connected Factory app are secured by Anti-Forgery-Tokens.</span></span>

12. <span data-ttu-id="9e0a7-218">On data updates, the Connected Factory WebApp sends updated data to the web browser.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-218">On data updates, the Connected Factory WebApp sends updated data to the web browser.</span></span>
    - <span data-ttu-id="9e0a7-219">Uses the SignalR protocol.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-219">Uses the SignalR protocol.</span></span>
    - <span data-ttu-id="9e0a7-220">Secured by TCP/TLS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-220">Secured by TCP/TLS.</span></span>

## <a name="browsing-data-flow"></a><span data-ttu-id="9e0a7-221">Browsing data flow</span><span class="sxs-lookup"><span data-stu-id="9e0a7-221">Browsing data flow</span></span>

![Browsing data flow](./media/iot-accelerators-connected-factory-sample-walkthrough/browsing_dataflow.png)

### <a name="flow-steps"></a><span data-ttu-id="9e0a7-223">Flow steps</span><span class="sxs-lookup"><span data-stu-id="9e0a7-223">Flow steps</span></span>

1. <span data-ttu-id="9e0a7-224">OPC Proxy (server component) starts up.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-224">OPC Proxy (server component) starts up.</span></span>
    - <span data-ttu-id="9e0a7-225">Reads the shared access keys from a local store.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-225">Reads the shared access keys from a local store.</span></span>
    - <span data-ttu-id="9e0a7-226">If necessary, stores missing access keys in the store.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-226">If necessary, stores missing access keys in the store.</span></span>

2. <span data-ttu-id="9e0a7-227">OPC Proxy (server component) registers itself with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-227">OPC Proxy (server component) registers itself with IoT Hub.</span></span>
    - <span data-ttu-id="9e0a7-228">Reads all it's known devices from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-228">Reads all it's known devices from IoT Hub.</span></span>
    - <span data-ttu-id="9e0a7-229">Uses MQTT over TLS over Socket or Secure Websocket.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-229">Uses MQTT over TLS over Socket or Secure Websocket.</span></span>

3. <span data-ttu-id="9e0a7-230">Web browser connects to the Connected Factory WebApp and renders the Connected Factory dashboard.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-230">Web browser connects to the Connected Factory WebApp and renders the Connected Factory dashboard.</span></span>
    - <span data-ttu-id="9e0a7-231">Uses HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-231">Uses HTTPS.</span></span>
    - <span data-ttu-id="9e0a7-232">A user selects an OPC UA server to connect to.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-232">A user selects an OPC UA server to connect to.</span></span>

4. <span data-ttu-id="9e0a7-233">Connected Factory WebApp establishes an OPC UA Session to the selected OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-233">Connected Factory WebApp establishes an OPC UA Session to the selected OPC UA server.</span></span>
    - <span data-ttu-id="9e0a7-234">Uses OPC UA stack.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-234">Uses OPC UA stack.</span></span>

5. <span data-ttu-id="9e0a7-235">OPC Proxy transport receives a request from the OPC UA stack to establish a TCP socket connection to OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-235">OPC Proxy transport receives a request from the OPC UA stack to establish a TCP socket connection to OPC UA server.</span></span>
    - <span data-ttu-id="9e0a7-236">It just retrieves the TCP payload and uses it unchanged.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-236">It just retrieves the TCP payload and uses it unchanged.</span></span>
    - <span data-ttu-id="9e0a7-237">This step is internal to the Connected Factory WebApp.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-237">This step is internal to the Connected Factory WebApp.</span></span>

6. <span data-ttu-id="9e0a7-238">OPC Proxy (client component) looks up OPC Proxy (server component) device in the IoT Hub device registry.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-238">OPC Proxy (client component) looks up OPC Proxy (server component) device in the IoT Hub device registry.</span></span> <span data-ttu-id="9e0a7-239">Then calls a device method of the OPC Proxy (server component) device in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-239">Then calls a device method of the OPC Proxy (server component) device in IoT Hub.</span></span>
    - <span data-ttu-id="9e0a7-240">Uses HTTPS over TCP/TLS to look up OPC Proxy.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-240">Uses HTTPS over TCP/TLS to look up OPC Proxy.</span></span>
    - <span data-ttu-id="9e0a7-241">Uses using HTTPS over TCP/TLS to establish a TCP socket connection to the OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-241">Uses using HTTPS over TCP/TLS to establish a TCP socket connection to the OPC UA server.</span></span>
    - <span data-ttu-id="9e0a7-242">This step is internal to the datacenter.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-242">This step is internal to the datacenter.</span></span>

7. <span data-ttu-id="9e0a7-243">IoT Hub calls a device method in the OPC Proxy (server component) device.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-243">IoT Hub calls a device method in the OPC Proxy (server component) device.</span></span>
    - <span data-ttu-id="9e0a7-244">Uses an established MQTT over TLS over Socket or Secure Websocket connection to establish a TCP socket connection to the OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-244">Uses an established MQTT over TLS over Socket or Secure Websocket connection to establish a TCP socket connection to the OPC UA server.</span></span>

8. <span data-ttu-id="9e0a7-245">OPC Proxy (server component) sends the TCP payload on to the shopfloor network.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-245">OPC Proxy (server component) sends the TCP payload on to the shopfloor network.</span></span>

9. <span data-ttu-id="9e0a7-246">The OPC UA server processes the payload and sends back the response.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-246">The OPC UA server processes the payload and sends back the response.</span></span>

10. <span data-ttu-id="9e0a7-247">The response is received by the socket of the OPC Proxy (server component).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-247">The response is received by the socket of the OPC Proxy (server component).</span></span>
    - <span data-ttu-id="9e0a7-248">OPC Proxy sends the data as return value of the device method to IoT Hub and the OPC Proxy (client component).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-248">OPC Proxy sends the data as return value of the device method to IoT Hub and the OPC Proxy (client component).</span></span>
    - <span data-ttu-id="9e0a7-249">This data is delivered to the OPC UA stack in the Connected Factory app.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-249">This data is delivered to the OPC UA stack in the Connected Factory app.</span></span>

11. <span data-ttu-id="9e0a7-250">Connected Factory WebApp returns OPC Browser UX enriched with the OPC UA-specific information it received from the OPC UA server to the Web Browser to render it.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-250">Connected Factory WebApp returns OPC Browser UX enriched with the OPC UA-specific information it received from the OPC UA server to the Web Browser to render it.</span></span>
    - <span data-ttu-id="9e0a7-251">While browsing through the OPC address-space and applying functions to nodes in the OPC address-space, the OPC Browser UX client part uses AJAX calls over HTTPS secured with Anti-Forgery Tokens to get data from the Connected Factory WebApp.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-251">While browsing through the OPC address-space and applying functions to nodes in the OPC address-space, the OPC Browser UX client part uses AJAX calls over HTTPS secured with Anti-Forgery Tokens to get data from the Connected Factory WebApp.</span></span>
    - <span data-ttu-id="9e0a7-252">If necessary, the client uses the communication explained in steps 4 through to 10 to exchange information with the OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-252">If necessary, the client uses the communication explained in steps 4 through to 10 to exchange information with the OPC UA server.</span></span>

> [!NOTE]
> <span data-ttu-id="9e0a7-253">The OPC Proxy (server component) and OPC Proxy (client) component complete steps #4 through #10 for all TCP traffic related to the OPC UA communication.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-253">The OPC Proxy (server component) and OPC Proxy (client) component complete steps #4 through #10 for all TCP traffic related to the OPC UA communication.</span></span>

> [!NOTE]
> <span data-ttu-id="9e0a7-254">For the OPC UA server and the OPC UA stack within the Connected Factory WebApp, the OPC Proxy communication is transparent and all OPC UA security features for authentication and encryption apply.</span><span class="sxs-lookup"><span data-stu-id="9e0a7-254">For the OPC UA server and the OPC UA stack within the Connected Factory WebApp, the OPC Proxy communication is transparent and all OPC UA security features for authentication and encryption apply.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e0a7-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e0a7-255">Next steps</span></span>

<span data-ttu-id="9e0a7-256">You can continue getting started with IoT solution accelerators by reading the following articles:</span><span class="sxs-lookup"><span data-stu-id="9e0a7-256">You can continue getting started with IoT solution accelerators by reading the following articles:</span></span>

* <span data-ttu-id="9e0a7-257">[Permissions on the azureiotsuite.com site][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="9e0a7-257">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="9e0a7-258">Deploy a gateway on Windows or Linux for the Connected Factory solution accelerator</span><span class="sxs-lookup"><span data-stu-id="9e0a7-258">Deploy a gateway on Windows or Linux for the Connected Factory solution accelerator</span></span>](iot-accelerators-connected-factory-gateway-deployment.md)
* <span data-ttu-id="9e0a7-259">[OPC Publisher reference implementation](https://github.com/Azure/iot-edge-opc-publisher/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="9e0a7-259">[OPC Publisher reference implementation](https://github.com/Azure/iot-edge-opc-publisher/blob/master/README.md).</span></span>

[connected-factory-logical]:media/iot-accelerators-connected-factory-sample-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]:about-iot-accelerators.md
[lnk-customize]: iot-accelerators-connected-factory-customize.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-accelerators-faq.md
