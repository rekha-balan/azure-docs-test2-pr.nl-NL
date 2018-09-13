---
title: Azure Event Hubs Archive walkthrough | Microsoft Docs
description: Sample that uses the Azure Python SDK to demonstrate using the Event Hubs Archive feature.
services: event-hubs
documentationcenter: ''
author: djrosanova
manager: timlt
editor: ''
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: darosa;sethm
ms.openlocfilehash: 281663498f51e3580e87294ddfcb35fa1efc1489
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555050"
---
# <a name="event-hubs-archive-walkthrough-python"></a><span data-ttu-id="d8dc8-103">Event Hubs Archive walkthrough: Python</span><span class="sxs-lookup"><span data-stu-id="d8dc8-103">Event Hubs Archive walkthrough: Python</span></span>
<span data-ttu-id="d8dc8-104">Event Hubs Archive is a new feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-104">Event Hubs Archive is a new feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="d8dc8-105">This makes it easy to perform batch processing on real-time streaming data.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-105">This makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="d8dc8-106">This article describes how to use Event Hubs Archive with Python.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-106">This article describes how to use Event Hubs Archive with Python.</span></span> <span data-ttu-id="d8dc8-107">For more information about Event Hubs Archive, see the [overview article](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8dc8-107">For more information about Event Hubs Archive, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="d8dc8-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Archive feature.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Archive feature.</span></span> <span data-ttu-id="d8dc8-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="d8dc8-110">The event hub is configured to use the Archive feature to write this data to blob storage in batches.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-110">The event hub is configured to use the Archive feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="d8dc8-111">The archivereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-111">The archivereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

<span data-ttu-id="d8dc8-112">What will be accomplished</span><span class="sxs-lookup"><span data-stu-id="d8dc8-112">What will be accomplished</span></span>

1. <span data-ttu-id="d8dc8-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="d8dc8-114">Create an Event Hub namespace, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="d8dc8-115">Create an event hub with the Archive feature enabled, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-115">Create an event hub with the Archive feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="d8dc8-116">Send data to the event hub with a Python script.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="d8dc8-117">Read the files from the archive and process them with another Python script.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-117">Read the files from the archive and process them with another Python script.</span></span>

<span data-ttu-id="d8dc8-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8dc8-118">Prerequisites</span></span>

- <span data-ttu-id="d8dc8-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="d8dc8-119">Python 2.7.x</span></span>
- <span data-ttu-id="d8dc8-120">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="d8dc8-120">An Azure subscription</span></span>
- <span data-ttu-id="d8dc8-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="d8dc8-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="d8dc8-122">Create an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="d8dc8-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="d8dc8-123">Log on to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="d8dc8-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="d8dc8-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="d8dc8-125">Complete the fields in the storage account blade and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="d8dc8-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="d8dc8-127">When the **Blob service** blade opens, click **+ Container** at the top.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="d8dc8-128">Name the container **archive**, then close the **Blob service** blade.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-128">Name the container **archive**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="d8dc8-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="d8dc8-130">Save these values to Notepad or some other temporary location.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="d8dc8-131">Create a Python script to send events to your event hub</span><span class="sxs-lookup"><span data-stu-id="d8dc8-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="d8dc8-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="d8dc8-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="d8dc8-133">Create a script called **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="d8dc8-134">This script will send 200 events to your event hub.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-134">This script will send 200 events to your event hub.</span></span> <span data-ttu-id="d8dc8-135">They are simple environmental readings sent in JSON.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="d8dc8-136">Paste the following code into sender.py:</span><span class="sxs-lookup"><span data-stu-id="d8dc8-136">Paste the following code into sender.py:</span></span>
   
   ```python
   import uuid
   import datetime
   import random
   import json
   from azure.servicebus import ServiceBusService
   
   sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
   devices = []
   for x in range(0, 10):
       devices.append(str(uuid.uuid4()))
   
   for y in range(0,20):
       for dev in devices:
           reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
           s = json.dumps(reading)
           sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
       print y
   ```
