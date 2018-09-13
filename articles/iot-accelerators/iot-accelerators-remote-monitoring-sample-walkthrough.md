---
title: Remote Monitoring solution accelerator overview - Azure | Microsoft Docs
description: An overview of the Remote Monitoring solution accelerator.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 11/10/2017
ms.author: dobett
ms.openlocfilehash: 097eba4f5bcbb74d4158cc8d4135255d31e03ebd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870744"
---
# <a name="remote-monitoring-solution-accelerator-overview"></a><span data-ttu-id="84a6b-103">Remote Monitoring solution accelerator overview</span><span class="sxs-lookup"><span data-stu-id="84a6b-103">Remote Monitoring solution accelerator overview</span></span>

<span data-ttu-id="84a6b-104">The Remote Monitoring [solution accelerator](../iot-accelerators/about-iot-accelerators.md) implements an end-to-end monitoring solution for multiple machines in remote locations.</span><span class="sxs-lookup"><span data-stu-id="84a6b-104">The Remote Monitoring [solution accelerator](../iot-accelerators/about-iot-accelerators.md) implements an end-to-end monitoring solution for multiple machines in remote locations.</span></span> <span data-ttu-id="84a6b-105">The solution combines key Azure services to provide a generic implementation of the business scenario.</span><span class="sxs-lookup"><span data-stu-id="84a6b-105">The solution combines key Azure services to provide a generic implementation of the business scenario.</span></span> <span data-ttu-id="84a6b-106">You can use the solution as a starting point for your own implementation and [customize](../iot-accelerators/iot-accelerators-remote-monitoring-customize.md) it to meet your own specific business requirements.</span><span class="sxs-lookup"><span data-stu-id="84a6b-106">You can use the solution as a starting point for your own implementation and [customize](../iot-accelerators/iot-accelerators-remote-monitoring-customize.md) it to meet your own specific business requirements.</span></span>

<span data-ttu-id="84a6b-107">This article walks you through some of the key elements of the Remote Monitoring solution to enable you to understand how it works.</span><span class="sxs-lookup"><span data-stu-id="84a6b-107">This article walks you through some of the key elements of the Remote Monitoring solution to enable you to understand how it works.</span></span> <span data-ttu-id="84a6b-108">This knowledge helps you to:</span><span class="sxs-lookup"><span data-stu-id="84a6b-108">This knowledge helps you to:</span></span>

* <span data-ttu-id="84a6b-109">Troubleshoot issues in the solution.</span><span class="sxs-lookup"><span data-stu-id="84a6b-109">Troubleshoot issues in the solution.</span></span>
* <span data-ttu-id="84a6b-110">Plan how to customize to the solution to meet your own specific requirements.</span><span class="sxs-lookup"><span data-stu-id="84a6b-110">Plan how to customize to the solution to meet your own specific requirements.</span></span>
* <span data-ttu-id="84a6b-111">Design your own IoT solution that uses Azure services.</span><span class="sxs-lookup"><span data-stu-id="84a6b-111">Design your own IoT solution that uses Azure services.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="84a6b-112">Logical architecture</span><span class="sxs-lookup"><span data-stu-id="84a6b-112">Logical architecture</span></span>

