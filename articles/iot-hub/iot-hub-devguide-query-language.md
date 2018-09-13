---
title: Understand the Azure IoT Hub query language | Microsoft Docs
description: Developer guide - description of the SQL-like IoT Hub query language used to retrieve information about device/module twins and jobs from your IoT hub.
author: fsautomata
manager: ''
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 02/26/2018
ms.author: elioda
ms.openlocfilehash: f6959e0fec77ff046e4db86bad30502259775a49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773285"
---
# <a name="iot-hub-query-language-for-device-and-module-twins-jobs-and-message-routing"></a><span data-ttu-id="55ba6-103">IoT Hub query language for device and module twins, jobs, and message routing</span><span class="sxs-lookup"><span data-stu-id="55ba6-103">IoT Hub query language for device and module twins, jobs, and message routing</span></span>

<span data-ttu-id="55ba6-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="55ba6-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="55ba6-105">This article presents:</span><span class="sxs-lookup"><span data-stu-id="55ba6-105">This article presents:</span></span>

* <span data-ttu-id="55ba6-106">An introduction to the major features of the IoT Hub query language, and</span><span class="sxs-lookup"><span data-stu-id="55ba6-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="55ba6-107">The detailed description of the language.</span><span class="sxs-lookup"><span data-stu-id="55ba6-107">The detailed description of the language.</span></span>

[!INCLUDE [iot-hub-basic](../../includes/iot-hub-basic-partial.md)]

## <a name="device-and-module-twin-queries"></a><span data-ttu-id="55ba6-108">Device and module twin queries</span><span class="sxs-lookup"><span data-stu-id="55ba6-108">Device and module twin queries</span></span>
<span data-ttu-id="55ba6-109">[Device twins][lnk-twins] and module twins can contain arbitrary JSON objects as both tags and properties.</span><span class="sxs-lookup"><span data-stu-id="55ba6-109">[Device twins][lnk-twins] and module twins can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="55ba6-110">IoT Hub enables you to query device twins and module twins as a single JSON document containing all twin information.</span><span class="sxs-lookup"><span data-stu-id="55ba6-110">IoT Hub enables you to query device twins and module twins as a single JSON document containing all twin information.</span></span>
<span data-ttu-id="55ba6-111">Assume, for instance, that your IoT hub device twins have the following structure (module twin would be similar just with an additional moduleId):</span><span class="sxs-lookup"><span data-stu-id="55ba6-111">Assume, for instance, that your IoT hub device twins have the following structure (module twin would be similar just with an additional moduleId):</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "status": "enabled",
    "statusUpdateTime": "0001-01-01T00:00:00",    
    "connectionState": "Disconnected",    
    "lastActivityTime": "0001-01-01T00:00:00",
    "cloudToDeviceMessageCount": 0,
    "authenticationType": "sas",    
    "x509Thumbprint": {    
        "primaryThumbprint": null,
        "secondaryThumbprint": null
    },
    "version": 2,
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

### <a name="device-twin-queries"></a><span data-ttu-id="55ba6-112">Device twin queries</span><span class="sxs-lookup"><span data-stu-id="55ba6-112">Device twin queries</span></span>

<span data-ttu-id="55ba6-113">IoT Hub exposes the device twins as a document collection called **devices**.</span><span class="sxs-lookup"><span data-stu-id="55ba6-113">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="55ba6-114">So the following query retrieves the whole set of device twins:</span><span class="sxs-lookup"><span data-stu-id="55ba6-114">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="55ba6-115">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span><span class="sxs-lookup"><span data-stu-id="55ba6-115">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="55ba6-116">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span><span class="sxs-lookup"><span data-stu-id="55ba6-116">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="55ba6-117">For instance, to receive device twins where the **location.region** tag is set to **US** use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-117">For instance, to receive device twins where the **location.region** tag is set to **US** use the following query:</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="55ba6-118">Boolean operators and arithmetic comparisons are supported as well.</span><span class="sxs-lookup"><span data-stu-id="55ba6-118">Boolean operators and arithmetic comparisons are supported as well.</span></span> <span data-ttu-id="55ba6-119">For example, to retrieve device twins located in the US and configured to send telemetry less than every minute use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-119">For example, to retrieve device twins located in the US and configured to send telemetry less than every minute use the following query:</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="55ba6-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span><span class="sxs-lookup"><span data-stu-id="55ba6-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="55ba6-121">For instance, to retrieve device twins that report WiFi or wired connectivity use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-121">For instance, to retrieve device twins that report WiFi or wired connectivity use the following query:</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="55ba6-122">It is often necessary to identify all device twins that contain a specific property.</span><span class="sxs-lookup"><span data-stu-id="55ba6-122">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="55ba6-123">IoT Hub supports the function `is_defined()` for this purpose.</span><span class="sxs-lookup"><span data-stu-id="55ba6-123">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="55ba6-124">For instance, to retrieve device twins that define the `connectivity` property use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-124">For instance, to retrieve device twins that define the `connectivity` property use the following query:</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="55ba6-125">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span><span class="sxs-lookup"><span data-stu-id="55ba6-125">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="55ba6-126">Grouping and aggregations are also supported.</span><span class="sxs-lookup"><span data-stu-id="55ba6-126">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="55ba6-127">For instance, to find the count of devices in each telemetry configuration status use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-127">For instance, to find the count of devices in each telemetry configuration status use the following query:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="55ba6-128">This grouping query would return a result similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="55ba6-128">This grouping query would return a result similar to the following example:</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="55ba6-129">In this example, three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span><span class="sxs-lookup"><span data-stu-id="55ba6-129">In this example, three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

