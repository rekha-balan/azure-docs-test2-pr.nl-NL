---
title: Create Service Bus namespace using an Azure Resource Manager template | Microsoft Docs
description: Use Azure Resource Manager template to create a Service Bus namespace
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 08dc0667ccbf9be4f5f4b9060a9c6b4d71088855
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554074"
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="d6976-103">Create a Service Bus namespace using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="d6976-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="d6976-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="d6976-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="d6976-105">The article also defines the parameters that are specified for the execution of the deployment.</span><span class="sxs-lookup"><span data-stu-id="d6976-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="d6976-106">You can use this template for your own deployments, or customize it to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="d6976-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="d6976-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="d6976-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="d6976-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6976-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="d6976-109">The following Azure Resource Manager templates are available for download and deployment.</span><span class="sxs-lookup"><span data-stu-id="d6976-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="d6976-110">Create a Service Bus namespace with queue</span><span class="sxs-lookup"><span data-stu-id="d6976-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="d6976-111">Create a Service Bus namespace with topic and subscription</span><span class="sxs-lookup"><span data-stu-id="d6976-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="d6976-112">Create a Service Bus namespace with queue and authorization rule</span><span class="sxs-lookup"><span data-stu-id="d6976-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="d6976-113">Create a Service Bus namespace with topic, subscription, and rule</span><span class="sxs-lookup"><span data-stu-id="d6976-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="d6976-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d6976-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="d6976-115">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="d6976-115">What will you deploy?</span></span>
<span data-ttu-id="d6976-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span><span class="sxs-lookup"><span data-stu-id="d6976-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="d6976-117">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="d6976-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="d6976-118">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d6976-118">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d6976-119">Parameters</span><span class="sxs-lookup"><span data-stu-id="d6976-119">Parameters</span></span>
<span data-ttu-id="d6976-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="d6976-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="d6976-121">The template includes a section called `Parameters` that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="d6976-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="d6976-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="d6976-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="d6976-123">Do not define parameters for values that will always stay the same.</span><span class="sxs-lookup"><span data-stu-id="d6976-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="d6976-124">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="d6976-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="d6976-125">This template defines the following parameters.</span><span class="sxs-lookup"><span data-stu-id="d6976-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="d6976-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="d6976-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="d6976-127">The name of the Service Bus namespace to create.</span><span class="sxs-lookup"><span data-stu-id="d6976-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="d6976-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="d6976-128">serviceBusSKU</span></span>
<span data-ttu-id="d6976-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span><span class="sxs-lookup"><span data-stu-id="d6976-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="d6976-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span><span class="sxs-lookup"><span data-stu-id="d6976-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="d6976-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="d6976-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="d6976-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="d6976-132">serviceBusApiVersion</span></span>
<span data-ttu-id="d6976-133">The Service Bus API version of the template.</span><span class="sxs-lookup"><span data-stu-id="d6976-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="d6976-134">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="d6976-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="d6976-135">Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="d6976-135">Service Bus namespace</span></span>
<span data-ttu-id="d6976-136">Creates a standard Service Bus namespace of type **Messaging**.</span><span class="sxs-lookup"><span data-stu-id="d6976-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="d6976-137">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="d6976-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d6976-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6976-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="d6976-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6976-139">Azure CLI</span></span>
```CLI
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="d6976-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6976-140">Next steps</span></span>
<span data-ttu-id="d6976-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span><span class="sxs-lookup"><span data-stu-id="d6976-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="d6976-142">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6976-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="d6976-143">Manage Service Bus resources with the Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="d6976-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