<span data-ttu-id="84a6b-113">The following diagram outlines the logical components of the Remote Monitoring solution accelerator overlaid on the [IoT architecture](../iot-fundamentals/iot-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="84a6b-113">The following diagram outlines the logical components of the Remote Monitoring solution accelerator overlaid on the [IoT architecture](../iot-fundamentals/iot-introduction.md):</span></span>

![Logical architecture](./media/iot-accelerators-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="why-microservices"></a><span data-ttu-id="84a6b-115">Why microservices?</span><span class="sxs-lookup"><span data-stu-id="84a6b-115">Why microservices?</span></span>

<span data-ttu-id="84a6b-116">Cloud architecture has evolved since Microsoft released the first solution accelerators.</span><span class="sxs-lookup"><span data-stu-id="84a6b-116">Cloud architecture has evolved since Microsoft released the first solution accelerators.</span></span> <span data-ttu-id="84a6b-117">[Microservices](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/) have emerged as a proven practice to achieve scale and flexibility without sacrificing development speed.</span><span class="sxs-lookup"><span data-stu-id="84a6b-117">[Microservices](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/) have emerged as a proven practice to achieve scale and flexibility without sacrificing development speed.</span></span> <span data-ttu-id="84a6b-118">Several Microsoft services use this architectural pattern internally with great reliability and scalability results.</span><span class="sxs-lookup"><span data-stu-id="84a6b-118">Several Microsoft services use this architectural pattern internally with great reliability and scalability results.</span></span> <span data-ttu-id="84a6b-119">The updated solution accelerators put these learnings into practice so you can also benefit from them.</span><span class="sxs-lookup"><span data-stu-id="84a6b-119">The updated solution accelerators put these learnings into practice so you can also benefit from them.</span></span>

> [!TIP]
> <span data-ttu-id="84a6b-120">To learn more about microservice architectures, see [.NET Application Architecture](https://www.microsoft.com/net/learn/architecture) and [Microservices: An application revolution powered by the cloud](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).</span><span class="sxs-lookup"><span data-stu-id="84a6b-120">To learn more about microservice architectures, see [.NET Application Architecture](https://www.microsoft.com/net/learn/architecture) and [Microservices: An application revolution powered by the cloud](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).</span></span>

## <a name="device-connectivity"></a><span data-ttu-id="84a6b-121">Device connectivity</span><span class="sxs-lookup"><span data-stu-id="84a6b-121">Device connectivity</span></span>

<span data-ttu-id="84a6b-122">The solution includes the following components in the device connectivity part of the logical architecture:</span><span class="sxs-lookup"><span data-stu-id="84a6b-122">The solution includes the following components in the device connectivity part of the logical architecture:</span></span>

### <a name="physical-devices"></a><span data-ttu-id="84a6b-123">Physical devices</span><span class="sxs-lookup"><span data-stu-id="84a6b-123">Physical devices</span></span>

<span data-ttu-id="84a6b-124">You can connect physical devices to the solution.</span><span class="sxs-lookup"><span data-stu-id="84a6b-124">You can connect physical devices to the solution.</span></span> <span data-ttu-id="84a6b-125">You can implement the behavior of your simulated devices using the Azure IoT device SDKs.</span><span class="sxs-lookup"><span data-stu-id="84a6b-125">You can implement the behavior of your simulated devices using the Azure IoT device SDKs.</span></span>

<span data-ttu-id="84a6b-126">You can provision physical devices from the dashboard in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="84a6b-126">You can provision physical devices from the dashboard in the solution portal.</span></span>

### <a name="device-simulation-microservice"></a><span data-ttu-id="84a6b-127">Device simulation microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-127">Device simulation microservice</span></span>

<span data-ttu-id="84a6b-128">The solution includes the [device simulation microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/device-simulation) that enables you to manage a pool of simulated devices from the solution dashboard to test the end-to-end flow in the solution.</span><span class="sxs-lookup"><span data-stu-id="84a6b-128">The solution includes the [device simulation microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/device-simulation) that enables you to manage a pool of simulated devices from the solution dashboard to test the end-to-end flow in the solution.</span></span> <span data-ttu-id="84a6b-129">The simulated devices:</span><span class="sxs-lookup"><span data-stu-id="84a6b-129">The simulated devices:</span></span>

* <span data-ttu-id="84a6b-130">Generate device-to-cloud telemetry.</span><span class="sxs-lookup"><span data-stu-id="84a6b-130">Generate device-to-cloud telemetry.</span></span>
* <span data-ttu-id="84a6b-131">Respond to cloud-to-device method calls from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="84a6b-131">Respond to cloud-to-device method calls from IoT Hub.</span></span>

<span data-ttu-id="84a6b-132">The microservice provides a RESTful endpoint for you to create, start, and stop simulations.</span><span class="sxs-lookup"><span data-stu-id="84a6b-132">The microservice provides a RESTful endpoint for you to create, start, and stop simulations.</span></span> <span data-ttu-id="84a6b-133">Each simulation consists of a set of virtual devices of different types, that send telemetry and respond to method calls.</span><span class="sxs-lookup"><span data-stu-id="84a6b-133">Each simulation consists of a set of virtual devices of different types, that send telemetry and respond to method calls.</span></span>

<span data-ttu-id="84a6b-134">You can provision simulated devices from the dashboard in the solution portal.</span><span class="sxs-lookup"><span data-stu-id="84a6b-134">You can provision simulated devices from the dashboard in the solution portal.</span></span>

### <a name="iot-hub"></a><span data-ttu-id="84a6b-135">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="84a6b-135">IoT Hub</span></span>

<span data-ttu-id="84a6b-136">The [IoT hub](../iot-hub/index.yml) ingests telemetry sent from both the physical and simulated devices into the cloud.</span><span class="sxs-lookup"><span data-stu-id="84a6b-136">The [IoT hub](../iot-hub/index.yml) ingests telemetry sent from both the physical and simulated devices into the cloud.</span></span> <span data-ttu-id="84a6b-137">The IoT hub makes the telemetry available to the services in the IoT solution backend for processing.</span><span class="sxs-lookup"><span data-stu-id="84a6b-137">The IoT hub makes the telemetry available to the services in the IoT solution backend for processing.</span></span>

<span data-ttu-id="84a6b-138">The IoT hub in the solution also:</span><span class="sxs-lookup"><span data-stu-id="84a6b-138">The IoT hub in the solution also:</span></span>

* <span data-ttu-id="84a6b-139">Maintains an identity registry that stores the IDs and authentication keys of all the devices permitted to connect to the portal.</span><span class="sxs-lookup"><span data-stu-id="84a6b-139">Maintains an identity registry that stores the IDs and authentication keys of all the devices permitted to connect to the portal.</span></span>
* <span data-ttu-id="84a6b-140">Invokes methods on your devices on behalf of the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="84a6b-140">Invokes methods on your devices on behalf of the solution accelerator.</span></span>
* <span data-ttu-id="84a6b-141">Maintains device twins for all registered devices.</span><span class="sxs-lookup"><span data-stu-id="84a6b-141">Maintains device twins for all registered devices.</span></span> <span data-ttu-id="84a6b-142">A device twin stores the property values reported by a device.</span><span class="sxs-lookup"><span data-stu-id="84a6b-142">A device twin stores the property values reported by a device.</span></span> <span data-ttu-id="84a6b-143">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span><span class="sxs-lookup"><span data-stu-id="84a6b-143">A device twin also stores desired properties, set in the solution portal, for the device to retrieve when it next connects.</span></span>
* <span data-ttu-id="84a6b-144">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span><span class="sxs-lookup"><span data-stu-id="84a6b-144">Schedules jobs to set properties for multiple devices or invoke methods on multiple devices.</span></span>

## <a name="data-processing-and-analytics"></a><span data-ttu-id="84a6b-145">Data processing and analytics</span><span class="sxs-lookup"><span data-stu-id="84a6b-145">Data processing and analytics</span></span>

<span data-ttu-id="84a6b-146">The solution includes the following components in the data processing and analytics part of the logical architecture:</span><span class="sxs-lookup"><span data-stu-id="84a6b-146">The solution includes the following components in the data processing and analytics part of the logical architecture:</span></span>

### <a name="iot-hub-manager-microservice"></a><span data-ttu-id="84a6b-147">IoT Hub manager microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-147">IoT Hub manager microservice</span></span>

<span data-ttu-id="84a6b-148">The solution includes the [IoT Hub manager microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/iothub-manager) to handle interactions with your IoT hub such as:</span><span class="sxs-lookup"><span data-stu-id="84a6b-148">The solution includes the [IoT Hub manager microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/iothub-manager) to handle interactions with your IoT hub such as:</span></span>

* <span data-ttu-id="84a6b-149">Creating and managing IoT devices.</span><span class="sxs-lookup"><span data-stu-id="84a6b-149">Creating and managing IoT devices.</span></span>
* <span data-ttu-id="84a6b-150">Managing device twins.</span><span class="sxs-lookup"><span data-stu-id="84a6b-150">Managing device twins.</span></span>
* <span data-ttu-id="84a6b-151">Invoking methods on devices.</span><span class="sxs-lookup"><span data-stu-id="84a6b-151">Invoking methods on devices.</span></span>
* <span data-ttu-id="84a6b-152">Managing IoT credentials.</span><span class="sxs-lookup"><span data-stu-id="84a6b-152">Managing IoT credentials.</span></span>

<span data-ttu-id="84a6b-153">This service also runs IoT Hub queries to retrieve devices belonging to user-defined groups.</span><span class="sxs-lookup"><span data-stu-id="84a6b-153">This service also runs IoT Hub queries to retrieve devices belonging to user-defined groups.</span></span>

<span data-ttu-id="84a6b-154">The microservice provides a RESTful endpoint to manage devices and device twins, invoke methods, and run IoT Hub queries.</span><span class="sxs-lookup"><span data-stu-id="84a6b-154">The microservice provides a RESTful endpoint to manage devices and device twins, invoke methods, and run IoT Hub queries.</span></span>

### <a name="telemetry-microservice"></a><span data-ttu-id="84a6b-155">Telemetry microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-155">Telemetry microservice</span></span>

<span data-ttu-id="84a6b-156">The [telemetry microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/device-telemetry) provides a RESTful endpoint for read access to device telemetry, CRUD operations on rules, and read/write access for alarm definitions from storage.</span><span class="sxs-lookup"><span data-stu-id="84a6b-156">The [telemetry microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/device-telemetry) provides a RESTful endpoint for read access to device telemetry, CRUD operations on rules, and read/write access for alarm definitions from storage.</span></span>

### <a name="storage-adapter-microservice"></a><span data-ttu-id="84a6b-157">Storage adapter microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-157">Storage adapter microservice</span></span>

<span data-ttu-id="84a6b-158">The [storage adapter microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/storage-adapter) manages key-value pairs, abstracting the storage service semantics, and presenting a simple interface to store data of any format using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="84a6b-158">The [storage adapter microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/storage-adapter) manages key-value pairs, abstracting the storage service semantics, and presenting a simple interface to store data of any format using Azure Cosmos DB.</span></span>

<span data-ttu-id="84a6b-159">Values are organized in collections.</span><span class="sxs-lookup"><span data-stu-id="84a6b-159">Values are organized in collections.</span></span> <span data-ttu-id="84a6b-160">You can work on individual values or fetch entire collections.</span><span class="sxs-lookup"><span data-stu-id="84a6b-160">You can work on individual values or fetch entire collections.</span></span> <span data-ttu-id="84a6b-161">Complex data structures are serialized by the clients and managed as simple text payload.</span><span class="sxs-lookup"><span data-stu-id="84a6b-161">Complex data structures are serialized by the clients and managed as simple text payload.</span></span>

<span data-ttu-id="84a6b-162">The service provides a RESTful endpoint for CRUD operations on key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="84a6b-162">The service provides a RESTful endpoint for CRUD operations on key-value pairs.</span></span> <span data-ttu-id="84a6b-163">values</span><span class="sxs-lookup"><span data-stu-id="84a6b-163">values</span></span>

### <a name="cosmos-db"></a><span data-ttu-id="84a6b-164">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="84a6b-164">Cosmos DB</span></span>

<span data-ttu-id="84a6b-165">The standard deployment of the solution accelerator uses [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/) as its main storage service.</span><span class="sxs-lookup"><span data-stu-id="84a6b-165">The standard deployment of the solution accelerator uses [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/) as its main storage service.</span></span>

### <a name="azure-stream-analytics-manager-microservice"></a><span data-ttu-id="84a6b-166">Azure Stream Analytics manager microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-166">Azure Stream Analytics manager microservice</span></span>

<span data-ttu-id="84a6b-167">The [Azure Stream Analytics manager microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/asa-manager) manages Azure Stream Analytics (ASA) jobs, including setting their configuration, starting and stopping them, and monitoring their status.</span><span class="sxs-lookup"><span data-stu-id="84a6b-167">The [Azure Stream Analytics manager microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/asa-manager) manages Azure Stream Analytics (ASA) jobs, including setting their configuration, starting and stopping them, and monitoring their status.</span></span>

<span data-ttu-id="84a6b-168">The ASA job is supported by two reference data sets.</span><span class="sxs-lookup"><span data-stu-id="84a6b-168">The ASA job is supported by two reference data sets.</span></span> <span data-ttu-id="84a6b-169">One data set defines rules and one defines device groups.</span><span class="sxs-lookup"><span data-stu-id="84a6b-169">One data set defines rules and one defines device groups.</span></span> <span data-ttu-id="84a6b-170">The rules reference data is generated from the information managed by the telemetry microservice.</span><span class="sxs-lookup"><span data-stu-id="84a6b-170">The rules reference data is generated from the information managed by the telemetry microservice.</span></span> <span data-ttu-id="84a6b-171">The Azure Stream Analytics manager microservice transforms telemetry rules into stream processing logic.</span><span class="sxs-lookup"><span data-stu-id="84a6b-171">The Azure Stream Analytics manager microservice transforms telemetry rules into stream processing logic.</span></span>

<span data-ttu-id="84a6b-172">The device groups reference data is used to identify which group of rules to apply to an incoming telemetry message.</span><span class="sxs-lookup"><span data-stu-id="84a6b-172">The device groups reference data is used to identify which group of rules to apply to an incoming telemetry message.</span></span> <span data-ttu-id="84a6b-173">The device groups are managed by the configuration microservice and use Azure IoT Hub device twin queries.</span><span class="sxs-lookup"><span data-stu-id="84a6b-173">The device groups are managed by the configuration microservice and use Azure IoT Hub device twin queries.</span></span>

### <a name="azure-stream-analytics"></a><span data-ttu-id="84a6b-174">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="84a6b-174">Azure Stream Analytics</span></span>

<span data-ttu-id="84a6b-175">[Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) is an event-processing engine that allows you to examine high volumes of data streaming from devices.</span><span class="sxs-lookup"><span data-stu-id="84a6b-175">[Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) is an event-processing engine that allows you to examine high volumes of data streaming from devices.</span></span>

### <a name="configuration-microservice"></a><span data-ttu-id="84a6b-176">Configuration microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-176">Configuration microservice</span></span>

<span data-ttu-id="84a6b-177">The [configuration microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/config) provides a RESTful endpoint for CRUD operations on device groups, solution settings, and user-settings in the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="84a6b-177">The [configuration microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/config) provides a RESTful endpoint for CRUD operations on device groups, solution settings, and user-settings in the solution accelerator.</span></span> <span data-ttu-id="84a6b-178">It works with the storage adapter microservice to persist the configuration data.</span><span class="sxs-lookup"><span data-stu-id="84a6b-178">It works with the storage adapter microservice to persist the configuration data.</span></span>

### <a name="authentication-and-authorization-microservice"></a><span data-ttu-id="84a6b-179">Authentication and authorization microservice</span><span class="sxs-lookup"><span data-stu-id="84a6b-179">Authentication and authorization microservice</span></span>

<span data-ttu-id="84a6b-180">The [authentication and authorization microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/auth) manages the users authorized to access the solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="84a6b-180">The [authentication and authorization microservice](https://github.com/Azure/remote-monitoring-services-dotnet/tree/master/auth) manages the users authorized to access the solution accelerator.</span></span> <span data-ttu-id="84a6b-181">User management can be done using any identity service provider that supports [OpenId Connect](http://openid.net/connect/).</span><span class="sxs-lookup"><span data-stu-id="84a6b-181">User management can be done using any identity service provider that supports [OpenId Connect](http://openid.net/connect/).</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="84a6b-182">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84a6b-182">Azure Active Directory</span></span>

<span data-ttu-id="84a6b-183">The standard deployment of the solution accelerator uses [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) as an OpenID Connect provider.</span><span class="sxs-lookup"><span data-stu-id="84a6b-183">The standard deployment of the solution accelerator uses [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) as an OpenID Connect provider.</span></span> <span data-ttu-id="84a6b-184">Azure Active Directory stores user information and provides certificates to validate JWT token signatures.</span><span class="sxs-lookup"><span data-stu-id="84a6b-184">Azure Active Directory stores user information and provides certificates to validate JWT token signatures.</span></span> 

## <a name="presentation"></a><span data-ttu-id="84a6b-185">Presentation</span><span class="sxs-lookup"><span data-stu-id="84a6b-185">Presentation</span></span>

<span data-ttu-id="84a6b-186">The solution includes the following components in the presentation part of the logical architecture:</span><span class="sxs-lookup"><span data-stu-id="84a6b-186">The solution includes the following components in the presentation part of the logical architecture:</span></span>

<span data-ttu-id="84a6b-187">The [web user interface is a React Javascript application](https://github.com/Azure/pcs-remote-monitoring-webui).</span><span class="sxs-lookup"><span data-stu-id="84a6b-187">The [web user interface is a React Javascript application](https://github.com/Azure/pcs-remote-monitoring-webui).</span></span> <span data-ttu-id="84a6b-188">The application:</span><span class="sxs-lookup"><span data-stu-id="84a6b-188">The application:</span></span>

* <span data-ttu-id="84a6b-189">Uses Javascript React only and runs entirely in the browser.</span><span class="sxs-lookup"><span data-stu-id="84a6b-189">Uses Javascript React only and runs entirely in the browser.</span></span>
* <span data-ttu-id="84a6b-190">Is styled with CSS.</span><span class="sxs-lookup"><span data-stu-id="84a6b-190">Is styled with CSS.</span></span>
* <span data-ttu-id="84a6b-191">Interacts with public facing microservices through AJAX calls.</span><span class="sxs-lookup"><span data-stu-id="84a6b-191">Interacts with public facing microservices through AJAX calls.</span></span>

<span data-ttu-id="84a6b-192">The user interface presents all the solution accelerator functionality, and interacts with other microservices such as:</span><span class="sxs-lookup"><span data-stu-id="84a6b-192">The user interface presents all the solution accelerator functionality, and interacts with other microservices such as:</span></span>

* <span data-ttu-id="84a6b-193">The authentication and authorization microservice to protect user data.</span><span class="sxs-lookup"><span data-stu-id="84a6b-193">The authentication and authorization microservice to protect user data.</span></span>
* <span data-ttu-id="84a6b-194">The IoT Hub manager microservice to list and manage the IoT devices.</span><span class="sxs-lookup"><span data-stu-id="84a6b-194">The IoT Hub manager microservice to list and manage the IoT devices.</span></span>

<span data-ttu-id="84a6b-195">The configuration microservice enables the user interface to store and retrieve configuration settings.</span><span class="sxs-lookup"><span data-stu-id="84a6b-195">The configuration microservice enables the user interface to store and retrieve configuration settings.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84a6b-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="84a6b-196">Next steps</span></span>

<span data-ttu-id="84a6b-197">If you want to explore the source code and developer documentation, start with one of the two GitHub repositories:</span><span class="sxs-lookup"><span data-stu-id="84a6b-197">If you want to explore the source code and developer documentation, start with one of the two GitHub repositories:</span></span>

* <span data-ttu-id="84a6b-198">[Solution accelerator for Remote Monitoring with Azure IoT (.NET)](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/).</span><span class="sxs-lookup"><span data-stu-id="84a6b-198">[Solution accelerator for Remote Monitoring with Azure IoT (.NET)](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/).</span></span>
* <span data-ttu-id="84a6b-199">[Solution accelerator for Remote Monitoring with Azure IoT (Java)](https://github.com/Azure/azure-iot-pcs-remote-monitoring-java).</span><span class="sxs-lookup"><span data-stu-id="84a6b-199">[Solution accelerator for Remote Monitoring with Azure IoT (Java)](https://github.com/Azure/azure-iot-pcs-remote-monitoring-java).</span></span>

<span data-ttu-id="84a6b-200">Detailed solution architecture diagrams:</span><span class="sxs-lookup"><span data-stu-id="84a6b-200">Detailed solution architecture diagrams:</span></span>
* <span data-ttu-id="84a6b-201">[Solution accelerator for Remote Monitoring architecture](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Architecture).</span><span class="sxs-lookup"><span data-stu-id="84a6b-201">[Solution accelerator for Remote Monitoring architecture](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Architecture).</span></span>

<span data-ttu-id="84a6b-202">For more conceptual information about the Remote Monitoring solution accelerator, see [Customize the solution accelerator](../iot-accelerators/iot-accelerators-remote-monitoring-customize.md).</span><span class="sxs-lookup"><span data-stu-id="84a6b-202">For more conceptual information about the Remote Monitoring solution accelerator, see [Customize the solution accelerator](../iot-accelerators/iot-accelerators-remote-monitoring-customize.md).</span></span>
