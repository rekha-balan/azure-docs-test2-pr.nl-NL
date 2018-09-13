---
title: Configure the Connected Factory topology | Microsoft Docs
description: How to configure the topology of a Connected Factory solution accelerator.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 12/12/2017
ms.author: dobett
ms.openlocfilehash: 8cb3cae396016545c5d78a2ff7ccde4a053c4cf1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867161"
---
# <a name="configure-the-connected-factory-solution-accelerator"></a><span data-ttu-id="a7a63-103">Configure the Connected Factory solution accelerator</span><span class="sxs-lookup"><span data-stu-id="a7a63-103">Configure the Connected Factory solution accelerator</span></span>

<span data-ttu-id="a7a63-104">The Connected Factory solution accelerator shows a simulated dashboard for a fictional company Contoso.</span><span class="sxs-lookup"><span data-stu-id="a7a63-104">The Connected Factory solution accelerator shows a simulated dashboard for a fictional company Contoso.</span></span> <span data-ttu-id="a7a63-105">This company has factories in numerous global locations globally.</span><span class="sxs-lookup"><span data-stu-id="a7a63-105">This company has factories in numerous global locations globally.</span></span>

<span data-ttu-id="a7a63-106">This article uses Contoso as an example to describe how to configure the topology of a Connected Factory solution.</span><span class="sxs-lookup"><span data-stu-id="a7a63-106">This article uses Contoso as an example to describe how to configure the topology of a Connected Factory solution.</span></span>

## <a name="simulated-factories-configuration"></a><span data-ttu-id="a7a63-107">Simulated factories configuration</span><span class="sxs-lookup"><span data-stu-id="a7a63-107">Simulated factories configuration</span></span>

<span data-ttu-id="a7a63-108">Each Contoso factory has production lines that consist of three stations each.</span><span class="sxs-lookup"><span data-stu-id="a7a63-108">Each Contoso factory has production lines that consist of three stations each.</span></span> <span data-ttu-id="a7a63-109">Each station is a real OPC UA server with a specific role:</span><span class="sxs-lookup"><span data-stu-id="a7a63-109">Each station is a real OPC UA server with a specific role:</span></span>

* <span data-ttu-id="a7a63-110">Assembly station</span><span class="sxs-lookup"><span data-stu-id="a7a63-110">Assembly station</span></span>
* <span data-ttu-id="a7a63-111">Test station</span><span class="sxs-lookup"><span data-stu-id="a7a63-111">Test station</span></span>
* <span data-ttu-id="a7a63-112">Packaging station</span><span class="sxs-lookup"><span data-stu-id="a7a63-112">Packaging station</span></span>

<span data-ttu-id="a7a63-113">These OPC UA servers have OPC UA nodes and [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) sends the values of these nodes to Connected Factory.</span><span class="sxs-lookup"><span data-stu-id="a7a63-113">These OPC UA servers have OPC UA nodes and [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) sends the values of these nodes to Connected Factory.</span></span> <span data-ttu-id="a7a63-114">This includes:</span><span class="sxs-lookup"><span data-stu-id="a7a63-114">This includes:</span></span>

* <span data-ttu-id="a7a63-115">Current operational status such as current power consumption.</span><span class="sxs-lookup"><span data-stu-id="a7a63-115">Current operational status such as current power consumption.</span></span>
* <span data-ttu-id="a7a63-116">Production information such as the number of products produced.</span><span class="sxs-lookup"><span data-stu-id="a7a63-116">Production information such as the number of products produced.</span></span>

<span data-ttu-id="a7a63-117">You can use the dashboard to drill into the Contoso factory topology from a global view down to a station level view.</span><span class="sxs-lookup"><span data-stu-id="a7a63-117">You can use the dashboard to drill into the Contoso factory topology from a global view down to a station level view.</span></span> <span data-ttu-id="a7a63-118">The Connected Factory dashboard enables:</span><span class="sxs-lookup"><span data-stu-id="a7a63-118">The Connected Factory dashboard enables:</span></span>

* <span data-ttu-id="a7a63-119">The visualization of OEE and KPI figures for each layer in the topology.</span><span class="sxs-lookup"><span data-stu-id="a7a63-119">The visualization of OEE and KPI figures for each layer in the topology.</span></span>
* <span data-ttu-id="a7a63-120">The visualization of current values of OPC UA nodes in the stations.</span><span class="sxs-lookup"><span data-stu-id="a7a63-120">The visualization of current values of OPC UA nodes in the stations.</span></span>
* <span data-ttu-id="a7a63-121">The aggregation of the OEE and KPI figures from the station level to the global level.</span><span class="sxs-lookup"><span data-stu-id="a7a63-121">The aggregation of the OEE and KPI figures from the station level to the global level.</span></span>
* <span data-ttu-id="a7a63-122">The visualization of alerts and actions to perform if values reach specific thresholds.</span><span class="sxs-lookup"><span data-stu-id="a7a63-122">The visualization of alerts and actions to perform if values reach specific thresholds.</span></span>

## <a name="connected-factory-topology"></a><span data-ttu-id="a7a63-123">Connected Factory topology</span><span class="sxs-lookup"><span data-stu-id="a7a63-123">Connected Factory topology</span></span>

<span data-ttu-id="a7a63-124">The topology of factories, production lines, and stations is hierarchical:</span><span class="sxs-lookup"><span data-stu-id="a7a63-124">The topology of factories, production lines, and stations is hierarchical:</span></span>

