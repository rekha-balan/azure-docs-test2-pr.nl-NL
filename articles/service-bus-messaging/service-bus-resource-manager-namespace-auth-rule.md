---
title: Create Service Bus authorization rule using Azure Resource Manager template | Microsoft Docs
description: Create a Service Bus authorization rule for namespace and queue using Azure Resource Manager template
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 04/18/2017
ms.author: sethm;shvija
ms.openlocfilehash: d80f374d0e42c1c14fc2de0d5150e7cc62b5a224
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555200"
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="8e520-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="8e520-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="8e520-104">This article shows how to use an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span><span class="sxs-lookup"><span data-stu-id="8e520-104">This article shows how to use an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="8e520-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="8e520-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="8e520-106">You can use this template for your own deployments, or customize it to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="8e520-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="8e520-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8e520-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="8e520-108">For the complete template, see the [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="8e520-108">For the complete template, see the [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="8e520-109">The following Azure Resource Manager templates are available for download and deployment.</span><span class="sxs-lookup"><span data-stu-id="8e520-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="8e520-110">Create a Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="8e520-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="8e520-111">Create a Service Bus namespace with queue</span><span class="sxs-lookup"><span data-stu-id="8e520-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="8e520-112">Create a Service Bus namespace with topic and subscription</span><span class="sxs-lookup"><span data-stu-id="8e520-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="8e520-113">Create a Service Bus namespace with topic, subscription, and rule</span><span class="sxs-lookup"><span data-stu-id="8e520-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="8e520-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span><span class="sxs-lookup"><span data-stu-id="8e520-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="8e520-115">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="8e520-115">What will you deploy?</span></span>
<span data-ttu-id="8e520-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span><span class="sxs-lookup"><span data-stu-id="8e520-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="8e520-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span><span class="sxs-lookup"><span data-stu-id="8e520-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="8e520-118">SAS enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span><span class="sxs-lookup"><span data-stu-id="8e520-118">SAS enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="8e520-119">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8e520-119">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span></span>

<span data-ttu-id="8e520-120">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="8e520-120">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="8e520-121">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8e520-121">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8e520-122">Parameters</span><span class="sxs-lookup"><span data-stu-id="8e520-122">Parameters</span></span>

<span data-ttu-id="8e520-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="8e520-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="8e520-124">The template includes a section called `Parameters` that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="8e520-124">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="8e520-125">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="8e520-125">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="8e520-126">Do not define parameters for values that will always stay the same.</span><span class="sxs-lookup"><span data-stu-id="8e520-126">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="8e520-127">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="8e520-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="8e520-128">The template defines the following parameters.</span><span class="sxs-lookup"><span data-stu-id="8e520-128">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="8e520-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="8e520-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="8e520-130">The name of the Service Bus namespace to create.</span><span class="sxs-lookup"><span data-stu-id="8e520-130">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="8e520-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="8e520-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="8e520-132">The name of the authorization rule for the namespace.</span><span class="sxs-lookup"><span data-stu-id="8e520-132">The name of the authorization rule for the namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="8e520-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="8e520-133">serviceBusQueueName</span></span>
<span data-ttu-id="8e520-134">The name of the queue in the Service Bus namespace.</span><span class="sxs-lookup"><span data-stu-id="8e520-134">The name of the queue in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="8e520-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="8e520-135">serviceBusApiVersion</span></span>
<span data-ttu-id="8e520-136">The Service Bus API version of the template.</span><span class="sxs-lookup"><span data-stu-id="8e520-136">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="8e520-137">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="8e520-137">Resources to deploy</span></span>
<span data-ttu-id="8e520-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span><span class="sxs-lookup"><span data-stu-id="8e520-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="8e520-139">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="8e520-139">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="8e520-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e520-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="8e520-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e520-141">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="8e520-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e520-142">Next steps</span></span>
<span data-ttu-id="8e520-143">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span><span class="sxs-lookup"><span data-stu-id="8e520-143">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="8e520-144">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e520-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="8e520-145">Manage Service Bus resources with the Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="8e520-145">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="8e520-146">Service Bus authentication and authorization</span><span class="sxs-lookup"><span data-stu-id="8e520-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/

