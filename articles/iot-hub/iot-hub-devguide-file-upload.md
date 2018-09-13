---
title: Understand Azure IoT Hub file upload | Microsoft Docs
description: Developer guide - use the file upload feature of IoT Hub to manage uploading files from a device to an Azure storage blob container.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e16d32bdba1374540c03d1034a94192a54e6a109
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776678"
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="ccd65-103">Upload files with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ccd65-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="ccd65-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="ccd65-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="ccd65-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span><span class="sxs-lookup"><span data-stu-id="ccd65-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="ccd65-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="ccd65-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="ccd65-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span><span class="sxs-lookup"><span data-stu-id="ccd65-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="ccd65-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd65-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="ccd65-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span><span class="sxs-lookup"><span data-stu-id="ccd65-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="ccd65-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span><span class="sxs-lookup"><span data-stu-id="ccd65-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="ccd65-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span><span class="sxs-lookup"><span data-stu-id="ccd65-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="ccd65-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="ccd65-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="ccd65-113">When to use</span><span class="sxs-lookup"><span data-stu-id="ccd65-113">When to use</span></span>

<span data-ttu-id="ccd65-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span><span class="sxs-lookup"><span data-stu-id="ccd65-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="ccd65-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span><span class="sxs-lookup"><span data-stu-id="ccd65-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="ccd65-116">Associate an Azure Storage account with IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ccd65-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="ccd65-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd65-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="ccd65-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="ccd65-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="ccd65-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span><span class="sxs-lookup"><span data-stu-id="ccd65-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd65-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span><span class="sxs-lookup"><span data-stu-id="ccd65-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="ccd65-121">Initialize a file upload</span><span class="sxs-lookup"><span data-stu-id="ccd65-121">Initialize a file upload</span></span>
<span data-ttu-id="ccd65-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span><span class="sxs-lookup"><span data-stu-id="ccd65-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="ccd65-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span><span class="sxs-lookup"><span data-stu-id="ccd65-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="ccd65-124">IoT Hub returns the following data, which the device uses to upload the file:</span><span class="sxs-lookup"><span data-stu-id="ccd65-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="ccd65-125">Deprecated: initialize a file upload with a GET</span><span class="sxs-lookup"><span data-stu-id="ccd65-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="ccd65-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd65-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="ccd65-127">Use the POST method described previously.</span><span class="sxs-lookup"><span data-stu-id="ccd65-127">Use the POST method described previously.</span></span>

<span data-ttu-id="ccd65-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span><span class="sxs-lookup"><span data-stu-id="ccd65-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="ccd65-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="ccd65-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="ccd65-130">The IoT hub returns:</span><span class="sxs-lookup"><span data-stu-id="ccd65-130">The IoT hub returns:</span></span>

* <span data-ttu-id="ccd65-131">A SAS URI specific to the file to be uploaded.</span><span class="sxs-lookup"><span data-stu-id="ccd65-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="ccd65-132">A correlation ID to be used once the upload is completed.</span><span class="sxs-lookup"><span data-stu-id="ccd65-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="ccd65-133">Notify IoT Hub of a completed file upload</span><span class="sxs-lookup"><span data-stu-id="ccd65-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="ccd65-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span><span class="sxs-lookup"><span data-stu-id="ccd65-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="ccd65-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span><span class="sxs-lookup"><span data-stu-id="ccd65-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="ccd65-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span><span class="sxs-lookup"><span data-stu-id="ccd65-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="ccd65-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="ccd65-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="ccd65-138">Reference topics:</span><span class="sxs-lookup"><span data-stu-id="ccd65-138">Reference topics:</span></span>

<span data-ttu-id="ccd65-139">The following reference topics provide you with more information about uploading files from a device.</span><span class="sxs-lookup"><span data-stu-id="ccd65-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="ccd65-140">File upload notifications</span><span class="sxs-lookup"><span data-stu-id="ccd65-140">File upload notifications</span></span>