* <span data-ttu-id="a7a63-125">The global level has factory nodes as children.</span><span class="sxs-lookup"><span data-stu-id="a7a63-125">The global level has factory nodes as children.</span></span>
* <span data-ttu-id="a7a63-126">The factories have production line nodes as children.</span><span class="sxs-lookup"><span data-stu-id="a7a63-126">The factories have production line nodes as children.</span></span>
* <span data-ttu-id="a7a63-127">The production lines have station nodes as children.</span><span class="sxs-lookup"><span data-stu-id="a7a63-127">The production lines have station nodes as children.</span></span>
* <span data-ttu-id="a7a63-128">The stations (OPC UA servers) have OPC UA nodes as children.</span><span class="sxs-lookup"><span data-stu-id="a7a63-128">The stations (OPC UA servers) have OPC UA nodes as children.</span></span>

<span data-ttu-id="a7a63-129">Every node in the topology has a common set of properties that define:</span><span class="sxs-lookup"><span data-stu-id="a7a63-129">Every node in the topology has a common set of properties that define:</span></span>

* <span data-ttu-id="a7a63-130">A unique identifier for the topology node.</span><span class="sxs-lookup"><span data-stu-id="a7a63-130">A unique identifier for the topology node.</span></span>
* <span data-ttu-id="a7a63-131">A name.</span><span class="sxs-lookup"><span data-stu-id="a7a63-131">A name.</span></span>
* <span data-ttu-id="a7a63-132">A description.</span><span class="sxs-lookup"><span data-stu-id="a7a63-132">A description.</span></span>
* <span data-ttu-id="a7a63-133">An image.</span><span class="sxs-lookup"><span data-stu-id="a7a63-133">An image.</span></span>
* <span data-ttu-id="a7a63-134">The children of the topology node.</span><span class="sxs-lookup"><span data-stu-id="a7a63-134">The children of the topology node.</span></span>
* <span data-ttu-id="a7a63-135">Minimum, target, and maximum values for OEE and KPI figures and the alert actions to execute.</span><span class="sxs-lookup"><span data-stu-id="a7a63-135">Minimum, target, and maximum values for OEE and KPI figures and the alert actions to execute.</span></span>

## <a name="topology-configuration-file"></a><span data-ttu-id="a7a63-136">Topology configuration file</span><span class="sxs-lookup"><span data-stu-id="a7a63-136">Topology configuration file</span></span>

