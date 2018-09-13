---
title: Order device connection events from Azure IoT Hub using Azure Cosmos DB | Microsoft Docs
description: This article describes how to order and record device connection events from Azure IoT Hub using Azure Cosmos DB to maintain the latest connection state
services: iot-hub
documentationcenter: ''
author: ash2017
manager: briz
editor: ''
ms.service: iot-hub
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2018
ms.author: asrastog
ms.openlocfilehash: dd3c750e93646624e46c46afd871ef75af905bf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870131"
---
# <a name="order-device-connection-events-from-azure-iot-hub-using-azure-cosmos-db"></a><span data-ttu-id="47817-103">Order device connection events from Azure IoT Hub using Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47817-103">Order device connection events from Azure IoT Hub using Azure Cosmos DB</span></span>

<span data-ttu-id="47817-104">Azure Event Grid helps you build event based applications and easily integrate IoT events in your business solutions.</span><span class="sxs-lookup"><span data-stu-id="47817-104">Azure Event Grid helps you build event based applications and easily integrate IoT events in your business solutions.</span></span> <span data-ttu-id="47817-105">This article walks you through a set up which can be used to track and store the latest device connection state in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47817-105">This article walks you through a set up which can be used to track and store the latest device connection state in Cosmos DB.</span></span> <span data-ttu-id="47817-106">We will use the sequence number available in the Device Connected and Device Disconnected events and store the latest state in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47817-106">We will use the sequence number available in the Device Connected and Device Disconnected events and store the latest state in Cosmos DB.</span></span> <span data-ttu-id="47817-107">We are going to use a stored procedure, which is an application logic that is executed against a collection in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="47817-107">We are going to use a stored procedure, which is an application logic that is executed against a collection in Cosmos DB.</span></span>

<span data-ttu-id="47817-108">The sequence number is a string representation of a hexadecimal number.</span><span class="sxs-lookup"><span data-stu-id="47817-108">The sequence number is a string representation of a hexadecimal number.</span></span> <span data-ttu-id="47817-109">You can use string compare to identify the larger number.</span><span class="sxs-lookup"><span data-stu-id="47817-109">You can use string compare to identify the larger number.</span></span> <span data-ttu-id="47817-110">If you are converting the string to hex, then the number will be a 256 bit number.</span><span class="sxs-lookup"><span data-stu-id="47817-110">If you are converting the string to hex, then the number will be a 256 bit number.</span></span> <span data-ttu-id="47817-111">The sequence number is strictly increasing, and the latest event will have a higher number than other events.</span><span class="sxs-lookup"><span data-stu-id="47817-111">The sequence number is strictly increasing, and the latest event will have a higher number than other events.</span></span> <span data-ttu-id="47817-112">This is useful if you have frequent device connects and disconnects, and want to ensure only the latest event is used to trigger a downstream action, as Azure Event Grid doesn’t support ordering of events.</span><span class="sxs-lookup"><span data-stu-id="47817-112">This is useful if you have frequent device connects and disconnects, and want to ensure only the latest event is used to trigger a downstream action, as Azure Event Grid doesn’t support ordering of events.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47817-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="47817-113">Prerequisites</span></span>

