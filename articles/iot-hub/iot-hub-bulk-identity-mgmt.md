---
title: Import export of Azure IoT Hub device identities | Microsoft Docs
description: How to use the Azure IoT service SDK to perform bulk operations against the identity registry to import and export device identities. Import operations enable you to create, update, and delete device identities in bulk.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: dobett
ms.openlocfilehash: 6d878b00094f573adc440d2384c426506fea0a40
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553558"
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="4684f-104">Manage your IoT Hub device identities in bulk</span><span class="sxs-lookup"><span data-stu-id="4684f-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="4684f-105">Each IoT hub has an identity registry you can use to create per-device resources in the service, such as a queue that contains in-flight cloud-to-device messages.</span><span class="sxs-lookup"><span data-stu-id="4684f-105">Each IoT hub has an identity registry you can use to create per-device resources in the service, such as a queue that contains in-flight cloud-to-device messages.</span></span> <span data-ttu-id="4684f-106">The identity registry also enables you to control access to the device-facing endpoints.</span><span class="sxs-lookup"><span data-stu-id="4684f-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="4684f-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span><span class="sxs-lookup"><span data-stu-id="4684f-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="4684f-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4684f-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="4684f-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span><span class="sxs-lookup"><span data-stu-id="4684f-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="4684f-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span><span class="sxs-lookup"><span data-stu-id="4684f-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="4684f-111">What are jobs?</span><span class="sxs-lookup"><span data-stu-id="4684f-111">What are jobs?</span></span>

<span data-ttu-id="4684f-112">Identity registry operations use the **Job** system when the operation:</span><span class="sxs-lookup"><span data-stu-id="4684f-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="4684f-113">Has a potentially long execution time compared to standard run-time operations.</span><span class="sxs-lookup"><span data-stu-id="4684f-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="4684f-114">Returns a large amount of data to the user.</span><span class="sxs-lookup"><span data-stu-id="4684f-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="4684f-115">In these cases, instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4684f-115">In these cases, instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="4684f-116">The operation then immediately returns a **JobProperties** object.</span><span class="sxs-lookup"><span data-stu-id="4684f-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="4684f-117">The following C# code snippet shows how to create an export job:</span><span class="sxs-lookup"><span data-stu-id="4684f-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="4684f-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span><span class="sxs-lookup"><span data-stu-id="4684f-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="4684f-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span><span class="sxs-lookup"><span data-stu-id="4684f-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>


<span data-ttu-id="4684f-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span><span class="sxs-lookup"><span data-stu-id="4684f-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="4684f-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span><span class="sxs-lookup"><span data-stu-id="4684f-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="4684f-122">Export devices</span><span class="sxs-lookup"><span data-stu-id="4684f-122">Export devices</span></span>

<span data-ttu-id="4684f-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="4684f-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="4684f-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span><span class="sxs-lookup"><span data-stu-id="4684f-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="4684f-125">The **ExportDevicesAsync** method requires two parameters:</span><span class="sxs-lookup"><span data-stu-id="4684f-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="4684f-126">A *string* that contains a URI of a blob container.</span><span class="sxs-lookup"><span data-stu-id="4684f-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="4684f-127">This URI must contain a SAS token that grants write access to the container.</span><span class="sxs-lookup"><span data-stu-id="4684f-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="4684f-128">The job creates a block blob in this container to store the serialized export device data.</span><span class="sxs-lookup"><span data-stu-id="4684f-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="4684f-129">The SAS token must include these permissions:</span><span class="sxs-lookup"><span data-stu-id="4684f-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="4684f-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span><span class="sxs-lookup"><span data-stu-id="4684f-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="4684f-131">If **false**, authentication keys are included in export output.</span><span class="sxs-lookup"><span data-stu-id="4684f-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="4684f-132">Otherwise, keys are exported as **null**.</span><span class="sxs-lookup"><span data-stu-id="4684f-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="4684f-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span><span class="sxs-lookup"><span data-stu-id="4684f-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="4684f-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="4684f-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="4684f-135">The output data consists of JSON serialized device data, with one device per line.</span><span class="sxs-lookup"><span data-stu-id="4684f-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="4684f-136">The following example shows the output data:</span><span class="sxs-lookup"><span data-stu-id="4684f-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class. <span data-ttu-id="4684f-138">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span><span class="sxs-lookup"><span data-stu-id="4684f-138">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), RequestOptions, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="4684f-139">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span><span class="sxs-lookup"><span data-stu-id="4684f-139">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="4684f-140">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span><span class="sxs-lookup"><span data-stu-id="4684f-140">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="4684f-141">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span><span class="sxs-lookup"><span data-stu-id="4684f-141">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="4684f-142">Import devices</span><span class="sxs-lookup"><span data-stu-id="4684f-142">Import devices</span></span>

