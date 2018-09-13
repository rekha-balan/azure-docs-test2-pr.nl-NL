---
title: Use Azure Event Grid to automate resizing uploaded images | Microsoft Docs
description: Azure Event Grid can trigger on blob uploads in Azure Storage. You can use this to send image files uploaded to Azure Storage to other services, such as Azure Functions, for resizing and other improvements.
services: event-grid, functions
author: ggailey777
manager: cfowler
editor: ''
ms.service: event-grid
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 06/20/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 922c87f2d577aff86d51a1fde53f221ebd2fa82c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868816"
---
# <a name="automate-resizing-uploaded-images-using-event-grid"></a><span data-ttu-id="7d20b-104">Automate resizing uploaded images using Event Grid</span><span class="sxs-lookup"><span data-stu-id="7d20b-104">Automate resizing uploaded images using Event Grid</span></span>

<span data-ttu-id="7d20b-105">[Azure Event Grid](overview.md) is an eventing service for the cloud.</span><span class="sxs-lookup"><span data-stu-id="7d20b-105">[Azure Event Grid](overview.md) is an eventing service for the cloud.</span></span> <span data-ttu-id="7d20b-106">Event Grid enables you to create subscriptions to events raised by Azure services or third-party resources.</span><span class="sxs-lookup"><span data-stu-id="7d20b-106">Event Grid enables you to create subscriptions to events raised by Azure services or third-party resources.</span></span>  

<span data-ttu-id="7d20b-107">This tutorial is part two of a series of Storage tutorials.</span><span class="sxs-lookup"><span data-stu-id="7d20b-107">This tutorial is part two of a series of Storage tutorials.</span></span> <span data-ttu-id="7d20b-108">It extends the [previous Storage tutorial][previous-tutorial] to add serverless automatic thumbnail generation using Azure Event Grid and Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7d20b-108">It extends the [previous Storage tutorial][previous-tutorial] to add serverless automatic thumbnail generation using Azure Event Grid and Azure Functions.</span></span> <span data-ttu-id="7d20b-109">Event Grid enables [Azure Functions](..\azure-functions\functions-overview.md) to respond to [Azure Blob storage](..\storage\blobs\storage-blobs-introduction.md) events and generate thumbnails of uploaded images.</span><span class="sxs-lookup"><span data-stu-id="7d20b-109">Event Grid enables [Azure Functions](..\azure-functions\functions-overview.md) to respond to [Azure Blob storage](..\storage\blobs\storage-blobs-introduction.md) events and generate thumbnails of uploaded images.</span></span> <span data-ttu-id="7d20b-110">An event subscription is created against the Blob storage create event.</span><span class="sxs-lookup"><span data-stu-id="7d20b-110">An event subscription is created against the Blob storage create event.</span></span> <span data-ttu-id="7d20b-111">When a blob is added to a specific Blob storage container, a function endpoint is called.</span><span class="sxs-lookup"><span data-stu-id="7d20b-111">When a blob is added to a specific Blob storage container, a function endpoint is called.</span></span> <span data-ttu-id="7d20b-112">Data passed to the function binding from Event Grid is used to access the blob and generate the thumbnail image.</span><span class="sxs-lookup"><span data-stu-id="7d20b-112">Data passed to the function binding from Event Grid is used to access the blob and generate the thumbnail image.</span></span>

<span data-ttu-id="7d20b-113">You use the Azure CLI and the Azure portal to add the resizing functionality to an existing image upload app.</span><span class="sxs-lookup"><span data-stu-id="7d20b-113">You use the Azure CLI and the Azure portal to add the resizing functionality to an existing image upload app.</span></span>

![Published web app in Edge browser](./media/resize-images-on-storage-blob-upload-event/tutorial-completed.png)

<span data-ttu-id="7d20b-115">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="7d20b-115">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d20b-116">Create a general Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="7d20b-116">Create a general Azure Storage account</span></span>
> * <span data-ttu-id="7d20b-117">Deploy serverless code using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7d20b-117">Deploy serverless code using Azure Functions</span></span>
> * <span data-ttu-id="7d20b-118">Create a Blob storage event subscription in Event Grid</span><span class="sxs-lookup"><span data-stu-id="7d20b-118">Create a Blob storage event subscription in Event Grid</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d20b-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7d20b-119">Prerequisites</span></span>