4. <span data-ttu-id="d8dc8-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-archive-files"></a><span data-ttu-id="d8dc8-138">Create a Python script to read your archive files</span><span class="sxs-lookup"><span data-stu-id="d8dc8-138">Create a Python script to read your archive files</span></span>
1. <span data-ttu-id="d8dc8-139">Fill out the blade and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="d8dc8-140">Create a script called **archivereader.py**.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-140">Create a script called **archivereader.py**.</span></span> <span data-ttu-id="d8dc8-141">This script will read the archive files and create a file per device to write the data only for that device.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-141">This script will read the archive files and create a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="d8dc8-142">Paste the following code into archivereader.py:</span><span class="sxs-lookup"><span data-stu-id="d8dc8-142">Paste the following code into archivereader.py:</span></span>
   
   ```python
   import os
   import string
   import json
   import avro.schema
   from avro.datafile import DataFileReader, DataFileWriter
   from avro.io import DatumReader, DatumWriter
   from azure.storage.blob import BlockBlobService
   
   def processBlob(filename):
       reader = DataFileReader(open(filename, 'rb'), DatumReader())
       dict = {}
       for reading in reader:
           parsed_json = json.loads(reading["Body"])
           if not 'id' in parsed_json:
               return
           if not dict.has_key(parsed_json['id']):
           list = []
           dict[parsed_json['id']] = list
       else:
           list = dict[parsed_json['id']]
           list.append(parsed_json)
       reader.close()
       for device in dict.keys():
           deviceFile = open(device + '.csv', "a")
           for r in dict[device]:
               deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
   def startProcessing(accountName, key, container):
       print 'Processor started using path: ' + os.getcwd()
       block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
       generator = block_blob_service.list_blobs(container)
       for blob in generator:
           if blob.properties.content_length != 0:
               print('Downloaded a non empty blob: ' + blob.name)
               cleanName = string.replace(blob.name, '/', '_')
               block_blob_service.get_blob_to_path(container, blob.name, cleanName)
               processBlob(cleanName)
               os.remove(cleanName)
           block_blob_service.delete_blob(container, blob.name)
   startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'archive')
   ```
4. <span data-ttu-id="d8dc8-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="d8dc8-144">Run the scripts</span><span class="sxs-lookup"><span data-stu-id="d8dc8-144">Run the scripts</span></span>
1. <span data-ttu-id="d8dc8-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span><span class="sxs-lookup"><span data-stu-id="d8dc8-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
   ```
   pip install azure-storage
   pip install azure-servicebus
   pip install avro
   ```
   
   <span data-ttu-id="d8dc8-146">If you have an earlier version of either azure-storage or azure you may need to use the **--upgrade** option</span><span class="sxs-lookup"><span data-stu-id="d8dc8-146">If you have an earlier version of either azure-storage or azure you may need to use the **--upgrade** option</span></span>
   
   <span data-ttu-id="d8dc8-147">You might also need to run the following (not necessary on most systems):</span><span class="sxs-lookup"><span data-stu-id="d8dc8-147">You might also need to run the following (not necessary on most systems):</span></span>
   
   ```
   pip install cryptography
   ```
2. <span data-ttu-id="d8dc8-148">Change your directory to wherever you saved sender.py and archivereader.py, and run this command:</span><span class="sxs-lookup"><span data-stu-id="d8dc8-148">Change your directory to wherever you saved sender.py and archivereader.py, and run this command:</span></span>
   
   ```
   start python sender.py
   ```
   
   <span data-ttu-id="d8dc8-149">This starts a new Python process to run the sender.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-149">This starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="d8dc8-150">Now wait a few minutes for the archive to run.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-150">Now wait a few minutes for the archive to run.</span></span> <span data-ttu-id="d8dc8-151">Then type the following command into your original command window:</span><span class="sxs-lookup"><span data-stu-id="d8dc8-151">Then type the following command into your original command window:</span></span>
   
    ```
    python archivereader.py
    ```

    <span data-ttu-id="d8dc8-152">This archive processor uses the local directory to download all the blobs from the storage account/container.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-152">This archive processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="d8dc8-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8dc8-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="d8dc8-154">Next steps</span></span>
<span data-ttu-id="d8dc8-155">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="d8dc8-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="d8dc8-156">[Overview of Event Hubs Archive][Overview of Event Hubs Archive]</span><span class="sxs-lookup"><span data-stu-id="d8dc8-156">[Overview of Event Hubs Archive][Overview of Event Hubs Archive]</span></span>
* <span data-ttu-id="d8dc8-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="d8dc8-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="d8dc8-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span><span class="sxs-lookup"><span data-stu-id="d8dc8-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="d8dc8-159">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="d8dc8-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Archive]: event-hubs-archive-overview.md
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]: ../storage/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3

