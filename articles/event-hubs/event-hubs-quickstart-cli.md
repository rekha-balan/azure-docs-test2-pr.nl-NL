---
title: Azure Quickstart - Create an event hub using Azure CLI | Microsoft Docs
description: This quickstart describes how to create an event hub using Azure CLI and then send and receive events using Java.
services: event-hubs
author: ShubhaVijayasarathy
manager: timlt
ms.service: event-hubs
ms.devlang: java
ms.topic: quickstart
ms.custom: mvc
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: dfaed2222d16564cd1f573b4e9038b7019780944
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871526"
---
# <a name="quickstart-create-an-event-hub-using-azure-cli"></a><span data-ttu-id="2d249-103">Quickstart: Create an event hub using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2d249-103">Quickstart: Create an event hub using Azure CLI</span></span>

<span data-ttu-id="2d249-104">Azure Event Hubs is a highly scalable data streaming platform and ingestion service capable of receiving and processing millions of events per second.</span><span class="sxs-lookup"><span data-stu-id="2d249-104">Azure Event Hubs is a highly scalable data streaming platform and ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="2d249-105">This quickstart shows how to create Event Hubs resources using Azure CLI, then send and receive event streams from an event hub using Java code.</span><span class="sxs-lookup"><span data-stu-id="2d249-105">This quickstart shows how to create Event Hubs resources using Azure CLI, then send and receive event streams from an event hub using Java code.</span></span>

<span data-ttu-id="2d249-106">To complete this quickstart, you need an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2d249-106">To complete this quickstart, you need an Azure subscription.</span></span> <span data-ttu-id="2d249-107">If you don't have one, [create a free account][] before you begin.</span><span class="sxs-lookup"><span data-stu-id="2d249-107">If you don't have one, [create a free account][] before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d249-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d249-108">Prerequisites</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2d249-109">If you choose to install and use Azure CLI locally, this tutorial requires that you are running Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="2d249-109">If you choose to install and use Azure CLI locally, this tutorial requires that you are running Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2d249-110">Run `az --version` to check your version.</span><span class="sxs-lookup"><span data-stu-id="2d249-110">Run `az --version` to check your version.</span></span> <span data-ttu-id="2d249-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2d249-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="log-on-to-azure"></a><span data-ttu-id="2d249-112">Log on to Azure</span><span class="sxs-lookup"><span data-stu-id="2d249-112">Log on to Azure</span></span>

<span data-ttu-id="2d249-113">The following steps are not required if you're running commands in Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="2d249-113">The following steps are not required if you're running commands in Cloud Shell.</span></span> <span data-ttu-id="2d249-114">If you're running the CLI locally, perform the following steps to log on to Azure and set your current subscription:</span><span class="sxs-lookup"><span data-stu-id="2d249-114">If you're running the CLI locally, perform the following steps to log on to Azure and set your current subscription:</span></span>

<span data-ttu-id="2d249-115">Run the following command to log on to Azure:</span><span class="sxs-lookup"><span data-stu-id="2d249-115">Run the following command to log on to Azure:</span></span>

```azurecli-interactive
az login
```

<span data-ttu-id="2d249-116">Set the current subscription context.</span><span class="sxs-lookup"><span data-stu-id="2d249-116">Set the current subscription context.</span></span> <span data-ttu-id="2d249-117">Replace `MyAzureSub` with the name of the Azure subscription you want to use:</span><span class="sxs-lookup"><span data-stu-id="2d249-117">Replace `MyAzureSub` with the name of the Azure subscription you want to use:</span></span>

```azurecli-interactive
az account set --subscription MyAzureSub
``` 

## <a name="provision-resources"></a><span data-ttu-id="2d249-118">Provision resources</span><span class="sxs-lookup"><span data-stu-id="2d249-118">Provision resources</span></span>

