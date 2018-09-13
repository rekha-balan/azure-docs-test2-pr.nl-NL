---
title: Create a static HTML web app in Azure in five minutes | Microsoft Docs
description: Learn how easy it is to run web apps in App Service by deploying a sample app.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: wpickett
editor: ''
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: cephalin
ms.openlocfilehash: 472353a2d099db869f43649cd46c8b004ebd53cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564463"
---
# <a name="create-a-static-html-web-app-in-azure-in-five-minutes"></a>Create a static HTML web app in Azure in five minutes
[!INCLUDE [app-service-web-selector-get-started](../../includes/app-service-web-selector-get-started.md)] 

This Quickstart helps you deploy a simple HTML+CSS site to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in just a few minutes.

Before you start, make sure that the Azure CLI has been installed. For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-to-azure"></a>Log in to Azure
Log in to Azure by running `az login` and following the on-screen directions.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Create a resource group   
Create a [resource group](../azure-resource-manager/resource-group-overview.md). This is where you put all the Azure resources that you want to manage together, such as the web app and its SQL Database back end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

To see what possible values you can use for `---location`, use the `az appservice list-locations` Azure CLI command.


## <a name="create-an-app-service-plan"></a>Create an App Service plan
Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

## <a name="create-a-web-app"></a>Create a web app
Create a web app with a unique name in `<app_name>`.

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan my-free-appservice-plan
```

## <a name="deploy-sample-application"></a>Deploy sample application
Deploy a sample HTML site from GitHub.

```azurecli
az appservice web source-control config --name <app_name> --resource-group myResourceGroup \
--repo-url "https://github.com/Azure-Samples/app-service-web-html-get-started.git" --branch master --manual-integration 
```

## <a name="browse-to-web-app"></a>Browse to web app
To see your app running live in Azure, run this command.

```azurecli
az appservice web browse --name <app_name> --resource-group myResourceGroup
```

Congratulations, your first static HTML site is running live in Azure App Service.

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Next steps

Explore pre-created [Web apps CLI scripts](app-service-cli-samples.md).
