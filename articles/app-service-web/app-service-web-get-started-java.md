---
title: Create your first Java web app in Azure in five minutes | Microsoft Docs
description: Learn how easy it is to run web apps in App Service by deploying a sample app.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: wpickett
editor: ''
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: cephalin
ms.openlocfilehash: ab9b49cd86f37499ebf8fd8162779be305019f36
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552492"
---
# <a name="create-your-first-java-web-app-in-azure-in-five-minutes"></a><span data-ttu-id="0beee-103">Create your first Java web app in Azure in five minutes</span><span class="sxs-lookup"><span data-stu-id="0beee-103">Create your first Java web app in Azure in five minutes</span></span>
[!INCLUDE [app-service-web-selector-get-started](../../includes/app-service-web-selector-get-started.md)]

<span data-ttu-id="0beee-104">This QuickStart helps you deploy your first Java web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="0beee-104">This QuickStart helps you deploy your first Java web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in just a few minutes.</span></span>

<span data-ttu-id="0beee-105">Before you start, make sure that the Azure CLI has been installed.</span><span class="sxs-lookup"><span data-stu-id="0beee-105">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="0beee-106">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0beee-106">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="0beee-107">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="0beee-107">Log in to Azure</span></span>
<span data-ttu-id="0beee-108">Log in to Azure by running `az login` and following the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="0beee-108">Log in to Azure by running `az login` and following the on-screen directions.</span></span>
   
```azurecli
az login
```
   
## <a name="create-a-resource-group"></a><span data-ttu-id="0beee-109">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="0beee-109">Create a resource group</span></span>   
<span data-ttu-id="0beee-110">Create a [resource group](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0beee-110">Create a [resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="0beee-111">This is where you put all the Azure resources that you want to manage together, such as the web app and its SQL Database back end.</span><span class="sxs-lookup"><span data-stu-id="0beee-111">This is where you put all the Azure resources that you want to manage together, such as the web app and its SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="0beee-112">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="0beee-112">To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="0beee-113">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="0beee-113">Create an App Service plan</span></span>
<span data-ttu-id="0beee-114">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0beee-114">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

## <a name="create-a-web-app"></a><span data-ttu-id="0beee-115">Create a web app</span><span class="sxs-lookup"><span data-stu-id="0beee-115">Create a web app</span></span>
<span data-ttu-id="0beee-116">Create a web app with a unique name in `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="0beee-116">Create a web app with a unique name in `<app_name>`.</span></span>

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan my-free-appservice-plan
```

## <a name="deploy-sample-application"></a><span data-ttu-id="0beee-117">Deploy sample application</span><span class="sxs-lookup"><span data-stu-id="0beee-117">Deploy sample application</span></span>
<span data-ttu-id="0beee-118">Deploy a sample Java app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="0beee-118">Deploy a sample Java app from GitHub.</span></span>

```azurecli
az appservice web source-control config --name <app_name> --resource-group myResourceGroup \
--repo-url "https://github.com/azure-appservice-samples/JavaCoffeeShopTemplate.git" --branch master --manual-integration 
```

## <a name="browse-to-web-app"></a><span data-ttu-id="0beee-119">Browse to web app</span><span class="sxs-lookup"><span data-stu-id="0beee-119">Browse to web app</span></span>
<span data-ttu-id="0beee-120">To see your app running live in Azure, run this command.</span><span class="sxs-lookup"><span data-stu-id="0beee-120">To see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="0beee-121">Congratulations, your first Java web app is running live in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0beee-121">Congratulations, your first Java web app is running live in Azure App Service.</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="0beee-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="0beee-122">Next steps</span></span>

<span data-ttu-id="0beee-123">Explore pre-created [Web apps CLI scripts](app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0beee-123">Explore pre-created [Web apps CLI scripts](app-service-cli-samples.md).</span></span>