<span data-ttu-id="2d249-119">Issue the following commands to provision Event Hubs resources.</span><span class="sxs-lookup"><span data-stu-id="2d249-119">Issue the following commands to provision Event Hubs resources.</span></span> <span data-ttu-id="2d249-120">Be sure to replace the placeholders `myResourceGroup`, `namespaceName`, `eventHubName`, and `storageAccountName` with the appropriate values:</span><span class="sxs-lookup"><span data-stu-id="2d249-120">Be sure to replace the placeholders `myResourceGroup`, `namespaceName`, `eventHubName`, and `storageAccountName` with the appropriate values:</span></span>

```azurecli-interactive
# Create a resource group
az group create --name myResourceGroup --location eastus

# Create an Event Hubs namespace
az eventhubs namespace create --name namespaceName --resource-group myResourceGroup -l eastus2

# Create an event hub
az eventhubs eventhub create --name eventHubName --resource-group myResourceGroup --namespace-name namespaceName

# Create a general purpose standard storage account
az storage account create --name storageAccountName --resource-group myResourceGroup --location eastus2 --sku Standard_RAGRS --encryption blob

# List the storage account access keys
az storage account keys list --resource-group myResourceGroup --account-name storageAccountName

# Get namespace connection string
az eventhubs namespace authorization-rule keys list --resource-group myResourceGroup --namespace-name namespaceName --name RootManageSharedAccessKey
```

<span data-ttu-id="2d249-121">Copy and paste the connection string to a temporary location, such as Notepad, to use later.</span><span class="sxs-lookup"><span data-stu-id="2d249-121">Copy and paste the connection string to a temporary location, such as Notepad, to use later.</span></span>

## <a name="stream-into-event-hubs"></a><span data-ttu-id="2d249-122">Stream into Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2d249-122">Stream into Event Hubs</span></span>

<span data-ttu-id="2d249-123">The next step is to download the sample code that streams events to an event hub, and receives those events using the Event Processor Host.</span><span class="sxs-lookup"><span data-stu-id="2d249-123">The next step is to download the sample code that streams events to an event hub, and receives those events using the Event Processor Host.</span></span> <span data-ttu-id="2d249-124">First, send the messages:</span><span class="sxs-lookup"><span data-stu-id="2d249-124">First, send the messages:</span></span>

