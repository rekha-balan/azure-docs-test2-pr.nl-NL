---
title: Understand the Azure IoT Hub query language | Microsoft Docs
description: Developer guide - description of the SQL-like IoT Hub query language used to retrieve information about device twins and jobs from your IoT hub.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: ''
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: elioda
ms.openlocfilehash: 1eacd13562adcff96fdd0dd3fd91c78ef6a26dbf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563194"
---
# <a name="reference---iot-hub-query-language-for-device-twins-and-jobs"></a><span data-ttu-id="3b838-103">Reference - IoT Hub query language for device twins and jobs</span><span class="sxs-lookup"><span data-stu-id="3b838-103">Reference - IoT Hub query language for device twins and jobs</span></span>
## <a name="overview"></a><span data-ttu-id="3b838-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3b838-104">Overview</span></span>
<span data-ttu-id="3b838-105">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="3b838-105">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs].</span></span> <span data-ttu-id="3b838-106">This article presents:</span><span class="sxs-lookup"><span data-stu-id="3b838-106">This article presents:</span></span>

* <span data-ttu-id="3b838-107">An introduction to the major features of the IoT Hub query language, and</span><span class="sxs-lookup"><span data-stu-id="3b838-107">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="3b838-108">The detailed description of the language.</span><span class="sxs-lookup"><span data-stu-id="3b838-108">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="3b838-109">Get started with device twin queries</span><span class="sxs-lookup"><span data-stu-id="3b838-109">Get started with device twin queries</span></span>
<span data-ttu-id="3b838-110">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span><span class="sxs-lookup"><span data-stu-id="3b838-110">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="3b838-111">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span><span class="sxs-lookup"><span data-stu-id="3b838-111">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="3b838-112">Assume, for instance, that your IoT hub device twins have the following structure:</span><span class="sxs-lookup"><span data-stu-id="3b838-112">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

        {                                                                      
            "deviceId": "myDeviceId",                                            
            "etag": "AAAAAAAAAAc=",                                              
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

<span data-ttu-id="3b838-113">IoT Hub exposes the device twins as a document collection called **devices**.</span><span class="sxs-lookup"><span data-stu-id="3b838-113">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="3b838-114">So the following query retrieves the whole set of device twins:</span><span class="sxs-lookup"><span data-stu-id="3b838-114">So the following query retrieves the whole set of device twins:</span></span>

        SELECT * FROM devices

> [!NOTE]
> <span data-ttu-id="3b838-115">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span><span class="sxs-lookup"><span data-stu-id="3b838-115">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>
>
>

<span data-ttu-id="3b838-116">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span><span class="sxs-lookup"><span data-stu-id="3b838-116">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="3b838-117">For instance,</span><span class="sxs-lookup"><span data-stu-id="3b838-117">For instance,</span></span>

        SELECT * FROM devices
        WHERE tags.location.region = 'US'

<span data-ttu-id="3b838-118">retrieves the device twins with the **location.region** tag set to **US**.</span><span class="sxs-lookup"><span data-stu-id="3b838-118">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="3b838-119">Boolean operators and arithmetic comparisons are supported as well, for example</span><span class="sxs-lookup"><span data-stu-id="3b838-119">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

        SELECT * FROM devices
        WHERE tags.location.region = 'US'
            AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60

<span data-ttu-id="3b838-120">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span><span class="sxs-lookup"><span data-stu-id="3b838-120">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="3b838-121">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span><span class="sxs-lookup"><span data-stu-id="3b838-121">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="3b838-122">For instance,</span><span class="sxs-lookup"><span data-stu-id="3b838-122">For instance,</span></span>

        SELECT * FROM devices
        WHERE property.reported.connectivity IN ['wired', 'wifi']

<span data-ttu-id="3b838-123">retrieves all device twins that reported WiFi or wired connectivity.</span><span class="sxs-lookup"><span data-stu-id="3b838-123">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="3b838-124">It is often necessary to identify all device twins that contain a specific property.</span><span class="sxs-lookup"><span data-stu-id="3b838-124">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="3b838-125">IoT Hub supports the function `is_defined()` for this purpose.</span><span class="sxs-lookup"><span data-stu-id="3b838-125">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="3b838-126">For instance,</span><span class="sxs-lookup"><span data-stu-id="3b838-126">For instance,</span></span>

        SELECT * FROM devices
        WHERE is_defined(property.reported.connectivity)

<span data-ttu-id="3b838-127">retrieved all device twins that define the `connectivity` reported property.</span><span class="sxs-lookup"><span data-stu-id="3b838-127">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="3b838-128">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span><span class="sxs-lookup"><span data-stu-id="3b838-128">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="3b838-129">Grouping and aggregations are also supported.</span><span class="sxs-lookup"><span data-stu-id="3b838-129">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="3b838-130">For instance,</span><span class="sxs-lookup"><span data-stu-id="3b838-130">For instance,</span></span>

        SELECT properties.reported.telemetryConfig.status AS status,
            COUNT() AS numberOfDevices
        FROM devices
        GROUP BY properties.reported.telemetryConfig.status

<span data-ttu-id="3b838-131">returns the count of the devices in each telemetry configuration status.</span><span class="sxs-lookup"><span data-stu-id="3b838-131">returns the count of the devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="3b838-132">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span><span class="sxs-lookup"><span data-stu-id="3b838-132">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="3b838-133">C# example</span><span class="sxs-lookup"><span data-stu-id="3b838-133">C# example</span></span>
<span data-ttu-id="3b838-134">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span><span class="sxs-lookup"><span data-stu-id="3b838-134">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="3b838-135">Here is an example of a simple query:</span><span class="sxs-lookup"><span data-stu-id="3b838-135">Here is an example of a simple query:</span></span>

        var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
        while (query.HasMoreResults)
        {
            var page = await query.GetNextAsTwinAsync();
            foreach (var twin in page)
            {
                // do work on twin object
            }
        }

<span data-ttu-id="3b838-136">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span><span class="sxs-lookup"><span data-stu-id="3b838-136">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="3b838-137">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span><span class="sxs-lookup"><span data-stu-id="3b838-137">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="3b838-138">Node.js example</span><span class="sxs-lookup"><span data-stu-id="3b838-138">Node.js example</span></span>
<span data-ttu-id="3b838-139">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span><span class="sxs-lookup"><span data-stu-id="3b838-139">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="3b838-140">Here is an example of a simple query:</span><span class="sxs-lookup"><span data-stu-id="3b838-140">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="3b838-141">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span><span class="sxs-lookup"><span data-stu-id="3b838-141">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="3b838-142">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span><span class="sxs-lookup"><span data-stu-id="3b838-142">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="3b838-143">Limitations</span><span class="sxs-lookup"><span data-stu-id="3b838-143">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3b838-144">Query results can have a few minutes of delay with respect to the latest values in device twins.</span><span class="sxs-lookup"><span data-stu-id="3b838-144">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="3b838-145">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span><span class="sxs-lookup"><span data-stu-id="3b838-145">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>
>
>

<span data-ttu-id="3b838-146">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span><span class="sxs-lookup"><span data-stu-id="3b838-146">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="3b838-147">Get started with jobs queries</span><span class="sxs-lookup"><span data-stu-id="3b838-147">Get started with jobs queries</span></span>
<span data-ttu-id="3b838-148">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span><span class="sxs-lookup"><span data-stu-id="3b838-148">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="3b838-149">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span><span class="sxs-lookup"><span data-stu-id="3b838-149">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="3b838-150">Logically,</span><span class="sxs-lookup"><span data-stu-id="3b838-150">Logically,</span></span>

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

<span data-ttu-id="3b838-151">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span><span class="sxs-lookup"><span data-stu-id="3b838-151">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b838-152">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span><span class="sxs-lookup"><span data-stu-id="3b838-152">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="3b838-153">It can only be accessed directly with queries using `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="3b838-153">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="3b838-154">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span><span class="sxs-lookup"><span data-stu-id="3b838-154">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

        SELECT * FROM devices.jobs
        WHERE devices.jobs.deviceId = 'myDeviceId'

<span data-ttu-id="3b838-155">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span><span class="sxs-lookup"><span data-stu-id="3b838-155">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="3b838-156">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span><span class="sxs-lookup"><span data-stu-id="3b838-156">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="3b838-157">For instance, the following query:</span><span class="sxs-lookup"><span data-stu-id="3b838-157">For instance, the following query:</span></span>

        SELECT * FROM devices.jobs
        WHERE devices.jobs.deviceId = 'myDeviceId'
            AND devices.jobs.jobType = 'scheduleTwinUpdate'
            AND devices.jobs.status = 'completed'
            AND devices.jobs.createdTimeUtc > '2016-09-01'

<span data-ttu-id="3b838-158">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span><span class="sxs-lookup"><span data-stu-id="3b838-158">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="3b838-159">It is also possible to retrieve the per-device outcomes of a single job.</span><span class="sxs-lookup"><span data-stu-id="3b838-159">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

        SELECT * FROM devices.jobs
        WHERE devices.jobs.jobId = 'myJobId'

### <a name="limitations"></a><span data-ttu-id="3b838-160">Limitations</span><span class="sxs-lookup"><span data-stu-id="3b838-160">Limitations</span></span>
<span data-ttu-id="3b838-161">Currently, queries on **devices.jobs** do not support:</span><span class="sxs-lookup"><span data-stu-id="3b838-161">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="3b838-162">Projections, therefore only `SELECT *` is possible.</span><span class="sxs-lookup"><span data-stu-id="3b838-162">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="3b838-163">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span><span class="sxs-lookup"><span data-stu-id="3b838-163">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="3b838-164">Performing aggregations, such as count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="3b838-164">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="3b838-165">Get started with device-to-cloud message routes query expressions</span><span class="sxs-lookup"><span data-stu-id="3b838-165">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="3b838-166">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span><span class="sxs-lookup"><span data-stu-id="3b838-166">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="3b838-167">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span><span class="sxs-lookup"><span data-stu-id="3b838-167">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="3b838-168">Route conditions are evaluated on the message properties assuming the following JSON representation:</span><span class="sxs-lookup"><span data-stu-id="3b838-168">Route conditions are evaluated on the message properties assuming the following JSON representation:</span></span>

        {
            "$messageId": "",
            "$enqueuedTime": "",
            "$to": "",
            "$expiryTimeUtc": "",
            "$correlationId": "",
            "$userId": "",
            "$ack": "",
            "$connectionDeviceId": "",
            "$connectionDeviceGenerationId": "",
            "$connectionAuthMethod": "",
            "$content-type": "",
            "$content-encoding": ""

            "userProperty1": "",
            "userProperty2": ""
        }

<span data-ttu-id="3b838-169">Message system properties are prefixed with the `'$'` symbol.</span><span class="sxs-lookup"><span data-stu-id="3b838-169">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="3b838-170">User properties are always accessed with their name.</span><span class="sxs-lookup"><span data-stu-id="3b838-170">User properties are always accessed with their name.</span></span> <span data-ttu-id="3b838-171">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span><span class="sxs-lookup"><span data-stu-id="3b838-171">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="3b838-172">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span><span class="sxs-lookup"><span data-stu-id="3b838-172">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="3b838-173">Bracketed property names always retrieve the corresponding system property.</span><span class="sxs-lookup"><span data-stu-id="3b838-173">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="3b838-174">Remember that property names are case insensitive.</span><span class="sxs-lookup"><span data-stu-id="3b838-174">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="3b838-175">All message properties are strings.</span><span class="sxs-lookup"><span data-stu-id="3b838-175">All message properties are strings.</span></span> <span data-ttu-id="3b838-176">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span><span class="sxs-lookup"><span data-stu-id="3b838-176">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="3b838-177">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span><span class="sxs-lookup"><span data-stu-id="3b838-177">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="3b838-178">You can write the following expression to route the telemetry:</span><span class="sxs-lookup"><span data-stu-id="3b838-178">You can write the following expression to route the telemetry:</span></span>

        messageType = 'telemetry'

<span data-ttu-id="3b838-179">And the following expression to route the alert messages:</span><span class="sxs-lookup"><span data-stu-id="3b838-179">And the following expression to route the alert messages:</span></span>

        messageType = 'alert'

<span data-ttu-id="3b838-180">Boolean expressions and functions are also supported.</span><span class="sxs-lookup"><span data-stu-id="3b838-180">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="3b838-181">This feature enables you to distinguish between severity level, for example:</span><span class="sxs-lookup"><span data-stu-id="3b838-181">This feature enables you to distinguish between severity level, for example:</span></span>

        messageType = 'alerts' AND as_number(severity) <= 2

<span data-ttu-id="3b838-182">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span><span class="sxs-lookup"><span data-stu-id="3b838-182">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="3b838-183">Basics of an IoT Hub query</span><span class="sxs-lookup"><span data-stu-id="3b838-183">Basics of an IoT Hub query</span></span>
<span data-ttu-id="3b838-184">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span><span class="sxs-lookup"><span data-stu-id="3b838-184">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="3b838-185">Every query is run on a collection of JSON documents, for example device twins.</span><span class="sxs-lookup"><span data-stu-id="3b838-185">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="3b838-186">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="3b838-186">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="3b838-187">Then, the filter in the WHERE clause is applied.</span><span class="sxs-lookup"><span data-stu-id="3b838-187">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="3b838-188">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span><span class="sxs-lookup"><span data-stu-id="3b838-188">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

        SELECT <select_list>
        FROM <from_specification>
        [WHERE <filter_condition>]
        [GROUP BY <group_specification>]

## <a name="from-clause"></a><span data-ttu-id="3b838-189">FROM clause</span><span class="sxs-lookup"><span data-stu-id="3b838-189">FROM clause</span></span>
<span data-ttu-id="3b838-190">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span><span class="sxs-lookup"><span data-stu-id="3b838-190">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="3b838-191">WHERE clause</span><span class="sxs-lookup"><span data-stu-id="3b838-191">WHERE clause</span></span>
<span data-ttu-id="3b838-192">The **WHERE <filter_condition>** clause is optional.</span><span class="sxs-lookup"><span data-stu-id="3b838-192">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="3b838-193">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span><span class="sxs-lookup"><span data-stu-id="3b838-193">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="3b838-194">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span><span class="sxs-lookup"><span data-stu-id="3b838-194">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="3b838-195">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="3b838-195">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="3b838-196">SELECT clause</span><span class="sxs-lookup"><span data-stu-id="3b838-196">SELECT clause</span></span>
<span data-ttu-id="3b838-197">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span><span class="sxs-lookup"><span data-stu-id="3b838-197">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="3b838-198">It specifies the JSON values to be used to generate new JSON objects.</span><span class="sxs-lookup"><span data-stu-id="3b838-198">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="3b838-199">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span><span class="sxs-lookup"><span data-stu-id="3b838-199">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="3b838-200">Following is the grammar of the SELECT clause:</span><span class="sxs-lookup"><span data-stu-id="3b838-200">Following is the grammar of the SELECT clause:</span></span>

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

<span data-ttu-id="3b838-201">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span><span class="sxs-lookup"><span data-stu-id="3b838-201">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="3b838-202">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span><span class="sxs-lookup"><span data-stu-id="3b838-202">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="3b838-203">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span><span class="sxs-lookup"><span data-stu-id="3b838-203">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="3b838-204">GROUP BY clause</span><span class="sxs-lookup"><span data-stu-id="3b838-204">GROUP BY clause</span></span>
<span data-ttu-id="3b838-205">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span><span class="sxs-lookup"><span data-stu-id="3b838-205">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="3b838-206">It groups documents based on the value of an attribute.</span><span class="sxs-lookup"><span data-stu-id="3b838-206">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="3b838-207">These groups are used to generate aggregated values as specified in the SELECT clause.</span><span class="sxs-lookup"><span data-stu-id="3b838-207">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="3b838-208">An example of a query using GROUP BY is:</span><span class="sxs-lookup"><span data-stu-id="3b838-208">An example of a query using GROUP BY is:</span></span>

        SELECT properties.reported.telemetryConfig.status AS status,
            COUNT() AS numberOfDevices
        FROM devices
        GROUP BY properties.reported.telemetryConfig.status

<span data-ttu-id="3b838-209">The formal syntax for GROUP BY is:</span><span class="sxs-lookup"><span data-stu-id="3b838-209">The formal syntax for GROUP BY is:</span></span>

        GROUP BY <group_by_element>
        <group_by_element> :==
            attribute_name
            | < group_by_element > '.' attribute_name

<span data-ttu-id="3b838-210">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span><span class="sxs-lookup"><span data-stu-id="3b838-210">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="3b838-211">Currently, the GROUP BY clause is only supported when querying device twins.</span><span class="sxs-lookup"><span data-stu-id="3b838-211">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="3b838-212">Expressions and conditions</span><span class="sxs-lookup"><span data-stu-id="3b838-212">Expressions and conditions</span></span>
<span data-ttu-id="3b838-213">At a high level, an *expression*:</span><span class="sxs-lookup"><span data-stu-id="3b838-213">At a high level, an *expression*:</span></span>

* <span data-ttu-id="3b838-214">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span><span class="sxs-lookup"><span data-stu-id="3b838-214">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="3b838-215">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span><span class="sxs-lookup"><span data-stu-id="3b838-215">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="3b838-216">*Conditions* are expressions that evaluate to a Boolean.</span><span class="sxs-lookup"><span data-stu-id="3b838-216">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="3b838-217">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span><span class="sxs-lookup"><span data-stu-id="3b838-217">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="3b838-218">The syntax for expressions is:</span><span class="sxs-lookup"><span data-stu-id="3b838-218">The syntax for expressions is:</span></span>

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

<span data-ttu-id="3b838-219">where:</span><span class="sxs-lookup"><span data-stu-id="3b838-219">where:</span></span>

| <span data-ttu-id="3b838-220">Symbol</span><span class="sxs-lookup"><span data-stu-id="3b838-220">Symbol</span></span> | <span data-ttu-id="3b838-221">Definition</span><span class="sxs-lookup"><span data-stu-id="3b838-221">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="3b838-222">attribute_name</span><span class="sxs-lookup"><span data-stu-id="3b838-222">attribute_name</span></span> | <span data-ttu-id="3b838-223">Any property of the JSON document in the **FROM** collection.</span><span class="sxs-lookup"><span data-stu-id="3b838-223">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="3b838-224">binary_operator</span><span class="sxs-lookup"><span data-stu-id="3b838-224">binary_operator</span></span> | <span data-ttu-id="3b838-225">Any binary operator listed in the [Operators](#operators) section.</span><span class="sxs-lookup"><span data-stu-id="3b838-225">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="3b838-226">function_name</span><span class="sxs-lookup"><span data-stu-id="3b838-226">function_name</span></span>| <span data-ttu-id="3b838-227">Any function listed in the [Functions](#functions) section.</span><span class="sxs-lookup"><span data-stu-id="3b838-227">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="3b838-228">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="3b838-228">decimal_literal</span></span> |<span data-ttu-id="3b838-229">A float expressed in decimal notation.</span><span class="sxs-lookup"><span data-stu-id="3b838-229">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="3b838-230">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="3b838-230">hexadecimal_literal</span></span> |<span data-ttu-id="3b838-231">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="3b838-231">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="3b838-232">string_literal</span><span class="sxs-lookup"><span data-stu-id="3b838-232">string_literal</span></span> |<span data-ttu-id="3b838-233">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span><span class="sxs-lookup"><span data-stu-id="3b838-233">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="3b838-234">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span><span class="sxs-lookup"><span data-stu-id="3b838-234">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="3b838-235">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span><span class="sxs-lookup"><span data-stu-id="3b838-235">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="3b838-236">Operators</span><span class="sxs-lookup"><span data-stu-id="3b838-236">Operators</span></span>
<span data-ttu-id="3b838-237">The following operators are supported:</span><span class="sxs-lookup"><span data-stu-id="3b838-237">The following operators are supported:</span></span>

| <span data-ttu-id="3b838-238">Family</span><span class="sxs-lookup"><span data-stu-id="3b838-238">Family</span></span> | <span data-ttu-id="3b838-239">Operators</span><span class="sxs-lookup"><span data-stu-id="3b838-239">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="3b838-240">Arithmetic</span><span class="sxs-lookup"><span data-stu-id="3b838-240">Arithmetic</span></span> |<span data-ttu-id="3b838-241">+,-,\*,/,%</span><span class="sxs-lookup"><span data-stu-id="3b838-241">+,-,\*,/,%</span></span> |
| <span data-ttu-id="3b838-242">Logical</span><span class="sxs-lookup"><span data-stu-id="3b838-242">Logical</span></span> |<span data-ttu-id="3b838-243">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="3b838-243">AND, OR, NOT</span></span> |
| <span data-ttu-id="3b838-244">Comparison</span><span class="sxs-lookup"><span data-stu-id="3b838-244">Comparison</span></span> |<span data-ttu-id="3b838-245">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="3b838-245">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="3b838-246">Functions</span><span class="sxs-lookup"><span data-stu-id="3b838-246">Functions</span></span>
<span data-ttu-id="3b838-247">When querying twins and jobs the only supported function is:</span><span class="sxs-lookup"><span data-stu-id="3b838-247">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="3b838-248">Function</span><span class="sxs-lookup"><span data-stu-id="3b838-248">Function</span></span> | <span data-ttu-id="3b838-249">Description</span><span class="sxs-lookup"><span data-stu-id="3b838-249">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3b838-250">IS_DEFINED(property)</span><span class="sxs-lookup"><span data-stu-id="3b838-250">IS_DEFINED(property)</span></span> | <span data-ttu-id="3b838-251">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span><span class="sxs-lookup"><span data-stu-id="3b838-251">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="3b838-252">In routes conditions, the following math functions are supported:</span><span class="sxs-lookup"><span data-stu-id="3b838-252">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="3b838-253">Function</span><span class="sxs-lookup"><span data-stu-id="3b838-253">Function</span></span> | <span data-ttu-id="3b838-254">Description</span><span class="sxs-lookup"><span data-stu-id="3b838-254">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3b838-255">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-255">ABS(x)</span></span> | <span data-ttu-id="3b838-256">Returns the absolute (positive) value of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="3b838-256">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="3b838-257">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-257">EXP(x)</span></span> | <span data-ttu-id="3b838-258">Returns the exponential value of the specified numeric expression (e^x).</span><span class="sxs-lookup"><span data-stu-id="3b838-258">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="3b838-259">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="3b838-259">POWER(x,y)</span></span> | <span data-ttu-id="3b838-260">Returns the value of the specified expression to the specified power (x^y).</span><span class="sxs-lookup"><span data-stu-id="3b838-260">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="3b838-261">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-261">SQUARE(x)</span></span> | <span data-ttu-id="3b838-262">Returns the square of the specified numeric value.</span><span class="sxs-lookup"><span data-stu-id="3b838-262">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="3b838-263">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-263">CEILING(x)</span></span> | <span data-ttu-id="3b838-264">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="3b838-264">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="3b838-265">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-265">FLOOR(x)</span></span> | <span data-ttu-id="3b838-266">Returns the largest integer less than or equal to the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="3b838-266">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="3b838-267">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-267">SIGN(x)</span></span> | <span data-ttu-id="3b838-268">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span><span class="sxs-lookup"><span data-stu-id="3b838-268">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="3b838-269">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-269">SQRT(x)</span></span> | <span data-ttu-id="3b838-270">Returns the square of the specified numeric value.</span><span class="sxs-lookup"><span data-stu-id="3b838-270">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="3b838-271">In routes conditions, the following type checking and casting functions are supported:</span><span class="sxs-lookup"><span data-stu-id="3b838-271">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="3b838-272">Function</span><span class="sxs-lookup"><span data-stu-id="3b838-272">Function</span></span> | <span data-ttu-id="3b838-273">Description</span><span class="sxs-lookup"><span data-stu-id="3b838-273">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3b838-274">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="3b838-274">AS_NUMBER</span></span> | <span data-ttu-id="3b838-275">Converts the input string to a number.</span><span class="sxs-lookup"><span data-stu-id="3b838-275">Converts the input string to a number.</span></span> <span data-ttu-id="3b838-276">`noop` if input is a number; `Undefined` if string does not represent a number.</span><span class="sxs-lookup"><span data-stu-id="3b838-276">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="3b838-277">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="3b838-277">IS_ARRAY</span></span> | <span data-ttu-id="3b838-278">Returns a Boolean value indicating if the type of the specified expression is an array.</span><span class="sxs-lookup"><span data-stu-id="3b838-278">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="3b838-279">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="3b838-279">IS_BOOL</span></span> | <span data-ttu-id="3b838-280">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span><span class="sxs-lookup"><span data-stu-id="3b838-280">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="3b838-281">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="3b838-281">IS_DEFINED</span></span> | <span data-ttu-id="3b838-282">Returns a Boolean indicating if the property has been assigned a value.</span><span class="sxs-lookup"><span data-stu-id="3b838-282">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="3b838-283">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="3b838-283">IS_NULL</span></span> | <span data-ttu-id="3b838-284">Returns a Boolean value indicating if the type of the specified expression is null.</span><span class="sxs-lookup"><span data-stu-id="3b838-284">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="3b838-285">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="3b838-285">IS_NUMBER</span></span> | <span data-ttu-id="3b838-286">Returns a Boolean value indicating if the type of the specified expression is a number.</span><span class="sxs-lookup"><span data-stu-id="3b838-286">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="3b838-287">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="3b838-287">IS_OBJECT</span></span> | <span data-ttu-id="3b838-288">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span><span class="sxs-lookup"><span data-stu-id="3b838-288">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="3b838-289">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="3b838-289">IS_PRIMITIVE</span></span> | <span data-ttu-id="3b838-290">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span><span class="sxs-lookup"><span data-stu-id="3b838-290">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="3b838-291">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="3b838-291">IS_STRING</span></span> | <span data-ttu-id="3b838-292">Returns a Boolean value indicating if the type of the specified expression is a string.</span><span class="sxs-lookup"><span data-stu-id="3b838-292">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="3b838-293">In routes conditions, the following string functions are supported:</span><span class="sxs-lookup"><span data-stu-id="3b838-293">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="3b838-294">Function</span><span class="sxs-lookup"><span data-stu-id="3b838-294">Function</span></span> | <span data-ttu-id="3b838-295">Description</span><span class="sxs-lookup"><span data-stu-id="3b838-295">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="3b838-296">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="3b838-296">CONCAT(x, …)</span></span> | <span data-ttu-id="3b838-297">Returns a string that is the result of concatenating two or more string values.</span><span class="sxs-lookup"><span data-stu-id="3b838-297">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="3b838-298">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-298">LENGTH(x)</span></span> | <span data-ttu-id="3b838-299">Returns the number of characters of the specified string expression.</span><span class="sxs-lookup"><span data-stu-id="3b838-299">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="3b838-300">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-300">LOWER(x)</span></span> | <span data-ttu-id="3b838-301">Returns a string expression after converting uppercase character data to lowercase.</span><span class="sxs-lookup"><span data-stu-id="3b838-301">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="3b838-302">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="3b838-302">UPPER(x)</span></span> | <span data-ttu-id="3b838-303">Returns a string expression after converting lowercase character data to uppercase.</span><span class="sxs-lookup"><span data-stu-id="3b838-303">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="3b838-304">SUBSTRING(string, start [, length])</span><span class="sxs-lookup"><span data-stu-id="3b838-304">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="3b838-305">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span><span class="sxs-lookup"><span data-stu-id="3b838-305">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="3b838-306">INDEX_OF(string, fragment)</span><span class="sxs-lookup"><span data-stu-id="3b838-306">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="3b838-307">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span><span class="sxs-lookup"><span data-stu-id="3b838-307">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="3b838-308">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="3b838-308">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="3b838-309">Returns a Boolean indicating whether the first string expression starts with the second.</span><span class="sxs-lookup"><span data-stu-id="3b838-309">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="3b838-310">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="3b838-310">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="3b838-311">Returns a Boolean indicating whether the first string expression ends with the second.</span><span class="sxs-lookup"><span data-stu-id="3b838-311">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="3b838-312">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="3b838-312">CONTAINS(x,y)</span></span> | <span data-ttu-id="3b838-313">Returns a Boolean indicating whether the first string expression contains the second.</span><span class="sxs-lookup"><span data-stu-id="3b838-313">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3b838-314">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b838-314">Next steps</span></span>
<span data-ttu-id="3b838-315">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="3b838-315">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messaging.md#routing-rules
[lnk-devguide-messaging-format]: iot-hub-devguide-messaging.md#message-format


[lnk-hub-sdks]: iot-hub-devguide-sdks.md
