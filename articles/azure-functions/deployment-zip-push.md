---
title: Zip push deployment for Azure Functions | Microsoft Docs
description: Use the .zip file deployment facilities of the Kudu deployment service to publish your Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 08/12/2018
ms.author: glenga
ms.openlocfilehash: d7396ddb94017048247050726f83b0302e946633
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868333"
---
# <a name="zip-deployment-for-azure-functions"></a><span data-ttu-id="f6b2d-103">Zip deployment for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f6b2d-103">Zip deployment for Azure Functions</span></span>

<span data-ttu-id="f6b2d-104">This article describes how to deploy your function app project files to Azure from a .zip (compressed) file.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-104">This article describes how to deploy your function app project files to Azure from a .zip (compressed) file.</span></span> <span data-ttu-id="f6b2d-105">You learn how to do a push deployment, both by using Azure CLI and by using the REST APIs.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-105">You learn how to do a push deployment, both by using Azure CLI and by using the REST APIs.</span></span> <span data-ttu-id="f6b2d-106">[Azure Functions Core Tools](functions-run-local.md) also uses these deployment APIs when publishing a local project to Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-106">[Azure Functions Core Tools](functions-run-local.md) also uses these deployment APIs when publishing a local project to Azure.</span></span>

<span data-ttu-id="f6b2d-107">Azure Functions has the full range of continuous deployment and integration options that are provided by Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-107">Azure Functions has the full range of continuous deployment and integration options that are provided by Azure App Service.</span></span> <span data-ttu-id="f6b2d-108">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f6b2d-108">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span>

<span data-ttu-id="f6b2d-109">To speed development, you may find it easier to deploy your function app project files directly from a .zip file.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-109">To speed development, you may find it easier to deploy your function app project files directly from a .zip file.</span></span> <span data-ttu-id="f6b2d-110">The .zip deployment API takes the contents of a .zip file and extracts the contents into the `wwwroot` folder of your function app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-110">The .zip deployment API takes the contents of a .zip file and extracts the contents into the `wwwroot` folder of your function app.</span></span> <span data-ttu-id="f6b2d-111">This .zip file deployment uses the same Kudu service that powers continuous integration-based deployments, including:</span><span class="sxs-lookup"><span data-stu-id="f6b2d-111">This .zip file deployment uses the same Kudu service that powers continuous integration-based deployments, including:</span></span>

+ <span data-ttu-id="f6b2d-112">Deletion of files that were left over from earlier deployments.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-112">Deletion of files that were left over from earlier deployments.</span></span>
+ <span data-ttu-id="f6b2d-113">Deployment customization, including running deployment scripts.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-113">Deployment customization, including running deployment scripts.</span></span>
+ <span data-ttu-id="f6b2d-114">Deployment logs.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-114">Deployment logs.</span></span>
+ <span data-ttu-id="f6b2d-115">Syncing function triggers in a [Consumption plan](functions-scale.md) function app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-115">Syncing function triggers in a [Consumption plan](functions-scale.md) function app.</span></span>

<span data-ttu-id="f6b2d-116">For more information, see the [.zip deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).</span><span class="sxs-lookup"><span data-stu-id="f6b2d-116">For more information, see the [.zip deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).</span></span>

## <a name="deployment-zip-file-requirements"></a><span data-ttu-id="f6b2d-117">Deployment .zip file requirements</span><span class="sxs-lookup"><span data-stu-id="f6b2d-117">Deployment .zip file requirements</span></span>

<span data-ttu-id="f6b2d-118">The .zip file that you use for push deployment must contain all of the files needed to run your function.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-118">The .zip file that you use for push deployment must contain all of the files needed to run your function.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f6b2d-119">When you use .zip deployment, any files from an existing deployment that aren't found in the .zip file are deleted from your function app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-119">When you use .zip deployment, any files from an existing deployment that aren't found in the .zip file are deleted from your function app.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

<span data-ttu-id="f6b2d-120">A function app includes all of the files and folders in the `wwwroot` directory.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-120">A function app includes all of the files and folders in the `wwwroot` directory.</span></span> <span data-ttu-id="f6b2d-121">A .zip file deployment includes the contents of the `wwwroot` directory, but not the directory itself.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-121">A .zip file deployment includes the contents of the `wwwroot` directory, but not the directory itself.</span></span> <span data-ttu-id="f6b2d-122">When deploying a C# class library project, you must include the compiled library files and dependencies in a `bin` subfolder in your .zip package.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-122">When deploying a C# class library project, you must include the compiled library files and dependencies in a `bin` subfolder in your .zip package.</span></span>

## <a name="download-your-function-app-files"></a><span data-ttu-id="f6b2d-123">Download your function app files</span><span class="sxs-lookup"><span data-stu-id="f6b2d-123">Download your function app files</span></span>

