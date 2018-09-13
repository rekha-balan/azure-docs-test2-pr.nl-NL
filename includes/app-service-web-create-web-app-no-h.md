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
ms.openlocfilehash: 70548db9ef98cc8fa59ebc11c1371325e63e02fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45404142"
---
<span data-ttu-id="f21d4-103">In the Cloud Shell, create a [web app](../articles/app-service/app-service-web-overview.md) in the `myAppServicePlan` App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f21d4-103">In the Cloud Shell, create a [web app](../articles/app-service/app-service-web-overview.md) in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="f21d4-104">You can do it by using the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span><span class="sxs-lookup"><span data-stu-id="f21d4-104">You can do it by using the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) command.</span></span> <span data-ttu-id="f21d4-105">In the following example, replace *\<app_name>* with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="f21d4-105">In the following example, replace *\<app_name>* with a globally unique app name (valid characters are `a-z`, `0-9`, and `-`).</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan --deployment-local-git
```

<span data-ttu-id="f21d4-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="f21d4-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="f21d4-107">You’ve created an empty web app, with git deployment enabled.</span><span class="sxs-lookup"><span data-stu-id="f21d4-107">You’ve created an empty web app, with git deployment enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="f21d4-108">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span><span class="sxs-lookup"><span data-stu-id="f21d4-108">The URL of the Git remote is shown in the `deploymentLocalGitUrl` property, with the format `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`.</span></span> <span data-ttu-id="f21d4-109">Save this URL as you need it later.</span><span class="sxs-lookup"><span data-stu-id="f21d4-109">Save this URL as you need it later.</span></span>
>

<span data-ttu-id="f21d4-110">Browse to the newly created web app.</span><span class="sxs-lookup"><span data-stu-id="f21d4-110">Browse to the newly created web app.</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="f21d4-111">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="f21d4-111">Here is what your new web app should look like:</span></span>