<span data-ttu-id="2d249-125">Clone the [Event Hubs GitHub repo](https://github.com/Azure/azure-event-hubs) by issuing the following command:</span><span class="sxs-lookup"><span data-stu-id="2d249-125">Clone the [Event Hubs GitHub repo](https://github.com/Azure/azure-event-hubs) by issuing the following command:</span></span>

```bash
git clone https://github.com/Azure/azure-event-hubs.git
```

<span data-ttu-id="2d249-126">Navigate to the **SimpleSend** folder: `\azure-event-hubs\samples\Java\Basic\SimpleSend\src\main\java\com\microsoft\azure\eventhubs\samples\SimpleSend`.</span><span class="sxs-lookup"><span data-stu-id="2d249-126">Navigate to the **SimpleSend** folder: `\azure-event-hubs\samples\Java\Basic\SimpleSend\src\main\java\com\microsoft\azure\eventhubs\samples\SimpleSend`.</span></span> <span data-ttu-id="2d249-127">Open the SimpleSend.java file and replace the `"Your Event Hubs namaspace name"` string with the Event Hubs namespace you obtained in the "Create an Event Hubs namespace" section of this article.</span><span class="sxs-lookup"><span data-stu-id="2d249-127">Open the SimpleSend.java file and replace the `"Your Event Hubs namaspace name"` string with the Event Hubs namespace you obtained in the "Create an Event Hubs namespace" section of this article.</span></span>

<span data-ttu-id="2d249-128">Replace `"Your event hub"` with the name of the event hub you created within that namespace, and `"Your policy name"` with the name of the Shared access policy for the namespace.</span><span class="sxs-lookup"><span data-stu-id="2d249-128">Replace `"Your event hub"` with the name of the event hub you created within that namespace, and `"Your policy name"` with the name of the Shared access policy for the namespace.</span></span> <span data-ttu-id="2d249-129">Unless you created a new policy, the default is **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2d249-129">Unless you created a new policy, the default is **RootManageSharedAccessKey**.</span></span> 

<span data-ttu-id="2d249-130">Finally, replace `"Your primary SAS key"` with the value of the SAS key for the policy in the previous step.</span><span class="sxs-lookup"><span data-stu-id="2d249-130">Finally, replace `"Your primary SAS key"` with the value of the SAS key for the policy in the previous step.</span></span>

### <a name="build-the-application"></a><span data-ttu-id="2d249-131">Build the application</span><span class="sxs-lookup"><span data-stu-id="2d249-131">Build the application</span></span> 

<span data-ttu-id="2d249-132">Navigate back to the `\azure-event-hubs\samples\Java\Basic\SimpleSend` folder, and issue the following build command:</span><span class="sxs-lookup"><span data-stu-id="2d249-132">Navigate back to the `\azure-event-hubs\samples\Java\Basic\SimpleSend` folder, and issue the following build command:</span></span>

```shell
mvn clean package -DskipTests
```

### <a name="receive"></a><span data-ttu-id="2d249-133">Receive</span><span class="sxs-lookup"><span data-stu-id="2d249-133">Receive</span></span>

<span data-ttu-id="2d249-134">Now download the Event Processor Host sample, which receives the messages you just sent.</span><span class="sxs-lookup"><span data-stu-id="2d249-134">Now download the Event Processor Host sample, which receives the messages you just sent.</span></span> <span data-ttu-id="2d249-135">Navigate to the **EventProcessorSample** folder: `\azure-event-hubs\samples\Java\Basic\EventProcessorSample\src\main\java\com\microsoft\azure\eventhubs\samples\eventprocessorsample`.</span><span class="sxs-lookup"><span data-stu-id="2d249-135">Navigate to the **EventProcessorSample** folder: `\azure-event-hubs\samples\Java\Basic\EventProcessorSample\src\main\java\com\microsoft\azure\eventhubs\samples\eventprocessorsample`.</span></span>

<span data-ttu-id="2d249-136">In the EventProcessorSample.java file, replace the `----EventHubsNamespaceName-----` value with the Event Hubs namespace you obtained in the "Create an Event Hubs namespace" section of this article.</span><span class="sxs-lookup"><span data-stu-id="2d249-136">In the EventProcessorSample.java file, replace the `----EventHubsNamespaceName-----` value with the Event Hubs namespace you obtained in the "Create an Event Hubs namespace" section of this article.</span></span> 

<span data-ttu-id="2d249-137">Replace the other string values in this file: replace `----EventHubName-----` with the name of the event hub you created within that namespace, and `-----SharedAccessSignatureKeyName-----` with the name of the Shared access policy for the namespace.</span><span class="sxs-lookup"><span data-stu-id="2d249-137">Replace the other string values in this file: replace `----EventHubName-----` with the name of the event hub you created within that namespace, and `-----SharedAccessSignatureKeyName-----` with the name of the Shared access policy for the namespace.</span></span> <span data-ttu-id="2d249-138">Unless you created a new policy, the default is **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2d249-138">Unless you created a new policy, the default is **RootManageSharedAccessKey**.</span></span>

<span data-ttu-id="2d249-139">Replace `---SharedAccessSignatureKey----` with the value of the SAS key for the policy in the previous step, replace `----AzureStorageConnectionString----` with the connection string for the storage account you created, and `----StorageContainerName----` with the name of the container under the storage account you created.</span><span class="sxs-lookup"><span data-stu-id="2d249-139">Replace `---SharedAccessSignatureKey----` with the value of the SAS key for the policy in the previous step, replace `----AzureStorageConnectionString----` with the connection string for the storage account you created, and `----StorageContainerName----` with the name of the container under the storage account you created.</span></span> 

<span data-ttu-id="2d249-140">Finally, replace `----HostNamePrefix----` with the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="2d249-140">Finally, replace `----HostNamePrefix----` with the name of the storage account.</span></span>

### <a name="build-the-receiver"></a><span data-ttu-id="2d249-141">Build the receiver</span><span class="sxs-lookup"><span data-stu-id="2d249-141">Build the receiver</span></span> 

<span data-ttu-id="2d249-142">To build the receiving application, navigate to the `\azure-event-hubs\samples\Java\Basic\EventProcessorSample` folder, and issue the following command:</span><span class="sxs-lookup"><span data-stu-id="2d249-142">To build the receiving application, navigate to the `\azure-event-hubs\samples\Java\Basic\EventProcessorSample` folder, and issue the following command:</span></span>

```shell
mvn clean package -DskipTests
```

### <a name="run-the-apps"></a><span data-ttu-id="2d249-143">Run the apps</span><span class="sxs-lookup"><span data-stu-id="2d249-143">Run the apps</span></span>

<span data-ttu-id="2d249-144">If the builds completed successfully, you are ready to send and receive events.</span><span class="sxs-lookup"><span data-stu-id="2d249-144">If the builds completed successfully, you are ready to send and receive events.</span></span> <span data-ttu-id="2d249-145">First, run the **SimpleSend** application and observe events being sent.</span><span class="sxs-lookup"><span data-stu-id="2d249-145">First, run the **SimpleSend** application and observe events being sent.</span></span> <span data-ttu-id="2d249-146">To run the program, navigate to the `\azure-event-hubs\samples\Java\Basic\SimpleSend` folder, and issue the following command:</span><span class="sxs-lookup"><span data-stu-id="2d249-146">To run the program, navigate to the `\azure-event-hubs\samples\Java\Basic\SimpleSend` folder, and issue the following command:</span></span>

```shell
java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
```

<span data-ttu-id="2d249-147">Next, run the **EventProcessorSample** app, and observe the events being received.</span><span class="sxs-lookup"><span data-stu-id="2d249-147">Next, run the **EventProcessorSample** app, and observe the events being received.</span></span> <span data-ttu-id="2d249-148">To run the program, navigate to the `\azure-event-hubs\samples\Java\Basic\EventProcessorSample` folder, and issue the following command:</span><span class="sxs-lookup"><span data-stu-id="2d249-148">To run the program, navigate to the `\azure-event-hubs\samples\Java\Basic\EventProcessorSample` folder, and issue the following command:</span></span>
   
```shell
java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
```

<span data-ttu-id="2d249-149">After running both programs, you can check the Azure portal overview page for the event hub to see the incoming and outgoing message count:</span><span class="sxs-lookup"><span data-stu-id="2d249-149">After running both programs, you can check the Azure portal overview page for the event hub to see the incoming and outgoing message count:</span></span>

![send and receive](./media/event-hubs-quickstart-cli/ephjava.png)

## <a name="clean-up-resources"></a><span data-ttu-id="2d249-151">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="2d249-151">Clean up resources</span></span>

<span data-ttu-id="2d249-152">Run the following command to remove the resource group, namespace, storage account, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="2d249-152">Run the following command to remove the resource group, namespace, storage account, and all related resources.</span></span> <span data-ttu-id="2d249-153">Replace `myResourceGroup` with the name of the resource group you created:</span><span class="sxs-lookup"><span data-stu-id="2d249-153">Replace `myResourceGroup` with the name of the resource group you created:</span></span>

```azurecli
az group delete --resource-group myResourceGroup
```

## <a name="understand-the-sample-code"></a><span data-ttu-id="2d249-154">Understand the sample code</span><span class="sxs-lookup"><span data-stu-id="2d249-154">Understand the sample code</span></span>

<span data-ttu-id="2d249-155">This section contains more details about what the sample code does.</span><span class="sxs-lookup"><span data-stu-id="2d249-155">This section contains more details about what the sample code does.</span></span>

### <a name="send"></a><span data-ttu-id="2d249-156">Send</span><span class="sxs-lookup"><span data-stu-id="2d249-156">Send</span></span>

<span data-ttu-id="2d249-157">In the SimpleSend.java file, most of the work is done in the main() method.</span><span class="sxs-lookup"><span data-stu-id="2d249-157">In the SimpleSend.java file, most of the work is done in the main() method.</span></span> <span data-ttu-id="2d249-158">First, the code uses a `ConnectionStringBuilder` instance to construct the connection string using the user-defined values for the namespace name, event hub name, SAS key name, and the SAS key itself:</span><span class="sxs-lookup"><span data-stu-id="2d249-158">First, the code uses a `ConnectionStringBuilder` instance to construct the connection string using the user-defined values for the namespace name, event hub name, SAS key name, and the SAS key itself:</span></span>

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
        .setNamespaceName("Your Event Hubs namespace name")
        .setEventHubName("Your event hub")
        .setSasKeyName("Your policy name")
        .setSasKey("Your primary SAS key");
```

<span data-ttu-id="2d249-159">The Java object containing the event payload is then converted to Json:</span><span class="sxs-lookup"><span data-stu-id="2d249-159">The Java object containing the event payload is then converted to Json:</span></span>

```java
final Gson gson = new GsonBuilder().create();

final PayloadEvent payload = new PayloadEvent(1);
byte[] payloadBytes = gson.toJson(payload).getBytes(Charset.defaultCharset());
EventData sendEvent = EventData.create(payloadBytes);  
```

<span data-ttu-id="2d249-160">The Event Hubs client is created in this line of code:</span><span class="sxs-lookup"><span data-stu-id="2d249-160">The Event Hubs client is created in this line of code:</span></span>

```java
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString(), executorService);
```

<span data-ttu-id="2d249-161">The try/finally block sends one event round robin to a non-specified partition:</span><span class="sxs-lookup"><span data-stu-id="2d249-161">The try/finally block sends one event round robin to a non-specified partition:</span></span>

```java
try {
    for (int i = 0; i < 100; i++) {

        String payload = "Message " + Integer.toString(i);
        //PayloadEvent payload = new PayloadEvent(i);
        byte[] payloadBytes = gson.toJson(payload).getBytes(Charset.defaultCharset());
        EventData sendEvent = EventData.create(payloadBytes);

        // Send - not tied to any partition
        // Event Hubs service will round-robin the events across all EventHubs partitions.
        // This is the recommended & most reliable way to send to EventHubs.
        ehClient.sendSync(sendEvent);
    }

    System.out.println(Instant.now() + ": Send Complete...");
    System.in.read();
} finally {
    ehClient.closeSync();
    executorService.shutdown();
}
```

### <a name="receive"></a><span data-ttu-id="2d249-162">Receive</span><span class="sxs-lookup"><span data-stu-id="2d249-162">Receive</span></span> 

<span data-ttu-id="2d249-163">The receive operation occurs in the EventProcessorSample.java file.</span><span class="sxs-lookup"><span data-stu-id="2d249-163">The receive operation occurs in the EventProcessorSample.java file.</span></span> <span data-ttu-id="2d249-164">First, it declares constants to hold the Event Hubs namespace name and other credentials:</span><span class="sxs-lookup"><span data-stu-id="2d249-164">First, it declares constants to hold the Event Hubs namespace name and other credentials:</span></span>

```java
String consumerGroupName = "$Default";
String namespaceName = "----NamespaceName----";
String eventHubName = "----EventHubName----";
String sasKeyName = "----SharedAccessSignatureKeyName----";
String sasKey = "----SharedAccessSignatureKey----";
String storageConnectionString = "----AzureStorageConnectionString----";
String storageContainerName = "----StorageContainerName----";
String hostNamePrefix = "----HostNamePrefix----";
```

<span data-ttu-id="2d249-165">Similar to the SimpleSend program, the code then creates a ConnectionStringBuilder instance to construct the connection string:</span><span class="sxs-lookup"><span data-stu-id="2d249-165">Similar to the SimpleSend program, the code then creates a ConnectionStringBuilder instance to construct the connection string:</span></span>

```java
ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder()
    .setNamespaceName(namespaceName)
    .setEventHubName(eventHubName)
    .setSasKeyName(sasKeyName)
    .setSasKey(sasKey);
