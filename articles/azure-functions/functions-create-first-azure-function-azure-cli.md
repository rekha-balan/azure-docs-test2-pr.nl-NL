---
title: Create your first function from the Azure CLI | Microsoft Docs
description: Learn how to create your first Azure Function for serverless execution using the Azure CLI.
services: functions
keywords: ''
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 01/24/2018
ms.topic: quickstart
ms.service: azure-functions
ms.custom: mvc
ms.devlang: azure-cli
manager: jeconnoc
ms.openlocfilehash: 54773190a638a74096de1b5b500659639edb78ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967381"
---
# <a name="create-your-first-function-using-the-azure-cli"></a><span data-ttu-id="e452e-103">Create your first function using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e452e-103">Create your first function using the Azure CLI</span></span>

<span data-ttu-id="e452e-104">This quickstart topic walks you through how to use Azure Functions to create your first function.</span><span class="sxs-lookup"><span data-stu-id="e452e-104">This quickstart topic walks you through how to use Azure Functions to create your first function.</span></span> <span data-ttu-id="e452e-105">You use the Azure CLI to create a function app, which is the [serverless](https://azure.microsoft.com/overview/serverless-computing/) infrastructure that hosts your function.</span><span class="sxs-lookup"><span data-stu-id="e452e-105">You use the Azure CLI to create a function app, which is the [serverless](https://azure.microsoft.com/overview/serverless-computing/) infrastructure that hosts your function.</span></span> <span data-ttu-id="e452e-106">The function code itself is deployed from a GitHub sample repository.</span><span class="sxs-lookup"><span data-stu-id="e452e-106">The function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="e452e-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span><span class="sxs-lookup"><span data-stu-id="e452e-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e452e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e452e-108">Prerequisites</span></span> 

<span data-ttu-id="e452e-109">Before running this sample, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="e452e-109">Before running this sample, you must have the following:</span></span>

+ <span data-ttu-id="e452e-110">An active [GitHub](https://github.com) account.</span><span class="sxs-lookup"><span data-stu-id="e452e-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="e452e-111">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e452e-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e452e-112">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="e452e-112">If you choose to install and use the CLI locally, this topic requires the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e452e-113">Run `az --version` to find the version you have.</span><span class="sxs-lookup"><span data-stu-id="e452e-113">Run `az --version` to find the version you have.</span></span> <span data-ttu-id="e452e-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e452e-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


[!INCLUDE [functions-create-resource-group](../../includes/functions-create-resource-group.md)]

[!INCLUDE [functions-create-storage-account](../../includes/functions-create-storage-account.md)]

## <a name="create-a-function-app"></a><span data-ttu-id="e452e-115">Create a function app</span><span class="sxs-lookup"><span data-stu-id="e452e-115">Create a function app</span></span>

<span data-ttu-id="e452e-116">You must have a function app to host the execution of your functions.</span><span class="sxs-lookup"><span data-stu-id="e452e-116">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="e452e-117">The function app provides an environment for serverless execution of your function code.</span><span class="sxs-lookup"><span data-stu-id="e452e-117">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="e452e-118">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span><span class="sxs-lookup"><span data-stu-id="e452e-118">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="e452e-119">Create a function app by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="e452e-119">Create a function app by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command.</span></span> 

<span data-ttu-id="e452e-120">In the following command, substitute a unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="e452e-120">In the following command, substitute a unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="e452e-121">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="e452e-121">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="e452e-122">The _deployment-source-url_ parameter is a sample repository in GitHub that contains a "Hello World" HTTP triggered function.</span><span class="sxs-lookup"><span data-stu-id="e452e-122">The _deployment-source-url_ parameter is a sample repository in GitHub that contains a "Hello World" HTTP triggered function.</span></span>

```azurecli-interactive
az functionapp create --deployment-source-url https://github.com/Azure-Samples/functions-quickstart  \
--resource-group myResourceGroup --consumption-plan-location westeurope \
--name <app_name> --storage-account  <storage_name>  
```
<span data-ttu-id="e452e-123">Setting the _consumption-plan-location_ parameter means that the function app is hosted in a Consumption hosting plan.</span><span class="sxs-lookup"><span data-stu-id="e452e-123">Setting the _consumption-plan-location_ parameter means that the function app is hosted in a Consumption hosting plan.</span></span> <span data-ttu-id="e452e-124">In this plan, resources are added dynamically as required by your functions and you only pay when functions are running.</span><span class="sxs-lookup"><span data-stu-id="e452e-124">In this plan, resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="e452e-125">For more information, see [Choose the correct hosting plan](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="e452e-125">For more information, see [Choose the correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="e452e-126">After the function app has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e452e-126">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
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

[!INCLUDE [functions-test-function-code](../../includes/functions-test-function-code.md)]

[!INCLUDE [functions-cleanup-resources](../../includes/functions-cleanup-resources.md)]

[!INCLUDE [functions-quickstart-next-steps-cli](../../includes/functions-quickstart-next-steps-cli.md)]
