---
title: Create Azure Service Bus resources using Azure Resource Manager templates | Microsoft Docs
description: Use Azure Resource Manager templates to automate the creation of Service Bus resources
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 04/18/2017
ms.author: sethm
ms.openlocfilehash: f5727f6c761715dfff70025bb275ac8db4947a2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549569"
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="8647b-103">Create Service Bus resources using Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="8647b-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="8647b-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span><span class="sxs-lookup"><span data-stu-id="8647b-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="8647b-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span><span class="sxs-lookup"><span data-stu-id="8647b-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="8647b-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span><span class="sxs-lookup"><span data-stu-id="8647b-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="8647b-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8647b-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8647b-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span><span class="sxs-lookup"><span data-stu-id="8647b-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="8647b-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span><span class="sxs-lookup"><span data-stu-id="8647b-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="8647b-110">Service Bus Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="8647b-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="8647b-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span><span class="sxs-lookup"><span data-stu-id="8647b-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="8647b-112">Click the following links for details about each one, with links to the templates on GitHub:</span><span class="sxs-lookup"><span data-stu-id="8647b-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="8647b-113">Create a Service Bus namespace</span><span class="sxs-lookup"><span data-stu-id="8647b-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="8647b-114">Create a Service Bus namespace with queue</span><span class="sxs-lookup"><span data-stu-id="8647b-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="8647b-115">Create a Service Bus namespace with topic and subscription</span><span class="sxs-lookup"><span data-stu-id="8647b-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="8647b-116">Create a Service Bus namespace with queue and authorization rule</span><span class="sxs-lookup"><span data-stu-id="8647b-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="8647b-117">Create a Service Bus namespace with topic, subscription, and rule</span><span class="sxs-lookup"><span data-stu-id="8647b-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="8647b-118">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="8647b-118">Deploy with PowerShell</span></span>

<span data-ttu-id="8647b-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span><span class="sxs-lookup"><span data-stu-id="8647b-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="8647b-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span><span class="sxs-lookup"><span data-stu-id="8647b-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="8647b-121">The approximate workflow is as follows:</span><span class="sxs-lookup"><span data-stu-id="8647b-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="8647b-122">Install PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8647b-122">Install PowerShell.</span></span>
2. <span data-ttu-id="8647b-123">Create the template and (optionally) a parameter file.</span><span class="sxs-lookup"><span data-stu-id="8647b-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="8647b-124">In PowerShell, log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="8647b-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="8647b-125">Create a new resource group if one does not exist.</span><span class="sxs-lookup"><span data-stu-id="8647b-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="8647b-126">Test the deployment.</span><span class="sxs-lookup"><span data-stu-id="8647b-126">Test the deployment.</span></span>
6. <span data-ttu-id="8647b-127">If desired, set the deployment mode.</span><span class="sxs-lookup"><span data-stu-id="8647b-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="8647b-128">Deploy the template.</span><span class="sxs-lookup"><span data-stu-id="8647b-128">Deploy the template.</span></span>

<span data-ttu-id="8647b-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8647b-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="8647b-130">Install PowerShell</span><span class="sxs-lookup"><span data-stu-id="8647b-130">Install PowerShell</span></span>

<span data-ttu-id="8647b-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="8647b-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="8647b-132">Create a template</span><span class="sxs-lookup"><span data-stu-id="8647b-132">Create a template</span></span>

<span data-ttu-id="8647b-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span><span class="sxs-lookup"><span data-stu-id="8647b-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="8647b-134">Create a parameters file (optional)</span><span class="sxs-lookup"><span data-stu-id="8647b-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="8647b-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span><span class="sxs-lookup"><span data-stu-id="8647b-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="8647b-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span><span class="sxs-lookup"><span data-stu-id="8647b-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="8647b-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameters) topic.</span><span class="sxs-lookup"><span data-stu-id="8647b-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameters) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="8647b-138">Log in to Azure and set the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="8647b-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="8647b-139">From a PowerShell prompt, run the following command:</span><span class="sxs-lookup"><span data-stu-id="8647b-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8647b-140">You are prompted to log on to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="8647b-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="8647b-141">After logging on, run the following command to view your available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8647b-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="8647b-142">This command returns a list of available Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8647b-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="8647b-143">Choose a subscription for the current session by running the following command.</span><span class="sxs-lookup"><span data-stu-id="8647b-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="8647b-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span><span class="sxs-lookup"><span data-stu-id="8647b-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="8647b-145">Set the resource group</span><span class="sxs-lookup"><span data-stu-id="8647b-145">Set the resource group</span></span>

<span data-ttu-id="8647b-146">If you do not have an existing resource group, create a new resource group with the \*\*New-AzureRmResourceGroup \*\* command.</span><span class="sxs-lookup"><span data-stu-id="8647b-146">If you do not have an existing resource group, create a new resource group with the \*\*New-AzureRmResourceGroup \*\* command.</span></span> <span data-ttu-id="8647b-147">Provide the name of the resource group and location you want to use.</span><span class="sxs-lookup"><span data-stu-id="8647b-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="8647b-148">For example:</span><span class="sxs-lookup"><span data-stu-id="8647b-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="8647b-149">If successful, a summary of the new resource group is displayed.</span><span class="sxs-lookup"><span data-stu-id="8647b-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="8647b-150">Test the deployment</span><span class="sxs-lookup"><span data-stu-id="8647b-150">Test the deployment</span></span>

<span data-ttu-id="8647b-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8647b-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="8647b-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span><span class="sxs-lookup"><span data-stu-id="8647b-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="8647b-153">Create the deployment</span><span class="sxs-lookup"><span data-stu-id="8647b-153">Create the deployment</span></span>

<span data-ttu-id="8647b-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span><span class="sxs-lookup"><span data-stu-id="8647b-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="8647b-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span><span class="sxs-lookup"><span data-stu-id="8647b-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="8647b-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span><span class="sxs-lookup"><span data-stu-id="8647b-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="8647b-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="8647b-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="8647b-158">The following command prompts you for the three parameters in the PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="8647b-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="8647b-159">To specify a parameters file instead, use the following command.</span><span class="sxs-lookup"><span data-stu-id="8647b-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="8647b-160">You can also use inline parameters when you run the deployment cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8647b-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="8647b-161">The command is as follows:</span><span class="sxs-lookup"><span data-stu-id="8647b-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="8647b-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span><span class="sxs-lookup"><span data-stu-id="8647b-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="8647b-163">Verify the deployment</span><span class="sxs-lookup"><span data-stu-id="8647b-163">Verify the deployment</span></span>
<span data-ttu-id="8647b-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="8647b-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="8647b-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="8647b-165">Next steps</span></span>
<span data-ttu-id="8647b-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="8647b-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="8647b-167">For more detailed information, visit the following links:</span><span class="sxs-lookup"><span data-stu-id="8647b-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="8647b-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="8647b-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="8647b-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="8647b-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="8647b-170">Authoring Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="8647b-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
