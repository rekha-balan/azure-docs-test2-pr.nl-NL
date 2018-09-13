---
title: Create an Azure Event Hubs namespace and enable Capture using a template | Microsoft Docs
description: Create an Azure Event Hubs namespace with one event hub and enable Capture using Azure Resource Manager template
services: event-hubs
documentationcenter: .net
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.assetid: 8bdda6a2-5ff1-45e3-b696-c553768f1090
ms.service: event-hubs
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/16/2018
ms.author: shvija
ms.openlocfilehash: c8341b40ba7616add1415178a2f0775fbbc66ec1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968838"
---
# <a name="create-a-namespace-with-event-hub-and-enable-capture-using-a-template"></a><span data-ttu-id="bd3f0-103">Create a namespace with event hub and enable Capture using a template</span><span class="sxs-lookup"><span data-stu-id="bd3f0-103">Create a namespace with event hub and enable Capture using a template</span></span>

<span data-ttu-id="bd3f0-104">This article shows how to use an Azure Resource Manager template that creates an [Event Hubs](event-hubs-what-is-event-hubs.md) namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-104">This article shows how to use an Azure Resource Manager template that creates an [Event Hubs](event-hubs-what-is-event-hubs.md) namespace, with one event hub instance, and also enables the [Capture feature](event-hubs-capture-overview.md) on the event hub.</span></span> <span data-ttu-id="bd3f0-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-105">The article describes how to define which resources are deployed, and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="bd3f0-106">You can use this template for your own deployments, or customize it to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="bd3f0-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-107">This article also shows how to specify that events are captured into either Azure Storage Blobs or an Azure Data Lake Store, based on the destination you choose.</span></span>

<span data-ttu-id="bd3f0-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="bd3f0-108">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="bd3f0-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span><span class="sxs-lookup"><span data-stu-id="bd3f0-109">For more information about patterns and practices for Azure Resources naming conventions, see [Azure Resources naming conventions][Azure Resources naming conventions].</span></span>

<span data-ttu-id="bd3f0-110">For the complete templates, click the following GitHub links:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-110">For the complete templates, click the following GitHub links:</span></span>

- <span data-ttu-id="bd3f0-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span><span class="sxs-lookup"><span data-stu-id="bd3f0-111">[Event hub and enable Capture to Storage template][Event Hub and enable Capture to Storage template]</span></span> 
- <span data-ttu-id="bd3f0-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span><span class="sxs-lookup"><span data-stu-id="bd3f0-112">[Event hub and enable Capture to Azure Data Lake Store template][Event Hub and enable Capture to Azure Data Lake Store template]</span></span>

> [!NOTE]
> <span data-ttu-id="bd3f0-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-113">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="bd3f0-114">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="bd3f0-114">What will you deploy?</span></span>

<span data-ttu-id="bd3f0-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd3f0-115">With this template, you deploy an Event Hubs namespace with an event hub, and also enable [Event Hubs Capture](event-hubs-capture-overview.md).</span></span> <span data-ttu-id="bd3f0-116">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-116">Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to Azure Blob storage or Azure Data Lake Store, within a specified time or size interval of your choosing.</span></span> <span data-ttu-id="bd3f0-117">Click the following button to enable Event Hubs Capture into Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-117">Click the following button to enable Event Hubs Capture into Azure Storage:</span></span>

<span data-ttu-id="bd3f0-118">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bd3f0-118">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture%2Fazuredeploy.json)</span></span>

<span data-ttu-id="bd3f0-119">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-119">Click the following button to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

<span data-ttu-id="bd3f0-120">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bd3f0-120">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-eventhubs-create-namespace-and-enable-capture-for-adls%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bd3f0-121">Parameters</span><span class="sxs-lookup"><span data-stu-id="bd3f0-121">Parameters</span></span>

<span data-ttu-id="bd3f0-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="bd3f0-123">The template includes a section called `Parameters` that contains all the parameter values.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-123">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="bd3f0-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="bd3f0-125">Do not define parameters for values that always stay the same.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="bd3f0-126">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-126">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="bd3f0-127">The template defines the following parameters.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-127">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="bd3f0-128">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="bd3f0-128">eventHubNamespaceName</span></span>

<span data-ttu-id="bd3f0-129">The name of the Event Hubs namespace to create.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-129">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName":{  
     "type":"string",
     "metadata":{  
         "description":"Name of the EventHub namespace"
      }
}
```

### <a name="eventhubname"></a><span data-ttu-id="bd3f0-130">eventHubName</span><span class="sxs-lookup"><span data-stu-id="bd3f0-130">eventHubName</span></span>

<span data-ttu-id="bd3f0-131">The name of the event hub created in the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-131">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName":{  
    "type":"string",
    "metadata":{  
        "description":"Name of the event hub"
    }
}
```

### <a name="messageretentionindays"></a><span data-ttu-id="bd3f0-132">messageRetentionInDays</span><span class="sxs-lookup"><span data-stu-id="bd3f0-132">messageRetentionInDays</span></span>

<span data-ttu-id="bd3f0-133">The number of days to retain the messages in the event hub.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-133">The number of days to retain the messages in the event hub.</span></span> 

```json
"messageRetentionInDays":{
    "type":"int",
    "defaultValue": 1,
    "minValue":"1",
    "maxValue":"7",
    "metadata":{
       "description":"How long to retain the data in event hub"
     }
 }
```

### <a name="partitioncount"></a><span data-ttu-id="bd3f0-134">partitionCount</span><span class="sxs-lookup"><span data-stu-id="bd3f0-134">partitionCount</span></span>

<span data-ttu-id="bd3f0-135">The number of partitions to create in the event hub.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-135">The number of partitions to create in the event hub.</span></span>

```json
"partitionCount":{
    "type":"int",
    "defaultValue":2,
    "minValue":2,
    "maxValue":32,
    "metadata":{
        "description":"Number of partitions chosen"
    }
 }
```

### <a name="captureenabled"></a><span data-ttu-id="bd3f0-136">captureEnabled</span><span class="sxs-lookup"><span data-stu-id="bd3f0-136">captureEnabled</span></span>

<span data-ttu-id="bd3f0-137">Enable Capture on the event hub.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-137">Enable Capture on the event hub.</span></span>

```json
"captureEnabled":{
    "type":"string",
    "defaultValue":"true",
    "allowedValues": [
    "false",
    "true"],
    "metadata":{
        "description":"Enable or disable the Capture for your event hub"
    }
 }
```
### <a name="captureencodingformat"></a><span data-ttu-id="bd3f0-138">captureEncodingFormat</span><span class="sxs-lookup"><span data-stu-id="bd3f0-138">captureEncodingFormat</span></span>

<span data-ttu-id="bd3f0-139">The encoding format you specify to serialize the event data.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-139">The encoding format you specify to serialize the event data.</span></span>

```json
"captureEncodingFormat":{
    "type":"string",
    "defaultValue":"Avro",
    "allowedValues":[
    "Avro"],
    "metadata":{
        "description":"The encoding format in which Capture serializes the EventData"
    }
}
```

### <a name="capturetime"></a><span data-ttu-id="bd3f0-140">captureTime</span><span class="sxs-lookup"><span data-stu-id="bd3f0-140">captureTime</span></span>

<span data-ttu-id="bd3f0-141">The time interval in which Event Hubs Capture starts capturing the data.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-141">The time interval in which Event Hubs Capture starts capturing the data.</span></span>

```json
"captureTime":{
    "type":"int",
    "defaultValue":300,
    "minValue":60,
    "maxValue":900,
    "metadata":{
         "description":"The time window in seconds for the capture"
    }
}
```

