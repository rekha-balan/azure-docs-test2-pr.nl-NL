---
title: Understand Azure IoT Hub  file upload | Microsoft Docs
description: Developer guide - use the file upload feature of IoT Hub to manage uploading files from a device to an Azure storage blob container.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: dobett
ms.openlocfilehash: fd637a589f91057d579fe3f2871af0164e114bb1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563609"
---
# <a name="file-uploads-with-iot-hub"></a><span data-ttu-id="f7c90-103">File uploads with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f7c90-103">File uploads with IoT Hub</span></span>

## <a name="overview"></a><span data-ttu-id="f7c90-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f7c90-104">Overview</span></span>

<span data-ttu-id="f7c90-105">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, devices can initiate file uploads by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="f7c90-105">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, devices can initiate file uploads by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span>  <span data-ttu-id="f7c90-106">When a device notifies IoT Hub of a completed upload, IoT Hub generates file upload notifications that you can receive through a service-facing endpoint (**/messages/servicebound/filenotifications**) as messages.</span><span class="sxs-lookup"><span data-stu-id="f7c90-106">When a device notifies IoT Hub of a completed upload, IoT Hub generates file upload notifications that you can receive through a service-facing endpoint (**/messages/servicebound/filenotifications**) as messages.</span></span>

<span data-ttu-id="f7c90-107">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f7c90-107">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="f7c90-108">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span><span class="sxs-lookup"><span data-stu-id="f7c90-108">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="f7c90-109">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7c90-109">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="f7c90-110">IoT Hub verifies that the file was uploaded and then adds a file upload notification to the new service-facing file notification messaging endpoint.</span><span class="sxs-lookup"><span data-stu-id="f7c90-110">IoT Hub verifies that the file was uploaded and then adds a file upload notification to the new service-facing file notification messaging endpoint.</span></span>

<span data-ttu-id="f7c90-111">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span><span class="sxs-lookup"><span data-stu-id="f7c90-111">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="f7c90-112">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span><span class="sxs-lookup"><span data-stu-id="f7c90-112">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="f7c90-113">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="f7c90-113">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="f7c90-114">When to use</span><span class="sxs-lookup"><span data-stu-id="f7c90-114">When to use</span></span>

<span data-ttu-id="f7c90-115">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span><span class="sxs-lookup"><span data-stu-id="f7c90-115">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="f7c90-116">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span><span class="sxs-lookup"><span data-stu-id="f7c90-116">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="f7c90-117">Associate an Azure Storage account with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f7c90-117">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="f7c90-118">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7c90-118">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="f7c90-119">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="f7c90-119">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="f7c90-120">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span><span class="sxs-lookup"><span data-stu-id="f7c90-120">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="f7c90-121">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span><span class="sxs-lookup"><span data-stu-id="f7c90-121">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="f7c90-122">Initialize a file upload</span><span class="sxs-lookup"><span data-stu-id="f7c90-122">Initialize a file upload</span></span>
<span data-ttu-id="f7c90-123">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span><span class="sxs-lookup"><span data-stu-id="f7c90-123">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="f7c90-124">The device initiates the file upload process by sending a POST to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span><span class="sxs-lookup"><span data-stu-id="f7c90-124">The device initiates the file upload process by sending a POST to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="f7c90-125">IoT Hub returns the following data, which the device uses to upload the file:</span><span class="sxs-lookup"><span data-stu-id="f7c90-125">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostname": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="f7c90-126">Deprecated: initialize a file upload with a GET</span><span class="sxs-lookup"><span data-stu-id="f7c90-126">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="f7c90-127">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7c90-127">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="f7c90-128">You should use the POST method described previously.</span><span class="sxs-lookup"><span data-stu-id="f7c90-128">You should use the POST method described previously.</span></span>