<span data-ttu-id="7d20b-120">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="7d20b-120">To complete this tutorial:</span></span>

<span data-ttu-id="7d20b-121">You must have completed the previous Blob storage tutorial: [Upload image data in the cloud with Azure Storage][previous-tutorial].</span><span class="sxs-lookup"><span data-stu-id="7d20b-121">You must have completed the previous Blob storage tutorial: [Upload image data in the cloud with Azure Storage][previous-tutorial].</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7d20b-122">If you choose to install and use the CLI locally, this tutorial requires the Azure CLI version 2.0.14 or later.</span><span class="sxs-lookup"><span data-stu-id="7d20b-122">If you choose to install and use the CLI locally, this tutorial requires the Azure CLI version 2.0.14 or later.</span></span> <span data-ttu-id="7d20b-123">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="7d20b-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="7d20b-124">If you need to install or upgrade, see [Install Azure CLI]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7d20b-124">If you need to install or upgrade, see [Install Azure CLI]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="7d20b-125">If you are not using Cloud Shell, you must first sign in using `az login`.</span><span class="sxs-lookup"><span data-stu-id="7d20b-125">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="7d20b-126">Create an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="7d20b-126">Create an Azure Storage account</span></span>

<span data-ttu-id="7d20b-127">Azure Functions requires a general storage account.</span><span class="sxs-lookup"><span data-stu-id="7d20b-127">Azure Functions requires a general storage account.</span></span> <span data-ttu-id="7d20b-128">Create a separate general storage account in the resource group by using the [az storage account create](/cli/azure/storage/account#az-storage-account-create) command.</span><span class="sxs-lookup"><span data-stu-id="7d20b-128">Create a separate general storage account in the resource group by using the [az storage account create](/cli/azure/storage/account#az-storage-account-create) command.</span></span>

<span data-ttu-id="7d20b-129">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span><span class="sxs-lookup"><span data-stu-id="7d20b-129">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span> 

<span data-ttu-id="7d20b-130">In the following command, substitute your own globally unique name for the general storage account where you see the `<general_storage_account>` placeholder.</span><span class="sxs-lookup"><span data-stu-id="7d20b-130">In the following command, substitute your own globally unique name for the general storage account where you see the `<general_storage_account>` placeholder.</span></span> 

```azurecli-interactive
az storage account create --name <general_storage_account> \
--location westcentralus --resource-group myResourceGroup \
--sku Standard_LRS --kind storage
```

## <a name="create-a-function-app"></a><span data-ttu-id="7d20b-131">Create a function app</span><span class="sxs-lookup"><span data-stu-id="7d20b-131">Create a function app</span></span>  

<span data-ttu-id="7d20b-132">You must have a function app to host the execution of your function.</span><span class="sxs-lookup"><span data-stu-id="7d20b-132">You must have a function app to host the execution of your function.</span></span> <span data-ttu-id="7d20b-133">The function app provides an environment for serverless execution of your function code.</span><span class="sxs-lookup"><span data-stu-id="7d20b-133">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="7d20b-134">Create a function app by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="7d20b-134">Create a function app by using the [az functionapp create](/cli/azure/functionapp#az-functionapp-create) command.</span></span> 

<span data-ttu-id="7d20b-135">In the following command, substitute your own unique function app name where you see the `<function_app>` placeholder.</span><span class="sxs-lookup"><span data-stu-id="7d20b-135">In the following command, substitute your own unique function app name where you see the `<function_app>` placeholder.</span></span> <span data-ttu-id="7d20b-136">The function app name is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="7d20b-136">The function app name is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="7d20b-137">For `<general_storage_account>`, substitute the name of the general storage account you created.</span><span class="sxs-lookup"><span data-stu-id="7d20b-137">For `<general_storage_account>`, substitute the name of the general storage account you created.</span></span>

```azurecli-interactive
az functionapp create --name <function_app> --storage-account  <general_storage_account>  \
--resource-group myResourceGroup --consumption-plan-location westcentralus
```

<span data-ttu-id="7d20b-138">Now you must configure the function app to connect to the Blob storage account you created in the [previous tutorial][previous-tutorial].</span><span class="sxs-lookup"><span data-stu-id="7d20b-138">Now you must configure the function app to connect to the Blob storage account you created in the [previous tutorial][previous-tutorial].</span></span>

## <a name="configure-the-function-app"></a><span data-ttu-id="7d20b-139">Configure the function app</span><span class="sxs-lookup"><span data-stu-id="7d20b-139">Configure the function app</span></span>

<span data-ttu-id="7d20b-140">The function needs the connection string to connect to the Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="7d20b-140">The function needs the connection string to connect to the Blob storage account.</span></span> <span data-ttu-id="7d20b-141">The function code that you deploy to Azure in the following step looks for the connection string in the app setting myblobstorage_STORAGE, and it looks for the thumbnail image container name in app setting myContainerName.</span><span class="sxs-lookup"><span data-stu-id="7d20b-141">The function code that you deploy to Azure in the following step looks for the connection string in the app setting myblobstorage_STORAGE, and it looks for the thumbnail image container name in app setting myContainerName.</span></span> <span data-ttu-id="7d20b-142">Get the connection string with the [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string) command.</span><span class="sxs-lookup"><span data-stu-id="7d20b-142">Get the connection string with the [az storage account show-connection-string](/cli/azure/storage/account#show-connection-string) command.</span></span> <span data-ttu-id="7d20b-143">Set application settings with the [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#set) command.</span><span class="sxs-lookup"><span data-stu-id="7d20b-143">Set application settings with the [az functionapp config appsettings set](/cli/azure/functionapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="7d20b-144">In the following CLI commands, `<blob_storage_account>` is the name of the Blob storage account you created in the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="7d20b-144">In the following CLI commands, `<blob_storage_account>` is the name of the Blob storage account you created in the previous tutorial.</span></span>

```azurecli-interactive
storageConnectionString=$(az storage account show-connection-string \
--resource-group myResourceGroup --name <blob_storage_account> \
--query connectionString --output tsv)

az functionapp config appsettings set --name <function_app> \
--resource-group myResourceGroup \
--settings myblobstorage_STORAGE=$storageConnectionString \
myContainerName=thumbnails
```

<span data-ttu-id="7d20b-145">You can now deploy a function code project to this function app.</span><span class="sxs-lookup"><span data-stu-id="7d20b-145">You can now deploy a function code project to this function app.</span></span>

## <a name="deploy-the-function-code"></a><span data-ttu-id="7d20b-146">Deploy the function code</span><span class="sxs-lookup"><span data-stu-id="7d20b-146">Deploy the function code</span></span> 

# <a name="nettabnet"></a>[<span data-ttu-id="7d20b-147">\.NET</span><span class="sxs-lookup"><span data-stu-id="7d20b-147">\.NET</span></span>](#tab/net)

<span data-ttu-id="7d20b-148">The sample C# script (.csx) resize is available on [GitHub](https://github.com/Azure-Samples/function-image-upload-resize).</span><span class="sxs-lookup"><span data-stu-id="7d20b-148">The sample C# script (.csx) resize is available on [GitHub](https://github.com/Azure-Samples/function-image-upload-resize).</span></span> <span data-ttu-id="7d20b-149">Deploy this Functions code project to the function app by using the [az functionapp deployment source config](/cli/azure/functionapp/deployment/source#config) command.</span><span class="sxs-lookup"><span data-stu-id="7d20b-149">Deploy this Functions code project to the function app by using the [az functionapp deployment source config](/cli/azure/functionapp/deployment/source#config) command.</span></span> 

<span data-ttu-id="7d20b-150">In the following command, `<function_app>` is the name of the function app you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7d20b-150">In the following command, `<function_app>` is the name of the function app you created earlier.</span></span>

```azurecli-interactive
az functionapp deployment source config --name <function_app> \
--resource-group myResourceGroup --branch master --manual-integration \
--repo-url https://github.com/Azure-Samples/function-image-upload-resize
```

# <a name="nodejstabnodejs"></a>[<span data-ttu-id="7d20b-151">Node.js</span><span class="sxs-lookup"><span data-stu-id="7d20b-151">Node.js</span></span>](#tab/nodejs)
<span data-ttu-id="7d20b-152">The sample Node.js resize function is available on [GitHub](https://github.com/Azure-Samples/storage-blob-resize-function-node).</span><span class="sxs-lookup"><span data-stu-id="7d20b-152">The sample Node.js resize function is available on [GitHub](https://github.com/Azure-Samples/storage-blob-resize-function-node).</span></span> <span data-ttu-id="7d20b-153">Deploy this Functions code project to the function app by using the [az functionapp deployment source config](/cli/azure/functionapp/deployment/source#config) command.</span><span class="sxs-lookup"><span data-stu-id="7d20b-153">Deploy this Functions code project to the function app by using the [az functionapp deployment source config](/cli/azure/functionapp/deployment/source#config) command.</span></span> 


<span data-ttu-id="7d20b-154">In the following command, `<function_app>` is the name of the function app you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7d20b-154">In the following command, `<function_app>` is the name of the function app you created earlier.</span></span>

```azurecli-interactive
az functionapp deployment source config --name <function_app> \
--resource-group myResourceGroup --branch master --manual-integration \
--repo-url https://github.com/Azure-Samples/storage-blob-resize-function-node
```
---

<span data-ttu-id="7d20b-155">The image resize function is triggered by HTTP requests sent to it from the Event Grid service.</span><span class="sxs-lookup"><span data-stu-id="7d20b-155">The image resize function is triggered by HTTP requests sent to it from the Event Grid service.</span></span> <span data-ttu-id="7d20b-156">You tell Event Grid that you want to get these notifications at your function's URL by creating an event subscription.</span><span class="sxs-lookup"><span data-stu-id="7d20b-156">You tell Event Grid that you want to get these notifications at your function's URL by creating an event subscription.</span></span> <span data-ttu-id="7d20b-157">For this tutorial you subscribe to blob-created events.</span><span class="sxs-lookup"><span data-stu-id="7d20b-157">For this tutorial you subscribe to blob-created events.</span></span>

<span data-ttu-id="7d20b-158">The data passed to the function from the Event Grid notification includes the URL of the blob.</span><span class="sxs-lookup"><span data-stu-id="7d20b-158">The data passed to the function from the Event Grid notification includes the URL of the blob.</span></span> <span data-ttu-id="7d20b-159">That URL is in turn passed to the input binding to obtain the uploaded image from Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7d20b-159">That URL is in turn passed to the input binding to obtain the uploaded image from Blob storage.</span></span> <span data-ttu-id="7d20b-160">The function generates a thumbnail image and writes the resulting stream to a separate container in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="7d20b-160">The function generates a thumbnail image and writes the resulting stream to a separate container in Blob storage.</span></span> 

<span data-ttu-id="7d20b-161">This project uses `EventGridTrigger` for the trigger type.</span><span class="sxs-lookup"><span data-stu-id="7d20b-161">This project uses `EventGridTrigger` for the trigger type.</span></span> <span data-ttu-id="7d20b-162">Using the Event Grid trigger is recommended over generic HTTP triggers.</span><span class="sxs-lookup"><span data-stu-id="7d20b-162">Using the Event Grid trigger is recommended over generic HTTP triggers.</span></span> <span data-ttu-id="7d20b-163">Event Grid automatically validates Event Grid Function triggers.</span><span class="sxs-lookup"><span data-stu-id="7d20b-163">Event Grid automatically validates Event Grid Function triggers.</span></span> <span data-ttu-id="7d20b-164">With generic HTTP triggers, you must implement the [validation response](security-authentication.md#webhook-event-delivery).</span><span class="sxs-lookup"><span data-stu-id="7d20b-164">With generic HTTP triggers, you must implement the [validation response](security-authentication.md#webhook-event-delivery).</span></span>

<span data-ttu-id="7d20b-165">To learn more about this function, see the [function.json and run.csx files](https://github.com/Azure-Samples/function-image-upload-resize/tree/master/imageresizerfunc).</span><span class="sxs-lookup"><span data-stu-id="7d20b-165">To learn more about this function, see the [function.json and run.csx files](https://github.com/Azure-Samples/function-image-upload-resize/tree/master/imageresizerfunc).</span></span>
 
<span data-ttu-id="7d20b-166">The function project code is deployed directly from the public sample repository.</span><span class="sxs-lookup"><span data-stu-id="7d20b-166">The function project code is deployed directly from the public sample repository.</span></span> <span data-ttu-id="7d20b-167">To learn more about deployment options for Azure Functions, see [Continuous deployment for Azure Functions](../azure-functions/functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7d20b-167">To learn more about deployment options for Azure Functions, see [Continuous deployment for Azure Functions](../azure-functions/functions-continuous-deployment.md).</span></span>

## <a name="create-an-event-subscription"></a><span data-ttu-id="7d20b-168">Create an event subscription</span><span class="sxs-lookup"><span data-stu-id="7d20b-168">Create an event subscription</span></span>

<span data-ttu-id="7d20b-169">An event subscription indicates which provider-generated events you want sent to a specific endpoint.</span><span class="sxs-lookup"><span data-stu-id="7d20b-169">An event subscription indicates which provider-generated events you want sent to a specific endpoint.</span></span> <span data-ttu-id="7d20b-170">In this case, the endpoint is exposed by your function.</span><span class="sxs-lookup"><span data-stu-id="7d20b-170">In this case, the endpoint is exposed by your function.</span></span> <span data-ttu-id="7d20b-171">Use the following steps to create an event subscription that sends notifications to your function in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="7d20b-171">Use the following steps to create an event subscription that sends notifications to your function in the Azure portal:</span></span> 

1. <span data-ttu-id="7d20b-172">In the [Azure portal](https://portal.azure.com), click the arrow at the bottom left to expand all services, type *functions* in the **Filter** field, and then choose **Function Apps**.</span><span class="sxs-lookup"><span data-stu-id="7d20b-172">In the [Azure portal](https://portal.azure.com), click the arrow at the bottom left to expand all services, type *functions* in the **Filter** field, and then choose **Function Apps**.</span></span> 

    ![Browse to Function Apps in the Azure portal](./media/resize-images-on-storage-blob-upload-event/portal-find-functions.png)

2. <span data-ttu-id="7d20b-174">Expand your function app, choose the **imageresizerfunc** function, and then select **Add Event Grid subscription**.</span><span class="sxs-lookup"><span data-stu-id="7d20b-174">Expand your function app, choose the **imageresizerfunc** function, and then select **Add Event Grid subscription**.</span></span>

    ![Browse to Function Apps in the Azure portal](./media/resize-images-on-storage-blob-upload-event/add-event-subscription.png)

3. <span data-ttu-id="7d20b-176">Use the event subscription settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="7d20b-176">Use the event subscription settings as specified in the table.</span></span>
    
    ![Create event subscription from the function in the Azure portal](./media/resize-images-on-storage-blob-upload-event/event-subscription-create-flow.png)

    | <span data-ttu-id="7d20b-178">Setting</span><span class="sxs-lookup"><span data-stu-id="7d20b-178">Setting</span></span>      | <span data-ttu-id="7d20b-179">Suggested value</span><span class="sxs-lookup"><span data-stu-id="7d20b-179">Suggested value</span></span>  | <span data-ttu-id="7d20b-180">Description</span><span class="sxs-lookup"><span data-stu-id="7d20b-180">Description</span></span>                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="7d20b-181">**Name**</span><span class="sxs-lookup"><span data-stu-id="7d20b-181">**Name**</span></span> | <span data-ttu-id="7d20b-182">imageresizersub</span><span class="sxs-lookup"><span data-stu-id="7d20b-182">imageresizersub</span></span> | <span data-ttu-id="7d20b-183">Name that identifies your new event subscription.</span><span class="sxs-lookup"><span data-stu-id="7d20b-183">Name that identifies your new event subscription.</span></span> | 
    | <span data-ttu-id="7d20b-184">**Topic type**</span><span class="sxs-lookup"><span data-stu-id="7d20b-184">**Topic type**</span></span> |  <span data-ttu-id="7d20b-185">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="7d20b-185">Storage accounts</span></span> | <span data-ttu-id="7d20b-186">Choose the Storage account event provider.</span><span class="sxs-lookup"><span data-stu-id="7d20b-186">Choose the Storage account event provider.</span></span> | 
    | <span data-ttu-id="7d20b-187">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="7d20b-187">**Subscription**</span></span> | <span data-ttu-id="7d20b-188">Your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7d20b-188">Your Azure subscription</span></span> | <span data-ttu-id="7d20b-189">By default, your current Azure subscription is selected.</span><span class="sxs-lookup"><span data-stu-id="7d20b-189">By default, your current Azure subscription is selected.</span></span>   |
    | <span data-ttu-id="7d20b-190">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="7d20b-190">**Resource group**</span></span> | <span data-ttu-id="7d20b-191">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7d20b-191">myResourceGroup</span></span> | <span data-ttu-id="7d20b-192">Select **Use existing** and choose the resource group you have been using in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7d20b-192">Select **Use existing** and choose the resource group you have been using in this tutorial.</span></span>  |
    | <span data-ttu-id="7d20b-193">**Instance**</span><span class="sxs-lookup"><span data-stu-id="7d20b-193">**Instance**</span></span> |  <span data-ttu-id="7d20b-194">Your Blob storage account</span><span class="sxs-lookup"><span data-stu-id="7d20b-194">Your Blob storage account</span></span> |  <span data-ttu-id="7d20b-195">Choose the Blob storage account you created.</span><span class="sxs-lookup"><span data-stu-id="7d20b-195">Choose the Blob storage account you created.</span></span> |
    | <span data-ttu-id="7d20b-196">**Event types**</span><span class="sxs-lookup"><span data-stu-id="7d20b-196">**Event types**</span></span> | <span data-ttu-id="7d20b-197">Blob created</span><span class="sxs-lookup"><span data-stu-id="7d20b-197">Blob created</span></span> | <span data-ttu-id="7d20b-198">Uncheck all types other than **Blob created**.</span><span class="sxs-lookup"><span data-stu-id="7d20b-198">Uncheck all types other than **Blob created**.</span></span> <span data-ttu-id="7d20b-199">Only event types of `Microsoft.Storage.BlobCreated` are passed to the function.</span><span class="sxs-lookup"><span data-stu-id="7d20b-199">Only event types of `Microsoft.Storage.BlobCreated` are passed to the function.</span></span>| 
    | <span data-ttu-id="7d20b-200">**Subscriber type**</span><span class="sxs-lookup"><span data-stu-id="7d20b-200">**Subscriber type**</span></span> |  <span data-ttu-id="7d20b-201">Web Hook</span><span class="sxs-lookup"><span data-stu-id="7d20b-201">Web Hook</span></span> |  <span data-ttu-id="7d20b-202">Choices are Web Hook or Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7d20b-202">Choices are Web Hook or Event Hubs.</span></span> |
    | <span data-ttu-id="7d20b-203">**Subscriber endpoint**</span><span class="sxs-lookup"><span data-stu-id="7d20b-203">**Subscriber endpoint**</span></span> | <span data-ttu-id="7d20b-204">autogenerated</span><span class="sxs-lookup"><span data-stu-id="7d20b-204">autogenerated</span></span> | <span data-ttu-id="7d20b-205">Use the endpoint URL that is generated for you.</span><span class="sxs-lookup"><span data-stu-id="7d20b-205">Use the endpoint URL that is generated for you.</span></span> | 
    | <span data-ttu-id="7d20b-206">**Prefix filter**</span><span class="sxs-lookup"><span data-stu-id="7d20b-206">**Prefix filter**</span></span> | <span data-ttu-id="7d20b-207">/blobServices/default/containers/images/blobs/</span><span class="sxs-lookup"><span data-stu-id="7d20b-207">/blobServices/default/containers/images/blobs/</span></span> | <span data-ttu-id="7d20b-208">Filters storage events to only those on the **images** container.</span><span class="sxs-lookup"><span data-stu-id="7d20b-208">Filters storage events to only those on the **images** container.</span></span>| 

4. <span data-ttu-id="7d20b-209">Click **Create** to add the event subscription.</span><span class="sxs-lookup"><span data-stu-id="7d20b-209">Click **Create** to add the event subscription.</span></span> <span data-ttu-id="7d20b-210">This creates an event subscription that triggers  `imageresizerfunc` when a blob is added to the *images* container.</span><span class="sxs-lookup"><span data-stu-id="7d20b-210">This creates an event subscription that triggers  `imageresizerfunc` when a blob is added to the *images* container.</span></span> <span data-ttu-id="7d20b-211">The function resizes the images and adds them to the *thumbnails* container.</span><span class="sxs-lookup"><span data-stu-id="7d20b-211">The function resizes the images and adds them to the *thumbnails* container.</span></span>

<span data-ttu-id="7d20b-212">Now that the backend services are configured, you test the image resize functionality in the sample web app.</span><span class="sxs-lookup"><span data-stu-id="7d20b-212">Now that the backend services are configured, you test the image resize functionality in the sample web app.</span></span> 

## <a name="test-the-sample-app"></a><span data-ttu-id="7d20b-213">Test the sample app</span><span class="sxs-lookup"><span data-stu-id="7d20b-213">Test the sample app</span></span>

<span data-ttu-id="7d20b-214">To test image resizing in the web app, browse to the URL of your published app.</span><span class="sxs-lookup"><span data-stu-id="7d20b-214">To test image resizing in the web app, browse to the URL of your published app.</span></span> <span data-ttu-id="7d20b-215">The default URL of the web app is `https://<web_app>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="7d20b-215">The default URL of the web app is `https://<web_app>.azurewebsites.net`.</span></span>

<span data-ttu-id="7d20b-216">Click the **Upload photos** region to select and upload a file.</span><span class="sxs-lookup"><span data-stu-id="7d20b-216">Click the **Upload photos** region to select and upload a file.</span></span> <span data-ttu-id="7d20b-217">You can also drag a photo to this region.</span><span class="sxs-lookup"><span data-stu-id="7d20b-217">You can also drag a photo to this region.</span></span> 

<span data-ttu-id="7d20b-218">Notice that after the uploaded image disappears, a copy of the uploaded image is displayed in the **Generated thumbnails** carousel.</span><span class="sxs-lookup"><span data-stu-id="7d20b-218">Notice that after the uploaded image disappears, a copy of the uploaded image is displayed in the **Generated thumbnails** carousel.</span></span> <span data-ttu-id="7d20b-219">This image was resized by the function, added to the *thumbnails* container, and downloaded by the web client.</span><span class="sxs-lookup"><span data-stu-id="7d20b-219">This image was resized by the function, added to the *thumbnails* container, and downloaded by the web client.</span></span>

![Published web app in Edge browser](./media/resize-images-on-storage-blob-upload-event/tutorial-completed.png) 

## <a name="next-steps"></a><span data-ttu-id="7d20b-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d20b-221">Next steps</span></span>

<span data-ttu-id="7d20b-222">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="7d20b-222">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d20b-223">Create a general Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="7d20b-223">Create a general Azure Storage account</span></span>
> * <span data-ttu-id="7d20b-224">Deploy serverless code using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7d20b-224">Deploy serverless code using Azure Functions</span></span>
> * <span data-ttu-id="7d20b-225">Create a Blob storage event subscription in Event Grid</span><span class="sxs-lookup"><span data-stu-id="7d20b-225">Create a Blob storage event subscription in Event Grid</span></span>

<span data-ttu-id="7d20b-226">Advance to part three of the Storage tutorial series to learn how to secure access to the storage account.</span><span class="sxs-lookup"><span data-stu-id="7d20b-226">Advance to part three of the Storage tutorial series to learn how to secure access to the storage account.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d20b-227">Secure access to an applications data in the cloud</span><span class="sxs-lookup"><span data-stu-id="7d20b-227">Secure access to an applications data in the cloud</span></span>](../storage/blobs/storage-secure-access-application.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

+ <span data-ttu-id="7d20b-228">To learn more about Event Grid, see [An introduction to Azure Event Grid](overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d20b-228">To learn more about Event Grid, see [An introduction to Azure Event Grid](overview.md).</span></span> 
+ <span data-ttu-id="7d20b-229">To try another tutorial that features Azure Functions, see [Create a function that integrates with Azure Logic Apps](..\azure-functions\functions-twitter-email.md).</span><span class="sxs-lookup"><span data-stu-id="7d20b-229">To try another tutorial that features Azure Functions, see [Create a function that integrates with Azure Logic Apps](..\azure-functions\functions-twitter-email.md).</span></span> 

[previous-tutorial]: ../storage/blobs/storage-upload-process-images.md
