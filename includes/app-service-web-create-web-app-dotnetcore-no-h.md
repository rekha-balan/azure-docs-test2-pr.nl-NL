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
ms.openlocfilehash: 727b82692400da166d892f2385e01b0ec19863e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866093"
---
<span data-ttu-id="49064-103">Create a [web app](../articles/app-service/containers/app-service-linux-intro.md) in the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="49064-103">Create a [web app](../articles/app-service/containers/app-service-linux-intro.md) in the `myAppServicePlan` App Service plan.</span></span> 

<span data-ttu-id="49064-104">In the Cloud Shell, you can use the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span><span class="sxs-lookup"><span data-stu-id="49064-104">In the Cloud Shell, you can use the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span></span> <span data-ttu-id="49064-105">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="49064-105">In the following example, replace `<app_name>` with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="49064-106">The runtime is set to `dotnetcore|1.1`.</span><span class="sxs-lookup"><span data-stu-id="49064-106">The runtime is set to `dotnetcore|1.1`.</span></span> <span data-ttu-id="49064-107">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_list_runtimes).</span><span class="sxs-lookup"><span data-stu-id="49064-107">To see all supported runtimes, run [`az webapp list-runtimes`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_list_runtimes).</span></span> 

```azurecli-interactive
# Bash
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "dotnetcore|1.1" --deployment-local-git
# Powershell
az --% webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "dotnetcore|1.1" --deployment-local-git
```

<span data-ttu-id="49064-108">When the web app has been created, the Azure CLI shows output similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="49064-108">When the web app has been created, the Azure CLI shows output similar to the following example:</span></span>

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

<span data-ttu-id="49064-109">You’ve created an empty web app in a Linux container, with git deployment enabled.</span><span class="sxs-lookup"><span data-stu-id="49064-109">You’ve created an empty web app in a Linux container, with git deployment enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="49064-110">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span><span class="sxs-lookup"><span data-stu-id="49064-110">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span></span> <span data-ttu-id="49064-111">Save this URL as you need it later.</span><span class="sxs-lookup"><span data-stu-id="49064-111">Save this URL as you need it later.</span></span>
>
