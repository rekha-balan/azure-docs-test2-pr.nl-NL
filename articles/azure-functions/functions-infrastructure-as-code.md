---
title: Automate resource deployment for an Azure Functions app | Microsoft Docs
description: Learn how to build an Azure Resource Manager template that deploys your Azure Functions app.
services: Functions
documtationcenter: na
author: mattchenderson
manager: erikre
editor: ''
tags: ''
keywords: azure functions, functions, serverless architecture, infrastructure as code, azure resource manager
ms.assetid: ''
ms.server: functions
ms.devlang: multiple
ms.topic: ''
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/23/2017
ms.author: cfowler;glenga
ms.openlocfilehash: 979537bfe6b0e14a9208871fc9862661d2fb2e6c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44668952"
---
# <a name="automate-resource-deployment-for-your-azure-functions-app"></a><span data-ttu-id="370e5-104">Automate resource deployment for your Azure Functions app</span><span class="sxs-lookup"><span data-stu-id="370e5-104">Automate resource deployment for your Azure Functions app</span></span>

<span data-ttu-id="370e5-105">You can use an Azure Resource Manager template to deploy an Azure Functions app.</span><span class="sxs-lookup"><span data-stu-id="370e5-105">You can use an Azure Resource Manager template to deploy an Azure Functions app.</span></span> <span data-ttu-id="370e5-106">Learn how to define the baseline resources that are required for an Azure Functions app, and the parameters that are specified during deployment.</span><span class="sxs-lookup"><span data-stu-id="370e5-106">Learn how to define the baseline resources that are required for an Azure Functions app, and the parameters that are specified during deployment.</span></span> <span data-ttu-id="370e5-107">Depending on the [triggers and bindings](functions-triggers-bindings.md) in your Functions app, for a successful Infrastructure as Code configuration of your application, you might need to deploy additional resources.</span><span class="sxs-lookup"><span data-stu-id="370e5-107">Depending on the [triggers and bindings](functions-triggers-bindings.md) in your Functions app, for a successful Infrastructure as Code configuration of your application, you might need to deploy additional resources.</span></span>

