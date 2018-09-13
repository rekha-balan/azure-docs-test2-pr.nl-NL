---
title: App Service API Apps metadata for API discovery and code generation | Microsoft Docs
description: Learn how API Apps in Azure App Service use Swagger metadata to facilitate API discovery and code generation.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: ''
ms.assetid: c7f8e33a-61cc-486f-89df-4a97dc3c71d4
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: alkarche
ms.openlocfilehash: 1fff267f263d6058ceef13feca54234434e6d1a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548739"
---
# <a name="app-service-api-apps-metadata-for-api-discovery-and-code-generation"></a><span data-ttu-id="6f690-103">App Service API Apps metadata for API discovery and code generation</span><span class="sxs-lookup"><span data-stu-id="6f690-103">App Service API Apps metadata for API discovery and code generation</span></span>
<span data-ttu-id="6f690-104">Support for [Swagger 2.0](http://swagger.io/) API metadata is built into App Service API Apps.</span><span class="sxs-lookup"><span data-stu-id="6f690-104">Support for [Swagger 2.0](http://swagger.io/) API metadata is built into App Service API Apps.</span></span> <span data-ttu-id="6f690-105">You don't have to use Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier.</span><span class="sxs-lookup"><span data-stu-id="6f690-105">You don't have to use Swagger, but if you do use it, you can take advantage of API Apps features that make discovery and consumption easier.</span></span>   

## <a name="swagger-endpoint"></a><span data-ttu-id="6f690-106">Swagger endpoint</span><span class="sxs-lookup"><span data-stu-id="6f690-106">Swagger endpoint</span></span>
<span data-ttu-id="6f690-107">You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of the API app.</span><span class="sxs-lookup"><span data-stu-id="6f690-107">You can specify an endpoint that provides Swagger 2.0 JSON metadata for an API app in a property of the API app.</span></span> <span data-ttu-id="6f690-108">The endpoint can be relative to the base URL of the API app or an absolute URL.</span><span class="sxs-lookup"><span data-stu-id="6f690-108">The endpoint can be relative to the base URL of the API app or an absolute URL.</span></span> <span data-ttu-id="6f690-109">Absolute URLs can point outside the API app.</span><span class="sxs-lookup"><span data-stu-id="6f690-109">Absolute URLs can point outside the API app.</span></span> 

<span data-ttu-id="6f690-110">Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), the URL must be publicly accessible (not protected by user or service authentication).</span><span class="sxs-lookup"><span data-stu-id="6f690-110">Many downstream clients (for example, Visual Studio code generation and PowerApps "Add API" flow), the URL must be publicly accessible (not protected by user or service authentication).</span></span> <span data-ttu-id="6f690-111">This means that if you're using App Service authentication and want to expose the API definition from within your app itself, you need to use authentication option that allows anonymous traffic to reach your API.</span><span class="sxs-lookup"><span data-stu-id="6f690-111">This means that if you're using App Service authentication and want to expose the API definition from within your app itself, you need to use authentication option that allows anonymous traffic to reach your API.</span></span> <span data-ttu-id="6f690-112">For more information, see [Authentication and authorization for App Service API Apps](app-service-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6f690-112">For more information, see [Authentication and authorization for App Service API Apps](app-service-api-authentication.md).</span></span>

### <a name="portal-blade"></a><span data-ttu-id="6f690-113">Portal blade</span><span class="sxs-lookup"><span data-stu-id="6f690-113">Portal blade</span></span>
<span data-ttu-id="6f690-114">In the [Azure portal](https://portal.azure.com/) the endpoint URL can be seen and changed on the **API Definition** blade.</span><span class="sxs-lookup"><span data-stu-id="6f690-114">In the [Azure portal](https://portal.azure.com/) the endpoint URL can be seen and changed on the **API Definition** blade.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-metadata/apidefblade.png)

### <a name="azure-resource-manager-property"></a><span data-ttu-id="6f690-115">Azure Resource Manager property</span><span class="sxs-lookup"><span data-stu-id="6f690-115">Azure Resource Manager property</span></span>
<span data-ttu-id="6f690-116">You can also configure the API definition URL for an API app by using [Resource Explorer](https://resources.azure.com/) or [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6f690-116">You can also configure the API definition URL for an API app by using [Resource Explorer](https://resources.azure.com/) or [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="6f690-117">In **Resource Explorer**, go to **subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Web > sites > {your site} > config > web**, and you'll see the `apiDefinition` property:</span><span class="sxs-lookup"><span data-stu-id="6f690-117">In **Resource Explorer**, go to **subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Web > sites > {your site} > config > web**, and you'll see the `apiDefinition` property:</span></span>

        "apiDefinition": {
          "url": "https://contactslistapi.azurewebsites.net/swagger/docs/v1"
        }

<span data-ttu-id="6f690-118">For an example of an Azure Resource Manager template that sets the `apiDefinition` property, open the [azuredeploy.json file in the To-Do List sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6f690-118">For an example of an Azure Resource Manager template that sets the `apiDefinition` property, open the [azuredeploy.json file in the To-Do List sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="6f690-119">Find the section of the template that looks like the JSON sample shown above.</span><span class="sxs-lookup"><span data-stu-id="6f690-119">Find the section of the template that looks like the JSON sample shown above.</span></span>

### <a name="default-value"></a><span data-ttu-id="6f690-120">Default value</span><span class="sxs-lookup"><span data-stu-id="6f690-120">Default value</span></span>
<span data-ttu-id="6f690-121">When you use Visual Studio to create an API app, the API definition endpoint is automatically set to the base URL of the API app plus `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="6f690-121">When you use Visual Studio to create an API app, the API definition endpoint is automatically set to the base URL of the API app plus `/swagger/docs/v1`.</span></span> <span data-ttu-id="6f690-122">This is the default URL that the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package uses to serve dynamically generated Swagger metadata for an ASP.NET Web API project.</span><span class="sxs-lookup"><span data-stu-id="6f690-122">This is the default URL that the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package uses to serve dynamically generated Swagger metadata for an ASP.NET Web API project.</span></span> 

## <a name="code-generation"></a><span data-ttu-id="6f690-123">Code generation</span><span class="sxs-lookup"><span data-stu-id="6f690-123">Code generation</span></span>
<span data-ttu-id="6f690-124">One of the benefits of integrating Swagger into Azure API apps is automatic code generation.</span><span class="sxs-lookup"><span data-stu-id="6f690-124">One of the benefits of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="6f690-125">Generated client classes make it easier to write code that calls an API app.</span><span class="sxs-lookup"><span data-stu-id="6f690-125">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="6f690-126">You can generate client code for an API app by using Visual Studio or from the command line.</span><span class="sxs-lookup"><span data-stu-id="6f690-126">You can generate client code for an API app by using Visual Studio or from the command line.</span></span> <span data-ttu-id="6f690-127">For information about how to generate client classes in Visual Studio for an ASP.NET Web API project, see [Get started with API Apps and ASP.NET](app-service-api-dotnet-get-started.md#codegen).</span><span class="sxs-lookup"><span data-stu-id="6f690-127">For information about how to generate client classes in Visual Studio for an ASP.NET Web API project, see [Get started with API Apps and ASP.NET](app-service-api-dotnet-get-started.md#codegen).</span></span> <span data-ttu-id="6f690-128">For information about how to do it from the command line for all supported languages, see the readme file of the [Azure/autorest](https://github.com/azure/autorest) repository on GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="6f690-128">For information about how to do it from the command line for all supported languages, see the readme file of the [Azure/autorest](https://github.com/azure/autorest) repository on GitHub.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f690-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f690-129">Next steps</span></span>
<span data-ttu-id="6f690-130">For a step-by-step tutorial that guides you through creating, deploying, and consuming an API app, see [Get started with API Apps in Azure App Service](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6f690-130">For a step-by-step tutorial that guides you through creating, deploying, and consuming an API app, see [Get started with API Apps in Azure App Service](app-service-api-dotnet-get-started.md).</span></span>

<span data-ttu-id="6f690-131">If you use Azure API Management with API Apps, you can use Swagger metadata to import your API into API Management.</span><span class="sxs-lookup"><span data-stu-id="6f690-131">If you use Azure API Management with API Apps, you can use Swagger metadata to import your API into API Management.</span></span> <span data-ttu-id="6f690-132">For more information, see [How to import the definition of an API with operations in Azure API Management](../api-management/api-management-howto-import-api.md).</span><span class="sxs-lookup"><span data-stu-id="6f690-132">For more information, see [How to import the definition of an API with operations in Azure API Management](../api-management/api-management-howto-import-api.md).</span></span> 


