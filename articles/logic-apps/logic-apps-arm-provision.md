---
title: Create a logic app using a template in Azure | Microsoft Docs
description: Use an Azure Resource Manager template to deploy a logic app for defining workflows.
services: logic-apps
documentationcenter: ''
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: mandia
ms.openlocfilehash: db08984ff86218ca3ebc45f9e8e3bca9433bfe5d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563220"
---
# <a name="create-a-logic-app-using-a-template"></a>Create a Logic App using a template
Templates provide a quick way to use different connectors within a logic app. Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows. You can define which resources are deployed, and how to define parameters when you deploy your logic app. You can use this template for your own business scenarios, or customize it to meet your requirements.

For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md). 

For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).

For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>What you deploy
With this template, you deploy a logic app.

To run the deployment automatically, select the following button:  

[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>Parameters
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a>Resources to deploy
### <a name="logic-app"></a>Logic app
Creates the logic app.

The templates uses a parameter value for the logic app name. It sets the location of the logic app to the same location as the resource group. 

This particular definition runs once an hour, and pings the location specified in the **testUri** parameter. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-to-run-deployment"></a>Commands to run deployment
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup




