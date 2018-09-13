---
title: Create Azure Service Bus topic subscription and rule using Azure Resource Manager template | Microsoft Docs
description: Create a Service Bus namespace with topic, subscription, and rule using Azure Resource Manager template
services: service-bus-messaging
documentationcenter: .net
author: spelluru
manager: timlt
editor: ''
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 04/11/2018
ms.author: spelluru
ms.openlocfilehash: dd0ef94c7efb27641d5f0bf50d87bf852bcd1e9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821163"
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="15924-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="15924-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="15924-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span><span class="sxs-lookup"><span data-stu-id="15924-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="15924-105">The article explains how to specify which resources are deployed and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="15924-105">The article explains how to specify which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="15924-106">You can use this template for your own deployments, or customize it to meet your requirements</span><span class="sxs-lookup"><span data-stu-id="15924-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="15924-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="15924-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="15924-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="15924-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="15924-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span><span class="sxs-lookup"><span data-stu-id="15924-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="15924-110">The following Azure Resource Manager templates are available for download and deployment.</span><span class="sxs-lookup"><span data-stu-id="15924-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="15924-111">Create a Service Bus namespace with queue and authorization rule</span><span class="sxs-lookup"><span data-stu-id="15924-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="15924-112">Create a Service Bus namespace with queue</span><span class="sxs-lookup"><span data-stu-id="15924-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="15924-113">Create a Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="15924-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="15924-114">Create a Service Bus namespace with topic and subscription</span><span class="sxs-lookup"><span data-stu-id="15924-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="15924-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span><span class="sxs-lookup"><span data-stu-id="15924-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="15924-116">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="15924-116">What will you deploy?</span></span>

<span data-ttu-id="15924-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span><span class="sxs-lookup"><span data-stu-id="15924-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="15924-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span><span class="sxs-lookup"><span data-stu-id="15924-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="15924-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span><span class="sxs-lookup"><span data-stu-id="15924-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="15924-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span><span class="sxs-lookup"><span data-stu-id="15924-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="15924-121">What are rules (filters)?</span><span class="sxs-lookup"><span data-stu-id="15924-121">What are rules (filters)?</span></span>

<span data-ttu-id="15924-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span><span class="sxs-lookup"><span data-stu-id="15924-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="15924-123">To enable this custom processing, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span><span class="sxs-lookup"><span data-stu-id="15924-123">To enable this custom processing, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="15924-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span><span class="sxs-lookup"><span data-stu-id="15924-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="15924-125">This is accomplished using subscription filters.</span><span class="sxs-lookup"><span data-stu-id="15924-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="15924-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="15924-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="15924-127">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="15924-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="15924-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="15924-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="15924-129">Parameters</span><span class="sxs-lookup"><span data-stu-id="15924-129">Parameters</span></span>

<span data-ttu-id="15924-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="15924-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="15924-131">The template includes a section called `Parameters` that contains all the parameter values.</span><span class="sxs-lookup"><span data-stu-id="15924-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="15924-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="15924-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="15924-133">Do not define parameters for values that always stay the same.</span><span class="sxs-lookup"><span data-stu-id="15924-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="15924-134">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="15924-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="15924-135">The template defines the following parameters:</span><span class="sxs-lookup"><span data-stu-id="15924-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="15924-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="15924-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="15924-137">The name of the Service Bus namespace to create.</span><span class="sxs-lookup"><span data-stu-id="15924-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="15924-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="15924-138">serviceBusTopicName</span></span>
<span data-ttu-id="15924-139">The name of the topic created in the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="15924-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="15924-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="15924-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="15924-141">The name of the subscription created in the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="15924-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="15924-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="15924-142">serviceBusRuleName</span></span>
<span data-ttu-id="15924-143">The name of the rule(filter) created in the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="15924-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="15924-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="15924-144">serviceBusApiVersion</span></span>
<span data-ttu-id="15924-145">The Service Bus API version of the template.</span><span class="sxs-lookup"><span data-stu-id="15924-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2017-04-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       }
```
## <a name="resources-to-deploy"></a><span data-ttu-id="15924-146">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="15924-146">Resources to deploy</span></span>
<span data-ttu-id="15924-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span><span class="sxs-lookup"><span data-stu-id="15924-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filterType": "SqlFilter",
                        "sqlFilter": {
                            "sqlExpression": "StoreName = 'Store1'",
                            "requiresPreprocessing": "false"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="15924-148">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="15924-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="15924-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15924-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="15924-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15924-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="15924-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="15924-151">Next steps</span></span>
<span data-ttu-id="15924-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span><span class="sxs-lookup"><span data-stu-id="15924-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="15924-153">Manage Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="15924-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="15924-154">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="15924-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="15924-155">Manage Service Bus resources with the Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="15924-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