<span data-ttu-id="f7c90-129">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span><span class="sxs-lookup"><span data-stu-id="f7c90-129">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="f7c90-130">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="f7c90-130">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="f7c90-131">The IoT hub returns a SAS URI specific to the file to be uploaded, and a correlation ID to be used once the upload is completed.</span><span class="sxs-lookup"><span data-stu-id="f7c90-131">The IoT hub returns a SAS URI specific to the file to be uploaded, and a correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="f7c90-132">Notify IoT Hub of a completed file upload</span><span class="sxs-lookup"><span data-stu-id="f7c90-132">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="f7c90-133">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span><span class="sxs-lookup"><span data-stu-id="f7c90-133">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="f7c90-134">Once the upload is completed, the device sends a POST to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span><span class="sxs-lookup"><span data-stu-id="f7c90-134">Once the upload is completed, the device sends a POST to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="f7c90-135">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span><span class="sxs-lookup"><span data-stu-id="f7c90-135">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="f7c90-136">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="f7c90-136">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="f7c90-137">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="f7c90-137">Reference topics:</span></span>

<span data-ttu-id="f7c90-138">The following reference topics provide you with more information about uploading files from a device.</span><span class="sxs-lookup"><span data-stu-id="f7c90-138">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="f7c90-139">File upload notifications</span><span class="sxs-lookup"><span data-stu-id="f7c90-139">File upload notifications</span></span>

<span data-ttu-id="f7c90-140">When a device uploads a file and notifies IoT Hub of upload completion, the service optionally generates a notification message that contains the name and storage location of the file.</span><span class="sxs-lookup"><span data-stu-id="f7c90-140">When a device uploads a file and notifies IoT Hub of upload completion, the service optionally generates a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="f7c90-141">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span><span class="sxs-lookup"><span data-stu-id="f7c90-141">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="f7c90-142">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="f7c90-142">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="f7c90-143">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span><span class="sxs-lookup"><span data-stu-id="f7c90-143">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="f7c90-144">Property</span><span class="sxs-lookup"><span data-stu-id="f7c90-144">Property</span></span> | <span data-ttu-id="f7c90-145">Description</span><span class="sxs-lookup"><span data-stu-id="f7c90-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7c90-146">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="f7c90-146">EnqueuedTimeUtc</span></span> |<span data-ttu-id="f7c90-147">Timestamp indicating when the notification was created.</span><span class="sxs-lookup"><span data-stu-id="f7c90-147">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="f7c90-148">DeviceId</span><span class="sxs-lookup"><span data-stu-id="f7c90-148">DeviceId</span></span> |<span data-ttu-id="f7c90-149">**DeviceId** of the device which uploaded the file.</span><span class="sxs-lookup"><span data-stu-id="f7c90-149">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="f7c90-150">BlobUri</span><span class="sxs-lookup"><span data-stu-id="f7c90-150">BlobUri</span></span> |<span data-ttu-id="f7c90-151">URI of the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="f7c90-151">URI of the uploaded file.</span></span> |
| <span data-ttu-id="f7c90-152">BlobName</span><span class="sxs-lookup"><span data-stu-id="f7c90-152">BlobName</span></span> |<span data-ttu-id="f7c90-153">Name of the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="f7c90-153">Name of the uploaded file.</span></span> |
| <span data-ttu-id="f7c90-154">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="f7c90-154">LastUpdatedTime</span></span> |<span data-ttu-id="f7c90-155">Timestamp indicating when the file was last updated.</span><span class="sxs-lookup"><span data-stu-id="f7c90-155">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="f7c90-156">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="f7c90-156">BlobSizeInBytes</span></span> |<span data-ttu-id="f7c90-157">Size of the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="f7c90-157">Size of the uploaded file.</span></span> |

<span data-ttu-id="f7c90-158">**Example**.</span><span class="sxs-lookup"><span data-stu-id="f7c90-158">**Example**.</span></span> <span data-ttu-id="f7c90-159">This example shows the body of a file upload notification message.</span><span class="sxs-lookup"><span data-stu-id="f7c90-159">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="f7c90-160">File upload notification configuration options</span><span class="sxs-lookup"><span data-stu-id="f7c90-160">File upload notification configuration options</span></span>