<span data-ttu-id="55ba6-130">Projection queries allow developers to return only the properties they care about.</span><span class="sxs-lookup"><span data-stu-id="55ba6-130">Projection queries allow developers to return only the properties they care about.</span></span> <span data-ttu-id="55ba6-131">For example, to retrieve the last activity time of all disconnected devices use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-131">For example, to retrieve the last activity time of all disconnected devices use the following query:</span></span>

```sql
SELECT LastActivityTime FROM devices WHERE status = 'enabled'
```

### <a name="module-twin-queries"></a><span data-ttu-id="55ba6-132">Module twin queries</span><span class="sxs-lookup"><span data-stu-id="55ba6-132">Module twin queries</span></span>

<span data-ttu-id="55ba6-133">Querying on module twins is similar to query on device twins, but using a different collection/namespace, i.e. instead of “from devices” you can query</span><span class="sxs-lookup"><span data-stu-id="55ba6-133">Querying on module twins is similar to query on device twins, but using a different collection/namespace, i.e. instead of “from devices” you can query</span></span>

```sql
SELECT * FROM devices.modules
```

<span data-ttu-id="55ba6-134">We don't allow join between the devices and devices.modules collections.</span><span class="sxs-lookup"><span data-stu-id="55ba6-134">We don't allow join between the devices and devices.modules collections.</span></span> <span data-ttu-id="55ba6-135">If you want to query module twins across devices, you do it based on tags.</span><span class="sxs-lookup"><span data-stu-id="55ba6-135">If you want to query module twins across devices, you do it based on tags.</span></span> <span data-ttu-id="55ba6-136">This query will return all module twins across all devices with the scanning status:</span><span class="sxs-lookup"><span data-stu-id="55ba6-136">This query will return all module twins across all devices with the scanning status:</span></span>

```sql
Select * from devices.modules where properties.reported.status = 'scanning'
```

<span data-ttu-id="55ba6-137">This query will return all module twins with the scanning status, but only on the specified subset of devices.</span><span class="sxs-lookup"><span data-stu-id="55ba6-137">This query will return all module twins with the scanning status, but only on the specified subset of devices.</span></span>

```sql
Select * from devices.modules where properties.reported.status = 'scanning' and deviceId IN ('device1', 'device2')  
```

### <a name="c-example"></a><span data-ttu-id="55ba6-138">C# example</span><span class="sxs-lookup"><span data-stu-id="55ba6-138">C# example</span></span>
<span data-ttu-id="55ba6-139">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span><span class="sxs-lookup"><span data-stu-id="55ba6-139">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="55ba6-140">Here is an example of a simple query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-140">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="55ba6-141">The **query** object is instantiated with a page size (up to 100).</span><span class="sxs-lookup"><span data-stu-id="55ba6-141">The **query** object is instantiated with a page size (up to 100).</span></span> <span data-ttu-id="55ba6-142">Then multiple pages are retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span><span class="sxs-lookup"><span data-stu-id="55ba6-142">Then multiple pages are retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>

<span data-ttu-id="55ba6-143">The query object exposes multiple **Next** values, depending on the deserialization option required by the query.</span><span class="sxs-lookup"><span data-stu-id="55ba6-143">The query object exposes multiple **Next** values, depending on the deserialization option required by the query.</span></span> <span data-ttu-id="55ba6-144">For example, device twin or job objects, or plain JSON when using projections.</span><span class="sxs-lookup"><span data-stu-id="55ba6-144">For example, device twin or job objects, or plain JSON when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="55ba6-145">Node.js example</span><span class="sxs-lookup"><span data-stu-id="55ba6-145">Node.js example</span></span>
<span data-ttu-id="55ba6-146">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span><span class="sxs-lookup"><span data-stu-id="55ba6-146">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="55ba6-147">Here is an example of a simple query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-147">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="55ba6-148">The **query** object is instantiated with a page size (up to 100).</span><span class="sxs-lookup"><span data-stu-id="55ba6-148">The **query** object is instantiated with a page size (up to 100).</span></span> <span data-ttu-id="55ba6-149">Then multiple pages are retrieved by calling the **nextAsTwin** method multiple times.</span><span class="sxs-lookup"><span data-stu-id="55ba6-149">Then multiple pages are retrieved by calling the **nextAsTwin** method multiple times.</span></span>