<span data-ttu-id="ccd65-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub generates a notification message that contains the name and storage location of the file.</span><span class="sxs-lookup"><span data-stu-id="ccd65-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub generates a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="ccd65-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span><span class="sxs-lookup"><span data-stu-id="ccd65-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="ccd65-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="ccd65-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="ccd65-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span><span class="sxs-lookup"><span data-stu-id="ccd65-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="ccd65-145">Property</span><span class="sxs-lookup"><span data-stu-id="ccd65-145">Property</span></span> | <span data-ttu-id="ccd65-146">Description</span><span class="sxs-lookup"><span data-stu-id="ccd65-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ccd65-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="ccd65-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="ccd65-148">Timestamp indicating when the notification was created.</span><span class="sxs-lookup"><span data-stu-id="ccd65-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="ccd65-149">DeviceId</span><span class="sxs-lookup"><span data-stu-id="ccd65-149">DeviceId</span></span> |<span data-ttu-id="ccd65-150">**DeviceId** of the device which uploaded the file.</span><span class="sxs-lookup"><span data-stu-id="ccd65-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="ccd65-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="ccd65-151">BlobUri</span></span> |<span data-ttu-id="ccd65-152">URI of the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="ccd65-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="ccd65-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="ccd65-153">BlobName</span></span> |<span data-ttu-id="ccd65-154">Name of the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="ccd65-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="ccd65-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="ccd65-155">LastUpdatedTime</span></span> |<span data-ttu-id="ccd65-156">Timestamp indicating when the file was last updated.</span><span class="sxs-lookup"><span data-stu-id="ccd65-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="ccd65-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="ccd65-157">BlobSizeInBytes</span></span> |<span data-ttu-id="ccd65-158">Size of the uploaded file.</span><span class="sxs-lookup"><span data-stu-id="ccd65-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="ccd65-159">**Example**.</span><span class="sxs-lookup"><span data-stu-id="ccd65-159">**Example**.</span></span> <span data-ttu-id="ccd65-160">This example shows the body of a file upload notification message.</span><span class="sxs-lookup"><span data-stu-id="ccd65-160">This example shows the body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="ccd65-161">File upload notification configuration options</span><span class="sxs-lookup"><span data-stu-id="ccd65-161">File upload notification configuration options</span></span>

<span data-ttu-id="ccd65-162">Each IoT hub exposes the following configuration options for file upload notifications:</span><span class="sxs-lookup"><span data-stu-id="ccd65-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="ccd65-163">Property</span><span class="sxs-lookup"><span data-stu-id="ccd65-163">Property</span></span> | <span data-ttu-id="ccd65-164">Description</span><span class="sxs-lookup"><span data-stu-id="ccd65-164">Description</span></span> | <span data-ttu-id="ccd65-165">Range and default</span><span class="sxs-lookup"><span data-stu-id="ccd65-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccd65-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="ccd65-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="ccd65-167">Controls whether file upload notifications are written to the file notifications endpoint.</span><span class="sxs-lookup"><span data-stu-id="ccd65-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="ccd65-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="ccd65-168">Bool.</span></span> <span data-ttu-id="ccd65-169">Default: True.</span><span class="sxs-lookup"><span data-stu-id="ccd65-169">Default: True.</span></span> |
| <span data-ttu-id="ccd65-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="ccd65-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="ccd65-171">Default TTL for file upload notifications.</span><span class="sxs-lookup"><span data-stu-id="ccd65-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="ccd65-172">ISO_8601 interval up to 48H (minimum 1 minute).</span><span class="sxs-lookup"><span data-stu-id="ccd65-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="ccd65-173">Default: 1 hour.</span><span class="sxs-lookup"><span data-stu-id="ccd65-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="ccd65-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="ccd65-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="ccd65-175">Lock duration for the file upload notifications queue.</span><span class="sxs-lookup"><span data-stu-id="ccd65-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="ccd65-176">5 to 300 seconds (minimum 5 seconds).</span><span class="sxs-lookup"><span data-stu-id="ccd65-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="ccd65-177">Default: 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="ccd65-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="ccd65-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="ccd65-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="ccd65-179">Maximum delivery count for the file upload notification queue.</span><span class="sxs-lookup"><span data-stu-id="ccd65-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="ccd65-180">1 to 100.</span><span class="sxs-lookup"><span data-stu-id="ccd65-180">1 to 100.</span></span> <span data-ttu-id="ccd65-181">Default: 100.</span><span class="sxs-lookup"><span data-stu-id="ccd65-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="ccd65-182">Additional reference material</span><span class="sxs-lookup"><span data-stu-id="ccd65-182">Additional reference material</span></span>

<span data-ttu-id="ccd65-183">Other reference topics in the IoT Hub developer guide include:</span><span class="sxs-lookup"><span data-stu-id="ccd65-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="ccd65-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span><span class="sxs-lookup"><span data-stu-id="ccd65-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="ccd65-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span><span class="sxs-lookup"><span data-stu-id="ccd65-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="ccd65-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd65-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="ccd65-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span><span class="sxs-lookup"><span data-stu-id="ccd65-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="ccd65-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="ccd65-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd65-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="ccd65-189">Next steps</span></span>

<span data-ttu-id="ccd65-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span><span class="sxs-lookup"><span data-stu-id="ccd65-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="ccd65-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="ccd65-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="ccd65-192">[Control access to IoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="ccd65-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="ccd65-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="ccd65-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="ccd65-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="ccd65-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="ccd65-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ccd65-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ccd65-196">To try out some of the concepts described in this article, see the following IoT Hub tutorial:</span><span class="sxs-lookup"><span data-stu-id="ccd65-196">To try out some of the concepts described in this article, see the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="ccd65-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="ccd65-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
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
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