* <span data-ttu-id="47817-114">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="47817-114">An active Azure account.</span></span> <span data-ttu-id="47817-115">If you don't have one, you can [create a free account](http://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47817-115">If you don't have one, you can [create a free account](http://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="47817-116">An active Azure Cosmos DB SQL API account.</span><span class="sxs-lookup"><span data-stu-id="47817-116">An active Azure Cosmos DB SQL API account.</span></span> <span data-ttu-id="47817-117">If you haven't created one yet, see [Create a database account](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet#create-a-database-account) for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="47817-117">If you haven't created one yet, see [Create a database account](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet#create-a-database-account) for a walkthrough.</span></span>
* <span data-ttu-id="47817-118">A collection in your database.</span><span class="sxs-lookup"><span data-stu-id="47817-118">A collection in your database.</span></span> <span data-ttu-id="47817-119">See [Add a collection](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet#add-a-collection) for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="47817-119">See [Add a collection](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet#add-a-collection) for a walkthrough.</span></span>
* <span data-ttu-id="47817-120">An IoT Hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="47817-120">An IoT Hub in Azure.</span></span> <span data-ttu-id="47817-121">If you haven't created one yet, see [Get started with IoT Hub](../iot-hub/iot-hub-csharp-csharp-getstarted.md) for a walkthrough.</span><span class="sxs-lookup"><span data-stu-id="47817-121">If you haven't created one yet, see [Get started with IoT Hub](../iot-hub/iot-hub-csharp-csharp-getstarted.md) for a walkthrough.</span></span> 

## <a name="create-a-stored-procedure"></a><span data-ttu-id="47817-122">Create a stored procedure</span><span class="sxs-lookup"><span data-stu-id="47817-122">Create a stored procedure</span></span>

<span data-ttu-id="47817-123">First, create a stored procedure and set it up to run a logic that compares sequence numbers of incoming events and records the latest event per device in the database.</span><span class="sxs-lookup"><span data-stu-id="47817-123">First, create a stored procedure and set it up to run a logic that compares sequence numbers of incoming events and records the latest event per device in the database.</span></span>

1. <span data-ttu-id="47817-124">In your Cosmos DB SQL API, select **Data Explorer** > **Items** > **New Stored Procedure**.</span><span class="sxs-lookup"><span data-stu-id="47817-124">In your Cosmos DB SQL API, select **Data Explorer** > **Items** > **New Stored Procedure**.</span></span>

   ![Create stored procedure](./media/iot-hub-how-to-order-connection-state-events/create-stored-procedure.png)

2. <span data-ttu-id="47817-126">Enter a stored procedure id and paste the following in the “Stored Procedure body”.</span><span class="sxs-lookup"><span data-stu-id="47817-126">Enter a stored procedure id and paste the following in the “Stored Procedure body”.</span></span> <span data-ttu-id="47817-127">Note that this code should replace any existing code in the stored procedure body.</span><span class="sxs-lookup"><span data-stu-id="47817-127">Note that this code should replace any existing code in the stored procedure body.</span></span> <span data-ttu-id="47817-128">This code maintains one row per device ID and records the latest connection state of that device id by identifying the highest sequence number.</span><span class="sxs-lookup"><span data-stu-id="47817-128">This code maintains one row per device ID and records the latest connection state of that device id by identifying the highest sequence number.</span></span> 

    ```javascript
    // SAMPLE STORED PROCEDURE
    function UpdateDevice(deviceId, moduleId, hubName, connectionState, connectionStateUpdatedTime, sequenceNumber) {
      var collection = getContext().getCollection();
      var response = {};
      
      var docLink = getDocumentLink(deviceId, moduleId);

      var isAccepted = collection.readDocument(docLink, function(err, doc) {
        if (err) {
          console.log('Cannot find device ' + docLink + ' - ');
          createDocument();
        } else {
          console.log('Document Found - ');
          replaceDocument(doc);
        }
      });

      function replaceDocument(document) {
        console.log(
          'Old Seq :' +
            document.sequenceNumber +
            ' New Seq: ' +
            sequenceNumber +
            ' - '
        );
        if (sequenceNumber > document.sequenceNumber) {
          document.connectionState = connectionState;
          document.connectionStateUpdatedTime = connectionStateUpdatedTime;
          document.sequenceNumber = sequenceNumber;

          console.log('replace doc - ');

          isAccepted = collection.replaceDocument(docLink, document, function(
            err,
            updated
          ) {
            if (err) {
              getContext()
                .getResponse()
                .setBody(err);
            } else {
              getContext()
                .getResponse()
                .setBody(updated);
            }
          });
        } else {
          getContext()
            .getResponse()
            .setBody('Old Event - current: ' + document.sequenceNumber + ' Incoming: ' + sequenceNumber);
        }
      }
      function createDocument() {
        document = {
          id: deviceId + '-' + moduleId,
          deviceId: deviceId,
          moduleId: moduleId,
          hubName: hubName,
          connectionState: connectionState,
          connectionStateUpdatedTime: connectionStateUpdatedTime,
          sequenceNumber: sequenceNumber
        };
        console.log('Add new device - ' + collection.getAltLink());
        isAccepted = collection.createDocument(
          collection.getAltLink(),
          document,
          function(err, doc) {
            if (err) {
              getContext()
                .getResponse()
                .setBody(err);
            } else {
              getContext()
                .getResponse()
                .setBody(doc);
            }
          }
        );
      }

      function getDocumentLink(deviceId, moduleId) {
        return collection.getAltLink() + '/docs/' + deviceId + '-' + moduleId;
      }
    }
    ```

3. <span data-ttu-id="47817-129">Save the stored procedure:</span><span class="sxs-lookup"><span data-stu-id="47817-129">Save the stored procedure:</span></span> 

    ![save stored procedure](./media/iot-hub-how-to-order-connection-state-events/save-stored-procedure.png)

## <a name="create-a-logic-app"></a><span data-ttu-id="47817-131">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="47817-131">Create a logic app</span></span>

<span data-ttu-id="47817-132">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="47817-132">First, create a logic app and add an Event grid trigger that monitors the resource group for your virtual machine.</span></span> 

### <a name="create-a-logic-app-resource"></a><span data-ttu-id="47817-133">Create a logic app resource</span><span class="sxs-lookup"><span data-stu-id="47817-133">Create a logic app resource</span></span>

1. <span data-ttu-id="47817-134">In the [Azure portal](https://portal.azure.com), select **New** > **Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="47817-134">In the [Azure portal](https://portal.azure.com), select **New** > **Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/iot-hub-how-to-order-connection-state-events/select-logic-app.png)

2. <span data-ttu-id="47817-136">Give your logic app a name that's unique in your subscription, then select the same subscription, resource group, and location as your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47817-136">Give your logic app a name that's unique in your subscription, then select the same subscription, resource group, and location as your IoT hub.</span></span> 
3. <span data-ttu-id="47817-137">When you're ready, select **Pin to dashboard**, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="47817-137">When you're ready, select **Pin to dashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="47817-138">You've now created an Azure resource for your logic app.</span><span class="sxs-lookup"><span data-stu-id="47817-138">You've now created an Azure resource for your logic app.</span></span> <span data-ttu-id="47817-139">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span><span class="sxs-lookup"><span data-stu-id="47817-139">After Azure deploys your logic app, the Logic Apps Designer shows you templates for common patterns so you can get started faster.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="47817-140">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="47817-140">When you select **Pin to dashboard**, your logic app automatically opens in Logic Apps Designer.</span></span> <span data-ttu-id="47817-141">Otherwise, you can manually find and open your logic app.</span><span class="sxs-lookup"><span data-stu-id="47817-141">Otherwise, you can manually find and open your logic app.</span></span>

4. <span data-ttu-id="47817-142">In the Logic App Designer under **Templates**, choose **Blank Logic App** so that you can build your logic app from scratch.</span><span class="sxs-lookup"><span data-stu-id="47817-142">In the Logic App Designer under **Templates**, choose **Blank Logic App** so that you can build your logic app from scratch.</span></span>

### <a name="select-a-trigger"></a><span data-ttu-id="47817-143">Select a trigger</span><span class="sxs-lookup"><span data-stu-id="47817-143">Select a trigger</span></span>

<span data-ttu-id="47817-144">A trigger is a specific event that starts your logic app.</span><span class="sxs-lookup"><span data-stu-id="47817-144">A trigger is a specific event that starts your logic app.</span></span> <span data-ttu-id="47817-145">For this tutorial, the trigger that sets off the workflow is receiving a request over HTTP.</span><span class="sxs-lookup"><span data-stu-id="47817-145">For this tutorial, the trigger that sets off the workflow is receiving a request over HTTP.</span></span>  

1. <span data-ttu-id="47817-146">In the connectors and triggers search bar, type **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="47817-146">In the connectors and triggers search bar, type **HTTP**.</span></span>
2. <span data-ttu-id="47817-147">Select **Request - When a HTTP request is received** as the trigger.</span><span class="sxs-lookup"><span data-stu-id="47817-147">Select **Request - When a HTTP request is received** as the trigger.</span></span> 

   ![Select HTTP request trigger](./media/iot-hub-how-to-order-connection-state-events/http-request-trigger.png)

3. <span data-ttu-id="47817-149">Select **Use sample payload to generate schema**.</span><span class="sxs-lookup"><span data-stu-id="47817-149">Select **Use sample payload to generate schema**.</span></span> 

   ![Select HTTP request trigger](./media/iot-hub-how-to-order-connection-state-events/sample-payload.png)

4. <span data-ttu-id="47817-151">Paste the following sample JSON code into the text box, then select **Done**:</span><span class="sxs-lookup"><span data-stu-id="47817-151">Paste the following sample JSON code into the text box, then select **Done**:</span></span>

   ```json
   [{
    "id": "fbfd8ee1-cf78-74c6-dbcf-e1c58638ccbd",
    "topic":
      "/SUBSCRIPTIONS/DEMO5CDD-8DAB-4CF4-9B2F-C22E8A755472/RESOURCEGROUPS/EGTESTRG/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/MYIOTHUB",
    "subject": "devices/Demo-Device-1",
    "eventType": "Microsoft.Devices.DeviceConnected",
    "eventTime": "2018-07-03T23:20:11.6921933+00:00",
    "data": {
      "deviceConnectionStateEventInfo": {
        "sequenceNumber":
          "000000000000000001D4132452F67CE200000002000000000000000000000001"
      },
      "hubName": "MYIOTHUB",
      "deviceId": "48e44e11-1437-4907-83b1-4a8d7e89859e",
      "moduleId": ""
    },
    "dataVersion": "1",
    "metadataVersion": "1"
   }]
   ```

5. <span data-ttu-id="47817-152">You may receive a pop-up notification that says, **Remember to include a Content-Type header set to application/json in your request.**</span><span class="sxs-lookup"><span data-stu-id="47817-152">You may receive a pop-up notification that says, **Remember to include a Content-Type header set to application/json in your request.**</span></span> <span data-ttu-id="47817-153">You can safely ignore this suggestion, and move on to the next section.</span><span class="sxs-lookup"><span data-stu-id="47817-153">You can safely ignore this suggestion, and move on to the next section.</span></span> 

### <a name="create-a-condition"></a><span data-ttu-id="47817-154">Create a condition</span><span class="sxs-lookup"><span data-stu-id="47817-154">Create a condition</span></span>

<span data-ttu-id="47817-155">Conditions help run specific actions after passing a specific condition, in your the logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="47817-155">Conditions help run specific actions after passing a specific condition, in your the logic app workflow.</span></span> <span data-ttu-id="47817-156">Once the condition is met, a desired action can be defined.</span><span class="sxs-lookup"><span data-stu-id="47817-156">Once the condition is met, a desired action can be defined.</span></span> <span data-ttu-id="47817-157">For this tutorial, the condition is to check whether eventType is device connected or device disconnected.</span><span class="sxs-lookup"><span data-stu-id="47817-157">For this tutorial, the condition is to check whether eventType is device connected or device disconnected.</span></span> <span data-ttu-id="47817-158">The action will be to execute the stored procedure in your database.</span><span class="sxs-lookup"><span data-stu-id="47817-158">The action will be to execute the stored procedure in your database.</span></span> 

1. <span data-ttu-id="47817-159">Select **New step** then **Built-ins** and **Condition**.</span><span class="sxs-lookup"><span data-stu-id="47817-159">Select **New step** then **Built-ins** and **Condition**.</span></span> 

2. <span data-ttu-id="47817-160">Fill the condition as shown below to only execute this for Device Connected and Device Disconnected events:</span><span class="sxs-lookup"><span data-stu-id="47817-160">Fill the condition as shown below to only execute this for Device Connected and Device Disconnected events:</span></span>
  * <span data-ttu-id="47817-161">Choose a value: **eventType**</span><span class="sxs-lookup"><span data-stu-id="47817-161">Choose a value: **eventType**</span></span>
  * <span data-ttu-id="47817-162">Change is equal to" to **ends with**</span><span class="sxs-lookup"><span data-stu-id="47817-162">Change is equal to" to **ends with**</span></span>
  * <span data-ttu-id="47817-163">Choose a value: **nected**</span><span class="sxs-lookup"><span data-stu-id="47817-163">Choose a value: **nected**</span></span>

   ![Fill Condition](./media/iot-hub-how-to-order-connection-state-events/condition-detail.png)

3. <span data-ttu-id="47817-165">If the condition is true, click on **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="47817-165">If the condition is true, click on **Add an action**.</span></span>
  
   ![Add action if true](./media/iot-hub-how-to-order-connection-state-events/action-if-true.png)

4. <span data-ttu-id="47817-167">Search for Cosmos DB and click on **Azure Cosmos DB - Execute stored procedure**</span><span class="sxs-lookup"><span data-stu-id="47817-167">Search for Cosmos DB and click on **Azure Cosmos DB - Execute stored procedure**</span></span>

   ![Search for CosmosDB](./media/iot-hub-how-to-order-connection-state-events/cosmosDB-search.png)

5. <span data-ttu-id="47817-169">Populate the form for Execute stored procure by selecting values from your database.</span><span class="sxs-lookup"><span data-stu-id="47817-169">Populate the form for Execute stored procure by selecting values from your database.</span></span> <span data-ttu-id="47817-170">Enter the partition key value and parameters as shown below.</span><span class="sxs-lookup"><span data-stu-id="47817-170">Enter the partition key value and parameters as shown below.</span></span> 

   ![populate logic app action](./media/iot-hub-how-to-order-connection-state-events/logicapp-stored-procedure.png)

6. <span data-ttu-id="47817-172">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="47817-172">Save your logic app.</span></span> 

### <a name="copy-the-http-url"></a><span data-ttu-id="47817-173">Copy the HTTP URL</span><span class="sxs-lookup"><span data-stu-id="47817-173">Copy the HTTP URL</span></span>

<span data-ttu-id="47817-174">Before you leave the Logic Apps Designer, copy the URL that your logic apps is listening to for a trigger.</span><span class="sxs-lookup"><span data-stu-id="47817-174">Before you leave the Logic Apps Designer, copy the URL that your logic apps is listening to for a trigger.</span></span> <span data-ttu-id="47817-175">You use this URL to configure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="47817-175">You use this URL to configure Event Grid.</span></span> 

1. <span data-ttu-id="47817-176">Expand the **When a HTTP request is received** trigger configuration box by clicking on it.</span><span class="sxs-lookup"><span data-stu-id="47817-176">Expand the **When a HTTP request is received** trigger configuration box by clicking on it.</span></span> 
2. <span data-ttu-id="47817-177">Copy the value of **HTTP POST URL** by selecting the copy button next to it.</span><span class="sxs-lookup"><span data-stu-id="47817-177">Copy the value of **HTTP POST URL** by selecting the copy button next to it.</span></span> 

   ![Copy the HTTP POST URL](./media/iot-hub-how-to-order-connection-state-events/copy-url.png)

3. <span data-ttu-id="47817-179">Save this URL so that you can refer to it in the next section.</span><span class="sxs-lookup"><span data-stu-id="47817-179">Save this URL so that you can refer to it in the next section.</span></span> 

## <a name="configure-subscription-for-iot-hub-events"></a><span data-ttu-id="47817-180">Configure subscription for IoT Hub events</span><span class="sxs-lookup"><span data-stu-id="47817-180">Configure subscription for IoT Hub events</span></span>

<span data-ttu-id="47817-181">In this section, you configure your IoT Hub to publish events as they occur.</span><span class="sxs-lookup"><span data-stu-id="47817-181">In this section, you configure your IoT Hub to publish events as they occur.</span></span> 

1. <span data-ttu-id="47817-182">In the Azure portal, navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47817-182">In the Azure portal, navigate to your IoT hub.</span></span> 
2. <span data-ttu-id="47817-183">Select **Events**.</span><span class="sxs-lookup"><span data-stu-id="47817-183">Select **Events**.</span></span>

   ![Open the Event Grid details](./media/iot-hub-how-to-order-connection-state-events/event-grid.png)

3. <span data-ttu-id="47817-185">Select **Event subscription**.</span><span class="sxs-lookup"><span data-stu-id="47817-185">Select **Event subscription**.</span></span> 

   ![Create new event subscription](./media/iot-hub-how-to-order-connection-state-events/event-subscription.png)

4. <span data-ttu-id="47817-187">Create the event subscription with the following values:</span><span class="sxs-lookup"><span data-stu-id="47817-187">Create the event subscription with the following values:</span></span> 
   * <span data-ttu-id="47817-188">**Event Type**: Uncheck Subscribe to all event types and select **Device Connected** and **Device Disconnected** from the menu.</span><span class="sxs-lookup"><span data-stu-id="47817-188">**Event Type**: Uncheck Subscribe to all event types and select **Device Connected** and **Device Disconnected** from the menu.</span></span>
   * <span data-ttu-id="47817-189">**Endpoint Details**: Select Endpoint Type as **Web Hook** and click on select endpoint and paste the URL that you copied from your logic app and confirm selection.</span><span class="sxs-lookup"><span data-stu-id="47817-189">**Endpoint Details**: Select Endpoint Type as **Web Hook** and click on select endpoint and paste the URL that you copied from your logic app and confirm selection.</span></span>

   ![select endpoint url](./media/iot-hub-how-to-order-connection-state-events/endpoint-url.png)

   * <span data-ttu-id="47817-191">**Event Subscription Details**: Provide a descriptive name and select **Event Grid Schema** When you're done, the form should look like the following example:</span><span class="sxs-lookup"><span data-stu-id="47817-191">**Event Subscription Details**: Provide a descriptive name and select **Event Grid Schema** When you're done, the form should look like the following example:</span></span> 

   ![Sample event subscription form](./media/iot-hub-how-to-order-connection-state-events/subscription-form.png)

5. <span data-ttu-id="47817-193">Select **Create** to save the event subscription.</span><span class="sxs-lookup"><span data-stu-id="47817-193">Select **Create** to save the event subscription.</span></span>

## <a name="observe-events"></a><span data-ttu-id="47817-194">Observe events</span><span class="sxs-lookup"><span data-stu-id="47817-194">Observe events</span></span>
<span data-ttu-id="47817-195">Now that your event subscription is set up, let's test by connecting a device.</span><span class="sxs-lookup"><span data-stu-id="47817-195">Now that your event subscription is set up, let's test by connecting a device.</span></span>

### <a name="register-a-device-in-iot-hub"></a><span data-ttu-id="47817-196">Register a device in IoT Hub</span><span class="sxs-lookup"><span data-stu-id="47817-196">Register a device in IoT Hub</span></span>

1. <span data-ttu-id="47817-197">From your IoT hub, select **IoT Devices**.</span><span class="sxs-lookup"><span data-stu-id="47817-197">From your IoT hub, select **IoT Devices**.</span></span> 
2. <span data-ttu-id="47817-198">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="47817-198">Select **Add**.</span></span>
3. <span data-ttu-id="47817-199">For **Device ID**, enter `Demo-Device-1`.</span><span class="sxs-lookup"><span data-stu-id="47817-199">For **Device ID**, enter `Demo-Device-1`.</span></span>
4. <span data-ttu-id="47817-200">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="47817-200">Select **Save**.</span></span> 
5. <span data-ttu-id="47817-201">You can add multiple devices with different device IDs.</span><span class="sxs-lookup"><span data-stu-id="47817-201">You can add multiple devices with different device IDs.</span></span>

   ![How to outcome](./media/iot-hub-how-to-order-connection-state-events/AddIoTDevice.png)

6. <span data-ttu-id="47817-203">Copy the **Connection string -- primary key** to use later.</span><span class="sxs-lookup"><span data-stu-id="47817-203">Copy the **Connection string -- primary key** to use later.</span></span>

   ![How to outcome](./media/iot-hub-how-to-order-connection-state-events/DeviceConnString.png)

### <a name="start-raspberry-pi-simulator"></a><span data-ttu-id="47817-205">Start Raspberry Pi simulator</span><span class="sxs-lookup"><span data-stu-id="47817-205">Start Raspberry Pi simulator</span></span>

1. <span data-ttu-id="47817-206">Let's use the Raspberry Pi web simulator to simulate device connection.</span><span class="sxs-lookup"><span data-stu-id="47817-206">Let's use the Raspberry Pi web simulator to simulate device connection.</span></span>

[<span data-ttu-id="47817-207">Start Raspberry Pi simulator</span><span class="sxs-lookup"><span data-stu-id="47817-207">Start Raspberry Pi simulator</span></span>](https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted)

### <a name="run-a-sample-applciation-on-the-raspberry-pi-web-simulator"></a><span data-ttu-id="47817-208">Run a sample applciation on the Raspberry Pi web simulator</span><span class="sxs-lookup"><span data-stu-id="47817-208">Run a sample applciation on the Raspberry Pi web simulator</span></span>
<span data-ttu-id="47817-209">This will trigger a device connected event.</span><span class="sxs-lookup"><span data-stu-id="47817-209">This will trigger a device connected event.</span></span>

1. <span data-ttu-id="47817-210">In the coding area, replace the placeholder in Line 15 with your Azure IoT Hub device connection string.</span><span class="sxs-lookup"><span data-stu-id="47817-210">In the coding area, replace the placeholder in Line 15 with your Azure IoT Hub device connection string.</span></span>

   ![How to outcome](./media/iot-hub-how-to-order-connection-state-events/raspconnstring.png)

2. <span data-ttu-id="47817-212">Run the application by clicking on **Run**.</span><span class="sxs-lookup"><span data-stu-id="47817-212">Run the application by clicking on **Run**.</span></span>

<span data-ttu-id="47817-213">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47817-213">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![How to outcome](./media/iot-hub-how-to-order-connection-state-events/raspmsg.png)

   <span data-ttu-id="47817-215">Click **Stop** to stop the simulator and trigger a **Device Disconnected** event.</span><span class="sxs-lookup"><span data-stu-id="47817-215">Click **Stop** to stop the simulator and trigger a **Device Disconnected** event.</span></span>

<span data-ttu-id="47817-216">You have now run a sample application to collect sensor data and send it to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47817-216">You have now run a sample application to collect sensor data and send it to your IoT hub.</span></span> 

### <a name="observe-events-in-cosmos-db"></a><span data-ttu-id="47817-217">Observe events in Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="47817-217">Observe events in Cosmos DB</span></span>

<span data-ttu-id="47817-218">You can see results of the executed stored procedure in your Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="47817-218">You can see results of the executed stored procedure in your Cosmos DB document.</span></span> <span data-ttu-id="47817-219">Here's what it will look like.</span><span class="sxs-lookup"><span data-stu-id="47817-219">Here's what it will look like.</span></span> <span data-ttu-id="47817-220">Note that each row contains latest device connection state per device</span><span class="sxs-lookup"><span data-stu-id="47817-220">Note that each row contains latest device connection state per device</span></span>

   ![How to outcome](./media/iot-hub-how-to-order-connection-state-events/cosmosDB-outcome.png)

## <a name="use-the-azure-cli"></a><span data-ttu-id="47817-222">Use the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="47817-222">Use the Azure CLI</span></span>

<span data-ttu-id="47817-223">Instead of using the Azure portal, you can accomplish the IoT Hub steps using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="47817-223">Instead of using the Azure portal, you can accomplish the IoT Hub steps using the Azure CLI.</span></span> <span data-ttu-id="47817-224">For details, see the Azure CLI pages for [creating an event subscription](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription) and [creating an IoT device](https://docs.microsoft.com/cli/azure/iot/device).</span><span class="sxs-lookup"><span data-stu-id="47817-224">For details, see the Azure CLI pages for [creating an event subscription](https://docs.microsoft.com/cli/azure/eventgrid/event-subscription) and [creating an IoT device](https://docs.microsoft.com/cli/azure/iot/device).</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="47817-225">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="47817-225">Clean up resources</span></span>

<span data-ttu-id="47817-226">This tutorial used resources that incur charges on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="47817-226">This tutorial used resources that incur charges on your Azure subscription.</span></span> <span data-ttu-id="47817-227">When you're done trying out the tutorial and testing your results, disable or delete resources that you don't want to keep.</span><span class="sxs-lookup"><span data-stu-id="47817-227">When you're done trying out the tutorial and testing your results, disable or delete resources that you don't want to keep.</span></span> 

<span data-ttu-id="47817-228">If you don't want to lose the work on your logic app, disable it instead of deleting it.</span><span class="sxs-lookup"><span data-stu-id="47817-228">If you don't want to lose the work on your logic app, disable it instead of deleting it.</span></span> 

1. <span data-ttu-id="47817-229">Navigate to your logic app.</span><span class="sxs-lookup"><span data-stu-id="47817-229">Navigate to your logic app.</span></span>
2. <span data-ttu-id="47817-230">On the **Overview** blade select **Delete** or **Disable**.</span><span class="sxs-lookup"><span data-stu-id="47817-230">On the **Overview** blade select **Delete** or **Disable**.</span></span> 

<span data-ttu-id="47817-231">Each subscription can have one free IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47817-231">Each subscription can have one free IoT hub.</span></span> <span data-ttu-id="47817-232">If you created a free hub for this tutorial, then you don't need to delete it to prevent charges.</span><span class="sxs-lookup"><span data-stu-id="47817-232">If you created a free hub for this tutorial, then you don't need to delete it to prevent charges.</span></span>

1. <span data-ttu-id="47817-233">Navigate to your IoT hub.</span><span class="sxs-lookup"><span data-stu-id="47817-233">Navigate to your IoT hub.</span></span> 
2. <span data-ttu-id="47817-234">On the **Overview** blade select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="47817-234">On the **Overview** blade select **Delete**.</span></span> 

<span data-ttu-id="47817-235">Even if you keep your IoT hub, you may want to delete the event subscription that you created.</span><span class="sxs-lookup"><span data-stu-id="47817-235">Even if you keep your IoT hub, you may want to delete the event subscription that you created.</span></span> 

1. <span data-ttu-id="47817-236">In your IoT hub, select **Event Grid**.</span><span class="sxs-lookup"><span data-stu-id="47817-236">In your IoT hub, select **Event Grid**.</span></span>
2. <span data-ttu-id="47817-237">Select the event subscription that you want to remove.</span><span class="sxs-lookup"><span data-stu-id="47817-237">Select the event subscription that you want to remove.</span></span> 
3. <span data-ttu-id="47817-238">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="47817-238">Select **Delete**.</span></span> 

<span data-ttu-id="47817-239">To remove an Azure Cosmos DB account from the Azure portal, righ-click the account name and click **Delete account**.</span><span class="sxs-lookup"><span data-stu-id="47817-239">To remove an Azure Cosmos DB account from the Azure portal, righ-click the account name and click **Delete account**.</span></span> <span data-ttu-id="47817-240">See detailed instructions for [deleting an Azure Cosmos DB account](https://docs.microsoft.com/azure/cosmos-db/manage-account#delete).</span><span class="sxs-lookup"><span data-stu-id="47817-240">See detailed instructions for [deleting an Azure Cosmos DB account](https://docs.microsoft.com/azure/cosmos-db/manage-account#delete).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47817-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="47817-241">Next steps</span></span>

* <span data-ttu-id="47817-242">Learn more about [Reacting to IoT Hub events by using Event Grid to trigger actions](../iot-hub/iot-hub-event-grid.md)</span><span class="sxs-lookup"><span data-stu-id="47817-242">Learn more about [Reacting to IoT Hub events by using Event Grid to trigger actions](../iot-hub/iot-hub-event-grid.md)</span></span>
* [<span data-ttu-id="47817-243">Try the IoT Hub events tutorial</span><span class="sxs-lookup"><span data-stu-id="47817-243">Try the IoT Hub events tutorial</span></span>](../event-grid/publish-iot-hub-events-to-logic-apps.md)
* <span data-ttu-id="47817-244">Learn about what else you can do with [Event Grid](../event-grid/overview.md)</span><span class="sxs-lookup"><span data-stu-id="47817-244">Learn about what else you can do with [Event Grid](../event-grid/overview.md)</span></span>