<span data-ttu-id="55ba6-150">The query object exposes multiple **Next** values, depending on the deserialization option required by the query.</span><span class="sxs-lookup"><span data-stu-id="55ba6-150">The query object exposes multiple **Next** values, depending on the deserialization option required by the query.</span></span> <span data-ttu-id="55ba6-151">For example, device twin or job objects, or plain JSON when using projections.</span><span class="sxs-lookup"><span data-stu-id="55ba6-151">For example, device twin or job objects, or plain JSON when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="55ba6-152">Limitations</span><span class="sxs-lookup"><span data-stu-id="55ba6-152">Limitations</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55ba6-153">Query results can have a few minutes of delay with respect to the latest values in device twins.</span><span class="sxs-lookup"><span data-stu-id="55ba6-153">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="55ba6-154">If querying individual device twins by ID, use the retrieve device twin API.</span><span class="sxs-lookup"><span data-stu-id="55ba6-154">If querying individual device twins by ID, use the retrieve device twin API.</span></span> <span data-ttu-id="55ba6-155">This API always contains the latest values and has higher throttling limits.</span><span class="sxs-lookup"><span data-stu-id="55ba6-155">This API always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="55ba6-156">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span><span class="sxs-lookup"><span data-stu-id="55ba6-156">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="55ba6-157">Get started with jobs queries</span><span class="sxs-lookup"><span data-stu-id="55ba6-157">Get started with jobs queries</span></span>

<span data-ttu-id="55ba6-158">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span><span class="sxs-lookup"><span data-stu-id="55ba6-158">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="55ba6-159">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span><span class="sxs-lookup"><span data-stu-id="55ba6-159">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="55ba6-160">Logically,</span><span class="sxs-lookup"><span data-stu-id="55ba6-160">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="55ba6-161">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span><span class="sxs-lookup"><span data-stu-id="55ba6-161">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55ba6-162">Currently, the jobs property is never returned when querying device twins.</span><span class="sxs-lookup"><span data-stu-id="55ba6-162">Currently, the jobs property is never returned when querying device twins.</span></span> <span data-ttu-id="55ba6-163">That is, queries that contain 'FROM devices'.</span><span class="sxs-lookup"><span data-stu-id="55ba6-163">That is, queries that contain 'FROM devices'.</span></span> <span data-ttu-id="55ba6-164">The jobs property can only be accessed directly with queries using `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="55ba6-164">The jobs property can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="55ba6-165">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-165">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="55ba6-166">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span><span class="sxs-lookup"><span data-stu-id="55ba6-166">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="55ba6-167">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span><span class="sxs-lookup"><span data-stu-id="55ba6-167">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="55ba6-168">For instance, to retrieve all completed device twin update jobs that were created after September 2016 for a specific device, use the following query:</span><span class="sxs-lookup"><span data-stu-id="55ba6-168">For instance, to retrieve all completed device twin update jobs that were created after September 2016 for a specific device, use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="55ba6-169">You can also retrieve the per-device outcomes of a single job.</span><span class="sxs-lookup"><span data-stu-id="55ba6-169">You can also retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="55ba6-170">Limitations</span><span class="sxs-lookup"><span data-stu-id="55ba6-170">Limitations</span></span>
<span data-ttu-id="55ba6-171">Currently, queries on **devices.jobs** do not support:</span><span class="sxs-lookup"><span data-stu-id="55ba6-171">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="55ba6-172">Projections, therefore only `SELECT *` is possible.</span><span class="sxs-lookup"><span data-stu-id="55ba6-172">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="55ba6-173">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span><span class="sxs-lookup"><span data-stu-id="55ba6-173">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="55ba6-174">Performing aggregations, such as count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="55ba6-174">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="55ba6-175">Device-to-cloud message routes query expressions</span><span class="sxs-lookup"><span data-stu-id="55ba6-175">Device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="55ba6-176">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints.</span><span class="sxs-lookup"><span data-stu-id="55ba6-176">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints.</span></span> <span data-ttu-id="55ba6-177">Dispatching is based on expressions evaluated against individual messages.</span><span class="sxs-lookup"><span data-stu-id="55ba6-177">Dispatching is based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="55ba6-178">The route [condition][lnk-query-expressions] uses the IoT Hub query language syntax as conditions in twin and job queries, but only a subset of the functions are available.</span><span class="sxs-lookup"><span data-stu-id="55ba6-178">The route [condition][lnk-query-expressions] uses the IoT Hub query language syntax as conditions in twin and job queries, but only a subset of the functions are available.</span></span> <span data-ttu-id="55ba6-179">Route conditions are evaluated on the message headers and body.</span><span class="sxs-lookup"><span data-stu-id="55ba6-179">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="55ba6-180">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span><span class="sxs-lookup"><span data-stu-id="55ba6-180">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="55ba6-181">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route.</span><span class="sxs-lookup"><span data-stu-id="55ba6-181">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route.</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="55ba6-182">Routing on message headers</span><span class="sxs-lookup"><span data-stu-id="55ba6-182">Routing on message headers</span></span>