### <a name="capturesize"></a><span data-ttu-id="bd3f0-142">captureSize</span><span class="sxs-lookup"><span data-stu-id="bd3f0-142">captureSize</span></span>
<span data-ttu-id="bd3f0-143">The size interval at which Capture starts capturing the data.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-143">The size interval at which Capture starts capturing the data.</span></span>

```json
"captureSize":{
    "type":"int",
    "defaultValue":314572800,
    "minValue":10485760,
    "maxValue":524288000,
    "metadata":{
        "description":"The size window in bytes for capture"
    }
}
```

### <a name="capturenameformat"></a><span data-ttu-id="bd3f0-144">captureNameFormat</span><span class="sxs-lookup"><span data-stu-id="bd3f0-144">captureNameFormat</span></span>

<span data-ttu-id="bd3f0-145">The name format used by Event Hubs Capture to write the Avro files.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-145">The name format used by Event Hubs Capture to write the Avro files.</span></span> <span data-ttu-id="bd3f0-146">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-146">Note that a Capture name format must contain `{Namespace}`, `{EventHub}`, `{PartitionId}`, `{Year}`, `{Month}`, `{Day}`, `{Hour}`, `{Minute}`, and `{Second}` fields.</span></span> <span data-ttu-id="bd3f0-147">These can be arranged in any order, with or without delimiters.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-147">These can be arranged in any order, with or without delimiters.</span></span>
 
```json
"captureNameFormat": {
      "type": "string",
      "defaultValue": "{Namespace}/{EventHub}/{PartitionId}/{Year}/{Month}/{Day}/{Hour}/{Minute}/{Second}",
      "metadata": {
        "description": "A Capture Name Format must contain {Namespace}, {EventHub}, {PartitionId}, {Year}, {Month}, {Day}, {Hour}, {Minute} and {Second} fields. These can be arranged in any order with or without delimeters. E.g.  Prod_{EventHub}/{Namespace}\\{PartitionId}_{Year}_{Month}/{Day}/{Hour}/{Minute}/{Second}"
      }
    }
  
```

### <a name="apiversion"></a><span data-ttu-id="bd3f0-148">apiVersion</span><span class="sxs-lookup"><span data-stu-id="bd3f0-148">apiVersion</span></span>

<span data-ttu-id="bd3f0-149">The API version of the template.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-149">The API version of the template.</span></span>

```json
 "apiVersion":{  
    "type":"string",
    "defaultValue":"2017-04-01",
    "metadata":{  
        "description":"ApiVersion used by the template"
    }
 }
```

<span data-ttu-id="bd3f0-150">Use the following parameters if you choose Azure Storage as your destination.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-150">Use the following parameters if you choose Azure Storage as your destination.</span></span>

### <a name="destinationstorageaccountresourceid"></a><span data-ttu-id="bd3f0-151">destinationStorageAccountResourceId</span><span class="sxs-lookup"><span data-stu-id="bd3f0-151">destinationStorageAccountResourceId</span></span>

<span data-ttu-id="bd3f0-152">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-152">Capture requires an Azure Storage account resource ID to enable capturing to your desired Storage account.</span></span>

```json
 "destinationStorageAccountResourceId":{
    "type":"string",
    "metadata":{
        "description":"Your existing Storage account resource ID where you want the blobs be captured"
    }
 }
```

### <a name="blobcontainername"></a><span data-ttu-id="bd3f0-153">blobContainerName</span><span class="sxs-lookup"><span data-stu-id="bd3f0-153">blobContainerName</span></span>

<span data-ttu-id="bd3f0-154">The blob container in which to capture your event data.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-154">The blob container in which to capture your event data.</span></span>

```json
 "blobContainerName":{
    "type":"string",
    "metadata":{
        "description":"Your existing storage container in which you want the blobs captured"
    }
}
```

