---
title: Create your first function on Linux from the Azure CLI (preview) | Microsoft Docs
description: Learn how to create your first Azure Function running on a default Linux image using the Azure CLI.
services: functions
keywords: ''
author: ggailey777
ms.author: glenga
ms.date: 11/15/2017
ms.topic: quickstart
ms.service: azure-functions
ms.custom: mvc
ms.devlang: azure-cli
manager: jeconnoc
ms.openlocfilehash: 288ba14bd10df3512ecea06ca97e036f4352ff3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869719"
---
# <a name="create-your-first-function-running-on-linux-using-the-azure-cli-preview"></a><span data-ttu-id="d7c0b-103">Create your first function running on Linux using the Azure CLI (preview)</span><span class="sxs-lookup"><span data-stu-id="d7c0b-103">Create your first function running on Linux using the Azure CLI (preview)</span></span>

<span data-ttu-id="d7c0b-104">Azure Functions lets you host your functions on Linux in a default Azure App Service container.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-104">Azure Functions lets you host your functions on Linux in a default Azure App Service container.</span></span> <span data-ttu-id="d7c0b-105">You can also [bring your own custom container](functions-create-function-linux-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="d7c0b-105">You can also [bring your own custom container](functions-create-function-linux-custom-image.md).</span></span> <span data-ttu-id="d7c0b-106">This functionality is currently in preview and requires [the Functions 2.0 runtime](functions-versions.md), which is also in preview.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-106">This functionality is currently in preview and requires [the Functions 2.0 runtime](functions-versions.md), which is also in preview.</span></span>

<span data-ttu-id="d7c0b-107">This quickstart topic walks you through how to use Azure Functions with the Azure CLI to create your first function app on Linux hosted on the default App Service container.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-107">This quickstart topic walks you through how to use Azure Functions with the Azure CLI to create your first function app on Linux hosted on the default App Service container.</span></span> <span data-ttu-id="d7c0b-108">The function code itself is deployed to the image from a GitHub sample repository.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-108">The function code itself is deployed to the image from a GitHub sample repository.</span></span>    

<span data-ttu-id="d7c0b-109">The following steps are supported on a Mac, Windows, or Linux computer.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-109">The following steps are supported on a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d7c0b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d7c0b-110">Prerequisites</span></span> 

<span data-ttu-id="d7c0b-111">To complete this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="d7c0b-111">To complete this quickstart, you need:</span></span>

+ <span data-ttu-id="d7c0b-112">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-112">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d7c0b-113">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0.21 or later.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-113">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0.21 or later.</span></span> <span data-ttu-id="d7c0b-114">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-114">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="d7c0b-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d7c0b-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [functions-create-resource-group](../../includes/functions-create-resource-group.md)]

[!INCLUDE [functions-create-storage-account](../../includes/functions-create-storage-account.md)]

## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="d7c0b-116">Create a Linux App Service plan</span><span class="sxs-lookup"><span data-stu-id="d7c0b-116">Create a Linux App Service plan</span></span>

<span data-ttu-id="d7c0b-117">Linux hosting for Functions is currently only supported on an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-117">Linux hosting for Functions is currently only supported on an App Service plan.</span></span> <span data-ttu-id="d7c0b-118">Consumption plan hosting is not yet supported.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-118">Consumption plan hosting is not yet supported.</span></span> <span data-ttu-id="d7c0b-119">To learn more about hosting, see [Azure Functions hosting plans comparison](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d7c0b-119">To learn more about hosting, see [Azure Functions hosting plans comparison](functions-scale.md).</span></span> 

[!INCLUDE [app-service-plan-no-h](../../includes/app-service-web-create-app-service-plan-linux-no-h.md)]

## <a name="create-a-function-app-on-linux"></a><span data-ttu-id="d7c0b-120">Create a function app on Linux</span><span class="sxs-lookup"><span data-stu-id="d7c0b-120">Create a function app on Linux</span></span>

<span data-ttu-id="d7c0b-121">You must have a function app to host the execution of your functions on Linux.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-121">You must have a function app to host the execution of your functions on Linux.</span></span> <span data-ttu-id="d7c0b-122">The function app provides an environment for execution of your function code.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-122">The function app provides an environment for execution of your function code.</span></span> <span data-ttu-id="d7c0b-123">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-123">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="d7c0b-124">Create a function app by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command with a Linux App Service plan.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-124">Create a function app by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command with a Linux App Service plan.</span></span> 

<span data-ttu-id="d7c0b-125">In the following command, substitute a unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-125">In the following command, substitute a unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="d7c0b-126">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-126">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="d7c0b-127">The _deployment-source-url_ parameter is a sample repository in GitHub that contains a "Hello World" HTTP triggered function.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-127">The _deployment-source-url_ parameter is a sample repository in GitHub that contains a "Hello World" HTTP triggered function.</span></span>

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--plan myAppServicePlan --deployment-source-url https://github.com/Azure-Samples/functions-quickstart-linux
```
<span data-ttu-id="d7c0b-128">After the function app has been created and deployed, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="d7c0b-128">After the function app has been created and deployed, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="d7c0b-129">Because `myAppServicePlan` is a Linux plan, the built-in docker image is used to create the container that runs the function app on Linux.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-129">Because `myAppServicePlan` is a Linux plan, the built-in docker image is used to create the container that runs the function app on Linux.</span></span> 

>[!NOTE]  
><span data-ttu-id="d7c0b-130">The sample repository currently includes two scripting files, [deploy.sh](https://github.com/Azure-Samples/functions-quickstart-linux/blob/master/deploy.sh) and [.deployment](https://github.com/Azure-Samples/functions-quickstart-linux/blob/master/.deployment).</span><span class="sxs-lookup"><span data-stu-id="d7c0b-130">The sample repository currently includes two scripting files, [deploy.sh](https://github.com/Azure-Samples/functions-quickstart-linux/blob/master/deploy.sh) and [.deployment](https://github.com/Azure-Samples/functions-quickstart-linux/blob/master/.deployment).</span></span> <span data-ttu-id="d7c0b-131">The .deployment file tells the deployment process to use deploy.sh as the [custom deployment script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="d7c0b-131">The .deployment file tells the deployment process to use deploy.sh as the [custom deployment script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span> <span data-ttu-id="d7c0b-132">In the current preview release, scripts are required to deploy the function app on a Linux image.</span><span class="sxs-lookup"><span data-stu-id="d7c0b-132">In the current preview release, scripts are required to deploy the function app on a Linux image.</span></span>  

[!INCLUDE [functions-test-function-code](../../includes/functions-test-function-code.md)]

[!INCLUDE [functions-cleanup-resources](../../includes/functions-cleanup-resources.md)]

[!INCLUDE [functions-quickstart-next-steps-cli](../../includes/functions-quickstart-next-steps-cli.md)]