<span data-ttu-id="55ba6-183">IoT Hub assumes the following JSON representation of message headers for message routing:</span><span class="sxs-lookup"><span data-stu-id="55ba6-183">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

```json
{
  "message": {
    "systemProperties": {
      "contentType": "application/json",
      "contentEncoding": "utf-8",
      "iothub-message-source": "deviceMessages",
      "iothub-enqueuedtime": "2017-05-08T18:55:31.8514657Z"
    },
    "appProperties": {
      "processingPath": "<optional>",
      "verbose": "<optional>",
      "severity": "<optional>",
      "testDevice": "<optional>"
    },
    "body": "{\"Weather\":{\"Temperature\":50}}"
  }
}
```

<span data-ttu-id="55ba6-184">Message system properties are prefixed with the `'$'` symbol.</span><span class="sxs-lookup"><span data-stu-id="55ba6-184">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="55ba6-185">User properties are always accessed with their name.</span><span class="sxs-lookup"><span data-stu-id="55ba6-185">User properties are always accessed with their name.</span></span> <span data-ttu-id="55ba6-186">If a user property name coincides with a system property (such as `$contentType`), the user property is retrieved with the `$contentType` expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-186">If a user property name coincides with a system property (such as `$contentType`), the user property is retrieved with the `$contentType` expression.</span></span>
<span data-ttu-id="55ba6-187">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$contentType}` to access the system property `contentType`.</span><span class="sxs-lookup"><span data-stu-id="55ba6-187">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$contentType}` to access the system property `contentType`.</span></span> <span data-ttu-id="55ba6-188">Bracketed property names always retrieve the corresponding system property.</span><span class="sxs-lookup"><span data-stu-id="55ba6-188">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="55ba6-189">Remember that property names are case insensitive.</span><span class="sxs-lookup"><span data-stu-id="55ba6-189">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="55ba6-190">All message properties are strings.</span><span class="sxs-lookup"><span data-stu-id="55ba6-190">All message properties are strings.</span></span> <span data-ttu-id="55ba6-191">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span><span class="sxs-lookup"><span data-stu-id="55ba6-191">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="55ba6-192">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span><span class="sxs-lookup"><span data-stu-id="55ba6-192">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="55ba6-193">You can write the following expression to route the telemetry:</span><span class="sxs-lookup"><span data-stu-id="55ba6-193">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="55ba6-194">And the following expression to route the alert messages:</span><span class="sxs-lookup"><span data-stu-id="55ba6-194">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="55ba6-195">Boolean expressions and functions are also supported.</span><span class="sxs-lookup"><span data-stu-id="55ba6-195">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="55ba6-196">This feature enables you to distinguish between severity level, for example:</span><span class="sxs-lookup"><span data-stu-id="55ba6-196">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="55ba6-197">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span><span class="sxs-lookup"><span data-stu-id="55ba6-197">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="55ba6-198">Routing on message bodies</span><span class="sxs-lookup"><span data-stu-id="55ba6-198">Routing on message bodies</span></span>

<span data-ttu-id="55ba6-199">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in UTF-8, UTF-16, or UTF-32.</span><span class="sxs-lookup"><span data-stu-id="55ba6-199">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="55ba6-200">Set the content type of the message to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="55ba6-200">Set the content type of the message to `application/json`.</span></span> <span data-ttu-id="55ba6-201">Set the content encoding to one of the supported UTF encodings in the message headers.</span><span class="sxs-lookup"><span data-stu-id="55ba6-201">Set the content encoding to one of the supported UTF encodings in the message headers.</span></span> <span data-ttu-id="55ba6-202">If either of the headers is not specified, IoT Hub does not attempt to evaluate any query expression involving the body against the message.</span><span class="sxs-lookup"><span data-stu-id="55ba6-202">If either of the headers is not specified, IoT Hub does not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="55ba6-203">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you can still use message routing to route the message based on the message headers.</span><span class="sxs-lookup"><span data-stu-id="55ba6-203">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you can still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="55ba6-204">The following example shows how to create a message with a properly formed and encoded JSON body:</span><span class="sxs-lookup"><span data-stu-id="55ba6-204">The following example shows how to create a message with a properly formed and encoded JSON body:</span></span>