<span data-ttu-id="370e5-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="370e5-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="370e5-109">For examples of complete templates, see [Create a Consumption plan-based Azure Functions app](https://github.com/Azure/azure-quickstart-templates/blob/052db5feeba11f85d57f170d8202123511f72044/101-function-app-create-dynamic/azuredeploy.json) and [Create an App Service plan-based Azure Functions app](https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="370e5-109">For examples of complete templates, see [Create a Consumption plan-based Azure Functions app](https://github.com/Azure/azure-quickstart-templates/blob/052db5feeba11f85d57f170d8202123511f72044/101-function-app-create-dynamic/azuredeploy.json) and [Create an App Service plan-based Azure Functions app](https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json).</span></span>

## <a name="required-resources"></a><span data-ttu-id="370e5-110">Required resources</span><span class="sxs-lookup"><span data-stu-id="370e5-110">Required resources</span></span>

<span data-ttu-id="370e5-111">You can use the examples in this article to create a baseline Azure Functions app.</span><span class="sxs-lookup"><span data-stu-id="370e5-111">You can use the examples in this article to create a baseline Azure Functions app.</span></span> <span data-ttu-id="370e5-112">You'll need these resources for your app:</span><span class="sxs-lookup"><span data-stu-id="370e5-112">You'll need these resources for your app:</span></span>

* <span data-ttu-id="370e5-113">[Azure Storage](../storage/index.md) account</span><span class="sxs-lookup"><span data-stu-id="370e5-113">[Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="370e5-114">Hosting plan (Consumption plan or Azure App Service plan)</span><span class="sxs-lookup"><span data-stu-id="370e5-114">Hosting plan (Consumption plan or Azure App Service plan)</span></span>
* <span data-ttu-id="370e5-115">Functions app (`type`: **Microsoft.Web/Site**, `kind`: **functionapp**)</span><span class="sxs-lookup"><span data-stu-id="370e5-115">Functions app (`type`: **Microsoft.Web/Site**, `kind`: **functionapp**)</span></span>

## <a name="parameters"></a><span data-ttu-id="370e5-116">Parameters</span><span class="sxs-lookup"><span data-stu-id="370e5-116">Parameters</span></span>

<span data-ttu-id="370e5-117">You can use Azure Resource Manager to define parameters for values that you want to specify when your template is deployed.</span><span class="sxs-lookup"><span data-stu-id="370e5-117">You can use Azure Resource Manager to define parameters for values that you want to specify when your template is deployed.</span></span> <span data-ttu-id="370e5-118">A template's **Parameters** section has all the parameter values.</span><span class="sxs-lookup"><span data-stu-id="370e5-118">A template's **Parameters** section has all the parameter values.</span></span> <span data-ttu-id="370e5-119">Define parameters for values that vary based either on the project you are deploying, or on the environment you are deploying to.</span><span class="sxs-lookup"><span data-stu-id="370e5-119">Define parameters for values that vary based either on the project you are deploying, or on the environment you are deploying to.</span></span>

<span data-ttu-id="370e5-120">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are useful for values that don't change based on an individual deployment, and for parameters that require transformation before being used in a template (for example, to pass validation rules).</span><span class="sxs-lookup"><span data-stu-id="370e5-120">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are useful for values that don't change based on an individual deployment, and for parameters that require transformation before being used in a template (for example, to pass validation rules).</span></span>

<span data-ttu-id="370e5-121">When you define parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span><span class="sxs-lookup"><span data-stu-id="370e5-121">When you define parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span></span> <span data-ttu-id="370e5-122">To assign a value to the parameter, if no value is provided during deployment, use the **defaultValue** field.</span><span class="sxs-lookup"><span data-stu-id="370e5-122">To assign a value to the parameter, if no value is provided during deployment, use the **defaultValue** field.</span></span>

<span data-ttu-id="370e5-123">An Azure Resource Manager template uses the following parameters.</span><span class="sxs-lookup"><span data-stu-id="370e5-123">An Azure Resource Manager template uses the following parameters.</span></span>

### <a name="appname"></a><span data-ttu-id="370e5-124">appName</span><span class="sxs-lookup"><span data-stu-id="370e5-124">appName</span></span>

<span data-ttu-id="370e5-125">The name of the Azure Functions app that you want to create.</span><span class="sxs-lookup"><span data-stu-id="370e5-125">The name of the Azure Functions app that you want to create.</span></span>

```json
"appName": {
    "type": "string"
}
```

### <a name="location"></a><span data-ttu-id="370e5-126">location</span><span class="sxs-lookup"><span data-stu-id="370e5-126">location</span></span>

<span data-ttu-id="370e5-127">Where to deploy the Functions app.</span><span class="sxs-lookup"><span data-stu-id="370e5-127">Where to deploy the Functions app.</span></span>

> [!NOTE]
> <span data-ttu-id="370e5-128">To inherit the location of the Resource Group, or if a parameter value isn't specified during a PowerShell or Azure CLI deployment, use the **defaultValue** parameter.</span><span class="sxs-lookup"><span data-stu-id="370e5-128">To inherit the location of the Resource Group, or if a parameter value isn't specified during a PowerShell or Azure CLI deployment, use the **defaultValue** parameter.</span></span> <span data-ttu-id="370e5-129">If you deploy your app from the Azure portal, select a value in the **allowedValues** parameter drop-down box.</span><span class="sxs-lookup"><span data-stu-id="370e5-129">If you deploy your app from the Azure portal, select a value in the **allowedValues** parameter drop-down box.</span></span>

> [!TIP]
> <span data-ttu-id="370e5-130">For an up-to-date list of regions where you can use Azure Functions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="370e5-130">For an up-to-date list of regions where you can use Azure Functions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>

```json
"location": {
    "type": "string",
    "allowedValues": [
        "Brazil South",
        "East US",
        "East US 2",
        "Central US",
        "North Central US",
        "South Central US",
        "West US",
        "West US 2"
    ],
    "defaultValue": "[resourceGroup().location]"
}
```

### <a name="sourcecoderepositoryurl-optional"></a><span data-ttu-id="370e5-131">sourceCodeRepositoryURL (optional)</span><span class="sxs-lookup"><span data-stu-id="370e5-131">sourceCodeRepositoryURL (optional)</span></span>

```json
"sourceCodeRepositoryURL": {
    "type": "string",
    "defaultValue": "",
    "metadata": {
    "description": "Source code repository URL"
}
```

### <a name="sourcecodebranch-optional"></a><span data-ttu-id="370e5-132">sourceCodeBranch (optional)</span><span class="sxs-lookup"><span data-stu-id="370e5-132">sourceCodeBranch (optional)</span></span>

```json
    "sourceCodeBranch": {
      "type": "string",
      "defaultValue": "master",
      "metadata": {
        "description": "Source code repository branch"
      }
    }
```

### <a name="sourcecodemanualintegration-optional"></a><span data-ttu-id="370e5-133">sourceCodeManualIntegration (optional)</span><span class="sxs-lookup"><span data-stu-id="370e5-133">sourceCodeManualIntegration (optional)</span></span>

```json
"sourceCodeManualIntegration": {
    "type": "bool",
    "defaultValue": false,
    "metadata": {
        "description": "Use 'true' if you are deploying from the base repo. Use 'false' if you are deploying from your own fork. If you use 'false', make sure that you have Administrator rights in the repo. If you get an error, manually add GitHub integration to another web app, to associate a GitHub access token with your Azure subscription."
    }
}
```

## <a name="variables"></a><span data-ttu-id="370e5-134">Variables</span><span class="sxs-lookup"><span data-stu-id="370e5-134">Variables</span></span>

<span data-ttu-id="370e5-135">Azure Resource Manager templates use variables to incorporate parameters, so you can use more specific settings in your template.</span><span class="sxs-lookup"><span data-stu-id="370e5-135">Azure Resource Manager templates use variables to incorporate parameters, so you can use more specific settings in your template.</span></span>

<span data-ttu-id="370e5-136">In the next example, to meet Azure storage account [naming requirements](../storage/storage-create-storage-account.md#create-a-storage-account), we use variables to apply [Azure Resource Manager template functions](../azure-resource-manager/resource-group-template-functions.md) to convert the entered **appName** value to lowercase.</span><span class="sxs-lookup"><span data-stu-id="370e5-136">In the next example, to meet Azure storage account [naming requirements](../storage/storage-create-storage-account.md#create-a-storage-account), we use variables to apply [Azure Resource Manager template functions](../azure-resource-manager/resource-group-template-functions.md) to convert the entered **appName** value to lowercase.</span></span>

```json
"variables": {
    "lowerSiteName": "[toLower(parameters('appName'))]",
    "storageAccountName": "[concat(variables('lowerSiteName'))]"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="370e5-137">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="370e5-137">Resources to deploy</span></span>

### <a name="storage-account"></a><span data-ttu-id="370e5-138">Storage account</span><span class="sxs-lookup"><span data-stu-id="370e5-138">Storage account</span></span>

<span data-ttu-id="370e5-139">An Azure storage account is required for an Azure Functions app.</span><span class="sxs-lookup"><span data-stu-id="370e5-139">An Azure storage account is required for an Azure Functions app.</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('storageLocation')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
}
```

### <a name="hosting-plan-consumption-vs-app-service"></a><span data-ttu-id="370e5-140">Hosting plan: Consumption vs. App Service</span><span class="sxs-lookup"><span data-stu-id="370e5-140">Hosting plan: Consumption vs. App Service</span></span>

<span data-ttu-id="370e5-141">In some scenarios, you might want your functions scaled on-demand by the platform, also called fully managed scaling (by using a Consumption hosting plan).</span><span class="sxs-lookup"><span data-stu-id="370e5-141">In some scenarios, you might want your functions scaled on-demand by the platform, also called fully managed scaling (by using a Consumption hosting plan).</span></span> <span data-ttu-id="370e5-142">Or, you might choose user-managed scaling for your functions.</span><span class="sxs-lookup"><span data-stu-id="370e5-142">Or, you might choose user-managed scaling for your functions.</span></span> <span data-ttu-id="370e5-143">In user-managed scaling, your functions run 24/7 on dedicated hardware (by using an App Service hosting plan).</span><span class="sxs-lookup"><span data-stu-id="370e5-143">In user-managed scaling, your functions run 24/7 on dedicated hardware (by using an App Service hosting plan).</span></span> <span data-ttu-id="370e5-144">The number of instances can be set manually or automatically.</span><span class="sxs-lookup"><span data-stu-id="370e5-144">The number of instances can be set manually or automatically.</span></span> <span data-ttu-id="370e5-145">Your choice of hosting plan might be based on available features in the plan, or on architecting by cost.</span><span class="sxs-lookup"><span data-stu-id="370e5-145">Your choice of hosting plan might be based on available features in the plan, or on architecting by cost.</span></span> <span data-ttu-id="370e5-146">To learn more about hosting plans, see [Scaling Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="370e5-146">To learn more about hosting plans, see [Scaling Azure Functions](functions-scale.md).</span></span>

#### <a name="consumption-plan"></a><span data-ttu-id="370e5-147">Consumption plan</span><span class="sxs-lookup"><span data-stu-id="370e5-147">Consumption plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

#### <a name="app-service-plan"></a><span data-ttu-id="370e5-148">App Service plan</span><span class="sxs-lookup"><span data-stu-id="370e5-148">App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="functions-app-a-site"></a><span data-ttu-id="370e5-149">Functions app (a site)</span><span class="sxs-lookup"><span data-stu-id="370e5-149">Functions app (a site)</span></span>

<span data-ttu-id="370e5-150">After you've selected a scaling option, create a Functions app.</span><span class="sxs-lookup"><span data-stu-id="370e5-150">After you've selected a scaling option, create a Functions app.</span></span> <span data-ttu-id="370e5-151">The app is the container that holds all your functions.</span><span class="sxs-lookup"><span data-stu-id="370e5-151">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="370e5-152">A Functions app has many child resources that you can use in your deployment, including app settings and source control options.</span><span class="sxs-lookup"><span data-stu-id="370e5-152">A Functions app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="370e5-153">You also might choose to remove the **sourcecontrols** child resource and use a different [deployment option](functions-continuous-deployment.md) instead.</span><span class="sxs-lookup"><span data-stu-id="370e5-153">You also might choose to remove the **sourcecontrols** child resource and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="370e5-154">To create a successful Infrastructure as Code configuration for your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span><span class="sxs-lookup"><span data-stu-id="370e5-154">To create a successful Infrastructure as Code configuration for your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="370e5-155">In the following example, top-level configurations are applied using **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="370e5-155">In the following example, top-level configurations are applied using **siteConfig**.</span></span> <span data-ttu-id="370e5-156">It's important to set these configurations at a top level because they convey information to the Azure Functions runtime and deployment engine.</span><span class="sxs-lookup"><span data-stu-id="370e5-156">It's important to set these configurations at a top level because they convey information to the Azure Functions runtime and deployment engine.</span></span> <span data-ttu-id="370e5-157">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span><span class="sxs-lookup"><span data-stu-id="370e5-157">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="370e5-158">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some scenarios, your Functions app and functions need to be deployed *before* **config/appSettings** is applied.</span><span class="sxs-lookup"><span data-stu-id="370e5-158">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some scenarios, your Functions app and functions need to be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="370e5-159">In those cases, for example, in [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span><span class="sxs-lookup"><span data-stu-id="370e5-159">In those cases, for example, in [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="370e5-160">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions Deployment Engine (Kudu) looks for deployable code.</span><span class="sxs-lookup"><span data-stu-id="370e5-160">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions Deployment Engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="370e5-161">In our repository, our functions are in a subfolder of the **src** folder.</span><span class="sxs-lookup"><span data-stu-id="370e5-161">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="370e5-162">So, in the preceding example, we set the app settings value to `src`.</span><span class="sxs-lookup"><span data-stu-id="370e5-162">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="370e5-163">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span><span class="sxs-lookup"><span data-stu-id="370e5-163">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="370e5-164">Deploy your template</span><span class="sxs-lookup"><span data-stu-id="370e5-164">Deploy your template</span></span>

* [<span data-ttu-id="370e5-165">PowerShell</span><span class="sxs-lookup"><span data-stu-id="370e5-165">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="370e5-166">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="370e5-166">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="370e5-167">Azure portal</span><span class="sxs-lookup"><span data-stu-id="370e5-167">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="370e5-168">REST API</span><span class="sxs-lookup"><span data-stu-id="370e5-168">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="370e5-169">Deploy to Azure button</span><span class="sxs-lookup"><span data-stu-id="370e5-169">Deploy to Azure button</span></span>

<span data-ttu-id="370e5-170">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span><span class="sxs-lookup"><span data-stu-id="370e5-170">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

#### <a name="markdown"></a><span data-ttu-id="370e5-171">Markdown</span><span class="sxs-lookup"><span data-stu-id="370e5-171">Markdown</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

#### <a name="html"></a><span data-ttu-id="370e5-172">HTML</span><span class="sxs-lookup"><span data-stu-id="370e5-172">HTML</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="370e5-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="370e5-173">Next steps</span></span>

<span data-ttu-id="370e5-174">Learn more about how to develop and configure Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="370e5-174">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="370e5-175">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="370e5-175">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="370e5-176">How to configure Azure Functions app settings</span><span class="sxs-lookup"><span data-stu-id="370e5-176">How to configure Azure Functions app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="370e5-177">Create your first Azure function</span><span class="sxs-lookup"><span data-stu-id="370e5-177">Create your first Azure function</span></span>](functions-create-first-azure-function.md)
