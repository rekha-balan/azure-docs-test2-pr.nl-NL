---
title: Run your Azure Functions from a package | Microsoft Docs
description: Have the Azure Functions runtime run your functions by mounting a deployment package file that contains your function app project files.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 09/10/2018
ms.author: glenga
ms.openlocfilehash: a0e643397372e5b132119a7c23f251ecec876916
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865907"
---
# <a name="run-your-azure-functions-from-a-package-file"></a><span data-ttu-id="63a88-103">Run your Azure Functions from a package file</span><span class="sxs-lookup"><span data-stu-id="63a88-103">Run your Azure Functions from a package file</span></span>

> [!NOTE]
> <span data-ttu-id="63a88-104">The functionality described in this article is not available for Functions on Linux.</span><span class="sxs-lookup"><span data-stu-id="63a88-104">The functionality described in this article is not available for Functions on Linux.</span></span>

<span data-ttu-id="63a88-105">In Azure, you can run your functions directly from a deployment package file in your function app.</span><span class="sxs-lookup"><span data-stu-id="63a88-105">In Azure, you can run your functions directly from a deployment package file in your function app.</span></span> <span data-ttu-id="63a88-106">The other option is to deploy your files in the `d:\home\site\wwwroot` directory of your function app.</span><span class="sxs-lookup"><span data-stu-id="63a88-106">The other option is to deploy your files in the `d:\home\site\wwwroot` directory of your function app.</span></span>

<span data-ttu-id="63a88-107">This article describes the benefits of running your functions from a package.</span><span class="sxs-lookup"><span data-stu-id="63a88-107">This article describes the benefits of running your functions from a package.</span></span> <span data-ttu-id="63a88-108">It also shows how to enable this functionality in your function app.</span><span class="sxs-lookup"><span data-stu-id="63a88-108">It also shows how to enable this functionality in your function app.</span></span>

## <a name="benefits-of-running-from-a-package-file"></a><span data-ttu-id="63a88-109">Benefits of running from a package file</span><span class="sxs-lookup"><span data-stu-id="63a88-109">Benefits of running from a package file</span></span>
  
<span data-ttu-id="63a88-110">There are several benefits to running from a package file:</span><span class="sxs-lookup"><span data-stu-id="63a88-110">There are several benefits to running from a package file:</span></span>

+ <span data-ttu-id="63a88-111">Reduces the risk of file copy locking issues.</span><span class="sxs-lookup"><span data-stu-id="63a88-111">Reduces the risk of file copy locking issues.</span></span>
+ <span data-ttu-id="63a88-112">Can be deployed to a production app (with restart).</span><span class="sxs-lookup"><span data-stu-id="63a88-112">Can be deployed to a production app (with restart).</span></span>
+ <span data-ttu-id="63a88-113">You can be certain of the files that are running in your app.</span><span class="sxs-lookup"><span data-stu-id="63a88-113">You can be certain of the files that are running in your app.</span></span>
+ <span data-ttu-id="63a88-114">Improves the performance of [Azure Resource Manager deployments](functions-infrastructure-as-code.md).</span><span class="sxs-lookup"><span data-stu-id="63a88-114">Improves the performance of [Azure Resource Manager deployments](functions-infrastructure-as-code.md).</span></span>
+ <span data-ttu-id="63a88-115">May reduce cold-start times, particularly for JavaScript functions with large npm package trees.</span><span class="sxs-lookup"><span data-stu-id="63a88-115">May reduce cold-start times, particularly for JavaScript functions with large npm package trees.</span></span>