```csharp
string messageBody = @"{ 
                            ""Weather"":{ 
                                ""Temperature"":50, 
                                ""Time"":""2017-03-09T00:00:00.000Z"", 
                                ""PrevTemperatures"":[ 
                                    20, 
                                    30, 
                                    40 
                                ], 
                                ""IsEnabled"":true, 
                                ""Location"":{ 
                                    ""Street"":""One Microsoft Way"", 
                                    ""City"":""Redmond"", 
                                    ""State"":""WA"" 
                                }, 
                                ""HistoricalData"":[ 
                                    { 
                                    ""Month"":""Feb"", 
                                    ""Temperature"":40 
                                    }, 
                                    { 
                                    ""Month"":""Jan"", 
                                    ""Temperature"":30 
                                    } 
                                ] 
                            } 
                        }"; 
 
// Encode message body using UTF-8 
byte[] messageBytes = Encoding.UTF8.GetBytes(messageBody); 
 
using (var message = new Message(messageBytes)) 
{ 
    // Set message body type and content encoding. 
    message.ContentEncoding = "utf-8"; 
    message.ContentType = "application/json"; 
 
    // Add other custom application properties.  
    message.Properties["Status"] = "Active";    
 
    await deviceClient.SendEventAsync(message); 
}
```

<span data-ttu-id="55ba6-205">You can use `$body` in the query expression to route the message.</span><span class="sxs-lookup"><span data-stu-id="55ba6-205">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="55ba6-206">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-206">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="55ba6-207">Your query expression can also combine a body reference with a message header reference.</span><span class="sxs-lookup"><span data-stu-id="55ba6-207">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="55ba6-208">For example, the following are all valid query expressions:</span><span class="sxs-lookup"><span data-stu-id="55ba6-208">For example, the following are all valid query expressions:</span></span>

