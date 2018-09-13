---
title: Azure CLI Script Sample - Continuously deploy web app from GitHub | Microsoft Docs
description: Azure CLI Script Sample - Continuously deploy web app from GitHub
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: cephalin
ms.openlocfilehash: 649521d6f3740b099ab41c8ef70f7e4430aa5de9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662690"
---
# <a name="continuously-deploy-web-app-from-github"></a>Continuously deploy web app from GitHub

This sample script does the following using Azure CLI 2.0: 

* Create a web app in Azure App Service in the West Europe Azure region. 
* Deploy your web app code from GitHub.
* Display the deployed web app in the browser.

## <a name="prerequisites"></a>Prerequisites

* Run `az login` to log in to Azure.
* Put your web app code in a GitHub repository you own.

> [!NOTE]
> If you use a public GitHub repository you don't own, App Service will deploy code from that GitHub repository, but cannot set up the SSH key and webhooks necessary for continuous deployment.
>
>

## <a name="create-vm-sample"></a>Create VM sample

[!code-azurecli[main](../../cli_scripts/app-service/deploy-github/deploy-github.sh "Continuously deploy web app from GitHub")]

## <a name="clean-up-deployment"></a>Clean up deployment 

After the script sample has been run, the follow command can be used to remove the Resource Group, web app, and all related resources.

```azurecli
az group delete --name $webappname
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az group create](https://docs.microsoft.com/en-us/cli/azure/group#create) | Creates a resource group in which all resources are stored. |
| [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) | Creates an App Service plan. |
| [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#delete) | Creates a web app. |
| [az appservice web source-control config](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config) | Associates a web app with a Git or Mercurial repository. |
| [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) | Open a web app in a browser. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/overview).

Additional CLI script samples for Azure App Service Web Apps can be found in the [Azure CLI samples]().
