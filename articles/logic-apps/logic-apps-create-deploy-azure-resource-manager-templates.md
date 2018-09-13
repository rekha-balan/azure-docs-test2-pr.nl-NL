---
title: Create logic apps with Azure Resource Manager templates - Azure Logic Apps | Microsoft Docs
description: Create and deploy logic app workflows with Azure Resource Manager templates in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.topic: article
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.date: 10/15/2017
ms.openlocfilehash: 70af92c2afd450d357bf9f30187ef200334698ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866114"
---
# <a name="create-and-deploy-logic-apps-with-azure-resource-manager-templates"></a><span data-ttu-id="f9a48-103">Create and deploy logic apps with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="f9a48-103">Create and deploy logic apps with Azure Resource Manager templates</span></span>

<span data-ttu-id="f9a48-104">Azure Logic Apps provides Azure Resource Manager templates that you can use, not only to create logic apps for automating workflows, but also to define the resources and parameters that are used for deployment.</span><span class="sxs-lookup"><span data-stu-id="f9a48-104">Azure Logic Apps provides Azure Resource Manager templates that you can use, not only to create logic apps for automating workflows, but also to define the resources and parameters that are used for deployment.</span></span> <span data-ttu-id="f9a48-105">You can use this template for your own business scenarios or customize the template to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="f9a48-105">You can use this template for your own business scenarios or customize the template to meet your requirements.</span></span> <span data-ttu-id="f9a48-106">Learn more about the [Resource Manager template for logic apps](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json) and [Azure Resource Manager template structure and syntax](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f9a48-106">Learn more about the [Resource Manager template for logic apps](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json) and [Azure Resource Manager template structure and syntax](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

## <a name="define-the-logic-app"></a><span data-ttu-id="f9a48-107">Define the logic app</span><span class="sxs-lookup"><span data-stu-id="f9a48-107">Define the logic app</span></span>

<span data-ttu-id="f9a48-108">This example logic app definition runs once an hour, and pings the location specified in the `testUri` parameter.</span><span class="sxs-lookup"><span data-stu-id="f9a48-108">This example logic app definition runs once an hour, and pings the location specified in the `testUri` parameter.</span></span>
<span data-ttu-id="f9a48-109">The template uses parameter values for the logic app name (```logicAppName```) and the location to ping for testing (```testUri```).</span><span class="sxs-lookup"><span data-stu-id="f9a48-109">The template uses parameter values for the logic app name (```logicAppName```) and the location to ping for testing (```testUri```).</span></span> <span data-ttu-id="f9a48-110">Learn more about [defining these parameters in your template](#define-parameters).</span><span class="sxs-lookup"><span data-stu-id="f9a48-110">Learn more about [defining these parameters in your template](#define-parameters).</span></span> <span data-ttu-id="f9a48-111">The template also sets the location for the logic app to the same location as the Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="f9a48-111">The template also sets the location for the logic app to the same location as the Azure resource group.</span></span> 

``` json
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
         "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
            "testURI": {
               "type": "string",
               "defaultValue": "[parameters('testUri')]"
            }
         },
         "triggers": {
            "Recurrence": {
               "type": "Recurrence",
               "recurrence": {
                  "frequency": "Hour",
                  "interval": 1
               }
            }
         },
         "actions": {
            "Http": {
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
``` 

<a name="define-parameters"></a>

### <a name="define-parameters"></a><span data-ttu-id="f9a48-112">Define parameters</span><span class="sxs-lookup"><span data-stu-id="f9a48-112">Define parameters</span></span>

[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

<span data-ttu-id="f9a48-113">Here are descriptions for the parameters in the template:</span><span class="sxs-lookup"><span data-stu-id="f9a48-113">Here are descriptions for the parameters in the template:</span></span>

| <span data-ttu-id="f9a48-114">Parameter</span><span class="sxs-lookup"><span data-stu-id="f9a48-114">Parameter</span></span> | <span data-ttu-id="f9a48-115">Description</span><span class="sxs-lookup"><span data-stu-id="f9a48-115">Description</span></span> | <span data-ttu-id="f9a48-116">JSON definition example</span><span class="sxs-lookup"><span data-stu-id="f9a48-116">JSON definition example</span></span> | 
| --------- | ----------- | ----------------------- | 
| `logicAppName` | <span data-ttu-id="f9a48-117">Defines the name of the logic app that template creates.</span><span class="sxs-lookup"><span data-stu-id="f9a48-117">Defines the name of the logic app that template creates.</span></span> | <span data-ttu-id="f9a48-118">"logicAppName": { "type": "string", "metadata": { "description": "myExampleLogicAppName" } }</span><span class="sxs-lookup"><span data-stu-id="f9a48-118">"logicAppName": { "type": "string", "metadata": { "description": "myExampleLogicAppName" } }</span></span> |
| `testUri` | <span data-ttu-id="f9a48-119">Defines the location to ping for testing.</span><span class="sxs-lookup"><span data-stu-id="f9a48-119">Defines the location to ping for testing.</span></span> | <span data-ttu-id="f9a48-120">"testUri": { "type": "string", "defaultValue": "http://azure.microsoft.com/status/feed/"}</span><span class="sxs-lookup"><span data-stu-id="f9a48-120">"testUri": { "type": "string", "defaultValue": "http://azure.microsoft.com/status/feed/"}</span></span> | 
||||

<span data-ttu-id="f9a48-121">Learn more about [REST API for Logic Apps Workflow definition and properties](https://docs.microsoft.com/rest/api/logic/workflows) and [building on logic app definitions with JSON](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="f9a48-121">Learn more about [REST API for Logic Apps Workflow definition and properties](https://docs.microsoft.com/rest/api/logic/workflows) and [building on logic app definitions with JSON](logic-apps-author-definitions.md).</span></span>

## <a name="deploy-logic-apps-automatically"></a><span data-ttu-id="f9a48-122">Deploy logic apps automatically</span><span class="sxs-lookup"><span data-stu-id="f9a48-122">Deploy logic apps automatically</span></span>

<span data-ttu-id="f9a48-123">To create and automatically deploy a logic app to Azure, choose **Deploy to Azure** here:</span><span class="sxs-lookup"><span data-stu-id="f9a48-123">To create and automatically deploy a logic app to Azure, choose **Deploy to Azure** here:</span></span>

<span data-ttu-id="f9a48-124">[![Deploy to Azure](./media/logic-apps-create-deploy-azure-resource-manager-templates/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="f9a48-124">[![Deploy to Azure](./media/logic-apps-create-deploy-azure-resource-manager-templates/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

<span data-ttu-id="f9a48-125">This action signs you in to the Azure portal where you can provide your logic app's details and make any changes to the template or parameters.</span><span class="sxs-lookup"><span data-stu-id="f9a48-125">This action signs you in to the Azure portal where you can provide your logic app's details and make any changes to the template or parameters.</span></span> <span data-ttu-id="f9a48-126">For example, the Azure portal prompts you for these details:</span><span class="sxs-lookup"><span data-stu-id="f9a48-126">For example, the Azure portal prompts you for these details:</span></span>

* <span data-ttu-id="f9a48-127">Azure subscription name</span><span class="sxs-lookup"><span data-stu-id="f9a48-127">Azure subscription name</span></span>
* <span data-ttu-id="f9a48-128">Resource group that you want to use</span><span class="sxs-lookup"><span data-stu-id="f9a48-128">Resource group that you want to use</span></span>
* <span data-ttu-id="f9a48-129">Logic app location</span><span class="sxs-lookup"><span data-stu-id="f9a48-129">Logic app location</span></span>
* <span data-ttu-id="f9a48-130">A name for your logic app</span><span class="sxs-lookup"><span data-stu-id="f9a48-130">A name for your logic app</span></span>
* <span data-ttu-id="f9a48-131">A test URI</span><span class="sxs-lookup"><span data-stu-id="f9a48-131">A test URI</span></span>
* <span data-ttu-id="f9a48-132">Acceptance of the specified terms and conditions</span><span class="sxs-lookup"><span data-stu-id="f9a48-132">Acceptance of the specified terms and conditions</span></span>

## <a name="deploy-logic-apps-with-commands"></a><span data-ttu-id="f9a48-133">Deploy logic apps with commands</span><span class="sxs-lookup"><span data-stu-id="f9a48-133">Deploy logic apps with commands</span></span>

[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="f9a48-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9a48-134">PowerShell</span></span>

```
New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup
``` 

### <a name="azure-cli"></a><span data-ttu-id="f9a48-135">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f9a48-135">Azure CLI</span></span>

```
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup
```

## <a name="get-support"></a><span data-ttu-id="f9a48-136">Get support</span><span class="sxs-lookup"><span data-stu-id="f9a48-136">Get support</span></span>

* <span data-ttu-id="f9a48-137">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="f9a48-137">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="f9a48-138">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="f9a48-138">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9a48-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9a48-139">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9a48-140">Monitor logic apps</span><span class="sxs-lookup"><span data-stu-id="f9a48-140">Monitor logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)