<span data-ttu-id="bd3f0-155">Use the following parameters if you choose Azure Data Lake Store as your destination.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-155">Use the following parameters if you choose Azure Data Lake Store as your destination.</span></span> <span data-ttu-id="bd3f0-156">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-156">You must set permissions on your Data Lake Store path, in which you want to Capture the event.</span></span> <span data-ttu-id="bd3f0-157">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="bd3f0-157">To set permissions, see [this article](event-hubs-capture-enable-through-portal.md#capture-data-to-an-azure-data-lake-store-account).</span></span>

### <a name="subscriptionid"></a><span data-ttu-id="bd3f0-158">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="bd3f0-158">subscriptionId</span></span>

<span data-ttu-id="bd3f0-159">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-159">Subscription ID for the Event Hubs namespace and Azure Data Lake Store.</span></span> <span data-ttu-id="bd3f0-160">Both these resources must be under the same subscription ID.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-160">Both these resources must be under the same subscription ID.</span></span>

```json
"subscriptionId": {
    "type": "string",
    "metadata": {
        "description": "Subscription ID of both Azure Data Lake Store and Event Hubs namespace"
     }
 }
```

### <a name="datalakeaccountname"></a><span data-ttu-id="bd3f0-161">dataLakeAccountName</span><span class="sxs-lookup"><span data-stu-id="bd3f0-161">dataLakeAccountName</span></span>

<span data-ttu-id="bd3f0-162">The Azure Data Lake Store name for the captured events.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-162">The Azure Data Lake Store name for the captured events.</span></span>

```json
"dataLakeAccountName": {
    "type": "string",
    "metadata": {
        "description": "Azure Data Lake Store name"
    }
}
```

### <a name="datalakefolderpath"></a><span data-ttu-id="bd3f0-163">dataLakeFolderPath</span><span class="sxs-lookup"><span data-stu-id="bd3f0-163">dataLakeFolderPath</span></span>

<span data-ttu-id="bd3f0-164">The destination folder path for the captured events.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-164">The destination folder path for the captured events.</span></span> <span data-ttu-id="bd3f0-165">This is the folder in your Data Lake Store to which the events will be pushed during the capture operation.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-165">This is the folder in your Data Lake Store to which the events will be pushed during the capture operation.</span></span> <span data-ttu-id="bd3f0-166">To set permissions on this folder, see [Use Azure Data Lake Store to capture data from Event Hubs](../data-lake-store/data-lake-store-archive-eventhub-capture.md).</span><span class="sxs-lookup"><span data-stu-id="bd3f0-166">To set permissions on this folder, see [Use Azure Data Lake Store to capture data from Event Hubs](../data-lake-store/data-lake-store-archive-eventhub-capture.md).</span></span>

```json
"dataLakeFolderPath": {
    "type": "string",
    "metadata": {
        "description": "Destination capture folder path"
    }
}
```

## <a name="resources-to-deploy-for-azure-storage-as-destination-to-captured-events"></a><span data-ttu-id="bd3f0-167">Resources to deploy for Azure Storage as destination to captured events</span><span class="sxs-lookup"><span data-stu-id="bd3f0-167">Resources to deploy for Azure Storage as destination to captured events</span></span>

<span data-ttu-id="bd3f0-168">Creates a namespace of type **EventHub**, with one event hub, and also enables Capture to Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-168">Creates a namespace of type **EventHub**, with one event hub, and also enables Capture to Azure Blob Storage.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('eventHubNamespaceName')]",
         "type":"Microsoft.EventHub/Namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources": [
    {
      "apiVersion": "2017-04-01",
      "name": "[parameters('eventHubNamespaceName')]",
      "type": "Microsoft.EventHub/Namespaces",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "Standard"
      },
      "properties": {
        "isAutoInflateEnabled": "true",
        "maximumThroughputUnits": "7"
      },
      "resources": [
        {
          "apiVersion": "2017-04-01",
          "name": "[parameters('eventHubName')]",
          "type": "EventHubs",
          "dependsOn": [
            "[concat('Microsoft.EventHub/namespaces/', parameters('eventHubNamespaceName'))]"
          ],
          "properties": {
            "messageRetentionInDays": "[parameters('messageRetentionInDays')]",
            "partitionCount": "[parameters('partitionCount')]",
            "captureDescription": {
              "enabled": "true",
              "encoding": "[parameters('captureEncodingFormat')]",
              "intervalInSeconds": "[parameters('captureTime')]",
              "sizeLimitInBytes": "[parameters('captureSize')]",
              "destination": {
                "name": "EventHubArchive.AzureBlockBlob",
                "properties": {
                  "storageAccountResourceId": "[parameters('destinationStorageAccountResourceId')]",
                  "blobContainer": "[parameters('blobContainerName')]",
                  "archiveNameFormat": "[parameters('captureNameFormat')]"
                }
              }
            }
          }

        }
      ]
    }
  ]