<span data-ttu-id="f6b2d-124">When you are developing on a local computer, it's easy to create a .zip file of the function app project folder on your development computer.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-124">When you are developing on a local computer, it's easy to create a .zip file of the function app project folder on your development computer.</span></span>

<span data-ttu-id="f6b2d-125">However, you might have created your functions by using the editor in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-125">However, you might have created your functions by using the editor in the Azure portal.</span></span> <span data-ttu-id="f6b2d-126">You can download an existing function app project in one of these ways:</span><span class="sxs-lookup"><span data-stu-id="f6b2d-126">You can download an existing function app project in one of these ways:</span></span>

+ <span data-ttu-id="f6b2d-127">**From the Azure portal:**</span><span class="sxs-lookup"><span data-stu-id="f6b2d-127">**From the Azure portal:**</span></span>

    1. <span data-ttu-id="f6b2d-128">Sign in to the [Azure portal](https://portal.azure.com), and then go to your function app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-128">Sign in to the [Azure portal](https://portal.azure.com), and then go to your function app.</span></span>

    2. <span data-ttu-id="f6b2d-129">On the **Overview** tab, select **Download app content**.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-129">On the **Overview** tab, select **Download app content**.</span></span> <span data-ttu-id="f6b2d-130">Select your download options, and then select **Download**.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-130">Select your download options, and then select **Download**.</span></span>

        ![Download the function app project](./media/deployment-zip-push/download-project.png)

    <span data-ttu-id="f6b2d-132">The downloaded .zip file is in the correct format to be republished to your function app by using .zip push deployment.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-132">The downloaded .zip file is in the correct format to be republished to your function app by using .zip push deployment.</span></span> <span data-ttu-id="f6b2d-133">The portal download can also add the files needed to open your function app directly in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-133">The portal download can also add the files needed to open your function app directly in Visual Studio.</span></span>

+ <span data-ttu-id="f6b2d-134">**Using REST APIs:**</span><span class="sxs-lookup"><span data-stu-id="f6b2d-134">**Using REST APIs:**</span></span>

    <span data-ttu-id="f6b2d-135">Use the following deployment GET API to download the files from your `<function_app>` project:</span><span class="sxs-lookup"><span data-stu-id="f6b2d-135">Use the following deployment GET API to download the files from your `<function_app>` project:</span></span> 

        https://<function_app>.scm.azurewebsites.net/api/zip/site/wwwroot/

    <span data-ttu-id="f6b2d-136">Including `/site/wwwroot/` makes sure your zip file includes only the function app project files and not the entire site.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-136">Including `/site/wwwroot/` makes sure your zip file includes only the function app project files and not the entire site.</span></span> <span data-ttu-id="f6b2d-137">If you are not already signed in to Azure, you will be asked to do so.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-137">If you are not already signed in to Azure, you will be asked to do so.</span></span>  

<span data-ttu-id="f6b2d-138">You can also download a .zip file from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-138">You can also download a .zip file from a GitHub repository.</span></span> <span data-ttu-id="f6b2d-139">When you download a GitHub repository as a .zip file, GitHub adds an extra folder level for the branch.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-139">When you download a GitHub repository as a .zip file, GitHub adds an extra folder level for the branch.</span></span> <span data-ttu-id="f6b2d-140">This extra folder level means that you can't deploy the .zip file directly as you downloaded it from GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-140">This extra folder level means that you can't deploy the .zip file directly as you downloaded it from GitHub.</span></span> <span data-ttu-id="f6b2d-141">If you're using a GitHub repository to maintain your function app, you should use [continuous integration](functions-continuous-deployment.md) to deploy your app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-141">If you're using a GitHub repository to maintain your function app, you should use [continuous integration](functions-continuous-deployment.md) to deploy your app.</span></span>  

## <a name="cli"></a><span data-ttu-id="f6b2d-142">Deploy by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6b2d-142">Deploy by using Azure CLI</span></span>

<span data-ttu-id="f6b2d-143">You can use Azure CLI to trigger a push deployment.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-143">You can use Azure CLI to trigger a push deployment.</span></span> <span data-ttu-id="f6b2d-144">Push deploy a .zip file to your function app by using the [az functionapp deployment source config-zip](/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip) command.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-144">Push deploy a .zip file to your function app by using the [az functionapp deployment source config-zip](/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip) command.</span></span> <span data-ttu-id="f6b2d-145">To use this command, you must use Azure CLI version 2.0.21 or later.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-145">To use this command, you must use Azure CLI version 2.0.21 or later.</span></span> <span data-ttu-id="f6b2d-146">To see what Azure CLI version you are using, use the `az --version` command.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-146">To see what Azure CLI version you are using, use the `az --version` command.</span></span>

<span data-ttu-id="f6b2d-147">In the following command, replace the `<zip_file_path>` placeholder with the path to the location of your .zip file.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-147">In the following command, replace the `<zip_file_path>` placeholder with the path to the location of your .zip file.</span></span> <span data-ttu-id="f6b2d-148">Also, replace `<app_name>` with the unique name of your function app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-148">Also, replace `<app_name>` with the unique name of your function app.</span></span> 

```azurecli-interactive
az functionapp deployment source config-zip  -g myResourceGroup -n \
<app_name> --src <zip_file_path>
```

<span data-ttu-id="f6b2d-149">This command deploys project files from the downloaded .zip file to your function app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-149">This command deploys project files from the downloaded .zip file to your function app in Azure.</span></span> <span data-ttu-id="f6b2d-150">It then restarts the app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-150">It then restarts the app.</span></span> <span data-ttu-id="f6b2d-151">To view the list of deployments for this function app, you must use the REST APIs.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-151">To view the list of deployments for this function app, you must use the REST APIs.</span></span>

<span data-ttu-id="f6b2d-152">When you're using Azure CLI on your local computer, `<zip_file_path>` is the path to the .zip file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-152">When you're using Azure CLI on your local computer, `<zip_file_path>` is the path to the .zip file on your computer.</span></span> <span data-ttu-id="f6b2d-153">You can also run Azure CLI in [Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6b2d-153">You can also run Azure CLI in [Azure Cloud Shell](../cloud-shell/overview.md).</span></span> <span data-ttu-id="f6b2d-154">When you use Cloud Shell, you must first upload your deployment .zip file to the Azure Files account that's associated with your Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-154">When you use Cloud Shell, you must first upload your deployment .zip file to the Azure Files account that's associated with your Cloud Shell.</span></span> <span data-ttu-id="f6b2d-155">In that case, `<zip_file_path>` is the storage location that your Cloud Shell account uses.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-155">In that case, `<zip_file_path>` is the storage location that your Cloud Shell account uses.</span></span> <span data-ttu-id="f6b2d-156">For more information, see [Persist files in Azure Cloud Shell](../cloud-shell/persisting-shell-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f6b2d-156">For more information, see [Persist files in Azure Cloud Shell](../cloud-shell/persisting-shell-storage.md).</span></span>

[!INCLUDE [app-service-deploy-zip-push-rest](../../includes/app-service-deploy-zip-push-rest.md)]

## <a name="run-functions-from-the-deployment-package"></a><span data-ttu-id="f6b2d-157">Run functions from the deployment package</span><span class="sxs-lookup"><span data-stu-id="f6b2d-157">Run functions from the deployment package</span></span>

<span data-ttu-id="f6b2d-158">You can also choose to run your functions directly from the deployment package file.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-158">You can also choose to run your functions directly from the deployment package file.</span></span> <span data-ttu-id="f6b2d-159">This method skips the deployment step of copying files from the package to the `wwwroot` directory of your function app.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-159">This method skips the deployment step of copying files from the package to the `wwwroot` directory of your function app.</span></span> <span data-ttu-id="f6b2d-160">Instead, the package file is mounted by the Functions runtime, and the contents of the `wwwroot` directory become read-only.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-160">Instead, the package file is mounted by the Functions runtime, and the contents of the `wwwroot` directory become read-only.</span></span>  

> [!NOTE]
> <span data-ttu-id="f6b2d-161">The ability to run your function app from the deployment package is in preview.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-161">The ability to run your function app from the deployment package is in preview.</span></span>

<span data-ttu-id="f6b2d-162">Zip deployment integrates with this feature, which you can enable by setting the function app setting `WEBSITE_RUN_FROM_PACKAGE` to a value of `1`.</span><span class="sxs-lookup"><span data-stu-id="f6b2d-162">Zip deployment integrates with this feature, which you can enable by setting the function app setting `WEBSITE_RUN_FROM_PACKAGE` to a value of `1`.</span></span> <span data-ttu-id="f6b2d-163">For more information, see [Run your functions from a deployment package file](run-functions-from-deployment-package.md).</span><span class="sxs-lookup"><span data-stu-id="f6b2d-163">For more information, see [Run your functions from a deployment package file](run-functions-from-deployment-package.md).</span></span>

[!INCLUDE [app-service-deploy-zip-push-custom](../../includes/app-service-deploy-zip-push-custom.md)]

## <a name="next-steps"></a><span data-ttu-id="f6b2d-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6b2d-164">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6b2d-165">Continuous deployment for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f6b2d-165">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)

[.zip push deployment reference topic]: https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file
