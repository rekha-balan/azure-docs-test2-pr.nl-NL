---
title: Create an Azure Event Hubs namespace and consumer group using a template | Microsoft Docs
description: Create an Event Hubs namespace with an event hub and a consumer group using Azure Resource Manager templates
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 03/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 8435e74e91351f6bcf6b577f9ad4acd90dccaca2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555173"
---
# <a name="create-an-event-hubs-namespace-with-an-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="a86d7-103">Create an Event Hubs namespace with an event hub and consumer group using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="a86d7-103">Create an Event Hubs namespace with an event hub and consumer group using an Azure Resource Manager template</span></span>
<span data-ttu-id="a86d7-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span><span class="sxs-lookup"><span data-stu-id="a86d7-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="a86d7-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="a86d7-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="a86d7-106">You can use this template for your own deployments, or customize it to meet your requirements</span><span class="sxs-lookup"><span data-stu-id="a86d7-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="a86d7-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="a86d7-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="a86d7-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="a86d7-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="a86d7-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="a86d7-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="a86d7-110">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="a86d7-110">What will you deploy?</span></span>
<span data-ttu-id="a86d7-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span><span class="sxs-lookup"><span data-stu-id="a86d7-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="a86d7-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span><span class="sxs-lookup"><span data-stu-id="a86d7-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="a86d7-113">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="a86d7-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="a86d7-114">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a86d7-114">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a86d7-115">Parameters</span><span class="sxs-lookup"><span data-stu-id="a86d7-115">Parameters</span></span>
<span data-ttu-id="a86d7-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="a86d7-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="a86d7-117">The template includes a section called `Parameters` that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="a86d7-117">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="a86d7-118">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="a86d7-118">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="a86d7-119">Do not define parameters for values that will always stay the same.</span><span class="sxs-lookup"><span data-stu-id="a86d7-119">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="a86d7-120">Each parameter value in the template defines the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="a86d7-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="a86d7-121">The template defines the following parameters.</span><span class="sxs-lookup"><span data-stu-id="a86d7-121">The template defines the following parameters.</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="a86d7-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="a86d7-122">eventHubNamespaceName</span></span>
<span data-ttu-id="a86d7-123">The name of the Event Hubs namespace to create.</span><span class="sxs-lookup"><span data-stu-id="a86d7-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="a86d7-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="a86d7-124">eventHubName</span></span>
<span data-ttu-id="a86d7-125">The name of the event hub created in the Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="a86d7-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="a86d7-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="a86d7-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="a86d7-127">The name of the consumer group created for the event hub.</span><span class="sxs-lookup"><span data-stu-id="a86d7-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="a86d7-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a86d7-128">apiVersion</span></span>
<span data-ttu-id="a86d7-129">The API version of the template.</span><span class="sxs-lookup"><span data-stu-id="a86d7-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="a86d7-130">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="a86d7-130">Resources to deploy</span></span>
<span data-ttu-id="a86d7-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span><span class="sxs-lookup"><span data-stu-id="a86d7-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="a86d7-132">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="a86d7-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="a86d7-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a86d7-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="a86d7-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a86d7-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="a86d7-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="a86d7-135">Next steps</span></span>
<span data-ttu-id="a86d7-136">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="a86d7-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a86d7-137">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="a86d7-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a86d7-138">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="a86d7-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a86d7-139">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="a86d7-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/

