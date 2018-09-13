---
title: Export your data in Azure IoT Central | Microsoft Docs
description: How to export data from your Azure IoT Central application
services: iot-central
author: viv-liu
ms.author: viviali
ms.date: 07/3/2018
ms.topic: article
ms.prod: azure-iot-central
manager: peterpr
ms.openlocfilehash: 3ca2bc56c03e5bbabbd9b2f17edc621bdd94b02f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967087"
---
# <a name="export-your-data-in-azure-iot-central"></a><span data-ttu-id="b7177-103">Export your data in Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="b7177-103">Export your data in Azure IoT Central</span></span>

<span data-ttu-id="b7177-104">This article describes how to use the continuous data export feature in Azure IoT Central to periodically export data to your Azure Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="b7177-104">This article describes how to use the continuous data export feature in Azure IoT Central to periodically export data to your Azure Blob storage account.</span></span> <span data-ttu-id="b7177-105">You can export **measurements**, **devices**, and **device templates** to files with the [Apache AVRO](https://avro.apache.org/docs/current/index.html) format.</span><span class="sxs-lookup"><span data-stu-id="b7177-105">You can export **measurements**, **devices**, and **device templates** to files with the [Apache AVRO](https://avro.apache.org/docs/current/index.html) format.</span></span> <span data-ttu-id="b7177-106">The exported data can be used for cold path analytics like training models in Azure Machine Learning or long-term trend analysis in Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="b7177-106">The exported data can be used for cold path analytics like training models in Azure Machine Learning or long-term trend analysis in Microsoft Power BI.</span></span>

> [!Note]
> <span data-ttu-id="b7177-107">When you turn on continuous data export, you get only the data from that moment onward.</span><span class="sxs-lookup"><span data-stu-id="b7177-107">When you turn on continuous data export, you get only the data from that moment onward.</span></span> <span data-ttu-id="b7177-108">Currently, data can't be retrieved for a time when continuous data export was off.</span><span class="sxs-lookup"><span data-stu-id="b7177-108">Currently, data can't be retrieved for a time when continuous data export was off.</span></span> <span data-ttu-id="b7177-109">To retain more historical data, turn on continuous data export early.</span><span class="sxs-lookup"><span data-stu-id="b7177-109">To retain more historical data, turn on continuous data export early.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7177-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7177-110">Prerequisites</span></span>

- <span data-ttu-id="b7177-111">An extended 30-day trial IoT Central application, or a paid application.</span><span class="sxs-lookup"><span data-stu-id="b7177-111">An extended 30-day trial IoT Central application, or a paid application.</span></span>
- <span data-ttu-id="b7177-112">An Azure account with an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b7177-112">An Azure account with an Azure subscription.</span></span>
- <span data-ttu-id="b7177-113">The same Azure account is an administrator in your IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="b7177-113">The same Azure account is an administrator in your IoT Central application.</span></span>
- <span data-ttu-id="b7177-114">The same Azure account has permissions to create a storage account or access an existing storage account in the same Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b7177-114">The same Azure account has permissions to create a storage account or access an existing storage account in the same Azure subscription.</span></span>

## <a name="types-of-data-to-export"></a><span data-ttu-id="b7177-115">Types of data to export</span><span class="sxs-lookup"><span data-stu-id="b7177-115">Types of data to export</span></span>

### <a name="measurements"></a><span data-ttu-id="b7177-116">Measurements</span><span class="sxs-lookup"><span data-stu-id="b7177-116">Measurements</span></span>

<span data-ttu-id="b7177-117">The measurements that devices send are exported to your storage account once per minute.</span><span class="sxs-lookup"><span data-stu-id="b7177-117">The measurements that devices send are exported to your storage account once per minute.</span></span> <span data-ttu-id="b7177-118">The data has all the new messages received by IoT Central from all devices during that time.</span><span class="sxs-lookup"><span data-stu-id="b7177-118">The data has all the new messages received by IoT Central from all devices during that time.</span></span> <span data-ttu-id="b7177-119">The exported AVRO files use the same format as the message files exported by [IoT Hub message routing](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-process-d2c) to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="b7177-119">The exported AVRO files use the same format as the message files exported by [IoT Hub message routing](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-process-d2c) to Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b7177-120">The devices that send the measurements are represented by device IDs (see the following sections).</span><span class="sxs-lookup"><span data-stu-id="b7177-120">The devices that send the measurements are represented by device IDs (see the following sections).</span></span> <span data-ttu-id="b7177-121">To get the names of the devices, export the device snapshots.</span><span class="sxs-lookup"><span data-stu-id="b7177-121">To get the names of the devices, export the device snapshots.</span></span> <span data-ttu-id="b7177-122">Correlate each message record by using the **connectionDeviceId** that matches the device ID.</span><span class="sxs-lookup"><span data-stu-id="b7177-122">Correlate each message record by using the **connectionDeviceId** that matches the device ID.</span></span>

<span data-ttu-id="b7177-123">The following example shows a record in a decoded AVRO file:</span><span class="sxs-lookup"><span data-stu-id="b7177-123">The following example shows a record in a decoded AVRO file:</span></span>

```json
{
    "EnqueuedTimeUtc": "2018-06-11T00:00:08.2250000Z",
    "Properties": {},
    "SystemProperties": {
        "connectionDeviceId": "2383d8ba-c98c-403a-b4d5-8963859643bb",
        "connectionAuthMethod": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\",\"acceptingIpFilterRule\":null}",
        "connectionDeviceGenerationId": "636614021491644195",
        "enqueuedTime": "2018-06-11T00:00:08.2250000Z"
    },
    "Body": "{\"humidity\":80.59100954598546,\"magnetometerX\":0.29451796907056726,\"magnetometerY\":0.5550332126050068,\"magnetometerZ\":-0.04116681874733441,\"connectivity\":\"connected\",\"opened\":\"triggered\"}"
}
```

### <a name="devices"></a><span data-ttu-id="b7177-124">Devices</span><span class="sxs-lookup"><span data-stu-id="b7177-124">Devices</span></span>

<span data-ttu-id="b7177-125">When continuous data export is first turned on, a single snapshot with all devices is exported.</span><span class="sxs-lookup"><span data-stu-id="b7177-125">When continuous data export is first turned on, a single snapshot with all devices is exported.</span></span> <span data-ttu-id="b7177-126">The snapshot includes:</span><span class="sxs-lookup"><span data-stu-id="b7177-126">The snapshot includes:</span></span>
- <span data-ttu-id="b7177-127">Device IDs.</span><span class="sxs-lookup"><span data-stu-id="b7177-127">Device IDs.</span></span>
- <span data-ttu-id="b7177-128">Device names.</span><span class="sxs-lookup"><span data-stu-id="b7177-128">Device names.</span></span>
- <span data-ttu-id="b7177-129">Device template IDs.</span><span class="sxs-lookup"><span data-stu-id="b7177-129">Device template IDs.</span></span>
- <span data-ttu-id="b7177-130">Property values.</span><span class="sxs-lookup"><span data-stu-id="b7177-130">Property values.</span></span>
- <span data-ttu-id="b7177-131">Setting values.</span><span class="sxs-lookup"><span data-stu-id="b7177-131">Setting values.</span></span>

<span data-ttu-id="b7177-132">A new snapshot is written once per minute.</span><span class="sxs-lookup"><span data-stu-id="b7177-132">A new snapshot is written once per minute.</span></span> <span data-ttu-id="b7177-133">The snapshot includes:</span><span class="sxs-lookup"><span data-stu-id="b7177-133">The snapshot includes:</span></span>

- <span data-ttu-id="b7177-134">New devices added since the last snapshot.</span><span class="sxs-lookup"><span data-stu-id="b7177-134">New devices added since the last snapshot.</span></span>
- <span data-ttu-id="b7177-135">Devices with changed property and setting values since the last snapshot.</span><span class="sxs-lookup"><span data-stu-id="b7177-135">Devices with changed property and setting values since the last snapshot.</span></span>

> [!NOTE]
> <span data-ttu-id="b7177-136">Devices deleted since the last snapshot aren't exported.</span><span class="sxs-lookup"><span data-stu-id="b7177-136">Devices deleted since the last snapshot aren't exported.</span></span> <span data-ttu-id="b7177-137">Currently, the snapshots don't have indicators for deleted devices.</span><span class="sxs-lookup"><span data-stu-id="b7177-137">Currently, the snapshots don't have indicators for deleted devices.</span></span>
>
> <span data-ttu-id="b7177-138">The device template that each device belongs to is represented by a device template ID.</span><span class="sxs-lookup"><span data-stu-id="b7177-138">The device template that each device belongs to is represented by a device template ID.</span></span> <span data-ttu-id="b7177-139">To get the name of the device template, export the device template snapshots.</span><span class="sxs-lookup"><span data-stu-id="b7177-139">To get the name of the device template, export the device template snapshots.</span></span>

<span data-ttu-id="b7177-140">Each record in the decoded AVRO file looks like:</span><span class="sxs-lookup"><span data-stu-id="b7177-140">Each record in the decoded AVRO file looks like:</span></span>

```json
{
    "id": "2383d8ba-c98c-403a-b4d5-8963859643bb",
    "name": "Refrigerator 2",
    "simulated": true,
    "deviceTemplate": {
        "id": "c318d580-39fc-4aca-b995-843719821049",
        "version": "1.0.0"
    },
    "properties": {
        "cloud": {
            "location": "New York",
            "maintCon": true,
            "tempThresh": 20
        },
        "device": {
            "lastReboot": "2018-02-09T22:22:47.156Z"
        }
    },
    "settings": {
        "device": {
            "fanSpeed": 0
        }
    }
}
```

### <a name="device-templates"></a><span data-ttu-id="b7177-141">Device templates</span><span class="sxs-lookup"><span data-stu-id="b7177-141">Device templates</span></span>

<span data-ttu-id="b7177-142">When continuous data export is first turned on, a single snapshot with all device templates is exported.</span><span class="sxs-lookup"><span data-stu-id="b7177-142">When continuous data export is first turned on, a single snapshot with all device templates is exported.</span></span> <span data-ttu-id="b7177-143">The snapshot includes:</span><span class="sxs-lookup"><span data-stu-id="b7177-143">The snapshot includes:</span></span> 
- <span data-ttu-id="b7177-144">Device template IDs.</span><span class="sxs-lookup"><span data-stu-id="b7177-144">Device template IDs.</span></span>
- <span data-ttu-id="b7177-145">Measurement data types and min/max values.</span><span class="sxs-lookup"><span data-stu-id="b7177-145">Measurement data types and min/max values.</span></span>
- <span data-ttu-id="b7177-146">Property data types and default values.</span><span class="sxs-lookup"><span data-stu-id="b7177-146">Property data types and default values.</span></span>
- <span data-ttu-id="b7177-147">Setting data types and default values.</span><span class="sxs-lookup"><span data-stu-id="b7177-147">Setting data types and default values.</span></span>

<span data-ttu-id="b7177-148">A new snapshot is written once per minute.</span><span class="sxs-lookup"><span data-stu-id="b7177-148">A new snapshot is written once per minute.</span></span> <span data-ttu-id="b7177-149">The snapshot includes:</span><span class="sxs-lookup"><span data-stu-id="b7177-149">The snapshot includes:</span></span>

- <span data-ttu-id="b7177-150">New device templates added since the last snapshot.</span><span class="sxs-lookup"><span data-stu-id="b7177-150">New device templates added since the last snapshot.</span></span>
- <span data-ttu-id="b7177-151">Device templates with changed measurements, property, and setting definitions since the last snapshot.</span><span class="sxs-lookup"><span data-stu-id="b7177-151">Device templates with changed measurements, property, and setting definitions since the last snapshot.</span></span>

> [!NOTE]
> <span data-ttu-id="b7177-152">Device templates deleted since the last snapshot aren't exported.</span><span class="sxs-lookup"><span data-stu-id="b7177-152">Device templates deleted since the last snapshot aren't exported.</span></span> <span data-ttu-id="b7177-153">Currently, the snapshots don't have indicators for deleted device templates.</span><span class="sxs-lookup"><span data-stu-id="b7177-153">Currently, the snapshots don't have indicators for deleted device templates.</span></span>

<span data-ttu-id="b7177-154">Each record in the decoded AVRO file looks like:</span><span class="sxs-lookup"><span data-stu-id="b7177-154">Each record in the decoded AVRO file looks like:</span></span>

```json
{
    "id": "c318d580-39fc-4aca-b995-843719821049",
    "name": "Refrigerated Vending Machine",
    "version": "1.0.0",
    "measurements": {
        "telemetry": {
            "humidity": {
                "dataType": "double",
                "name": "Humidity"
            },
            "magnetometerX": {
                "dataType": "double",
                "name": "Magnetometer X"
            },
            "magnetometerY": {
                "dataType": "double",
                "name": "Magnetometer Y"
            },
            "magnetometerZ": {
                "dataType": "double",
                "name": "Magnetometer Z"
            }
        },
        "states": {
            "connectivity": {
                "dataType": "enum",
                "name": "Connectivity"
            }
        },
        "events": {
            "opened": {
                "name": "Door Opened",
                "category": "informational"
            }
        }
    },
    "settings": {
        "device": {
            "fanSpeed": {
                "dataType": "double",
                "name": "Fan Speed",
                "initialValue": 0
            }
        }
    },
    "properties": {
        "cloud": {
            "location": {
                "dataType": "string",
                "name": "Location",
                "initialValue": "Seattle"
            },
            "maintCon": {
                "dataType": "boolean",
                "name": "Maintenance Contract",
                "initialValue": true
            },
            "tempThresh": {
                "dataType": "double",
                "name": "Temperature Alert Threshold",
                "initialValue": 30
            }
        },
        "device": {
            "lastReboot": {
                "dataType": "dateTime",
                "name": "Last Reboot"
            }
        }
    }
}
```

## <a name="set-up-continuous-data-export"></a><span data-ttu-id="b7177-155">Set up continuous data export</span><span class="sxs-lookup"><span data-stu-id="b7177-155">Set up continuous data export</span></span>

1. <span data-ttu-id="b7177-156">If you don't have an Azure storage account, [create a new storage account](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7177-156">If you don't have an Azure storage account, [create a new storage account](https://ms.portal.azure.com/#create/Microsoft.StorageAccount-ARM) in the Azure portal.</span></span> <span data-ttu-id="b7177-157">Create the storage account **in the Azure subscription that has your IoT Central application**.</span><span class="sxs-lookup"><span data-stu-id="b7177-157">Create the storage account **in the Azure subscription that has your IoT Central application**.</span></span>
    - <span data-ttu-id="b7177-158">For the account type, choose **General purpose** or **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="b7177-158">For the account type, choose **General purpose** or **Blob storage**.</span></span>
    - <span data-ttu-id="b7177-159">Select the subscription that has your IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="b7177-159">Select the subscription that has your IoT Central application.</span></span> <span data-ttu-id="b7177-160">If you don't see the subscription, you might need to sign in to a different Azure account or request access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="b7177-160">If you don't see the subscription, you might need to sign in to a different Azure account or request access to the subscription.</span></span>
    - <span data-ttu-id="b7177-161">Choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="b7177-161">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="b7177-162">Learn about [how to create a new storage account](https://aka.ms/blobdocscreatestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="b7177-162">Learn about [how to create a new storage account](https://aka.ms/blobdocscreatestorageaccount).</span></span>

2. <span data-ttu-id="b7177-163">Create a container in your storage account to export your IoT Central data.</span><span class="sxs-lookup"><span data-stu-id="b7177-163">Create a container in your storage account to export your IoT Central data.</span></span> <span data-ttu-id="b7177-164">Go to your storage account.</span><span class="sxs-lookup"><span data-stu-id="b7177-164">Go to your storage account.</span></span> <span data-ttu-id="b7177-165">Under **Blob Service**, select **Browse Blobs**.</span><span class="sxs-lookup"><span data-stu-id="b7177-165">Under **Blob Service**, select **Browse Blobs**.</span></span> <span data-ttu-id="b7177-166">Select **Container** to create a new container.</span><span class="sxs-lookup"><span data-stu-id="b7177-166">Select **Container** to create a new container.</span></span>

   ![Create a container](media/howto-export-data/createcontainer.png)

3. <span data-ttu-id="b7177-168">Sign in to your IoT Central application by using the same Azure account.</span><span class="sxs-lookup"><span data-stu-id="b7177-168">Sign in to your IoT Central application by using the same Azure account.</span></span>

4. <span data-ttu-id="b7177-169">Under **Administration**, select **Data Export**.</span><span class="sxs-lookup"><span data-stu-id="b7177-169">Under **Administration**, select **Data Export**.</span></span>

   ![Configure continuous data export](media/howto-export-data/continuousdataexport.PNG)

5. <span data-ttu-id="b7177-171">In the **Storage account** drop-down list box, select your storage account.</span><span class="sxs-lookup"><span data-stu-id="b7177-171">In the **Storage account** drop-down list box, select your storage account.</span></span> <span data-ttu-id="b7177-172">In the **Container** drop-down list box, select your container.</span><span class="sxs-lookup"><span data-stu-id="b7177-172">In the **Container** drop-down list box, select your container.</span></span> <span data-ttu-id="b7177-173">Under **Data to export**, specify each type of data to export by setting the type to **On**.</span><span class="sxs-lookup"><span data-stu-id="b7177-173">Under **Data to export**, specify each type of data to export by setting the type to **On**.</span></span>

6. <span data-ttu-id="b7177-174">To turn on continuous data export, set **Data export** to **On**.</span><span class="sxs-lookup"><span data-stu-id="b7177-174">To turn on continuous data export, set **Data export** to **On**.</span></span> <span data-ttu-id="b7177-175">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="b7177-175">Select **Save**.</span></span>

7. <span data-ttu-id="b7177-176">After a few minutes, your data appears in your storage account.</span><span class="sxs-lookup"><span data-stu-id="b7177-176">After a few minutes, your data appears in your storage account.</span></span> <span data-ttu-id="b7177-177">Browse to your storage account.</span><span class="sxs-lookup"><span data-stu-id="b7177-177">Browse to your storage account.</span></span> <span data-ttu-id="b7177-178">Select **Browse blobs** > your container.</span><span class="sxs-lookup"><span data-stu-id="b7177-178">Select **Browse blobs** > your container.</span></span> <span data-ttu-id="b7177-179">You see three folders for the export data.</span><span class="sxs-lookup"><span data-stu-id="b7177-179">You see three folders for the export data.</span></span> <span data-ttu-id="b7177-180">The default paths for the AVRO files with the export data are:</span><span class="sxs-lookup"><span data-stu-id="b7177-180">The default paths for the AVRO files with the export data are:</span></span>
    - <span data-ttu-id="b7177-181">Messages: {container}/measurements/{hubname}/{YYYY}/{MM}/{dd}/{hh}/{mm}/00.avro</span><span class="sxs-lookup"><span data-stu-id="b7177-181">Messages: {container}/measurements/{hubname}/{YYYY}/{MM}/{dd}/{hh}/{mm}/00.avro</span></span>
    - <span data-ttu-id="b7177-182">Devices: {container}/devices/{hubname}/{YYYY}/{MM}/{dd}/{hh}/{mm}/00.avro</span><span class="sxs-lookup"><span data-stu-id="b7177-182">Devices: {container}/devices/{hubname}/{YYYY}/{MM}/{dd}/{hh}/{mm}/00.avro</span></span>
    - <span data-ttu-id="b7177-183">Device templates: {container}/deviceTemplates/{hubname}/{YYYY}/{MM}/{dd}/{hh}/{mm}/00.avro</span><span class="sxs-lookup"><span data-stu-id="b7177-183">Device templates: {container}/deviceTemplates/{hubname}/{YYYY}/{MM}/{dd}/{hh}/{mm}/00.avro</span></span>

## <a name="read-exported-avro-files"></a><span data-ttu-id="b7177-184">Read exported AVRO files</span><span class="sxs-lookup"><span data-stu-id="b7177-184">Read exported AVRO files</span></span>

<span data-ttu-id="b7177-185">AVRO is a binary format, so the files can't be read in their raw state.</span><span class="sxs-lookup"><span data-stu-id="b7177-185">AVRO is a binary format, so the files can't be read in their raw state.</span></span> <span data-ttu-id="b7177-186">The files can be decoded to JSON format.</span><span class="sxs-lookup"><span data-stu-id="b7177-186">The files can be decoded to JSON format.</span></span> <span data-ttu-id="b7177-187">The following examples show how to parse the measurements, devices, and device templates AVRO files.</span><span class="sxs-lookup"><span data-stu-id="b7177-187">The following examples show how to parse the measurements, devices, and device templates AVRO files.</span></span> <span data-ttu-id="b7177-188">The examples correspond to the examples described in the previous section.</span><span class="sxs-lookup"><span data-stu-id="b7177-188">The examples correspond to the examples described in the previous section.</span></span>

### <a name="read-avro-files-by-using-python"></a><span data-ttu-id="b7177-189">Read AVRO files by using Python</span><span class="sxs-lookup"><span data-stu-id="b7177-189">Read AVRO files by using Python</span></span>

#### <a name="install-pandas-and-the-pandavro-package"></a><span data-ttu-id="b7177-190">Install pandas and the pandavro package</span><span class="sxs-lookup"><span data-stu-id="b7177-190">Install pandas and the pandavro package</span></span>

```python
pip install pandas
pip install pandavro
```

#### <a name="parse-a-measurements-avro-file"></a><span data-ttu-id="b7177-191">Parse a measurements AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-191">Parse a measurements AVRO file</span></span>

```python
import json
import pandavro as pdx
import pandas as pd

def parse(filePath):
    # Pandavro loads the AVRO file into a pandas DataFrame
    # where each record is a single row.
    measurements = pdx.from_avro(filePath)

    # This example creates a new DataFrame and loads a series
    # for each column that's mapped into a column in our new DataFrame.
    transformed = pd.DataFrame()

    # The SystemProperties column contains a dictionary
    # with the device ID located under the connectionDeviceId key.
    transformed["device_id"] = measurements["SystemProperties"].apply(lambda x: x["connectionDeviceId"])

    # The Body column is a series of UTF-8 bytes that is stringified
    # and parsed as JSON. This example pulls the humidity property
    # from each column to get the humidity field.
    transformed["humidity"] = measurements["Body"].apply(lambda x: json.loads(bytes(x).decode('utf-8'))["humidity"])

    # Finally, print the new DataFrame with our device IDs and humidities.
    print(transformed)

```

#### <a name="parse-a-devices-avro-file"></a><span data-ttu-id="b7177-192">Parse a devices AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-192">Parse a devices AVRO file</span></span>

```python
import json
import pandavro as pdx
import pandas as pd

def parse(filePath):
    # Pandavro loads the AVRO file into a pandas DataFrame
    # where each record is a single row.
    devices = pdx.from_avro(filePath)

    # This example creates a new DataFrame and loads a series
    # for each column that's mapped into a column in our new DataFrame.
    transformed = pd.DataFrame()

    # The device ID is available in the id column.
    transformed["device_id"] = devices["id"]

    # The template ID and version are present in a dictionary under
    # the deviceTemplate column.
    transformed["template_id"] = devices["deviceTemplate"].apply(lambda x: x["id"])
    transformed["template_version"] = devices["deviceTemplate"].apply(lambda x: x["version"])

    # The fanSpeed setting value is located in a nested dictionary
    # under the settings column.
    transformed["fan_speed"] = devices["settings"].apply(lambda x: x["device"]["fanSpeed"])

    # Finally, print the new DataFrame with our device and template
    # information, along with the value of the fan speed.
    print(transformed)

```

#### <a name="parse-a-device-templates-avro-file"></a><span data-ttu-id="b7177-193">Parse a device templates AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-193">Parse a device templates AVRO file</span></span>

```python
import json
import pandavro as pdx
import pandas as pd

def parse(filePath):
    # Pandavro loads the AVRO file into a pandas DataFrame
    # where each record is a single row.
    templates = pdx.from_avro(filePath)

    # This example creates a new DataFrame and loads a series
    # for each column that's mapped into a column in our new DataFrame.
    transformed = pd.DataFrame()

    # The template and version are available in the id and version columns.
    transformed["template_id"] = templates["id"]
    transformed["template_version"] = templates["version"]

    # The fanSpeed setting value is located in a nested dictionary
    # under the settings column.
    transformed["fan_speed"] = templates["settings"].apply(lambda x: x["device"]["fanSpeed"])

    # Finally, print the new DataFrame with our device and template
    # information, along with the value of the fan speed.
    print(transformed)
```

### <a name="read-avro-files-by-using-c"></a><span data-ttu-id="b7177-194">Read AVRO files by using C#</span><span class="sxs-lookup"><span data-stu-id="b7177-194">Read AVRO files by using C#</span></span>

#### <a name="install-the-microsofthadoopavro-package"></a><span data-ttu-id="b7177-195">Install the Microsoft.Hadoop.Avro package</span><span class="sxs-lookup"><span data-stu-id="b7177-195">Install the Microsoft.Hadoop.Avro package</span></span>

```csharp
Install-Package Microsoft.Hadoop.Avro -Version 1.5.6
```

#### <a name="parse-a-measurements-avro-file"></a><span data-ttu-id="b7177-196">Parse a measurements AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-196">Parse a measurements AVRO file</span></span>

```csharp
using Microsoft.Hadoop.Avro;
using Microsoft.Hadoop.Avro.Container;
using Newtonsoft.Json;

public static async Task Run(string filePath)
{
    using (var fileStream = File.OpenRead(filePath))
    {
        using (var reader = AvroContainer.CreateGenericReader(fileStream))
        {
            // For one AVRO container, where a container can contain multiple blocks,
            // loop through each block in the container.
            while (reader.MoveNext())
            {
                // Loop through the AVRO records in the block and extract the fields.
                foreach (AvroRecord record in reader.Current.Objects)
                {
                    var systemProperties = record.GetField<IDictionary<string, object>>("SystemProperties");
                    var deviceId = systemProperties["connectionDeviceId"] as string;
                    Console.WriteLine("Device ID: {0}", deviceId);

                    using (var stream = new MemoryStream(record.GetField<byte[]>("Body")))
                    {
                        using (var streamReader = new StreamReader(stream, Encoding.UTF8))
                        {
                            var body = JsonSerializer.Create().Deserialize(streamReader, typeof(IDictionary<string, dynamic>)) as IDictionary<string, dynamic>;
                            var humidity = body["humidity"];
                            Console.WriteLine("Humidity: {0}", humidity);
                        }
                    }
                }
            }
        }
    }
}
```

#### <a name="parse-a-devices-avro-file"></a><span data-ttu-id="b7177-197">Parse a devices AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-197">Parse a devices AVRO file</span></span>

```csharp
using Microsoft.Hadoop.Avro;
using Microsoft.Hadoop.Avro.Container;

public static async Task Run(string filePath)
{
    using (var fileStream = File.OpenRead(filePath))
    {
        using (var reader = AvroContainer.CreateGenericReader(fileStream))
        {
            // For one AVRO container, where a container can contain multiple blocks,
            // loop through each block in the container.
            while (reader.MoveNext())
            {
                // Loop through the AVRO records in the block and extract the fields.
                foreach (AvroRecord record in reader.Current.Objects)
                {
                    // Get the field value directly. You can also yield return
                    // records and make the function IEnumerable<AvroRecord>.
                    var deviceId = record.GetField<string>("id");

                    // The device template information is stored in a sub-record
                    // under the deviceTemplate field.
                    var deviceTemplateRecord = record.GetField<AvroRecord>("deviceTemplate");
                    var templateId = deviceTemplateRecord.GetField<string>("id");
                    var templateVersion = deviceTemplateRecord.GetField<string>("version");

                    // The settings and properties are nested two levels deep.
                    // The first level indicates settings or properties.
                    // The second level indicates the type of setting or property.
                    var settingsRecord = record.GetField<AvroRecord>("settings");
                    var deviceSettingsRecord = settingsRecord.GetField<IDictionary<string, dynamic>>("device");
                    var fanSpeed = deviceSettingsRecord["fanSpeed"];
                    
                    Console.WriteLine(
                        "ID: {0}, Template ID: {1}, Template Version: {2}, Fan Speed: {3}",
                        deviceId,
                        templateId,
                        templateVersion,
                        fanSpeed
                    );
                }
            }
        }
    }
}

```

#### <a name="parse-a-device-templates-avro-file"></a><span data-ttu-id="b7177-198">Parse a device templates AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-198">Parse a device templates AVRO file</span></span>

```csharp
using Microsoft.Hadoop.Avro;
using Microsoft.Hadoop.Avro.Container;

public static async Task Run(string filePath)
{
    using (var fileStream = File.OpenRead(filePath))
    {
        using (var reader = AvroContainer.CreateGenericReader(fileStream))
        {
            // For one AVRO container, where a container can contain multiple blocks,
            // loop through each block in the container.
            while (reader.MoveNext())
            {
                // Loop through the AVRO records in the block and extract the fields.
                foreach (AvroRecord record in reader.Current.Objects)
                {
                    // Get the field value directly. You can also yield return
                    // records and make the function IEnumerable<AvroRecord>.
                    var id = record.GetField<string>("id");
                    var version = record.GetField<string>("version");

                    // The settings and properties are nested two levels deep.
                    // The first level indicates settings or properties.
                    // The second level indicates the type of setting or property.
                    var settingsRecord = record.GetField<AvroRecord>("settings");
                    var deviceSettingsRecord = settingsRecord.GetField<IDictionary<string, dynamic>>("device");
                    var fanSpeed = deviceSettingsRecord["fanSpeed"];
                    
                    Console.WriteLine(
                        "ID: {1}, Version: {2}, Fan Speed: {3}",
                        id,
                        version,
                        fanSpeed
                    );
                }
            }
        }
    }
}
```

### <a name="read-avro-files-by-using-javascript"></a><span data-ttu-id="b7177-199">Read AVRO files by using Javascript</span><span class="sxs-lookup"><span data-stu-id="b7177-199">Read AVRO files by using Javascript</span></span>

#### <a name="install-the-avsc-package"></a><span data-ttu-id="b7177-200">Install the avsc package</span><span class="sxs-lookup"><span data-stu-id="b7177-200">Install the avsc package</span></span>

```javascript
npm install avsc
```

#### <a name="parse-a-measurements-avro-file"></a><span data-ttu-id="b7177-201">Parse a measurements AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-201">Parse a measurements AVRO file</span></span>

```javascript
const avro = require('avsc');

// Read the AVRO file. Parse the device ID and humidity from each record.
async function parse(filePath) {
    const records = await load(filePath);
    for (const record of records) {
        // Fetch the device ID from the system properties.
        const deviceId = record.SystemProperties.connectionDeviceId;

        // Convert the body from a buffer to a string and parse it.
        const body = JSON.parse(record.Body.toString());

        // Get the humidty property from the body.
        const humidity = body.humidity;

        // Log the retrieved device ID and humidity.
        console.log(`Device ID: ${deviceId}`);
        console.log(`Humidity: ${humidity}`);
    }
}

function load(filePath) {
    return new Promise((resolve, reject) => {
        // The file decoder emits each record as a data event on a stream.
        // Collect the records into an array and return them at the end.
        const records = [];
        avro.createFileDecoder(filePath)
            .on('data', record => { records.push(record); })
            .on('end', () => resolve(records))
            .on('error', reject);
    });
}
```

#### <a name="parse-a-devices-avro-file"></a><span data-ttu-id="b7177-202">Parse a devices AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-202">Parse a devices AVRO file</span></span>

```javascript
const avro = require('avsc');

// Read the AVRO file. Parse the device and template identification
// information and the fanSpeed setting for each device record.
async function parse(filePath) {
    const records = await load(filePath);
    for (const record of records) {
        // Fetch the device ID from the id property.
        const deviceId = record.id;

        // Fetch the template ID and version from the deviceTemplate property.
        const deviceTemplateId = record.deviceTemplate.id;
        const deviceTemplateVersion = record.deviceTemplate.version;

        // Get the fanSpeed from the nested device settings property.
        const fanSpeed = record.settings.device.fanSpeed;

        // Log the retrieved device ID and humidity.
        console.log(`ID: ${deviceId}, Template ID: ${deviceTemplateId}, Template Version: ${deviceTemplateVersion}, Fan Speed: ${fanSpeed}`);
    }
}

function load(filePath) {
    return new Promise((resolve, reject) => {
        // The file decoder emits each record as a data event on a stream.
        // Collect the records into an array and return them at the end.
        const records = [];
        avro.createFileDecoder(filePath)
            .on('data', record => { records.push(record); })
            .on('end', () => resolve(records))
            .on('error', reject);
    });
}
```

#### <a name="parse-a-device-templates-avro-file"></a><span data-ttu-id="b7177-203">Parse a device templates AVRO file</span><span class="sxs-lookup"><span data-stu-id="b7177-203">Parse a device templates AVRO file</span></span>

```javascript
const avro = require('avsc');

// Read the AVRO file. Parse the device and template identification
// information and the fanSpeed setting for each device record.
async function parse(filePath) {
    const records = await load(filePath);
    for (const record of records) {
        // Fetch the template ID and version from the id and verison properties.
        const templateId = record.id;
        const templateVersion = record.version;

        // Get the fanSpeed from the nested device settings property.
        const fanSpeed = record.settings.device.fanSpeed;

        // Log the retrieved device id and humidity.
        console.log(`Template ID: ${templateId}, Template Version: ${templateVersion}, Fan Speed: ${fanSpeed}`);
    }
}

function load(filePath) {
    return new Promise((resolve, reject) => {
        // The file decoder emits each record as a data event on a stream.
        // Collect the records into an array and return them at the end.
        const records = [];
        avro.createFileDecoder(filePath)
            .on('data', record => { records.push(record); })
            .on('end', () => resolve(records))
            .on('error', reject);
    });
}
```

## <a name="next-steps"></a><span data-ttu-id="b7177-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7177-204">Next steps</span></span>

<span data-ttu-id="b7177-205">Now that you know how to export your data, continue to the next step:</span><span class="sxs-lookup"><span data-stu-id="b7177-205">Now that you know how to export your data, continue to the next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7177-206">How to visualize your data in Power BI</span><span class="sxs-lookup"><span data-stu-id="b7177-206">How to visualize your data in Power BI</span></span>](howto-connect-powerbi.md)
