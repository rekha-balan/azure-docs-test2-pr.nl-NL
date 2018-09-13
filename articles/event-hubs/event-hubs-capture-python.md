---
title: Azure Event Hubs Capture walkthrough | Microsoft Docs
description: Sample that uses the Azure Python SDK to demonstrate using the Event Hubs Capture feature.
services: event-hubs
documentationcenter: ''
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: 76102e1238346cbbb8f5159d2ffcd94c788c16d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867347"
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="cab81-103">Event Hubs Capture walkthrough: Python</span><span class="sxs-lookup"><span data-stu-id="cab81-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="cab81-104">Capture is a feature of Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="cab81-104">Capture is a feature of Azure Event Hubs.</span></span> <span data-ttu-id="cab81-105">You can use it to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span><span class="sxs-lookup"><span data-stu-id="cab81-105">You can use it to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="cab81-106">This capability makes it easy to perform batch processing on real-time streaming data.</span><span class="sxs-lookup"><span data-stu-id="cab81-106">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="cab81-107">This article describes how to use Event Hubs Capture with Python.</span><span class="sxs-lookup"><span data-stu-id="cab81-107">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="cab81-108">For more information about Event Hubs Capture, see the [overview article](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cab81-108">For more information about Event Hubs Capture, see the [overview article](event-hubs-capture-overview.md).</span></span>

<span data-ttu-id="cab81-109">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span><span class="sxs-lookup"><span data-stu-id="cab81-109">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="cab81-110">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span><span class="sxs-lookup"><span data-stu-id="cab81-110">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="cab81-111">The event hub is configured to use the Capture feature to write this data to Blob storage in batches.</span><span class="sxs-lookup"><span data-stu-id="cab81-111">The event hub is configured to use the Capture feature to write this data to Blob storage in batches.</span></span> <span data-ttu-id="cab81-112">The capturereader.py app reads these blobs and creates an append file per device.</span><span class="sxs-lookup"><span data-stu-id="cab81-112">The capturereader.py app reads these blobs and creates an append file per device.</span></span> <span data-ttu-id="cab81-113">The app then writes the data into .csv files.</span><span class="sxs-lookup"><span data-stu-id="cab81-113">The app then writes the data into .csv files.</span></span>

## <a name="what-youll-accomplish"></a><span data-ttu-id="cab81-114">What you'll accomplish</span><span class="sxs-lookup"><span data-stu-id="cab81-114">What you'll accomplish</span></span>

1. <span data-ttu-id="cab81-115">Create an Azure Blob storage account and a blob container within it, by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cab81-115">Create an Azure Blob storage account and a blob container within it, by using the Azure portal.</span></span>
2. <span data-ttu-id="cab81-116">Create an Event Hubs namespace, by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cab81-116">Create an Event Hubs namespace, by using the Azure portal.</span></span>
3. <span data-ttu-id="cab81-117">Create an event hub with the Capture feature enabled, by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cab81-117">Create an event hub with the Capture feature enabled, by using the Azure portal.</span></span>
4. <span data-ttu-id="cab81-118">Send data to the event hub by using a Python script.</span><span class="sxs-lookup"><span data-stu-id="cab81-118">Send data to the event hub by using a Python script.</span></span>
5. <span data-ttu-id="cab81-119">Read the files from the capture and process them by using another Python script.</span><span class="sxs-lookup"><span data-stu-id="cab81-119">Read the files from the capture and process them by using another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cab81-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cab81-120">Prerequisites</span></span>