<span data-ttu-id="4684f-143">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span><span class="sxs-lookup"><span data-stu-id="4684f-143">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="4684f-144">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span><span class="sxs-lookup"><span data-stu-id="4684f-144">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="4684f-145">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span><span class="sxs-lookup"><span data-stu-id="4684f-145">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="4684f-146">An import operation cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="4684f-146">An import operation cannot be undone.</span></span> <span data-ttu-id="4684f-147">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span><span class="sxs-lookup"><span data-stu-id="4684f-147">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="4684f-148">The **ImportDevicesAsync** method takes two parameters:</span><span class="sxs-lookup"><span data-stu-id="4684f-148">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="4684f-149">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span><span class="sxs-lookup"><span data-stu-id="4684f-149">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="4684f-150">This URI must contain a SAS token that grants read access to the container.</span><span class="sxs-lookup"><span data-stu-id="4684f-150">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="4684f-151">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span><span class="sxs-lookup"><span data-stu-id="4684f-151">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="4684f-152">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="4684f-152">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="4684f-153">The SAS token must include these permissions:</span><span class="sxs-lookup"><span data-stu-id="4684f-153">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="4684f-154">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span><span class="sxs-lookup"><span data-stu-id="4684f-154">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="4684f-155">The job creates a block blob in this container to store any error information from the completed import **Job**.</span><span class="sxs-lookup"><span data-stu-id="4684f-155">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="4684f-156">The SAS token must include these permissions:</span><span class="sxs-lookup"><span data-stu-id="4684f-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="4684f-157">The two parameters can point to the same blob container.</span><span class="sxs-lookup"><span data-stu-id="4684f-157">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="4684f-158">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span><span class="sxs-lookup"><span data-stu-id="4684f-158">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="4684f-159">The following C# code snippet shows how to initiate an import job:</span><span class="sxs-lookup"><span data-stu-id="4684f-159">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

## <a name="import-behavior"></a><span data-ttu-id="4684f-160">Import behavior</span><span class="sxs-lookup"><span data-stu-id="4684f-160">Import behavior</span></span>

<span data-ttu-id="4684f-161">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span><span class="sxs-lookup"><span data-stu-id="4684f-161">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="4684f-162">Bulk registration of new devices</span><span class="sxs-lookup"><span data-stu-id="4684f-162">Bulk registration of new devices</span></span>
* <span data-ttu-id="4684f-163">Bulk deletions of existing devices</span><span class="sxs-lookup"><span data-stu-id="4684f-163">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="4684f-164">Bulk status changes (enable or disable devices)</span><span class="sxs-lookup"><span data-stu-id="4684f-164">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="4684f-165">Bulk assignment of new device authentication keys</span><span class="sxs-lookup"><span data-stu-id="4684f-165">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="4684f-166">Bulk auto-regeneration of device authentication keys</span><span class="sxs-lookup"><span data-stu-id="4684f-166">Bulk auto-regeneration of device authentication keys</span></span>