```

<span data-ttu-id="2d249-166">The *Event Processor Host* is a class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span><span class="sxs-lookup"><span data-stu-id="2d249-166">The *Event Processor Host* is a class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="2d249-167">The code now creates an instance of `EventProcessorHost`:</span><span class="sxs-lookup"><span data-stu-id="2d249-167">The code now creates an instance of `EventProcessorHost`:</span></span>

```java
EventProcessorHost host = new EventProcessorHost(
    EventProcessorHost.createHostName(hostNamePrefix),
    eventHubName,
    consumerGroupName,
    eventHubConnectionString.toString(),
    storageConnectionString,
    storageContainerName);
```

<span data-ttu-id="2d249-168">After declaring some error handling code, the app then defines the `EventProcessor` class, an implementation of the `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="2d249-168">After declaring some error handling code, the app then defines the `EventProcessor` class, an implementation of the `IEventProcessor` interface.</span></span> <span data-ttu-id="2d249-169">This class processes the received events:</span><span class="sxs-lookup"><span data-stu-id="2d249-169">This class processes the received events:</span></span>

```java
public static class EventProcessor implements IEventProcessor
{
    private int checkpointBatchingCount = 0;
    ...
```

<span data-ttu-id="2d249-170">The `onEvents()` method is called when events are received on this partition of the event hub:</span><span class="sxs-lookup"><span data-stu-id="2d249-170">The `onEvents()` method is called when events are received on this partition of the event hub:</span></span>

