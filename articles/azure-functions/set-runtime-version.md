---
title: How to target Azure Functions runtime versions
description: Azure Functions supports multiple versions of the runtime. Learn how to specify the runtime version of a function app hosted in Azure.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.topic: conceptual
ms.date: 01/24/2018
ms.author: glenga
ms.openlocfilehash: ced4b6846d291bfbb718c3346ea588ca9e961d07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856742"
---
# <a name="how-to-target-azure-functions-runtime-versions"></a><span data-ttu-id="8fa99-104">How to target Azure Functions runtime versions</span><span class="sxs-lookup"><span data-stu-id="8fa99-104">How to target Azure Functions runtime versions</span></span>

<span data-ttu-id="8fa99-105">A function app runs on a specific version of the Azure Functions runtime.</span><span class="sxs-lookup"><span data-stu-id="8fa99-105">A function app runs on a specific version of the Azure Functions runtime.</span></span> <span data-ttu-id="8fa99-106">There are two major versions: [1.x and 2.x](functions-versions.md).</span><span class="sxs-lookup"><span data-stu-id="8fa99-106">There are two major versions: [1.x and 2.x](functions-versions.md).</span></span> <span data-ttu-id="8fa99-107">This article explains how to configure a function app in Azure to run on the version you choose.</span><span class="sxs-lookup"><span data-stu-id="8fa99-107">This article explains how to configure a function app in Azure to run on the version you choose.</span></span> <span data-ttu-id="8fa99-108">For information about how to configure a local development environment for a specific version, see [Code and test Azure Functions locally](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="8fa99-108">For information about how to configure a local development environment for a specific version, see [Code and test Azure Functions locally](functions-run-local.md).</span></span>

>[!IMPORTANT]   
> <span data-ttu-id="8fa99-109">Azure Functions runtime 2.0 is in preview and currently not all features of Azure Functions are supported.</span><span class="sxs-lookup"><span data-stu-id="8fa99-109">Azure Functions runtime 2.0 is in preview and currently not all features of Azure Functions are supported.</span></span> <span data-ttu-id="8fa99-110">For more information, see [Azure Functions runtime versions overview](functions-versions.md).</span><span class="sxs-lookup"><span data-stu-id="8fa99-110">For more information, see [Azure Functions runtime versions overview](functions-versions.md).</span></span>

## <a name="automatic-and-manual-version-updates"></a><span data-ttu-id="8fa99-111">Automatic and manual version updates</span><span class="sxs-lookup"><span data-stu-id="8fa99-111">Automatic and manual version updates</span></span>

<span data-ttu-id="8fa99-112">Functions lets you target a specific version of the runtime by using the `FUNCTIONS_EXTENSION_VERSION` application setting in a function app.</span><span class="sxs-lookup"><span data-stu-id="8fa99-112">Functions lets you target a specific version of the runtime by using the `FUNCTIONS_EXTENSION_VERSION` application setting in a function app.</span></span> <span data-ttu-id="8fa99-113">The function app is kept on the specified major version until you explicitly choose to move to a new version.</span><span class="sxs-lookup"><span data-stu-id="8fa99-113">The function app is kept on the specified major version until you explicitly choose to move to a new version.</span></span>

<span data-ttu-id="8fa99-114">If you specify only the major version ("~1" for 1.x or "beta" for 2.x), the function app is automatically updated to new minor versions of the runtime when they become available.</span><span class="sxs-lookup"><span data-stu-id="8fa99-114">If you specify only the major version ("~1" for 1.x or "beta" for 2.x), the function app is automatically updated to new minor versions of the runtime when they become available.</span></span> <span data-ttu-id="8fa99-115">New minor versions do not introduce breaking changes.</span><span class="sxs-lookup"><span data-stu-id="8fa99-115">New minor versions do not introduce breaking changes.</span></span> <span data-ttu-id="8fa99-116">If you specify a minor version (for example, "1.0.11360"), the function app is kept on that version until you explicitly change it.</span><span class="sxs-lookup"><span data-stu-id="8fa99-116">If you specify a minor version (for example, "1.0.11360"), the function app is kept on that version until you explicitly change it.</span></span> 

<span data-ttu-id="8fa99-117">When a new version is publicly available, a prompt in the portal gives you the chance to move up to that version.</span><span class="sxs-lookup"><span data-stu-id="8fa99-117">When a new version is publicly available, a prompt in the portal gives you the chance to move up to that version.</span></span> <span data-ttu-id="8fa99-118">After moving to a new version, you can always use the `FUNCTIONS_EXTENSION_VERSION` application setting to move back to a previous version.</span><span class="sxs-lookup"><span data-stu-id="8fa99-118">After moving to a new version, you can always use the `FUNCTIONS_EXTENSION_VERSION` application setting to move back to a previous version.</span></span>

<span data-ttu-id="8fa99-119">A change to the runtime version causes a function app to restart.</span><span class="sxs-lookup"><span data-stu-id="8fa99-119">A change to the runtime version causes a function app to restart.</span></span>

<span data-ttu-id="8fa99-120">The values you can set in the `FUNCTIONS_EXTENSION_VERSION` app setting to enable automatic updates are currently "~1" for the 1.x runtime and "beta" for 2.x.</span><span class="sxs-lookup"><span data-stu-id="8fa99-120">The values you can set in the `FUNCTIONS_EXTENSION_VERSION` app setting to enable automatic updates are currently "~1" for the 1.x runtime and "beta" for 2.x.</span></span>

## <a name="view-the-current-runtime-version"></a><span data-ttu-id="8fa99-121">View the current runtime version</span><span class="sxs-lookup"><span data-stu-id="8fa99-121">View the current runtime version</span></span>

<span data-ttu-id="8fa99-122">Use the following procedure to view the runtime version currently used by a function app.</span><span class="sxs-lookup"><span data-stu-id="8fa99-122">Use the following procedure to view the runtime version currently used by a function app.</span></span> 

1. <span data-ttu-id="8fa99-123">In the [Azure portal](https://portal.azure.com), navigate to the function app, and under **Configured Features**, choose **Function app settings**.</span><span class="sxs-lookup"><span data-stu-id="8fa99-123">In the [Azure portal](https://portal.azure.com), navigate to the function app, and under **Configured Features**, choose **Function app settings**.</span></span> 

    ![Select function app settings](./media/functions-versions/add-update-app-setting.png)

2. <span data-ttu-id="8fa99-125">In the **Function app settings** tab, locate the **Runtime version**.</span><span class="sxs-lookup"><span data-stu-id="8fa99-125">In the **Function app settings** tab, locate the **Runtime version**.</span></span> <span data-ttu-id="8fa99-126">Note the specific runtime version and the requested major version.</span><span class="sxs-lookup"><span data-stu-id="8fa99-126">Note the specific runtime version and the requested major version.</span></span> <span data-ttu-id="8fa99-127">In the example below, the FUNCTIONS\_EXTENSION\_VERSION app setting is set to `~1`.</span><span class="sxs-lookup"><span data-stu-id="8fa99-127">In the example below, the FUNCTIONS\_EXTENSION\_VERSION app setting is set to `~1`.</span></span>
 
   ![Select function app settings](./media/functions-versions/function-app-view-version.png)

## <a name="target-a-version-using-the-portal"></a><span data-ttu-id="8fa99-129">Target a version using the portal</span><span class="sxs-lookup"><span data-stu-id="8fa99-129">Target a version using the portal</span></span>

<span data-ttu-id="8fa99-130">When you need to target a version other than the current major version or version 2.0, set the `FUNCTIONS_EXTENSION_VERSION` application setting.</span><span class="sxs-lookup"><span data-stu-id="8fa99-130">When you need to target a version other than the current major version or version 2.0, set the `FUNCTIONS_EXTENSION_VERSION` application setting.</span></span>

1. <span data-ttu-id="8fa99-131">In the [Azure portal](https://portal.azure.com), navigate to your function app, and under **Configured Features**, choose **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="8fa99-131">In the [Azure portal](https://portal.azure.com), navigate to your function app, and under **Configured Features**, choose **Application settings**.</span></span>

    ![Select function app settings](./media/functions-versions/add-update-app-setting1a.png)

2. <span data-ttu-id="8fa99-133">In the **Application settings** tab, find the `FUNCTIONS_EXTENSION_VERSION` setting and change the value to a valid version of the 1.x runtime or `beta` for version 2.0.</span><span class="sxs-lookup"><span data-stu-id="8fa99-133">In the **Application settings** tab, find the `FUNCTIONS_EXTENSION_VERSION` setting and change the value to a valid version of the 1.x runtime or `beta` for version 2.0.</span></span> <span data-ttu-id="8fa99-134">A tilde with major version means use the latest version of that major version (for example, "~1").</span><span class="sxs-lookup"><span data-stu-id="8fa99-134">A tilde with major version means use the latest version of that major version (for example, "~1").</span></span> 

    ![Set the function app setting](./media/functions-versions/add-update-app-setting2.png)

3. <span data-ttu-id="8fa99-136">Click **Save** to save the application setting update.</span><span class="sxs-lookup"><span data-stu-id="8fa99-136">Click **Save** to save the application setting update.</span></span> 

## <a name="target-a-version-using-azure-cli"></a><span data-ttu-id="8fa99-137">Target a version using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8fa99-137">Target a version using Azure CLI</span></span>

 <span data-ttu-id="8fa99-138">You can also set the `FUNCTIONS_EXTENSION_VERSION` from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8fa99-138">You can also set the `FUNCTIONS_EXTENSION_VERSION` from the Azure CLI.</span></span> <span data-ttu-id="8fa99-139">Using the Azure CLI, update the application setting in the function app with the [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#set) command.</span><span class="sxs-lookup"><span data-stu-id="8fa99-139">Using the Azure CLI, update the application setting in the function app with the [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#set) command.</span></span>

```azurecli-interactive
az functionapp config appsettings set --name <function_app> \
--resource-group <my_resource_group> \
--settings FUNCTIONS_EXTENSION_VERSION=<version>
```
<span data-ttu-id="8fa99-140">In this code, replace `<function_app>` with the name of your function app.</span><span class="sxs-lookup"><span data-stu-id="8fa99-140">In this code, replace `<function_app>` with the name of your function app.</span></span> <span data-ttu-id="8fa99-141">Also replace `<my_resource_group>` with the name of the resource group for your function app.</span><span class="sxs-lookup"><span data-stu-id="8fa99-141">Also replace `<my_resource_group>` with the name of the resource group for your function app.</span></span> <span data-ttu-id="8fa99-142">Replace `<version>` with a valid version of the 1.x runtime or `beta` for version 2.0.</span><span class="sxs-lookup"><span data-stu-id="8fa99-142">Replace `<version>` with a valid version of the 1.x runtime or `beta` for version 2.0.</span></span> 

<span data-ttu-id="8fa99-143">You can run this command from the [Azure Cloud Shell](../cloud-shell/overview.md) by choosing **Try it** in the preceding code sample.</span><span class="sxs-lookup"><span data-stu-id="8fa99-143">You can run this command from the [Azure Cloud Shell](../cloud-shell/overview.md) by choosing **Try it** in the preceding code sample.</span></span> <span data-ttu-id="8fa99-144">You can also use the [Azure CLI locally](/cli/azure/install-azure-cli) to execute this command after executing [az login](/cli/azure/reference-index#az-login) to sign in.</span><span class="sxs-lookup"><span data-stu-id="8fa99-144">You can also use the [Azure CLI locally](/cli/azure/install-azure-cli) to execute this command after executing [az login](/cli/azure/reference-index#az-login) to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fa99-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fa99-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8fa99-146">Target the 2.0 runtime in your local development environment</span><span class="sxs-lookup"><span data-stu-id="8fa99-146">Target the 2.0 runtime in your local development environment</span></span>](functions-run-local.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="8fa99-147">See Release notes for runtime versions</span><span class="sxs-lookup"><span data-stu-id="8fa99-147">See Release notes for runtime versions</span></span>](https://github.com/Azure/azure-webjobs-sdk-script/releases)