```sql
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="55ba6-209">Basics of an IoT Hub query</span><span class="sxs-lookup"><span data-stu-id="55ba6-209">Basics of an IoT Hub query</span></span>
<span data-ttu-id="55ba6-210">Every IoT Hub query consists of SELECT and FROM clauses, with optional WHERE and GROUP BY clauses.</span><span class="sxs-lookup"><span data-stu-id="55ba6-210">Every IoT Hub query consists of SELECT and FROM clauses, with optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="55ba6-211">Every query is run on a collection of JSON documents, for example device twins.</span><span class="sxs-lookup"><span data-stu-id="55ba6-211">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="55ba6-212">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="55ba6-212">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="55ba6-213">Then, the filter in the WHERE clause is applied.</span><span class="sxs-lookup"><span data-stu-id="55ba6-213">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="55ba6-214">With aggregations, the results of this step are grouped as specified in the GROUP BY clause.</span><span class="sxs-lookup"><span data-stu-id="55ba6-214">With aggregations, the results of this step are grouped as specified in the GROUP BY clause.</span></span> <span data-ttu-id="55ba6-215">For each group, a row is generated as specified in the SELECT clause.</span><span class="sxs-lookup"><span data-stu-id="55ba6-215">For each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="55ba6-216">FROM clause</span><span class="sxs-lookup"><span data-stu-id="55ba6-216">FROM clause</span></span>
<span data-ttu-id="55ba6-217">The **FROM <from_specification>** clause can assume only two values: **FROM devices** to query device twins, or **FROM devices.jobs** to query job per-device details.</span><span class="sxs-lookup"><span data-stu-id="55ba6-217">The **FROM <from_specification>** clause can assume only two values: **FROM devices** to query device twins, or **FROM devices.jobs** to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="55ba6-218">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="55ba6-218">WHERE clause</span></span>
<span data-ttu-id="55ba6-219">The **WHERE <filter_condition>** clause is optional.</span><span class="sxs-lookup"><span data-stu-id="55ba6-219">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="55ba6-220">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span><span class="sxs-lookup"><span data-stu-id="55ba6-220">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="55ba6-221">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span><span class="sxs-lookup"><span data-stu-id="55ba6-221">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="55ba6-222">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="55ba6-222">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="55ba6-223">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="55ba6-223">SELECT clause</span></span>
<span data-ttu-id="55ba6-224">The **SELECT <select_list>** is mandatory and specifies what values are retrieved from the query.</span><span class="sxs-lookup"><span data-stu-id="55ba6-224">The **SELECT <select_list>** is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="55ba6-225">It specifies the JSON values to be used to generate new JSON objects.</span><span class="sxs-lookup"><span data-stu-id="55ba6-225">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="55ba6-226">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object.</span><span class="sxs-lookup"><span data-stu-id="55ba6-226">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object.</span></span> <span data-ttu-id="55ba6-227">This object is constructed with the values specified in the SELECT clause.</span><span class="sxs-lookup"><span data-stu-id="55ba6-227">This object is constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="55ba6-228">Following is the grammar of the SELECT clause:</span><span class="sxs-lookup"><span data-stu-id="55ba6-228">Following is the grammar of the SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="55ba6-229">**Attribute_name** refers to any property of the JSON document in the FROM collection.</span><span class="sxs-lookup"><span data-stu-id="55ba6-229">**Attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="55ba6-230">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span><span class="sxs-lookup"><span data-stu-id="55ba6-230">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="55ba6-231">Currently, selection clauses different than **SELECT**\* are only supported in aggregate queries on device twins.</span><span class="sxs-lookup"><span data-stu-id="55ba6-231">Currently, selection clauses different than **SELECT**\* are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="55ba6-232">GROUP BY clause</span><span class="sxs-lookup"><span data-stu-id="55ba6-232">GROUP BY clause</span></span>
<span data-ttu-id="55ba6-233">The **GROUP BY <group_specification>** clause is an optional step that executes after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span><span class="sxs-lookup"><span data-stu-id="55ba6-233">The **GROUP BY <group_specification>** clause is an optional step that executes after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="55ba6-234">It groups documents based on the value of an attribute.</span><span class="sxs-lookup"><span data-stu-id="55ba6-234">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="55ba6-235">These groups are used to generate aggregated values as specified in the SELECT clause.</span><span class="sxs-lookup"><span data-stu-id="55ba6-235">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="55ba6-236">An example of a query using GROUP BY is:</span><span class="sxs-lookup"><span data-stu-id="55ba6-236">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="55ba6-237">The formal syntax for GROUP BY is:</span><span class="sxs-lookup"><span data-stu-id="55ba6-237">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="55ba6-238">**Attribute_name** refers to any property of the JSON document in the FROM collection.</span><span class="sxs-lookup"><span data-stu-id="55ba6-238">**Attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="55ba6-239">Currently, the GROUP BY clause is only supported when querying device twins.</span><span class="sxs-lookup"><span data-stu-id="55ba6-239">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="55ba6-240">Expressions and conditions</span><span class="sxs-lookup"><span data-stu-id="55ba6-240">Expressions and conditions</span></span>
<span data-ttu-id="55ba6-241">At a high level, an *expression*:</span><span class="sxs-lookup"><span data-stu-id="55ba6-241">At a high level, an *expression*:</span></span>

* <span data-ttu-id="55ba6-242">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object).</span><span class="sxs-lookup"><span data-stu-id="55ba6-242">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object).</span></span>
* <span data-ttu-id="55ba6-243">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span><span class="sxs-lookup"><span data-stu-id="55ba6-243">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="55ba6-244">*Conditions* are expressions that evaluate to a Boolean.</span><span class="sxs-lookup"><span data-stu-id="55ba6-244">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="55ba6-245">Any constant different than Boolean **true** is considered as **false**.</span><span class="sxs-lookup"><span data-stu-id="55ba6-245">Any constant different than Boolean **true** is considered as **false**.</span></span> <span data-ttu-id="55ba6-246">This rule includes **null**, **undefined**, any object or array instance, any string, and the Boolean **false**.</span><span class="sxs-lookup"><span data-stu-id="55ba6-246">This rule includes **null**, **undefined**, any object or array instance, any string, and the Boolean **false**.</span></span>

<span data-ttu-id="55ba6-247">The syntax for expressions is:</span><span class="sxs-lookup"><span data-stu-id="55ba6-247">The syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="55ba6-248">To understand what each symbol in the expressions syntax stands for, refer to the following table:</span><span class="sxs-lookup"><span data-stu-id="55ba6-248">To understand what each symbol in the expressions syntax stands for, refer to the following table:</span></span>

| <span data-ttu-id="55ba6-249">Symbol</span><span class="sxs-lookup"><span data-stu-id="55ba6-249">Symbol</span></span> | <span data-ttu-id="55ba6-250">Definition</span><span class="sxs-lookup"><span data-stu-id="55ba6-250">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="55ba6-251">attribute_name</span><span class="sxs-lookup"><span data-stu-id="55ba6-251">attribute_name</span></span> | <span data-ttu-id="55ba6-252">Any property of the JSON document in the **FROM** collection.</span><span class="sxs-lookup"><span data-stu-id="55ba6-252">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="55ba6-253">binary_operator</span><span class="sxs-lookup"><span data-stu-id="55ba6-253">binary_operator</span></span> | <span data-ttu-id="55ba6-254">Any binary operator listed in the [Operators](#operators) section.</span><span class="sxs-lookup"><span data-stu-id="55ba6-254">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="55ba6-255">function_name</span><span class="sxs-lookup"><span data-stu-id="55ba6-255">function_name</span></span>| <span data-ttu-id="55ba6-256">Any function listed in the [Functions](#functions) section.</span><span class="sxs-lookup"><span data-stu-id="55ba6-256">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="55ba6-257">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="55ba6-257">decimal_literal</span></span> |<span data-ttu-id="55ba6-258">A float expressed in decimal notation.</span><span class="sxs-lookup"><span data-stu-id="55ba6-258">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="55ba6-259">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="55ba6-259">hexadecimal_literal</span></span> |<span data-ttu-id="55ba6-260">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="55ba6-260">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="55ba6-261">string_literal</span><span class="sxs-lookup"><span data-stu-id="55ba6-261">string_literal</span></span> |<span data-ttu-id="55ba6-262">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span><span class="sxs-lookup"><span data-stu-id="55ba6-262">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="55ba6-263">String literals are enclosed in single quotes or double quotes.</span><span class="sxs-lookup"><span data-stu-id="55ba6-263">String literals are enclosed in single quotes or double quotes.</span></span> <span data-ttu-id="55ba6-264">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="55ba6-264">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="55ba6-265">Operators</span><span class="sxs-lookup"><span data-stu-id="55ba6-265">Operators</span></span>
<span data-ttu-id="55ba6-266">The following operators are supported:</span><span class="sxs-lookup"><span data-stu-id="55ba6-266">The following operators are supported:</span></span>

| <span data-ttu-id="55ba6-267">Family</span><span class="sxs-lookup"><span data-stu-id="55ba6-267">Family</span></span> | <span data-ttu-id="55ba6-268">Operators</span><span class="sxs-lookup"><span data-stu-id="55ba6-268">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="55ba6-269">Arithmetic</span><span class="sxs-lookup"><span data-stu-id="55ba6-269">Arithmetic</span></span> |<span data-ttu-id="55ba6-270">+, -, \*, /, %</span><span class="sxs-lookup"><span data-stu-id="55ba6-270">+, -, \*, /, %</span></span> |
| <span data-ttu-id="55ba6-271">Logical</span><span class="sxs-lookup"><span data-stu-id="55ba6-271">Logical</span></span> |<span data-ttu-id="55ba6-272">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="55ba6-272">AND, OR, NOT</span></span> |
| <span data-ttu-id="55ba6-273">Comparison</span><span class="sxs-lookup"><span data-stu-id="55ba6-273">Comparison</span></span> |<span data-ttu-id="55ba6-274">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="55ba6-274">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="55ba6-275">Functions</span><span class="sxs-lookup"><span data-stu-id="55ba6-275">Functions</span></span>
<span data-ttu-id="55ba6-276">When querying twins and jobs the only supported function is:</span><span class="sxs-lookup"><span data-stu-id="55ba6-276">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="55ba6-277">Function</span><span class="sxs-lookup"><span data-stu-id="55ba6-277">Function</span></span> | <span data-ttu-id="55ba6-278">Description</span><span class="sxs-lookup"><span data-stu-id="55ba6-278">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="55ba6-279">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="55ba6-279">IS_DEFINED(property)</span></span> | <span data-ttu-id="55ba6-280">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span><span class="sxs-lookup"><span data-stu-id="55ba6-280">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="55ba6-281">In routes conditions, the following math functions are supported:</span><span class="sxs-lookup"><span data-stu-id="55ba6-281">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="55ba6-282">Function</span><span class="sxs-lookup"><span data-stu-id="55ba6-282">Function</span></span> | <span data-ttu-id="55ba6-283">Description</span><span class="sxs-lookup"><span data-stu-id="55ba6-283">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="55ba6-284">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-284">ABS(x)</span></span> | <span data-ttu-id="55ba6-285">Returns the absolute (positive) value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-285">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="55ba6-286">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-286">EXP(x)</span></span> | <span data-ttu-id="55ba6-287">Returns the exponential value of the specified numeric expression (e^x).</span><span class="sxs-lookup"><span data-stu-id="55ba6-287">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="55ba6-288">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="55ba6-288">POWER(x,y)</span></span> | <span data-ttu-id="55ba6-289">Returns the value of the specified expression to the specified power (x^y).</span><span class="sxs-lookup"><span data-stu-id="55ba6-289">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="55ba6-290">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-290">SQUARE(x)</span></span> | <span data-ttu-id="55ba6-291">Returns the square of the specified numeric value.</span><span class="sxs-lookup"><span data-stu-id="55ba6-291">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="55ba6-292">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-292">CEILING(x)</span></span> | <span data-ttu-id="55ba6-293">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-293">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="55ba6-294">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-294">FLOOR(x)</span></span> | <span data-ttu-id="55ba6-295">Returns the largest integer less than or equal to the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-295">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="55ba6-296">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-296">SIGN(x)</span></span> | <span data-ttu-id="55ba6-297">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-297">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="55ba6-298">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-298">SQRT(x)</span></span> | <span data-ttu-id="55ba6-299">Returns the square root of the specified numeric value.</span><span class="sxs-lookup"><span data-stu-id="55ba6-299">Returns the square root of the specified numeric value.</span></span> |

<span data-ttu-id="55ba6-300">In routes conditions, the following type checking and casting functions are supported:</span><span class="sxs-lookup"><span data-stu-id="55ba6-300">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="55ba6-301">Function</span><span class="sxs-lookup"><span data-stu-id="55ba6-301">Function</span></span> | <span data-ttu-id="55ba6-302">Description</span><span class="sxs-lookup"><span data-stu-id="55ba6-302">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="55ba6-303">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="55ba6-303">AS_NUMBER</span></span> | <span data-ttu-id="55ba6-304">Converts the input string to a number.</span><span class="sxs-lookup"><span data-stu-id="55ba6-304">Converts the input string to a number.</span></span> <span data-ttu-id="55ba6-305">`noop` if input is a number; `Undefined` if string does not represent a number.</span><span class="sxs-lookup"><span data-stu-id="55ba6-305">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="55ba6-306">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="55ba6-306">IS_ARRAY</span></span> | <span data-ttu-id="55ba6-307">Returns a Boolean value indicating if the type of the specified expression is an array.</span><span class="sxs-lookup"><span data-stu-id="55ba6-307">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="55ba6-308">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="55ba6-308">IS_BOOL</span></span> | <span data-ttu-id="55ba6-309">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="55ba6-309">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="55ba6-310">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="55ba6-310">IS_DEFINED</span></span> | <span data-ttu-id="55ba6-311">Returns a Boolean indicating if the property has been assigned a value.</span><span class="sxs-lookup"><span data-stu-id="55ba6-311">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="55ba6-312">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="55ba6-312">IS_NULL</span></span> | <span data-ttu-id="55ba6-313">Returns a Boolean value indicating if the type of the specified expression is null.</span><span class="sxs-lookup"><span data-stu-id="55ba6-313">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="55ba6-314">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="55ba6-314">IS_NUMBER</span></span> | <span data-ttu-id="55ba6-315">Returns a Boolean value indicating if the type of the specified expression is a number.</span><span class="sxs-lookup"><span data-stu-id="55ba6-315">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="55ba6-316">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="55ba6-316">IS_OBJECT</span></span> | <span data-ttu-id="55ba6-317">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="55ba6-317">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="55ba6-318">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="55ba6-318">IS_PRIMITIVE</span></span> | <span data-ttu-id="55ba6-319">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric, or `null`).</span><span class="sxs-lookup"><span data-stu-id="55ba6-319">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric, or `null`).</span></span> |
| <span data-ttu-id="55ba6-320">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="55ba6-320">IS_STRING</span></span> | <span data-ttu-id="55ba6-321">Returns a Boolean value indicating if the type of the specified expression is a string.</span><span class="sxs-lookup"><span data-stu-id="55ba6-321">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="55ba6-322">In routes conditions, the following string functions are supported:</span><span class="sxs-lookup"><span data-stu-id="55ba6-322">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="55ba6-323">Function</span><span class="sxs-lookup"><span data-stu-id="55ba6-323">Function</span></span> | <span data-ttu-id="55ba6-324">Description</span><span class="sxs-lookup"><span data-stu-id="55ba6-324">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="55ba6-325">CONCAT(x, y, …)</span><span class="sxs-lookup"><span data-stu-id="55ba6-325">CONCAT(x, y, …)</span></span> | <span data-ttu-id="55ba6-326">Returns a string that is the result of concatenating two or more string values.</span><span class="sxs-lookup"><span data-stu-id="55ba6-326">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="55ba6-327">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-327">LENGTH(x)</span></span> | <span data-ttu-id="55ba6-328">Returns the number of characters of the specified string expression.</span><span class="sxs-lookup"><span data-stu-id="55ba6-328">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="55ba6-329">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-329">LOWER(x)</span></span> | <span data-ttu-id="55ba6-330">Returns a string expression after converting uppercase character data to lowercase.</span><span class="sxs-lookup"><span data-stu-id="55ba6-330">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="55ba6-331">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="55ba6-331">UPPER(x)</span></span> | <span data-ttu-id="55ba6-332">Returns a string expression after converting lowercase character data to uppercase.</span><span class="sxs-lookup"><span data-stu-id="55ba6-332">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="55ba6-333">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="55ba6-333">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="55ba6-334">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span><span class="sxs-lookup"><span data-stu-id="55ba6-334">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="55ba6-335">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="55ba6-335">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="55ba6-336">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="55ba6-336">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="55ba6-337">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="55ba6-337">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="55ba6-338">Returns a Boolean indicating whether the first string expression starts with the second.</span><span class="sxs-lookup"><span data-stu-id="55ba6-338">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="55ba6-339">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="55ba6-339">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="55ba6-340">Returns a Boolean indicating whether the first string expression ends with the second.</span><span class="sxs-lookup"><span data-stu-id="55ba6-340">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="55ba6-341">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="55ba6-341">CONTAINS(x,y)</span></span> | <span data-ttu-id="55ba6-342">Returns a Boolean indicating whether the first string expression contains the second.</span><span class="sxs-lookup"><span data-stu-id="55ba6-342">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55ba6-343">Next steps</span><span class="sxs-lookup"><span data-stu-id="55ba6-343">Next steps</span></span>
<span data-ttu-id="55ba6-344">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="55ba6-344">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