<span data-ttu-id="4684f-167">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span><span class="sxs-lookup"><span data-stu-id="4684f-167">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="4684f-168">For example, you can register new devices and delete or update existing devices at the same time.</span><span class="sxs-lookup"><span data-stu-id="4684f-168">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="4684f-169">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span><span class="sxs-lookup"><span data-stu-id="4684f-169">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="4684f-170">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span><span class="sxs-lookup"><span data-stu-id="4684f-170">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="4684f-171">The **importMode** property has the following options:</span><span class="sxs-lookup"><span data-stu-id="4684f-171">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="4684f-172">importMode</span><span class="sxs-lookup"><span data-stu-id="4684f-172">importMode</span></span> | <span data-ttu-id="4684f-173">Description</span><span class="sxs-lookup"><span data-stu-id="4684f-173">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4684f-174">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="4684f-174">**createOrUpdate**</span></span> |<span data-ttu-id="4684f-175">If a device does not exist with the specified **id**, it is newly registered.</span><span class="sxs-lookup"><span data-stu-id="4684f-175">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4684f-176">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span><span class="sxs-lookup"><span data-stu-id="4684f-176">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> |
| <span data-ttu-id="4684f-177">**create**</span><span class="sxs-lookup"><span data-stu-id="4684f-177">**create**</span></span> |<span data-ttu-id="4684f-178">If a device does not exist with the specified **id**, it is newly registered.</span><span class="sxs-lookup"><span data-stu-id="4684f-178">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4684f-179">If the device already exists, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-179">If the device already exists, an error is written to the log file.</span></span> |
| <span data-ttu-id="4684f-180">**update**</span><span class="sxs-lookup"><span data-stu-id="4684f-180">**update**</span></span> |<span data-ttu-id="4684f-181">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span><span class="sxs-lookup"><span data-stu-id="4684f-181">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="4684f-182">If the device does not exist, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-182">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="4684f-183">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4684f-183">**updateIfMatchETag**</span></span> |<span data-ttu-id="4684f-184">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span><span class="sxs-lookup"><span data-stu-id="4684f-184">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="4684f-185">If the device does not exist, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-185">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="4684f-186">If there is an **ETag** mismatch, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-186">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="4684f-187">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4684f-187">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="4684f-188">If a device does not exist with the specified **id**, it is newly registered.</span><span class="sxs-lookup"><span data-stu-id="4684f-188">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4684f-189">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span><span class="sxs-lookup"><span data-stu-id="4684f-189">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="4684f-190">If there is an **ETag** mismatch, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-190">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="4684f-191">**delete**</span><span class="sxs-lookup"><span data-stu-id="4684f-191">**delete**</span></span> |<span data-ttu-id="4684f-192">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span><span class="sxs-lookup"><span data-stu-id="4684f-192">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="4684f-193">If the device does not exist, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-193">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="4684f-194">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4684f-194">**deleteIfMatchETag**</span></span> |<span data-ttu-id="4684f-195">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span><span class="sxs-lookup"><span data-stu-id="4684f-195">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="4684f-196">If the device does not exist, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-196">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="4684f-197">If there is an ETag mismatch, an error is written to the log file.</span><span class="sxs-lookup"><span data-stu-id="4684f-197">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="4684f-198">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span><span class="sxs-lookup"><span data-stu-id="4684f-198">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="4684f-199">Import devices example – bulk device provisioning</span><span class="sxs-lookup"><span data-stu-id="4684f-199">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="4684f-200">The following C# code sample illustrates how to generate multiple device identities that:</span><span class="sxs-lookup"><span data-stu-id="4684f-200">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="4684f-201">Include authentication keys.</span><span class="sxs-lookup"><span data-stu-id="4684f-201">Include authentication keys.</span></span>
* <span data-ttu-id="4684f-202">Write that device information to a block blob.</span><span class="sxs-lookup"><span data-stu-id="4684f-202">Write that device information to a block blob.</span></span>
* <span data-ttu-id="4684f-203">Import the devices into the identity registry.</span><span class="sxs-lookup"><span data-stu-id="4684f-203">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
// Create a new ExportImportDevice
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device to existing list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write this list to the blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using the same blob to add new devices!
// This normally takes 1 minute per 100 devices the normal way
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="4684f-204">Import devices example – bulk deletion</span><span class="sxs-lookup"><span data-stu-id="4684f-204">Import devices example – bulk deletion</span></span>

<span data-ttu-id="4684f-205">The following code sample shows you how to delete the devices you added using the previous code sample:</span><span class="sxs-lookup"><span data-stu-id="4684f-205">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using the same blob to delete all devices!
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}

```

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="4684f-206">Get the container SAS URI</span><span class="sxs-lookup"><span data-stu-id="4684f-206">Get the container SAS URI</span></span>

<span data-ttu-id="4684f-207">The following code sample shows you how to generate a [SAS URI](../storage/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span><span class="sxs-lookup"><span data-stu-id="4684f-207">The following code sample shows you how to generate a [SAS URI](../storage/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}

```

## <a name="next-steps"></a><span data-ttu-id="4684f-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="4684f-208">Next steps</span></span>

<span data-ttu-id="4684f-209">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4684f-209">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="4684f-210">Follow these links to learn more about managing Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="4684f-210">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="4684f-211">[IoT Hub metrics][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="4684f-211">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="4684f-212">[Operations monitoring][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="4684f-212">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="4684f-213">To further explore the capabilities of IoT Hub, see:</span><span class="sxs-lookup"><span data-stu-id="4684f-213">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4684f-214">[IoT Hub developer guide][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="4684f-214">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="4684f-215">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span><span class="sxs-lookup"><span data-stu-id="4684f-215">[Simulating a device with the IoT Gateway SDK][lnk-gateway]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-gateway]: iot-hub-linux-gateway-sdk-simulated-device.md
