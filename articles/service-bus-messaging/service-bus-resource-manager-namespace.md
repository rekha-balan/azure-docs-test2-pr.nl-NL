---
title: Create Service Bus Messaging namespace using Azure Resource Manager template | Microsoft Docs
description: Use Azure Resource Manager template to create a Service Bus Messaging namespace
services: service-bus-messaging
documentationcenter: .net
author: spelluru
manager: timlt
editor: ''
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 04/11/2018
ms.author: spelluru
ms.openlocfilehash: 6c93c3d9ca46eda9e9bdce60b1047af9e9781142
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797685"
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="437ae-103">Create a Service Bus namespace using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="437ae-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="437ae-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard SKU.</span><span class="sxs-lookup"><span data-stu-id="437ae-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard SKU.</span></span> <span data-ttu-id="437ae-105">The article also defines the parameters that are specified for the execution of the deployment.</span><span class="sxs-lookup"><span data-stu-id="437ae-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="437ae-106">You can use this template for your own deployments, or customize it to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="437ae-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="437ae-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="437ae-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="437ae-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="437ae-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="437ae-109">The following Azure Resource Manager templates are available for download and deployment.</span><span class="sxs-lookup"><span data-stu-id="437ae-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="437ae-110">Create a Service Bus namespace with queue</span><span class="sxs-lookup"><span data-stu-id="437ae-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="437ae-111">Create a Service Bus namespace with topic and subscription</span><span class="sxs-lookup"><span data-stu-id="437ae-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="437ae-112">Create a Service Bus namespace with queue and authorization rule</span><span class="sxs-lookup"><span data-stu-id="437ae-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="437ae-113">Create a Service Bus namespace with topic, subscription, and rule</span><span class="sxs-lookup"><span data-stu-id="437ae-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="437ae-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span><span class="sxs-lookup"><span data-stu-id="437ae-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="437ae-115">What will you deploy?</span><span class="sxs-lookup"><span data-stu-id="437ae-115">What will you deploy?</span></span>

<span data-ttu-id="437ae-116">With this template, you deploy a Service Bus namespace with a [Standard or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span><span class="sxs-lookup"><span data-stu-id="437ae-116">With this template, you deploy a Service Bus namespace with a [Standard or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="437ae-117">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="437ae-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="437ae-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="437ae-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="437ae-119">Parameters</span><span class="sxs-lookup"><span data-stu-id="437ae-119">Parameters</span></span>

<span data-ttu-id="437ae-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="437ae-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="437ae-121">The template includes a section called `Parameters` that contains all of the parameter values.</span><span class="sxs-lookup"><span data-stu-id="437ae-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="437ae-122">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="437ae-122">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="437ae-123">Do not define parameters for values that always stay the same.</span><span class="sxs-lookup"><span data-stu-id="437ae-123">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="437ae-124">Each parameter value is used in the template to define the resources that are deployed.</span><span class="sxs-lookup"><span data-stu-id="437ae-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="437ae-125">This template defines the following parameters:</span><span class="sxs-lookup"><span data-stu-id="437ae-125">This template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="437ae-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="437ae-126">serviceBusNamespaceName</span></span>

<span data-ttu-id="437ae-127">The name of the Service Bus namespace to create.</span><span class="sxs-lookup"><span data-stu-id="437ae-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="437ae-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="437ae-128">serviceBusSKU</span></span>

<span data-ttu-id="437ae-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span><span class="sxs-lookup"><span data-stu-id="437ae-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="437ae-130">The template defines the values that are permitted for this parameter (Standard or Premium).</span><span class="sxs-lookup"><span data-stu-id="437ae-130">The template defines the values that are permitted for this parameter (Standard or Premium).</span></span> <span data-ttu-id="437ae-131">If no value is specified, the resource manager assigns a default value (Standard).</span><span class="sxs-lookup"><span data-stu-id="437ae-131">If no value is specified, the resource manager assigns a default value (Standard).</span></span>

<span data-ttu-id="437ae-132">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span><span class="sxs-lookup"><span data-stu-id="437ae-132">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="437ae-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="437ae-133">serviceBusApiVersion</span></span>

<span data-ttu-id="437ae-134">The Service Bus API version of the template.</span><span class="sxs-lookup"><span data-stu-id="437ae-134">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2017-04-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="437ae-135">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="437ae-135">Resources to deploy</span></span>

### <a name="service-bus-namespace"></a><span data-ttu-id="437ae-136">Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="437ae-136">Service Bus namespace</span></span>

<span data-ttu-id="437ae-137">Creates a standard Service Bus namespace of type **Messaging**.</span><span class="sxs-lookup"><span data-stu-id="437ae-137">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "Standard",
        },
        "properties": {
        }
    }
]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="437ae-138">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="437ae-138">Commands to run deployment</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="437ae-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="437ae-139">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="437ae-140">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="437ae-140">Azure CLI</span></span>

```azurecli-interactive
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="437ae-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="437ae-141">Next steps</span></span>
<span data-ttu-id="437ae-142">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span><span class="sxs-lookup"><span data-stu-id="437ae-142">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="437ae-143">Manage Service Bus with PowerShell</span><span class="sxs-lookup"><span data-stu-id="437ae-143">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="437ae-144">Manage Service Bus resources with the Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="437ae-144">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