```java
@Override
public void onEvents(PartitionContext context, Iterable<EventData> events) throws Exception
{
    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got event batch");
    int eventCount = 0;
    for (EventData data : events)
    {
        try
        {
         System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBytes(), "UTF8"));
             eventCount++;
                
         // Checkpointing persists the current position in the event stream for this partition and means that the next
         // time any host opens an event processor on this event hub+consumer group+partition combination, it will start
         // receiving at the event after this one. Checkpointing is usually not a fast operation, so there is a tradeoff
         // between checkpointing frequently (to minimize the number of events that will be reprocessed after a crash, or
         // if the partition lease is stolen) and checkpointing infrequently (to reduce the impact on event processing
         // performance). Checkpointing every five events is an arbitrary choice for this sample.
         this.checkpointBatchingCount++;
         if ((checkpointBatchingCount % 5) == 0)
         {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                    data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
            // Checkpoints are created asynchronously. It is important to wait for the result of checkpointing
            // before exiting onEvents or before creating the next checkpoint, to detect errors and to ensure proper ordering.
            context.checkpoint(data).get();
         }
    }
        catch (Exception e)
        {
            System.out.println("Processing failed for an event: " + e.toString());
        }
    }
    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + eventCount + " for host " + context.getOwner());
}
```

## <a name="next-steps"></a><span data-ttu-id="2d249-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d249-171">Next steps</span></span>

<span data-ttu-id="2d249-172">In this article, you created the Event Hubs namespace and other resources required to send and receive events from your event hub.</span><span class="sxs-lookup"><span data-stu-id="2d249-172">In this article, you created the Event Hubs namespace and other resources required to send and receive events from your event hub.</span></span> <span data-ttu-id="2d249-173">To learn more, continue with the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="2d249-173">To learn more, continue with the following tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d249-174">Visualize data anomalies on Event Hubs data streams</span><span class="sxs-lookup"><span data-stu-id="2d249-174">Visualize data anomalies on Event Hubs data streams</span></span>](event-hubs-tutorial-visualize-anomalies.md)

[create a free account]: https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio
[Install Azure CLI 2.0]: /cli/azure/install-azure-cli
[az group create]: /cli/azure/group#az-group-create
[fully qualified domain name]: https://wikipedia.org/wiki/Fully_qualified_domain_name