- <span data-ttu-id="cab81-121">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="cab81-121">Python 2.7.x</span></span>
- <span data-ttu-id="cab81-122">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="cab81-122">An Azure subscription</span></span>
- <span data-ttu-id="cab81-123">An active [Event Hubs namespace and event hub](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="cab81-123">An active [Event Hubs namespace and event hub](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="cab81-124">Create an Azure Blob storage account</span><span class="sxs-lookup"><span data-stu-id="cab81-124">Create an Azure Blob storage account</span></span>
1. <span data-ttu-id="cab81-125">Sign in to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="cab81-125">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="cab81-126">In the left pane of the portal, select **New** > **Storage** > **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="cab81-126">In the left pane of the portal, select **New** > **Storage** > **Storage Account**.</span></span>
3. <span data-ttu-id="cab81-127">Complete the selections in the **Create storage account** pane, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cab81-127">Complete the selections in the **Create storage account** pane, and then select **Create**.</span></span>
   
   !["Create storage account" pane][1]
4. <span data-ttu-id="cab81-129">After you see the **Deployments Succeeded** message, select the name of the new storage account and in the **Essentials** pane, and then select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="cab81-129">After you see the **Deployments Succeeded** message, select the name of the new storage account and in the **Essentials** pane, and then select **Blobs**.</span></span> <span data-ttu-id="cab81-130">When the **Blob service** pane opens, select **+ Container** at the top.</span><span class="sxs-lookup"><span data-stu-id="cab81-130">When the **Blob service** pane opens, select **+ Container** at the top.</span></span> <span data-ttu-id="cab81-131">Name the container **capture**, and then close the **Blob service** pane.</span><span class="sxs-lookup"><span data-stu-id="cab81-131">Name the container **capture**, and then close the **Blob service** pane.</span></span>
5. <span data-ttu-id="cab81-132">Select **Access keys** in the left pane and copy the name of the storage account and the value of **key1**.</span><span class="sxs-lookup"><span data-stu-id="cab81-132">Select **Access keys** in the left pane and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="cab81-133">Save these values to Notepad or some other temporary location.</span><span class="sxs-lookup"><span data-stu-id="cab81-133">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="cab81-134">Create a Python script to send events to your event hub</span><span class="sxs-lookup"><span data-stu-id="cab81-134">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="cab81-135">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="cab81-135">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="cab81-136">Create a script called **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="cab81-136">Create a script called **sender.py**.</span></span> <span data-ttu-id="cab81-137">This script sends 200 events to your event hub.</span><span class="sxs-lookup"><span data-stu-id="cab81-137">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="cab81-138">They are simple environmental readings sent in JSON.</span><span class="sxs-lookup"><span data-stu-id="cab81-138">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="cab81-139">Paste the following code into sender.py:</span><span class="sxs-lookup"><span data-stu-id="cab81-139">Paste the following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="cab81-140">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="cab81-140">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="cab81-141">Create a Python script to read your Capture files</span><span class="sxs-lookup"><span data-stu-id="cab81-141">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="cab81-142">Fill out the pane and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cab81-142">Fill out the pane and select **Create**.</span></span>
2. <span data-ttu-id="cab81-143">Create a script called **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="cab81-143">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="cab81-144">This script reads the captured files and creates a file per device to write the data only for that device.</span><span class="sxs-lookup"><span data-stu-id="cab81-144">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="cab81-145">Paste the following code into capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="cab81-145">Paste the following code into capturereader.py:</span></span>
   
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
           #content_length == 508 is an empty file, so only process content_length > 508 (skip empty files)
           if blob.properties.content_length > 508:
               print('Downloaded a non empty blob: ' + blob.name)
               cleanName = string.replace(blob.name, '/', '_')
               block_blob_service.get_blob_to_path(container, blob.name, cleanName)
               processBlob(cleanName)
               os.remove(cleanName)
           block_blob_service.delete_blob(container, blob.name)
   startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
   ```
4. <span data-ttu-id="cab81-146">Paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="cab81-146">Paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="cab81-147">Run the scripts</span><span class="sxs-lookup"><span data-stu-id="cab81-147">Run the scripts</span></span>
1. <span data-ttu-id="cab81-148">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span><span class="sxs-lookup"><span data-stu-id="cab81-148">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
   ```
   pip install azure-storage
   pip install azure-servicebus
   pip install avro
   ```
   
   <span data-ttu-id="cab81-149">If you have an earlier version of either **azure-storage** or **azure**, you might need to use the **--upgrade** option.</span><span class="sxs-lookup"><span data-stu-id="cab81-149">If you have an earlier version of either **azure-storage** or **azure**, you might need to use the **--upgrade** option.</span></span>
   
   <span data-ttu-id="cab81-150">You might also need to run the following command (not necessary on most systems):</span><span class="sxs-lookup"><span data-stu-id="cab81-150">You might also need to run the following command (not necessary on most systems):</span></span>
   
   ```
   pip install cryptography
   ```
2. <span data-ttu-id="cab81-151">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span><span class="sxs-lookup"><span data-stu-id="cab81-151">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
   ```
   start python sender.py
   ```
   
   <span data-ttu-id="cab81-152">This command starts a new Python process to run the sender.</span><span class="sxs-lookup"><span data-stu-id="cab81-152">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="cab81-153">Wait a few minutes for the capture to run.</span><span class="sxs-lookup"><span data-stu-id="cab81-153">Wait a few minutes for the capture to run.</span></span> <span data-ttu-id="cab81-154">Then type the following command into your original command window:</span><span class="sxs-lookup"><span data-stu-id="cab81-154">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="cab81-155">This capture processor uses the local directory to download all the blobs from the storage account/container.</span><span class="sxs-lookup"><span data-stu-id="cab81-155">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="cab81-156">It processes any that are not empty, and it writes the results as .csv files into the local directory.</span><span class="sxs-lookup"><span data-stu-id="cab81-156">It processes any that are not empty, and it writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cab81-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="cab81-157">Next steps</span></span>

<span data-ttu-id="cab81-158">You can learn more about Event Hubs by using the following links:</span><span class="sxs-lookup"><span data-stu-id="cab81-158">You can learn more about Event Hubs by using the following links:</span></span>

* <span data-ttu-id="cab81-159">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="cab81-159">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* [<span data-ttu-id="cab81-160">Sample applications that use Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cab81-160">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
* <span data-ttu-id="cab81-161">[Event Hubs overview][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="cab81-161">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-capture-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
