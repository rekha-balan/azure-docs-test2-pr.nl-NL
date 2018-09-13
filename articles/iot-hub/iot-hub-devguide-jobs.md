---
title: Understand Azure IoT Hub jobs | Microsoft Docs
description: Developer guide - scheduling jobs to run on multiple devices connected to your IoT hub. Jobs can update tags and desired properties and invoke direct methods on multiple devices.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: ''
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: b94ceac2298509817020b32b65125c5f767d8089
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661398"
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="5770b-104">Schedule jobs on multiple devices</span><span class="sxs-lookup"><span data-stu-id="5770b-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="5770b-105">Overview</span><span class="sxs-lookup"><span data-stu-id="5770b-105">Overview</span></span>
<span data-ttu-id="5770b-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="5770b-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="5770b-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span><span class="sxs-lookup"><span data-stu-id="5770b-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="5770b-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span><span class="sxs-lookup"><span data-stu-id="5770b-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="5770b-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span><span class="sxs-lookup"><span data-stu-id="5770b-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="5770b-110">When to use</span><span class="sxs-lookup"><span data-stu-id="5770b-110">When to use</span></span>
<span data-ttu-id="5770b-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span><span class="sxs-lookup"><span data-stu-id="5770b-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="5770b-112">Update desired properties</span><span class="sxs-lookup"><span data-stu-id="5770b-112">Update desired properties</span></span>
* <span data-ttu-id="5770b-113">Update tags</span><span class="sxs-lookup"><span data-stu-id="5770b-113">Update tags</span></span>
* <span data-ttu-id="5770b-114">Invoke direct methods</span><span class="sxs-lookup"><span data-stu-id="5770b-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="5770b-115">Job lifecycle</span><span class="sxs-lookup"><span data-stu-id="5770b-115">Job lifecycle</span></span>
<span data-ttu-id="5770b-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5770b-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="5770b-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="5770b-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="5770b-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span><span class="sxs-lookup"><span data-stu-id="5770b-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="5770b-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="5770b-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="5770b-120">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="5770b-120">Reference topics:</span></span>
<span data-ttu-id="5770b-121">The following reference topics provide you with more information about using jobs.</span><span class="sxs-lookup"><span data-stu-id="5770b-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="5770b-122">Jobs to execute direct methods</span><span class="sxs-lookup"><span data-stu-id="5770b-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="5770b-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span><span class="sxs-lookup"><span data-stu-id="5770b-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="5770b-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span><span class="sxs-lookup"><span data-stu-id="5770b-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="5770b-125">**Examples**</span><span class="sxs-lookup"><span data-stu-id="5770b-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="5770b-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span><span class="sxs-lookup"><span data-stu-id="5770b-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="5770b-127">Jobs to update device twin properties</span><span class="sxs-lookup"><span data-stu-id="5770b-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="5770b-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span><span class="sxs-lookup"><span data-stu-id="5770b-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="5770b-129">Querying for progress on jobs</span><span class="sxs-lookup"><span data-stu-id="5770b-129">Querying for progress on jobs</span></span>
<span data-ttu-id="5770b-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="5770b-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="5770b-131">The continuationToken is provided from the response.</span><span class="sxs-lookup"><span data-stu-id="5770b-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="5770b-132">Jobs Properties</span><span class="sxs-lookup"><span data-stu-id="5770b-132">Jobs Properties</span></span>
<span data-ttu-id="5770b-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span><span class="sxs-lookup"><span data-stu-id="5770b-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="5770b-134">Property</span><span class="sxs-lookup"><span data-stu-id="5770b-134">Property</span></span> | <span data-ttu-id="5770b-135">Description</span><span class="sxs-lookup"><span data-stu-id="5770b-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5770b-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="5770b-136">**jobId**</span></span> |<span data-ttu-id="5770b-137">Application provided ID for the job.</span><span class="sxs-lookup"><span data-stu-id="5770b-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="5770b-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="5770b-138">**startTime**</span></span> |<span data-ttu-id="5770b-139">Application provided start time (ISO-8601) for the job.</span><span class="sxs-lookup"><span data-stu-id="5770b-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="5770b-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="5770b-140">**endTime**</span></span> |<span data-ttu-id="5770b-141">IoT Hub provided date (ISO-8601) for when the job completed.</span><span class="sxs-lookup"><span data-stu-id="5770b-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="5770b-142">Valid only after the job reaches the 'completed' state.</span><span class="sxs-lookup"><span data-stu-id="5770b-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="5770b-143">**type**</span><span class="sxs-lookup"><span data-stu-id="5770b-143">**type**</span></span> |<span data-ttu-id="5770b-144">Types of jobs:</span><span class="sxs-lookup"><span data-stu-id="5770b-144">Types of jobs:</span></span> |
| <span data-ttu-id="5770b-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span><span class="sxs-lookup"><span data-stu-id="5770b-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="5770b-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span><span class="sxs-lookup"><span data-stu-id="5770b-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="5770b-147">**status**</span><span class="sxs-lookup"><span data-stu-id="5770b-147">**status**</span></span> |<span data-ttu-id="5770b-148">Current state of the job.</span><span class="sxs-lookup"><span data-stu-id="5770b-148">Current state of the job.</span></span> <span data-ttu-id="5770b-149">Possible values for status:</span><span class="sxs-lookup"><span data-stu-id="5770b-149">Possible values for status:</span></span> |
| <span data-ttu-id="5770b-150">**pending** : Scheduled and waiting to be picked up by the job service.</span><span class="sxs-lookup"><span data-stu-id="5770b-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="5770b-151">**scheduled** : Scheduled for a time in the future.</span><span class="sxs-lookup"><span data-stu-id="5770b-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="5770b-152">**running** : Currently active job.</span><span class="sxs-lookup"><span data-stu-id="5770b-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="5770b-153">**cancelled** : Job has been cancelled.</span><span class="sxs-lookup"><span data-stu-id="5770b-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="5770b-154">**failed** : Job failed.</span><span class="sxs-lookup"><span data-stu-id="5770b-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="5770b-155">**completed** : Job has completed.</span><span class="sxs-lookup"><span data-stu-id="5770b-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="5770b-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="5770b-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="5770b-157">Statistics about the job's execution.</span><span class="sxs-lookup"><span data-stu-id="5770b-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="5770b-158">**deviceJobStatistics** properties.</span><span class="sxs-lookup"><span data-stu-id="5770b-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="5770b-159">Property</span><span class="sxs-lookup"><span data-stu-id="5770b-159">Property</span></span> | <span data-ttu-id="5770b-160">Description</span><span class="sxs-lookup"><span data-stu-id="5770b-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5770b-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="5770b-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="5770b-162">Number of devices in the job.</span><span class="sxs-lookup"><span data-stu-id="5770b-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="5770b-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="5770b-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="5770b-164">Number of devices where the job failed.</span><span class="sxs-lookup"><span data-stu-id="5770b-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="5770b-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="5770b-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="5770b-166">Number of devices where the job succeeded.</span><span class="sxs-lookup"><span data-stu-id="5770b-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="5770b-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="5770b-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="5770b-168">Number of devices that are currently running the job.</span><span class="sxs-lookup"><span data-stu-id="5770b-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="5770b-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="5770b-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="5770b-170">Number of devices that are pending to run the job.</span><span class="sxs-lookup"><span data-stu-id="5770b-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="5770b-171">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="5770b-171">Additional reference material</span></span>
<span data-ttu-id="5770b-172">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="5770b-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="5770b-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="5770b-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="5770b-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span><span class="sxs-lookup"><span data-stu-id="5770b-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="5770b-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5770b-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="5770b-176">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="5770b-176">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="5770b-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="5770b-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5770b-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="5770b-178">Next steps</span></span>
<span data-ttu-id="5770b-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span><span class="sxs-lookup"><span data-stu-id="5770b-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="5770b-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="5770b-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
