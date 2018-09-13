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
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Create Service Bus resources using Azure Resource Manager templates

This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.

Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments. The template consists of JSON and expressions that you can use to construct values for your deployment. For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue). For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."
>
>

## <a name="service-bus-resource-manager-templates"></a>Service Bus Resource Manager templates

These Service Bus Azure Resource Manager templates are available for download and deployment. Click the following links for details about each one, with links to the templates on GitHub:

* [Create a Service Bus namespace](service-bus-resource-manager-namespace.md)
* [Create a Service Bus namespace with queue](service-bus-resource-manager-namespace-queue.md)
* [Create a Service Bus namespace with topic and subscription](service-bus-resource-manager-namespace-topic.md)
* [Create a Service Bus namespace with queue and authorization rule](service-bus-resource-manager-namespace-auth-rule.md)
* [Create a Service Bus namespace with topic, subscription, and rule](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Deploy with PowerShell

The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace. This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template. The approximate workflow is as follows:

1. Install PowerShell.
2. Create the template and (optionally) a parameter file.
3. In PowerShell, log in to your Azure account.
4. Create a new resource group if one does not exist.
5. Test the deployment.
6. If desired, set the deployment mode.
7. Deploy the template.

For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>Install PowerShell

Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Create a template

Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:

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

### <a name="create-a-parameters-file-optional"></a>Create a parameters file (optional)

To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file. Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.

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

For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameters) topic.

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a>Log in to Azure and set the Azure subscription

From a PowerShell prompt, run the following command:

```powershell
Login-AzureRmAccount
```

You are prompted to log on to your Azure account. After logging on, run the following command to view your available subscriptions.

```powershell
Get-AzureRMSubscription
```

This command returns a list of available Azure subscriptions. Choose a subscription for the current session by running the following command. Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a>Set the resource group

If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command. Provide the name of the resource group and location you want to use. For example:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

If successful, a summary of the new resource group is displayed.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a>Test the deployment

Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet. When testing the deployment, provide parameters exactly as you would when executing the deployment.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a>Create the deployment

To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted. The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file. If the **Mode** parameter is not specified, the default value of **Incremental** is used. For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

The following command prompts you for the three parameters in the PowerShell window:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

To specify a parameters file instead, use the following command.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

You can also use inline parameters when you run the deployment cmdlet. The command is as follows:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a>Verify the deployment
If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:

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

## <a name="next-steps"></a>Next steps
You've now seen the basic workflow and commands for deploying an Azure Resource Manager template. For more detailed information, visit the following links:

* [Azure Resource Manager overview][Azure Resource Manager overview]
* [Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