```

## <a name="resources-to-deploy-for-azure-data-lake-store-as-destination"></a><span data-ttu-id="bd3f0-169">Resources to deploy for Azure Data Lake Store as destination</span><span class="sxs-lookup"><span data-stu-id="bd3f0-169">Resources to deploy for Azure Data Lake Store as destination</span></span>

<span data-ttu-id="bd3f0-170">Creates a namespace of type **EventHub**, with one event hub, and also enables Capture to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bd3f0-170">Creates a namespace of type **EventHub**, with one event hub, and also enables Capture to Azure Data Lake Store.</span></span>

```json
 "resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('eventHubName')]",
                        "captureDescription": {
                            "enabled": "true",
                            "encoding": "[parameters('archiveEncodingFormat')]",
                            "intervalInSeconds": "[parameters('captureTime')]",
                            "sizeLimitInBytes": "[parameters('captureSize')]",
                            "destination": {
                                "name": "EventHubArchive.AzureDataLake",
                                "properties": {
                                    "DataLakeSubscriptionId": "[parameters('subscriptionId')]",
                                    "DataLakeAccountName": "[parameters('dataLakeAccountName')]",
                                    "DataLakeFolderPath": "[parameters('dataLakeFolderPath')]",
                                    "ArchiveNameFormat": "[parameters('captureNameFormat')]"
                                }
                            }
                        }
                    }
                }
            ]
        }
    ]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="bd3f0-171">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="bd3f0-171">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="bd3f0-172">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd3f0-172">PowerShell</span></span>

<span data-ttu-id="bd3f0-173">Deploy your template to enable Event Hubs Capture into Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-173">Deploy your template to enable Event Hubs Capture into Azure Storage:</span></span>
 
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json
```

<span data-ttu-id="bd3f0-174">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-174">Deploy your template to enable Event Hubs Capture into Azure Data Lake Store:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="bd3f0-175">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bd3f0-175">Azure CLI</span></span>

<span data-ttu-id="bd3f0-176">Azure Blob Storage as destination:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-176">Azure Blob Storage as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture/azuredeploy.json][]
```

<span data-ttu-id="bd3f0-177">Azure Data Lake Store as destination:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-177">Azure Data Lake Store as destination:</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-eventhubs-create-namespace-and-enable-capture-for-adls/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="bd3f0-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd3f0-178">Next steps</span></span>

<span data-ttu-id="bd3f0-179">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd3f0-179">You can also configure Event Hubs Capture via the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bd3f0-180">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bd3f0-180">For more information, see [Enable Event Hubs Capture using the Azure portal](event-hubs-capture-enable-through-portal.md).</span></span>

<span data-ttu-id="bd3f0-181">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="bd3f0-181">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="bd3f0-182">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="bd3f0-182">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="bd3f0-183">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="bd3f0-183">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="bd3f0-184">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="bd3f0-184">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Azure Resources naming conventions]: https://azure.microsoft.com/documentation/articles/guidance-naming-conventions/
[Event hub and enable Capture to Storage template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture
[Event hub and enable Capture to Azure Data Lake Store template]: https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-capture-for-adls