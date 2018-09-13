---
title: Create Azure Service Bus namespace topic subscription using Azure Resource Manager template | Microsoft Docs
description: Create a Service Bus namespace with topic and subscription using Azure Resource Manager template
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 04/18/2017
ms.author: sethm;shvija
ms.openlocfilehash: b8f4356bfd157c6ce8fdc0388be801cafa37024d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556438"
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="1348b-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="1348b-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="1348b-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span><span class="sxs-lookup"><span data-stu-id="1348b-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="1348b-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="1348b-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="1348b-106">You can use this template for your own deployments, or customize it to meet your requirements</span><span class="sxs-lookup"><span data-stu-id="1348b-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="1348b-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="1348b-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="1348b-108">For the complete template, see the [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span><span class="sxs-lookup"><span data-stu-id="1348b-108">For the complete template, see the [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="1348b-109">The following Azure Resource Manager templates are available for download and deployment.</span><span class="sxs-lookup"><span data-stu-id="1348b-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="1348b-110">Create a Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="1348b-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="1348b-111">Create a Service Bus namespace with queue</span><span class="sxs-lookup"><span data-stu-id="1348b-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="1348b-112">Create a Service Bus namespace with queue and authorization rule</span><span class="sxs-lookup"><span data-stu-id="1348b-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="1348b-113">Create a Service Bus namespace with topic, subscription, and rule</span><span class="sxs-lookup"><span data-stu-id="1348b-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="1348b-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span><span class="sxs-lookup"><span data-stu-id="1348b-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="1348b-115">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="1348b-115">What will you deploy?</span></span>

<span data-ttu-id="1348b-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span><span class="sxs-lookup"><span data-stu-id="1348b-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="1348b-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span><span class="sxs-lookup"><span data-stu-id="1348b-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="1348b-118">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="1348b-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="1348b-119">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="1348b-119">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="1348b-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="1348b-120">Parameters</span></span>

<span data-ttu-id="1348b-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="1348b-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="1348b-122">The template includes a section called `Parameters` that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="1348b-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="1348b-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="1348b-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="1348b-124">Do not define parameters for values that will always stay the same.</span><span class="sxs-lookup"><span data-stu-id="1348b-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="1348b-125">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="1348b-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="1348b-126">The template defines the following parameters.</span><span class="sxs-lookup"><span data-stu-id="1348b-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="1348b-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="1348b-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="1348b-128">The name of the Service Bus namespace to create.</span><span class="sxs-lookup"><span data-stu-id="1348b-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="1348b-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="1348b-129">serviceBusTopicName</span></span>
<span data-ttu-id="1348b-130">The name of the topic created in the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="1348b-130">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="1348b-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="1348b-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="1348b-132">The name of the subscription created in the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="1348b-132">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="1348b-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="1348b-133">serviceBusApiVersion</span></span>
<span data-ttu-id="1348b-134">The Service Bus API version of the template.</span><span class="sxs-lookup"><span data-stu-id="1348b-134">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="1348b-135">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="1348b-135">Resources to deploy</span></span>
<span data-ttu-id="1348b-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span><span class="sxs-lookup"><span data-stu-id="1348b-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="1348b-137">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="1348b-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="1348b-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1348b-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="1348b-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1348b-139">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="1348b-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="1348b-140">Next steps</span></span>
<span data-ttu-id="1348b-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span><span class="sxs-lookup"><span data-stu-id="1348b-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="1348b-142">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="1348b-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="1348b-143">Manage Service Bus resources with the Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="1348b-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/