<span data-ttu-id="a7a63-137">To configure the properties listed in the previous section, the Connected Factory solution uses a configuration file called [ContosoTopologyDescription.json](https://github.com/Azure/azure-iot-connected-factory/blob/master/WebApp/Contoso/Topology/ContosoTopologyDescription.json).</span><span class="sxs-lookup"><span data-stu-id="a7a63-137">To configure the properties listed in the previous section, the Connected Factory solution uses a configuration file called [ContosoTopologyDescription.json](https://github.com/Azure/azure-iot-connected-factory/blob/master/WebApp/Contoso/Topology/ContosoTopologyDescription.json).</span></span>

<span data-ttu-id="a7a63-138">You can find this file in the solution source code in the `WebApp/Contoso/Topology` folder.</span><span class="sxs-lookup"><span data-stu-id="a7a63-138">You can find this file in the solution source code in the `WebApp/Contoso/Topology` folder.</span></span>

<span data-ttu-id="a7a63-139">The following snippet shows an outline of the `ContosoTopologyDescription.json` configuration file:</span><span class="sxs-lookup"><span data-stu-id="a7a63-139">The following snippet shows an outline of the `ContosoTopologyDescription.json` configuration file:</span></span>

```json
{
  <global_configuration>,
  "Factories": [
    <factory_configuration>,
    "ProductionLines": [
      <production_line_configuration>,
      "Stations": [
        <station_configuration>,
        <more station_configurations>
      ],
      <more production_line_configurations>
    ]
    <more factory_configurations>
  ]
}
```

<span data-ttu-id="a7a63-140">The common properties of `<global_configuration>`, `<factory_configuration>`, `<production_line_configuration>`, and `<station_configuration>` are:</span><span class="sxs-lookup"><span data-stu-id="a7a63-140">The common properties of `<global_configuration>`, `<factory_configuration>`, `<production_line_configuration>`, and `<station_configuration>` are:</span></span>

* <span data-ttu-id="a7a63-141">**Name** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-141">**Name** (type string)</span></span>

  <span data-ttu-id="a7a63-142">Defines a descriptive name, which should be only one word for the topology node to show in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-142">Defines a descriptive name, which should be only one word for the topology node to show in the dashboard.</span></span>

* <span data-ttu-id="a7a63-143">**Description** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-143">**Description** (type string)</span></span>

  <span data-ttu-id="a7a63-144">Describes the topology node in more detail.</span><span class="sxs-lookup"><span data-stu-id="a7a63-144">Describes the topology node in more detail.</span></span>

* <span data-ttu-id="a7a63-145">**Image** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-145">**Image** (type string)</span></span>

  <span data-ttu-id="a7a63-146">The path to an image in the WebApp solution to show when information about the topology node is shown in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-146">The path to an image in the WebApp solution to show when information about the topology node is shown in the dashboard.</span></span>

* <span data-ttu-id="a7a63-147">**OeeOverall**, **OeePerformance**, **OeeAvailability**, **OeeQuality**, **Kpi1**, **Kpi2** (type `<performance_definition>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-147">**OeeOverall**, **OeePerformance**, **OeeAvailability**, **OeeQuality**, **Kpi1**, **Kpi2** (type `<performance_definition>`)</span></span>

  <span data-ttu-id="a7a63-148">These properties define minimal, target, and maximal values of the operational figure used to generate alerts.</span><span class="sxs-lookup"><span data-stu-id="a7a63-148">These properties define minimal, target, and maximal values of the operational figure used to generate alerts.</span></span> <span data-ttu-id="a7a63-149">These properties also define the actions to execute if an alert is detected.</span><span class="sxs-lookup"><span data-stu-id="a7a63-149">These properties also define the actions to execute if an alert is detected.</span></span>

<span data-ttu-id="a7a63-150">The `<factory_configuration>` and `<production_line_configuration>` items have a property:</span><span class="sxs-lookup"><span data-stu-id="a7a63-150">The `<factory_configuration>` and `<production_line_configuration>` items have a property:</span></span>

* <span data-ttu-id="a7a63-151">**Guid** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-151">**Guid** (type string)</span></span>

  <span data-ttu-id="a7a63-152">Uniquely identifies the topology node.</span><span class="sxs-lookup"><span data-stu-id="a7a63-152">Uniquely identifies the topology node.</span></span>

<span data-ttu-id="a7a63-153">`<factory_configuration>` has a property:</span><span class="sxs-lookup"><span data-stu-id="a7a63-153">`<factory_configuration>` has a property:</span></span>

* <span data-ttu-id="a7a63-154">**Location** (type `<location_definition>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-154">**Location** (type `<location_definition>`)</span></span>

  <span data-ttu-id="a7a63-155">Specifies where the factory is located.</span><span class="sxs-lookup"><span data-stu-id="a7a63-155">Specifies where the factory is located.</span></span>

<span data-ttu-id="a7a63-156">`<station_configuration>` has properties:</span><span class="sxs-lookup"><span data-stu-id="a7a63-156">`<station_configuration>` has properties:</span></span>

* <span data-ttu-id="a7a63-157">**OpcUri** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-157">**OpcUri** (type string)</span></span>

  <span data-ttu-id="a7a63-158">This property must be set to the OPC UA Application URI of the OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="a7a63-158">This property must be set to the OPC UA Application URI of the OPC UA server.</span></span>
  <span data-ttu-id="a7a63-159">Because it must be globally unique by OPC UA specification, this property is used to identify the station topology node.</span><span class="sxs-lookup"><span data-stu-id="a7a63-159">Because it must be globally unique by OPC UA specification, this property is used to identify the station topology node.</span></span>

* <span data-ttu-id="a7a63-160">**OpcNodes**, which are an array of OPC UA nodes (type `<opc_node_description>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-160">**OpcNodes**, which are an array of OPC UA nodes (type `<opc_node_description>`)</span></span>

<span data-ttu-id="a7a63-161">`<location_definition>` has properties:</span><span class="sxs-lookup"><span data-stu-id="a7a63-161">`<location_definition>` has properties:</span></span>

* <span data-ttu-id="a7a63-162">**City** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-162">**City** (type string)</span></span>

  <span data-ttu-id="a7a63-163">Name of city closest to the location</span><span class="sxs-lookup"><span data-stu-id="a7a63-163">Name of city closest to the location</span></span>

* <span data-ttu-id="a7a63-164">**Country** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-164">**Country** (type string)</span></span>

  <span data-ttu-id="a7a63-165">Country of the location</span><span class="sxs-lookup"><span data-stu-id="a7a63-165">Country of the location</span></span>

* <span data-ttu-id="a7a63-166">**Latitude** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-166">**Latitude** (type double)</span></span>

  <span data-ttu-id="a7a63-167">Latitude of the location</span><span class="sxs-lookup"><span data-stu-id="a7a63-167">Latitude of the location</span></span>

* <span data-ttu-id="a7a63-168">**Longitude** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-168">**Longitude** (type double)</span></span>

  <span data-ttu-id="a7a63-169">Longitude of the location</span><span class="sxs-lookup"><span data-stu-id="a7a63-169">Longitude of the location</span></span>

<span data-ttu-id="a7a63-170">`<performance_definition>` has properties:</span><span class="sxs-lookup"><span data-stu-id="a7a63-170">`<performance_definition>` has properties:</span></span>

* <span data-ttu-id="a7a63-171">**Minimum** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-171">**Minimum** (type double)</span></span>

  <span data-ttu-id="a7a63-172">Lower threshold the value can reach.</span><span class="sxs-lookup"><span data-stu-id="a7a63-172">Lower threshold the value can reach.</span></span> <span data-ttu-id="a7a63-173">If the current value is below this threshold, an alert is generated.</span><span class="sxs-lookup"><span data-stu-id="a7a63-173">If the current value is below this threshold, an alert is generated.</span></span>

* <span data-ttu-id="a7a63-174">**Target** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-174">**Target** (type double)</span></span>

  <span data-ttu-id="a7a63-175">Ideal target value.</span><span class="sxs-lookup"><span data-stu-id="a7a63-175">Ideal target value.</span></span>

* <span data-ttu-id="a7a63-176">**Maximum** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-176">**Maximum** (type double)</span></span>

  <span data-ttu-id="a7a63-177">Upper threshold the value can reach.</span><span class="sxs-lookup"><span data-stu-id="a7a63-177">Upper threshold the value can reach.</span></span> <span data-ttu-id="a7a63-178">If the current value is above this threshold, an alert is generated.</span><span class="sxs-lookup"><span data-stu-id="a7a63-178">If the current value is above this threshold, an alert is generated.</span></span>

* <span data-ttu-id="a7a63-179">**MinimumAlertActions** (type `<alert_action>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-179">**MinimumAlertActions** (type `<alert_action>`)</span></span>

  <span data-ttu-id="a7a63-180">Defines the set of actions, which can be taken as response to a minimum alert.</span><span class="sxs-lookup"><span data-stu-id="a7a63-180">Defines the set of actions, which can be taken as response to a minimum alert.</span></span>

* <span data-ttu-id="a7a63-181">**MaximumAlertActions** (type `<alert_action>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-181">**MaximumAlertActions** (type `<alert_action>`)</span></span>

  <span data-ttu-id="a7a63-182">Defines the set of actions, which can be taken as response to a maximum alert.</span><span class="sxs-lookup"><span data-stu-id="a7a63-182">Defines the set of actions, which can be taken as response to a maximum alert.</span></span>

<span data-ttu-id="a7a63-183">`<alert_action`> has properties:</span><span class="sxs-lookup"><span data-stu-id="a7a63-183">`<alert_action`> has properties:</span></span>

* <span data-ttu-id="a7a63-184">**Type** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-184">**Type** (type string)</span></span>

  <span data-ttu-id="a7a63-185">Type of the alert action.</span><span class="sxs-lookup"><span data-stu-id="a7a63-185">Type of the alert action.</span></span> <span data-ttu-id="a7a63-186">The following types are known:</span><span class="sxs-lookup"><span data-stu-id="a7a63-186">The following types are known:</span></span>

  * <span data-ttu-id="a7a63-187">**AcknowledgeAlert**: the status of the alert should change to acknowledged.</span><span class="sxs-lookup"><span data-stu-id="a7a63-187">**AcknowledgeAlert**: the status of the alert should change to acknowledged.</span></span>
  * <span data-ttu-id="a7a63-188">**CloseAlert**: all older alerts of the same type should no longer be shown in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-188">**CloseAlert**: all older alerts of the same type should no longer be shown in the dashboard.</span></span>
  * <span data-ttu-id="a7a63-189">**CallOpcMethod**: an OPC UA method should be called.</span><span class="sxs-lookup"><span data-stu-id="a7a63-189">**CallOpcMethod**: an OPC UA method should be called.</span></span>
  * <span data-ttu-id="a7a63-190">**OpenWebPage**: a browser window should be opened showing additional contextual information.</span><span class="sxs-lookup"><span data-stu-id="a7a63-190">**OpenWebPage**: a browser window should be opened showing additional contextual information.</span></span>

* <span data-ttu-id="a7a63-191">**Description** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-191">**Description** (type string)</span></span>

  <span data-ttu-id="a7a63-192">Description of the action shown in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-192">Description of the action shown in the dashboard.</span></span>

* <span data-ttu-id="a7a63-193">**Parameter** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-193">**Parameter** (type string)</span></span>

  <span data-ttu-id="a7a63-194">Parameters required to execute the action.</span><span class="sxs-lookup"><span data-stu-id="a7a63-194">Parameters required to execute the action.</span></span> <span data-ttu-id="a7a63-195">The value depends on the action type.</span><span class="sxs-lookup"><span data-stu-id="a7a63-195">The value depends on the action type.</span></span>

  * <span data-ttu-id="a7a63-196">**AcknowledgeAlert**: no parameter required.</span><span class="sxs-lookup"><span data-stu-id="a7a63-196">**AcknowledgeAlert**: no parameter required.</span></span>
  * <span data-ttu-id="a7a63-197">**CloseAlert**: no parameter required.</span><span class="sxs-lookup"><span data-stu-id="a7a63-197">**CloseAlert**: no parameter required.</span></span>
  * <span data-ttu-id="a7a63-198">**CallOpcMethod**: the node information and parameters of the OPC UA method to call in the format "NodeId of parent node, NodeId of method to call, URI of the OPC UA server."</span><span class="sxs-lookup"><span data-stu-id="a7a63-198">**CallOpcMethod**: the node information and parameters of the OPC UA method to call in the format "NodeId of parent node, NodeId of method to call, URI of the OPC UA server."</span></span>
  * <span data-ttu-id="a7a63-199">**OpenWebPage**: the URL to show in the browser window.</span><span class="sxs-lookup"><span data-stu-id="a7a63-199">**OpenWebPage**: the URL to show in the browser window.</span></span>

<span data-ttu-id="a7a63-200">`<opc_node_description>` contains information about OPC UA nodes in a station (OPC UA server).</span><span class="sxs-lookup"><span data-stu-id="a7a63-200">`<opc_node_description>` contains information about OPC UA nodes in a station (OPC UA server).</span></span> <span data-ttu-id="a7a63-201">Nodes that represent no existing OPC UA nodes, but are used as storage in the computation logic of Connected Factory are also valid.</span><span class="sxs-lookup"><span data-stu-id="a7a63-201">Nodes that represent no existing OPC UA nodes, but are used as storage in the computation logic of Connected Factory are also valid.</span></span> <span data-ttu-id="a7a63-202">It has the following properties:</span><span class="sxs-lookup"><span data-stu-id="a7a63-202">It has the following properties:</span></span>

* <span data-ttu-id="a7a63-203">**NodeId** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-203">**NodeId** (type string)</span></span>

  <span data-ttu-id="a7a63-204">Address of the OPC UA node in the station’s (OPC UA server’s) address space.</span><span class="sxs-lookup"><span data-stu-id="a7a63-204">Address of the OPC UA node in the station’s (OPC UA server’s) address space.</span></span> <span data-ttu-id="a7a63-205">Syntax must be as specified in the OPC UA specification for a NodeId.</span><span class="sxs-lookup"><span data-stu-id="a7a63-205">Syntax must be as specified in the OPC UA specification for a NodeId.</span></span>

* <span data-ttu-id="a7a63-206">**SymbolicName** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-206">**SymbolicName** (type string)</span></span>

  <span data-ttu-id="a7a63-207">Name to be shown in the dashboard when the value of this OPC UA node is shown.</span><span class="sxs-lookup"><span data-stu-id="a7a63-207">Name to be shown in the dashboard when the value of this OPC UA node is shown.</span></span>

* <span data-ttu-id="a7a63-208">**Relevance** (array of type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-208">**Relevance** (array of type string)</span></span>

  <span data-ttu-id="a7a63-209">Indicates for which computation of OEE or KPI the OPC UA node value is relevant.</span><span class="sxs-lookup"><span data-stu-id="a7a63-209">Indicates for which computation of OEE or KPI the OPC UA node value is relevant.</span></span> <span data-ttu-id="a7a63-210">Each array element can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="a7a63-210">Each array element can be one of the following values:</span></span>

  * <span data-ttu-id="a7a63-211">**OeeAvailability_Running**: the value is relevant for calculation of OEE Availability.</span><span class="sxs-lookup"><span data-stu-id="a7a63-211">**OeeAvailability_Running**: the value is relevant for calculation of OEE Availability.</span></span>
  * <span data-ttu-id="a7a63-212">**OeeAvailability_Fault**: the value is relevant for calculation of OEE Availability.</span><span class="sxs-lookup"><span data-stu-id="a7a63-212">**OeeAvailability_Fault**: the value is relevant for calculation of OEE Availability.</span></span>
  * <span data-ttu-id="a7a63-213">**OeePerformance_Ideal**: the value is relevant for calculation of OEE Performance and is typically a constant value.</span><span class="sxs-lookup"><span data-stu-id="a7a63-213">**OeePerformance_Ideal**: the value is relevant for calculation of OEE Performance and is typically a constant value.</span></span>
  * <span data-ttu-id="a7a63-214">**OeePerformance_Actual**: the value is relevant for calculation of OEE Performance.</span><span class="sxs-lookup"><span data-stu-id="a7a63-214">**OeePerformance_Actual**: the value is relevant for calculation of OEE Performance.</span></span>
  * <span data-ttu-id="a7a63-215">**OeeQuality_Good**: the value is relevant for calculation of OEE Quality.</span><span class="sxs-lookup"><span data-stu-id="a7a63-215">**OeeQuality_Good**: the value is relevant for calculation of OEE Quality.</span></span>
  * <span data-ttu-id="a7a63-216">**OeeQuality_Bad**: the value is relevant for calculation of OEE Quality.</span><span class="sxs-lookup"><span data-stu-id="a7a63-216">**OeeQuality_Bad**: the value is relevant for calculation of OEE Quality.</span></span>
  * <span data-ttu-id="a7a63-217">**Kpi1**: the value is relevant for calculation of KPI1.</span><span class="sxs-lookup"><span data-stu-id="a7a63-217">**Kpi1**: the value is relevant for calculation of KPI1.</span></span>
  * <span data-ttu-id="a7a63-218">**Kpi2**: the value is relevant for calculation of KPI2.</span><span class="sxs-lookup"><span data-stu-id="a7a63-218">**Kpi2**: the value is relevant for calculation of KPI2.</span></span>

* <span data-ttu-id="a7a63-219">**OpCode** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-219">**OpCode** (type string)</span></span>

  <span data-ttu-id="a7a63-220">Indicates how the value of the OPC UA node is handled in Time Series Insight queries and OEE/KPI calculations.</span><span class="sxs-lookup"><span data-stu-id="a7a63-220">Indicates how the value of the OPC UA node is handled in Time Series Insight queries and OEE/KPI calculations.</span></span> <span data-ttu-id="a7a63-221">Each Time Series Insight query targets a specific timespan, which is a parameter of the query and delivers a result.</span><span class="sxs-lookup"><span data-stu-id="a7a63-221">Each Time Series Insight query targets a specific timespan, which is a parameter of the query and delivers a result.</span></span> <span data-ttu-id="a7a63-222">The OpCode controls how the result is computed and can be one of the following values:</span><span class="sxs-lookup"><span data-stu-id="a7a63-222">The OpCode controls how the result is computed and can be one of the following values:</span></span>

  * <span data-ttu-id="a7a63-223">**Diff**: difference between the last and the first value in the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-223">**Diff**: difference between the last and the first value in the timespan.</span></span>
  * <span data-ttu-id="a7a63-224">**Avg**: the average of all values in the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-224">**Avg**: the average of all values in the timespan.</span></span>
  * <span data-ttu-id="a7a63-225">**Sum**: the sum of all values in the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-225">**Sum**: the sum of all values in the timespan.</span></span>
  * <span data-ttu-id="a7a63-226">**Last**: currently not used.</span><span class="sxs-lookup"><span data-stu-id="a7a63-226">**Last**: currently not used.</span></span>
  * <span data-ttu-id="a7a63-227">**Count**: the number of values in the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-227">**Count**: the number of values in the timespan.</span></span>
  * <span data-ttu-id="a7a63-228">**Max**: the maximal value in the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-228">**Max**: the maximal value in the timespan.</span></span>
  * <span data-ttu-id="a7a63-229">**Min**: the minimal value in the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-229">**Min**: the minimal value in the timespan.</span></span>
  * <span data-ttu-id="a7a63-230">**Const**: the result is the value specified by property ConstValue.</span><span class="sxs-lookup"><span data-stu-id="a7a63-230">**Const**: the result is the value specified by property ConstValue.</span></span>
  * <span data-ttu-id="a7a63-231">**SubMaxMin**: the difference between the maximal and the minimal value.</span><span class="sxs-lookup"><span data-stu-id="a7a63-231">**SubMaxMin**: the difference between the maximal and the minimal value.</span></span>
  * <span data-ttu-id="a7a63-232">**Timespan**: the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-232">**Timespan**: the timespan.</span></span>

* <span data-ttu-id="a7a63-233">**Units** (type string)</span><span class="sxs-lookup"><span data-stu-id="a7a63-233">**Units** (type string)</span></span>

  <span data-ttu-id="a7a63-234">Defines a unit of the value for display in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-234">Defines a unit of the value for display in the dashboard.</span></span>

* <span data-ttu-id="a7a63-235">**Visible** (type boolean)</span><span class="sxs-lookup"><span data-stu-id="a7a63-235">**Visible** (type boolean)</span></span>

  <span data-ttu-id="a7a63-236">Controls if the value should be shown in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-236">Controls if the value should be shown in the dashboard.</span></span>

* <span data-ttu-id="a7a63-237">**ConstValue** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-237">**ConstValue** (type double)</span></span>

  <span data-ttu-id="a7a63-238">If the **OpCode** is **Const**, then this property is the value of the node.</span><span class="sxs-lookup"><span data-stu-id="a7a63-238">If the **OpCode** is **Const**, then this property is the value of the node.</span></span>

* <span data-ttu-id="a7a63-239">**Minimum** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-239">**Minimum** (type double)</span></span>

  <span data-ttu-id="a7a63-240">If the current value falls below this value, then a minimum alert is generated.</span><span class="sxs-lookup"><span data-stu-id="a7a63-240">If the current value falls below this value, then a minimum alert is generated.</span></span>

* <span data-ttu-id="a7a63-241">**Maximum** (type double)</span><span class="sxs-lookup"><span data-stu-id="a7a63-241">**Maximum** (type double)</span></span>

  <span data-ttu-id="a7a63-242">If the current value raises above this value, then a maximum alert is generated.</span><span class="sxs-lookup"><span data-stu-id="a7a63-242">If the current value raises above this value, then a maximum alert is generated.</span></span>

* <span data-ttu-id="a7a63-243">**MinimumAlertActions** (type `<alert_action>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-243">**MinimumAlertActions** (type `<alert_action>`)</span></span>

  <span data-ttu-id="a7a63-244">Defines the set of actions, which can be taken as response to a minimum alert.</span><span class="sxs-lookup"><span data-stu-id="a7a63-244">Defines the set of actions, which can be taken as response to a minimum alert.</span></span>

* <span data-ttu-id="a7a63-245">**MaximumAlertActions** (type `<alert_action>`)</span><span class="sxs-lookup"><span data-stu-id="a7a63-245">**MaximumAlertActions** (type `<alert_action>`)</span></span>

  <span data-ttu-id="a7a63-246">Defines the set of actions, which can be taken as response to a maximum alert.</span><span class="sxs-lookup"><span data-stu-id="a7a63-246">Defines the set of actions, which can be taken as response to a maximum alert.</span></span>

<span data-ttu-id="a7a63-247">At the station level, you also see **Simulation** objects.</span><span class="sxs-lookup"><span data-stu-id="a7a63-247">At the station level, you also see **Simulation** objects.</span></span> <span data-ttu-id="a7a63-248">These objects are only used to configure the Connected Factory simulation and should not be used to configure a real topology.</span><span class="sxs-lookup"><span data-stu-id="a7a63-248">These objects are only used to configure the Connected Factory simulation and should not be used to configure a real topology.</span></span>

## <a name="how-the-configuration-data-is-used-at-runtime"></a><span data-ttu-id="a7a63-249">How the configuration data is used at runtime</span><span class="sxs-lookup"><span data-stu-id="a7a63-249">How the configuration data is used at runtime</span></span>

<span data-ttu-id="a7a63-250">All the properties used in the configuration file can be grouped into different categories depending on how they are used.</span><span class="sxs-lookup"><span data-stu-id="a7a63-250">All the properties used in the configuration file can be grouped into different categories depending on how they are used.</span></span> <span data-ttu-id="a7a63-251">Those categories are:</span><span class="sxs-lookup"><span data-stu-id="a7a63-251">Those categories are:</span></span>

### <a name="visual-appearance"></a><span data-ttu-id="a7a63-252">Visual appearance</span><span class="sxs-lookup"><span data-stu-id="a7a63-252">Visual appearance</span></span>

<span data-ttu-id="a7a63-253">Properties in this category define the visual appearance of the Connected Factory dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-253">Properties in this category define the visual appearance of the Connected Factory dashboard.</span></span> <span data-ttu-id="a7a63-254">Examples include:</span><span class="sxs-lookup"><span data-stu-id="a7a63-254">Examples include:</span></span>

* <span data-ttu-id="a7a63-255">Name</span><span class="sxs-lookup"><span data-stu-id="a7a63-255">Name</span></span>
* <span data-ttu-id="a7a63-256">Description</span><span class="sxs-lookup"><span data-stu-id="a7a63-256">Description</span></span>
* <span data-ttu-id="a7a63-257">Image</span><span class="sxs-lookup"><span data-stu-id="a7a63-257">Image</span></span>
* <span data-ttu-id="a7a63-258">Location</span><span class="sxs-lookup"><span data-stu-id="a7a63-258">Location</span></span>
* <span data-ttu-id="a7a63-259">Units</span><span class="sxs-lookup"><span data-stu-id="a7a63-259">Units</span></span>
* <span data-ttu-id="a7a63-260">Visible</span><span class="sxs-lookup"><span data-stu-id="a7a63-260">Visible</span></span>

### <a name="internal-topology-tree-addressing"></a><span data-ttu-id="a7a63-261">Internal topology tree addressing</span><span class="sxs-lookup"><span data-stu-id="a7a63-261">Internal topology tree addressing</span></span>

<span data-ttu-id="a7a63-262">The WebApp maintains an internal data dictionary containing information of all topology nodes.</span><span class="sxs-lookup"><span data-stu-id="a7a63-262">The WebApp maintains an internal data dictionary containing information of all topology nodes.</span></span> <span data-ttu-id="a7a63-263">The properties **Guid** and **OpcUri** are used as keys to access this dictionary and need to be unique.</span><span class="sxs-lookup"><span data-stu-id="a7a63-263">The properties **Guid** and **OpcUri** are used as keys to access this dictionary and need to be unique.</span></span>

### <a name="oeekpi-computation"></a><span data-ttu-id="a7a63-264">OEE/KPI computation</span><span class="sxs-lookup"><span data-stu-id="a7a63-264">OEE/KPI computation</span></span>

<span data-ttu-id="a7a63-265">The OEE/KPI figures for the Connected Factory simulation are parameterized by:</span><span class="sxs-lookup"><span data-stu-id="a7a63-265">The OEE/KPI figures for the Connected Factory simulation are parameterized by:</span></span>

* <span data-ttu-id="a7a63-266">The OPC UA node values to be included in the calculation.</span><span class="sxs-lookup"><span data-stu-id="a7a63-266">The OPC UA node values to be included in the calculation.</span></span>
* <span data-ttu-id="a7a63-267">How the figure is computed from the telemetry values.</span><span class="sxs-lookup"><span data-stu-id="a7a63-267">How the figure is computed from the telemetry values.</span></span>

<span data-ttu-id="a7a63-268">Connected Factory uses the OEE formulas as published by the http://www.oeefoundation.org.</span><span class="sxs-lookup"><span data-stu-id="a7a63-268">Connected Factory uses the OEE formulas as published by the http://www.oeefoundation.org.</span></span>

<span data-ttu-id="a7a63-269">OPC UA node objects in stations enable tagging for usage in OEE/KPI calculation.</span><span class="sxs-lookup"><span data-stu-id="a7a63-269">OPC UA node objects in stations enable tagging for usage in OEE/KPI calculation.</span></span> <span data-ttu-id="a7a63-270">The **Relevance** property indicates for which OEE/KPI figure the OPC UA node value should be used.</span><span class="sxs-lookup"><span data-stu-id="a7a63-270">The **Relevance** property indicates for which OEE/KPI figure the OPC UA node value should be used.</span></span> <span data-ttu-id="a7a63-271">The **OpCode** property defines how the value is included in the computation.</span><span class="sxs-lookup"><span data-stu-id="a7a63-271">The **OpCode** property defines how the value is included in the computation.</span></span>

### <a name="alert-handling"></a><span data-ttu-id="a7a63-272">Alert handling</span><span class="sxs-lookup"><span data-stu-id="a7a63-272">Alert handling</span></span>

<span data-ttu-id="a7a63-273">Connected Factory supports a simple minimum/maximum threshold-based alert generation mechanism.</span><span class="sxs-lookup"><span data-stu-id="a7a63-273">Connected Factory supports a simple minimum/maximum threshold-based alert generation mechanism.</span></span> <span data-ttu-id="a7a63-274">There are a number of predefined actions you can configure in response to those alerts.</span><span class="sxs-lookup"><span data-stu-id="a7a63-274">There are a number of predefined actions you can configure in response to those alerts.</span></span> <span data-ttu-id="a7a63-275">The following properties control this mechanism:</span><span class="sxs-lookup"><span data-stu-id="a7a63-275">The following properties control this mechanism:</span></span>

* <span data-ttu-id="a7a63-276">Maximum</span><span class="sxs-lookup"><span data-stu-id="a7a63-276">Maximum</span></span>
* <span data-ttu-id="a7a63-277">Minimum</span><span class="sxs-lookup"><span data-stu-id="a7a63-277">Minimum</span></span>
* <span data-ttu-id="a7a63-278">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="a7a63-278">MaximumAlertActions</span></span>
* <span data-ttu-id="a7a63-279">MinimumAlertActions</span><span class="sxs-lookup"><span data-stu-id="a7a63-279">MinimumAlertActions</span></span>

## <a name="correlating-to-telemetry-data"></a><span data-ttu-id="a7a63-280">Correlating to telemetry data</span><span class="sxs-lookup"><span data-stu-id="a7a63-280">Correlating to telemetry data</span></span>

<span data-ttu-id="a7a63-281">For certain operations, such as visualizing the last value or creating Time Series Insight queries, the WebApp needs an addressing scheme for the ingested telemetry data.</span><span class="sxs-lookup"><span data-stu-id="a7a63-281">For certain operations, such as visualizing the last value or creating Time Series Insight queries, the WebApp needs an addressing scheme for the ingested telemetry data.</span></span> <span data-ttu-id="a7a63-282">The telemetry sent to Connected Factory also needs to be stored in internal data structures.</span><span class="sxs-lookup"><span data-stu-id="a7a63-282">The telemetry sent to Connected Factory also needs to be stored in internal data structures.</span></span> <span data-ttu-id="a7a63-283">The two properties enabling these operations are at station (OPC UA server) and OPC UA node level:</span><span class="sxs-lookup"><span data-stu-id="a7a63-283">The two properties enabling these operations are at station (OPC UA server) and OPC UA node level:</span></span>

* <span data-ttu-id="a7a63-284">**OpcUri**</span><span class="sxs-lookup"><span data-stu-id="a7a63-284">**OpcUri**</span></span>

  <span data-ttu-id="a7a63-285">Identifies (globally unique) the OPC UA server the telemetry comes from.</span><span class="sxs-lookup"><span data-stu-id="a7a63-285">Identifies (globally unique) the OPC UA server the telemetry comes from.</span></span> <span data-ttu-id="a7a63-286">In the ingested messages, this property is sent as **ApplicationUri**.</span><span class="sxs-lookup"><span data-stu-id="a7a63-286">In the ingested messages, this property is sent as **ApplicationUri**.</span></span>

* <span data-ttu-id="a7a63-287">**NodeId**</span><span class="sxs-lookup"><span data-stu-id="a7a63-287">**NodeId**</span></span>

  <span data-ttu-id="a7a63-288">Identifies the node value in the OPC UA server.</span><span class="sxs-lookup"><span data-stu-id="a7a63-288">Identifies the node value in the OPC UA server.</span></span> <span data-ttu-id="a7a63-289">The format of the property must be as specified in the OPC UA specification.</span><span class="sxs-lookup"><span data-stu-id="a7a63-289">The format of the property must be as specified in the OPC UA specification.</span></span> <span data-ttu-id="a7a63-290">In the ingested messages, this property is sent as **NodeId**.</span><span class="sxs-lookup"><span data-stu-id="a7a63-290">In the ingested messages, this property is sent as **NodeId**.</span></span>

<span data-ttu-id="a7a63-291">Check [this](https://github.com/Azure/iot-edge-opc-publisher) GitHub page for more information on how the telemetry data is ingested to Connected Factory using the OPC Publisher.</span><span class="sxs-lookup"><span data-stu-id="a7a63-291">Check [this](https://github.com/Azure/iot-edge-opc-publisher) GitHub page for more information on how the telemetry data is ingested to Connected Factory using the OPC Publisher.</span></span>

## <a name="example-how-kpi1-is-calculated"></a><span data-ttu-id="a7a63-292">Example: How KPI1 is calculated</span><span class="sxs-lookup"><span data-stu-id="a7a63-292">Example: How KPI1 is calculated</span></span>

<span data-ttu-id="a7a63-293">The configuration in the `ContosoTopologyDescription.json` file controls how OEE/KPI figures are calculated.</span><span class="sxs-lookup"><span data-stu-id="a7a63-293">The configuration in the `ContosoTopologyDescription.json` file controls how OEE/KPI figures are calculated.</span></span> <span data-ttu-id="a7a63-294">The following example shows how properties in this file control the computation of KPI1.</span><span class="sxs-lookup"><span data-stu-id="a7a63-294">The following example shows how properties in this file control the computation of KPI1.</span></span>

<span data-ttu-id="a7a63-295">In Connected Factory KPI1 is used to measure the number of successfully manufactured products in the last hour.</span><span class="sxs-lookup"><span data-stu-id="a7a63-295">In Connected Factory KPI1 is used to measure the number of successfully manufactured products in the last hour.</span></span> <span data-ttu-id="a7a63-296">Each station (OPC UA server) in the Connected Factory simulation provides an OPC UA node (`NodeId: "ns=2;i=385"`), which provides the telemetry to compute this KPI.</span><span class="sxs-lookup"><span data-stu-id="a7a63-296">Each station (OPC UA server) in the Connected Factory simulation provides an OPC UA node (`NodeId: "ns=2;i=385"`), which provides the telemetry to compute this KPI.</span></span>

<span data-ttu-id="a7a63-297">The configuration for this OPC UA node looks like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="a7a63-297">The configuration for this OPC UA node looks like the following snippet:</span></span>

```json
{
  "NodeId": "ns=2;i=385",
  "SymbolicName": "NumberOfManufacturedProducts",
  "Relevance": [ "Kpi1", "OeeQuality_Good" ],
  "OpCode": "SubMaxMin"
},
```

<span data-ttu-id="a7a63-298">This configuration enables querying of the telemetry values of this node using Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="a7a63-298">This configuration enables querying of the telemetry values of this node using Time Series Insights.</span></span> <span data-ttu-id="a7a63-299">The Time Series Insights query retrieves:</span><span class="sxs-lookup"><span data-stu-id="a7a63-299">The Time Series Insights query retrieves:</span></span>

* <span data-ttu-id="a7a63-300">The number of values.</span><span class="sxs-lookup"><span data-stu-id="a7a63-300">The number of values.</span></span>
* <span data-ttu-id="a7a63-301">The minimal value.</span><span class="sxs-lookup"><span data-stu-id="a7a63-301">The minimal value.</span></span>
* <span data-ttu-id="a7a63-302">The maximal value.</span><span class="sxs-lookup"><span data-stu-id="a7a63-302">The maximal value.</span></span>
* <span data-ttu-id="a7a63-303">The average of all values.</span><span class="sxs-lookup"><span data-stu-id="a7a63-303">The average of all values.</span></span>
* <span data-ttu-id="a7a63-304">The sum of all values for all unique **OpcUri** (**ApplicationUri**), **NodeId** pairs in a given timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-304">The sum of all values for all unique **OpcUri** (**ApplicationUri**), **NodeId** pairs in a given timespan.</span></span>

<span data-ttu-id="a7a63-305">One characteristic of the **NumberOfManufactureredProducts** node value is that it only increases.</span><span class="sxs-lookup"><span data-stu-id="a7a63-305">One characteristic of the **NumberOfManufactureredProducts** node value is that it only increases.</span></span> <span data-ttu-id="a7a63-306">To calculate the number of products manufactured in the timespan, Connected Factory uses the **OpCode** **SubMaxMin**.</span><span class="sxs-lookup"><span data-stu-id="a7a63-306">To calculate the number of products manufactured in the timespan, Connected Factory uses the **OpCode** **SubMaxMin**.</span></span> <span data-ttu-id="a7a63-307">The calculation retrieves the minimum value at the start of the timespan and the maximum value at the end of the timespan.</span><span class="sxs-lookup"><span data-stu-id="a7a63-307">The calculation retrieves the minimum value at the start of the timespan and the maximum value at the end of the timespan.</span></span>

<span data-ttu-id="a7a63-308">The **OpCode** in the configuration configures the computation logic to calculate the result of the difference of maximum and minimum value.</span><span class="sxs-lookup"><span data-stu-id="a7a63-308">The **OpCode** in the configuration configures the computation logic to calculate the result of the difference of maximum and minimum value.</span></span> <span data-ttu-id="a7a63-309">Those results are then accumulated bottom up to the root (global) level and shown in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a7a63-309">Those results are then accumulated bottom up to the root (global) level and shown in the dashboard.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7a63-310">Next steps</span><span class="sxs-lookup"><span data-stu-id="a7a63-310">Next steps</span></span>

<span data-ttu-id="a7a63-311">A suggested next step is to learn how to [Deploy a gateway on Windows or Linux for the Connected Factory solution accelerator](iot-accelerators-connected-factory-gateway-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a7a63-311">A suggested next step is to learn how to [Deploy a gateway on Windows or Linux for the Connected Factory solution accelerator](iot-accelerators-connected-factory-gateway-deployment.md).</span></span>
