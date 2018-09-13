---
title: Deploy a web app that is linked to a GitHub repository | Microsoft Docs
description: Use an Azure Resource Manager template to deploy a web app that contains a project from a GitHub repository.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: ca056dad5466e7cb12310b9cc7961966002f3c77
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555072"
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="63ed7-103">Deploy a web app linked to a GitHub repository</span><span class="sxs-lookup"><span data-stu-id="63ed7-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="63ed7-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="63ed7-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="63ed7-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="63ed7-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="63ed7-106">You can use this template for your own deployments, or customize it to meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="63ed7-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="63ed7-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63ed7-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="63ed7-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="63ed7-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="63ed7-109">What you will deploy</span><span class="sxs-lookup"><span data-stu-id="63ed7-109">What you will deploy</span></span>
<span data-ttu-id="63ed7-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span><span class="sxs-lookup"><span data-stu-id="63ed7-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="63ed7-111">To run the deployment automatically, click the following button:</span><span class="sxs-lookup"><span data-stu-id="63ed7-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="63ed7-112">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="63ed7-112">[![Deploy to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="63ed7-113">Parameters</span><span class="sxs-lookup"><span data-stu-id="63ed7-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="63ed7-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="63ed7-114">repoURL</span></span>
<span data-ttu-id="63ed7-115">The URL for GitHub repository that contains the project to deploy.</span><span class="sxs-lookup"><span data-stu-id="63ed7-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="63ed7-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span><span class="sxs-lookup"><span data-stu-id="63ed7-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="63ed7-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span><span class="sxs-lookup"><span data-stu-id="63ed7-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="63ed7-118">branch</span><span class="sxs-lookup"><span data-stu-id="63ed7-118">branch</span></span>
<span data-ttu-id="63ed7-119">The branch of the repository to use when deploying the application.</span><span class="sxs-lookup"><span data-stu-id="63ed7-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="63ed7-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="63ed7-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="63ed7-121">Resources to deploy</span><span class="sxs-lookup"><span data-stu-id="63ed7-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="63ed7-122">Web app</span><span class="sxs-lookup"><span data-stu-id="63ed7-122">Web app</span></span>
<span data-ttu-id="63ed7-123">Creates the web app that is linked to the project in GitHub.</span><span class="sxs-lookup"><span data-stu-id="63ed7-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="63ed7-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span><span class="sxs-lookup"><span data-stu-id="63ed7-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="63ed7-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span><span class="sxs-lookup"><span data-stu-id="63ed7-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="63ed7-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span><span class="sxs-lookup"><span data-stu-id="63ed7-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="63ed7-127">The **dependsOn** element is only used to specify deployment order.</span><span class="sxs-lookup"><span data-stu-id="63ed7-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="63ed7-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span><span class="sxs-lookup"><span data-stu-id="63ed7-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="63ed7-129">The web app also has a child resource which is defined in **resources** section below.</span><span class="sxs-lookup"><span data-stu-id="63ed7-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="63ed7-130">This child resource defines source control for the project deployed with the web app.</span><span class="sxs-lookup"><span data-stu-id="63ed7-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="63ed7-131">In this template, the source control is linked to a particular GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="63ed7-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="63ed7-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span><span class="sxs-lookup"><span data-stu-id="63ed7-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="63ed7-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span><span class="sxs-lookup"><span data-stu-id="63ed7-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="63ed7-134">Commands to run deployment</span><span class="sxs-lookup"><span data-stu-id="63ed7-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="63ed7-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63ed7-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="63ed7-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="63ed7-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="63ed7-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="63ed7-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="63ed7-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="63ed7-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>