<span data-ttu-id="f7c90-161">Each IoT hub exposes the following configuration options for file upload notifications:</span><span class="sxs-lookup"><span data-stu-id="f7c90-161">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="f7c90-162">Property</span><span class="sxs-lookup"><span data-stu-id="f7c90-162">Property</span></span> | <span data-ttu-id="f7c90-163">Description</span><span class="sxs-lookup"><span data-stu-id="f7c90-163">Description</span></span> | <span data-ttu-id="f7c90-164">Range and default</span><span class="sxs-lookup"><span data-stu-id="f7c90-164">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f7c90-165">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="f7c90-165">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="f7c90-166">Controls whether file upload notifications are written to the file notifications endpoint.</span><span class="sxs-lookup"><span data-stu-id="f7c90-166">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="f7c90-167">Bool.</span><span class="sxs-lookup"><span data-stu-id="f7c90-167">Bool.</span></span> <span data-ttu-id="f7c90-168">Default: True.</span><span class="sxs-lookup"><span data-stu-id="f7c90-168">Default: True.</span></span> |
| <span data-ttu-id="f7c90-169">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="f7c90-169">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="f7c90-170">Default TTL for file upload notifications.</span><span class="sxs-lookup"><span data-stu-id="f7c90-170">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="f7c90-171">ISO_8601 interval up to 48H (minimum 1 minute).</span><span class="sxs-lookup"><span data-stu-id="f7c90-171">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="f7c90-172">Default: 1 hour.</span><span class="sxs-lookup"><span data-stu-id="f7c90-172">Default: 1 hour.</span></span> |
| <span data-ttu-id="f7c90-173">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="f7c90-173">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="f7c90-174">Lock duration for the file upload notifications queue.</span><span class="sxs-lookup"><span data-stu-id="f7c90-174">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="f7c90-175">5 to 300 seconds (minimum 5 seconds).</span><span class="sxs-lookup"><span data-stu-id="f7c90-175">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="f7c90-176">Default: 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="f7c90-176">Default: 60 seconds.</span></span> |
| <span data-ttu-id="f7c90-177">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="f7c90-177">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="f7c90-178">Maximum delivery count for the file upload notification queue.</span><span class="sxs-lookup"><span data-stu-id="f7c90-178">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="f7c90-179">1 to 100.</span><span class="sxs-lookup"><span data-stu-id="f7c90-179">1 to 100.</span></span> <span data-ttu-id="f7c90-180">Default: 100.</span><span class="sxs-lookup"><span data-stu-id="f7c90-180">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="f7c90-181">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="f7c90-181">Additional reference material</span></span>

<span data-ttu-id="f7c90-182">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="f7c90-182">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f7c90-183">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="f7c90-183">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f7c90-184">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span><span class="sxs-lookup"><span data-stu-id="f7c90-184">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="f7c90-185">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f7c90-185">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f7c90-186">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="f7c90-186">[IoT Hub query language for device twins and jobs][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f7c90-187">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="f7c90-187">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7c90-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7c90-188">Next steps</span></span>

<span data-ttu-id="f7c90-189">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span><span class="sxs-lookup"><span data-stu-id="f7c90-189">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="f7c90-190">[Manage device identities in IoT Hub][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="f7c90-190">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="f7c90-191">[Control access to IoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="f7c90-191">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="f7c90-192">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="f7c90-192">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="f7c90-193">[Invoke a direct method on a device][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="f7c90-193">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="f7c90-194">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="f7c90-194">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="f7c90-195">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span><span class="sxs-lookup"><span data-stu-id="f7c90-195">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="f7c90-196">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f7c90-196">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://msdn.microsoft.com/library/mt548492.aspx
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messaging.md#message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
