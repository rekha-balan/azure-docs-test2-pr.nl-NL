---
title: include file
description: include file
services: app-service
author: cephalin
ms.service: app-service
ms.topic: include
ms.date: 02/02/2018
ms.author: cephalin
ms.custom: include file
ms.openlocfilehash: 254649e1e7b9754100e82c8bb13e3228420c7aa5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866414"
---
<span data-ttu-id="7b960-103">Create a [web app](../articles/app-service/containers/app-service-linux-intro.md) in the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="7b960-103">Create a [web app](../articles/app-service/containers/app-service-linux-intro.md) in the `myAppServicePlan` App Service plan.</span></span> 

<span data-ttu-id="7b960-104">In the Cloud Shell, you can use the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span><span class="sxs-lookup"><span data-stu-id="7b960-104">In the Cloud Shell, you can use the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span></span> <span data-ttu-id="7b960-105">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="7b960-105">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="7b960-106">The runtime is set to `python|3.4`.</span><span class="sxs-lookup"><span data-stu-id="7b960-106">The runtime is set to `python|3.4`.</span></span> <span data-ttu-id="7b960-107">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_list_runtimes).</span><span class="sxs-lookup"><span data-stu-id="7b960-107">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_list_runtimes).</span></span> 

```azurecli-interactive
# Bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "python|3.4" --deployment-local-git
# PowerShell
az --% webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "python|3.4" --deployment-local-git
```

<span data-ttu-id="7b960-108">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7b960-108">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

```json
Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "deploymentLocalGitUrl": "https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

<span data-ttu-id="7b960-109">You’ve created an empty new web app, with git deployment enabled.</span><span class="sxs-lookup"><span data-stu-id="7b960-109">You’ve created an empty new web app, with git deployment enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="7b960-110">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span><span class="sxs-lookup"><span data-stu-id="7b960-110">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span></span> <span data-ttu-id="7b960-111">Save this URL as you need it later.</span><span class="sxs-lookup"><span data-stu-id="7b960-111">Save this URL as you need it later.</span></span>
>