<span data-ttu-id="63a88-116">For more information, see [this announcement](https://github.com/Azure/app-service-announcements/issues/84).</span><span class="sxs-lookup"><span data-stu-id="63a88-116">For more information, see [this announcement](https://github.com/Azure/app-service-announcements/issues/84).</span></span>

## <a name="enabling-functions-to-run-from-a-package"></a><span data-ttu-id="63a88-117">Enabling functions to run from a package</span><span class="sxs-lookup"><span data-stu-id="63a88-117">Enabling functions to run from a package</span></span>

<span data-ttu-id="63a88-118">To enable your function app to run from a package, you just add a `WEBSITE_RUN_FROM_PACKAGE` setting to your function app settings.</span><span class="sxs-lookup"><span data-stu-id="63a88-118">To enable your function app to run from a package, you just add a `WEBSITE_RUN_FROM_PACKAGE` setting to your function app settings.</span></span> <span data-ttu-id="63a88-119">The `WEBSITE_RUN_FROM_PACKAGE` setting can have one of the following values:</span><span class="sxs-lookup"><span data-stu-id="63a88-119">The `WEBSITE_RUN_FROM_PACKAGE` setting can have one of the following values:</span></span>

| <span data-ttu-id="63a88-120">Value</span><span class="sxs-lookup"><span data-stu-id="63a88-120">Value</span></span>  | <span data-ttu-id="63a88-121">Description</span><span class="sxs-lookup"><span data-stu-id="63a88-121">Description</span></span>  |
|---------|---------|
|**`<url>`**  | <span data-ttu-id="63a88-122">Location of a specific package file you want to run.</span><span class="sxs-lookup"><span data-stu-id="63a88-122">Location of a specific package file you want to run.</span></span> <span data-ttu-id="63a88-123">When using Blob storage, you should use a private container with a [Shared Access Signature (SAS)](../vs-azure-tools-storage-manage-with-storage-explorer.md#attach-a-storage-account-by-using-a-shared-access-signature-sas) to enable the Functions runtime to access to the package.</span><span class="sxs-lookup"><span data-stu-id="63a88-123">When using Blob storage, you should use a private container with a [Shared Access Signature (SAS)](../vs-azure-tools-storage-manage-with-storage-explorer.md#attach-a-storage-account-by-using-a-shared-access-signature-sas) to enable the Functions runtime to access to the package.</span></span> <span data-ttu-id="63a88-124">You can use the [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) to upload package files to your Blob storage account.</span><span class="sxs-lookup"><span data-stu-id="63a88-124">You can use the [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) to upload package files to your Blob storage account.</span></span>         |
| **`1`**  | <span data-ttu-id="63a88-125">Run from a package file in the `d:\home\data\SitePackages` folder of your function app.</span><span class="sxs-lookup"><span data-stu-id="63a88-125">Run from a package file in the `d:\home\data\SitePackages` folder of your function app.</span></span> <span data-ttu-id="63a88-126">This option requires the folder to also have a file named `packagename.txt`.</span><span class="sxs-lookup"><span data-stu-id="63a88-126">This option requires the folder to also have a file named `packagename.txt`.</span></span> <span data-ttu-id="63a88-127">This file contains only the name of the package file in folder, without any whitespace.</span><span class="sxs-lookup"><span data-stu-id="63a88-127">This file contains only the name of the package file in folder, without any whitespace.</span></span> |

<span data-ttu-id="63a88-128">The following shows a function app configured to run from a .zip file hosted in Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="63a88-128">The following shows a function app configured to run from a .zip file hosted in Azure Blob storage:</span></span>

![WEBSITE_RUN_FROM_ZIP app setting](./media/run-functions-from-deployment-package/run-from-zip-app-setting-portal.png)

> [!NOTE]
> <span data-ttu-id="63a88-130">Currently, only .zip package files are supported.</span><span class="sxs-lookup"><span data-stu-id="63a88-130">Currently, only .zip package files are supported.</span></span>

## <a name="integration-with-zip-deployment"></a><span data-ttu-id="63a88-131">Integration with zip deployment</span><span class="sxs-lookup"><span data-stu-id="63a88-131">Integration with zip deployment</span></span>

<span data-ttu-id="63a88-132">[Zip deployment][Zip deployment for Azure Functions] is a feature of Azure App Service that lets you deploy your function app project to the `wwwroot` directory.</span><span class="sxs-lookup"><span data-stu-id="63a88-132">[Zip deployment][Zip deployment for Azure Functions] is a feature of Azure App Service that lets you deploy your function app project to the `wwwroot` directory.</span></span> <span data-ttu-id="63a88-133">The project is packaged as a .zip deployment file.</span><span class="sxs-lookup"><span data-stu-id="63a88-133">The project is packaged as a .zip deployment file.</span></span> <span data-ttu-id="63a88-134">The same APIs can be used to deploy your package to the `d:\home\data\SitePackages` folder.</span><span class="sxs-lookup"><span data-stu-id="63a88-134">The same APIs can be used to deploy your package to the `d:\home\data\SitePackages` folder.</span></span> <span data-ttu-id="63a88-135">With the `WEBSITE_RUN_FROM_PACKAGE` app setting value of `1`, the zip deployment APIs copy your package to the `d:\home\data\SitePackages` folder instead of extracting the files to `d:\home\site\wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="63a88-135">With the `WEBSITE_RUN_FROM_PACKAGE` app setting value of `1`, the zip deployment APIs copy your package to the `d:\home\data\SitePackages` folder instead of extracting the files to `d:\home\site\wwwroot`.</span></span> <span data-ttu-id="63a88-136">It also creates the `packagename.txt` file.</span><span class="sxs-lookup"><span data-stu-id="63a88-136">It also creates the `packagename.txt` file.</span></span> <span data-ttu-id="63a88-137">The function app is then run from the package after a restart, and `wwwroot` becomes read-only.</span><span class="sxs-lookup"><span data-stu-id="63a88-137">The function app is then run from the package after a restart, and `wwwroot` becomes read-only.</span></span> <span data-ttu-id="63a88-138">For more information about zip deployment, see [Zip deployment for Azure Functions](deployment-zip-push.md).</span><span class="sxs-lookup"><span data-stu-id="63a88-138">For more information about zip deployment, see [Zip deployment for Azure Functions](deployment-zip-push.md).</span></span>

## <a name="adding-the-websiterunfrompackage-setting"></a><span data-ttu-id="63a88-139">Adding the WEBSITE_RUN_FROM_PACKAGE setting</span><span class="sxs-lookup"><span data-stu-id="63a88-139">Adding the WEBSITE_RUN_FROM_PACKAGE setting</span></span>

[!INCLUDE [Function app settings](../../includes/functions-app-settings.md)]

## <a name="next-steps"></a><span data-ttu-id="63a88-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="63a88-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="63a88-141">Continuous deployment for Azure Functions</span><span class="sxs-lookup"><span data-stu-id="63a88-141">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)

[Zip deployment for Azure Functions]: deployment-zip-push.md
