---
title: Deploy your app to Azure App Service with a ZIP or WAR file | Microsoft Docs
description: Learn how to deploy your app to Azure App Service with a ZIP file (or a WAR file for Java developers).
services: app-service
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2018
ms.author: cephalin;sisirap
ms.openlocfilehash: b628ae0806febb3ffd4edaf71be45841aff38516
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965996"
---
# <a name="deploy-your-app-to-azure-app-service-with-a-zip-or-war-file"></a><span data-ttu-id="53281-103">Deploy your app to Azure App Service with a ZIP or WAR file</span><span class="sxs-lookup"><span data-stu-id="53281-103">Deploy your app to Azure App Service with a ZIP or WAR file</span></span>

<span data-ttu-id="53281-104">This article shows you how to use a ZIP file or WAR file to deploy your web app to [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53281-104">This article shows you how to use a ZIP file or WAR file to deploy your web app to [Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="53281-105">This ZIP file deployment uses the same Kudu service that powers continuous integration-based deployments.</span><span class="sxs-lookup"><span data-stu-id="53281-105">This ZIP file deployment uses the same Kudu service that powers continuous integration-based deployments.</span></span> <span data-ttu-id="53281-106">Kudu supports the following functionality for ZIP file deployment:</span><span class="sxs-lookup"><span data-stu-id="53281-106">Kudu supports the following functionality for ZIP file deployment:</span></span> 

- <span data-ttu-id="53281-107">Deletion of files left over from a previous deployment.</span><span class="sxs-lookup"><span data-stu-id="53281-107">Deletion of files left over from a previous deployment.</span></span>
- <span data-ttu-id="53281-108">Option to turn on the default build process, which includes package restore.</span><span class="sxs-lookup"><span data-stu-id="53281-108">Option to turn on the default build process, which includes package restore.</span></span>
- <span data-ttu-id="53281-109">[Deployment customization](https://github.com/projectkudu/kudu/wiki/Configurable-settings#repository-and-deployment-related-settings), including running deployment scripts.</span><span class="sxs-lookup"><span data-stu-id="53281-109">[Deployment customization](https://github.com/projectkudu/kudu/wiki/Configurable-settings#repository-and-deployment-related-settings), including running deployment scripts.</span></span>  
- <span data-ttu-id="53281-110">Deployment logs.</span><span class="sxs-lookup"><span data-stu-id="53281-110">Deployment logs.</span></span> 

<span data-ttu-id="53281-111">For more information, see [Kudu documentation](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).</span><span class="sxs-lookup"><span data-stu-id="53281-111">For more information, see [Kudu documentation](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).</span></span>

<span data-ttu-id="53281-112">The WAR file deployment deploys your [WAR](https://wikipedia.org/wiki/WAR_(file_format)) file to App Service to run your Java web app.</span><span class="sxs-lookup"><span data-stu-id="53281-112">The WAR file deployment deploys your [WAR](https://wikipedia.org/wiki/WAR_(file_format)) file to App Service to run your Java web app.</span></span> <span data-ttu-id="53281-113">See [Deploy WAR file](#deploy-war-file).</span><span class="sxs-lookup"><span data-stu-id="53281-113">See [Deploy WAR file](#deploy-war-file).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="53281-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="53281-114">Prerequisites</span></span>

<span data-ttu-id="53281-115">To complete the steps in this article:</span><span class="sxs-lookup"><span data-stu-id="53281-115">To complete the steps in this article:</span></span>

* <span data-ttu-id="53281-116">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span><span class="sxs-lookup"><span data-stu-id="53281-116">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="create-a-project-zip-file"></a><span data-ttu-id="53281-117">Create a project ZIP file</span><span class="sxs-lookup"><span data-stu-id="53281-117">Create a project ZIP file</span></span>

>[!NOTE]
> <span data-ttu-id="53281-118">If you downloaded the files in a ZIP file, extract the files first.</span><span class="sxs-lookup"><span data-stu-id="53281-118">If you downloaded the files in a ZIP file, extract the files first.</span></span> <span data-ttu-id="53281-119">For example, if you downloaded a ZIP file from GitHub, you cannot deploy that file as-is.</span><span class="sxs-lookup"><span data-stu-id="53281-119">For example, if you downloaded a ZIP file from GitHub, you cannot deploy that file as-is.</span></span> <span data-ttu-id="53281-120">GitHub adds additional nested directories, which do not work with App Service.</span><span class="sxs-lookup"><span data-stu-id="53281-120">GitHub adds additional nested directories, which do not work with App Service.</span></span> 
>

<span data-ttu-id="53281-121">In a local terminal window, navigate to the root directory of your app project.</span><span class="sxs-lookup"><span data-stu-id="53281-121">In a local terminal window, navigate to the root directory of your app project.</span></span> 

<span data-ttu-id="53281-122">This directory should contain the entry file to your web app, such as _index.html_, _index.php_, and _app.js_.</span><span class="sxs-lookup"><span data-stu-id="53281-122">This directory should contain the entry file to your web app, such as _index.html_, _index.php_, and _app.js_.</span></span> <span data-ttu-id="53281-123">It can also contain package management files like _project.json_, _composer.json_, _package.json_, _bower.json_, and _requirements.txt_.</span><span class="sxs-lookup"><span data-stu-id="53281-123">It can also contain package management files like _project.json_, _composer.json_, _package.json_, _bower.json_, and _requirements.txt_.</span></span>

<span data-ttu-id="53281-124">Create a ZIP archive of everything in your project.</span><span class="sxs-lookup"><span data-stu-id="53281-124">Create a ZIP archive of everything in your project.</span></span> <span data-ttu-id="53281-125">The following command uses the default tool in your terminal:</span><span class="sxs-lookup"><span data-stu-id="53281-125">The following command uses the default tool in your terminal:</span></span>

```
# Bash
zip -r <file-name>.zip .

# PowerShell
Compress-Archive -Path * -DestinationPath <file-name>.zip
``` 

[!INCLUDE [Deploy ZIP file](../../includes/app-service-web-deploy-zip.md)]

## <a name="deploy-zip-file-with-azure-cli"></a><span data-ttu-id="53281-126">Deploy ZIP file with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53281-126">Deploy ZIP file with Azure CLI</span></span>

<span data-ttu-id="53281-127">Make sure your Azure CLI version is 2.0.21 or later.</span><span class="sxs-lookup"><span data-stu-id="53281-127">Make sure your Azure CLI version is 2.0.21 or later.</span></span> <span data-ttu-id="53281-128">To see which version you have, run `az --version` command in your terminal window.</span><span class="sxs-lookup"><span data-stu-id="53281-128">To see which version you have, run `az --version` command in your terminal window.</span></span>

<span data-ttu-id="53281-129">Deploy the uploaded ZIP file to your web app by using the [az webapp deployment source config-zip](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config-zip) command.</span><span class="sxs-lookup"><span data-stu-id="53281-129">Deploy the uploaded ZIP file to your web app by using the [az webapp deployment source config-zip](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config-zip) command.</span></span>  

<span data-ttu-id="53281-130">The following example deploys the ZIP file you uploaded.</span><span class="sxs-lookup"><span data-stu-id="53281-130">The following example deploys the ZIP file you uploaded.</span></span> <span data-ttu-id="53281-131">When using a local installation of Azure CLI, specify the path to your local ZIP file for `--src`.</span><span class="sxs-lookup"><span data-stu-id="53281-131">When using a local installation of Azure CLI, specify the path to your local ZIP file for `--src`.</span></span>   

```azurecli-interactive
az webapp deployment source config-zip --resource-group myResourceGroup --name <app_name> --src clouddrive/<filename>.zip
```

<span data-ttu-id="53281-132">This command deploys the files and directories from the ZIP file to your default App Service application folder (`\home\site\wwwroot`) and restarts the app.</span><span class="sxs-lookup"><span data-stu-id="53281-132">This command deploys the files and directories from the ZIP file to your default App Service application folder (`\home\site\wwwroot`) and restarts the app.</span></span> <span data-ttu-id="53281-133">If any additional custom build process is configured, it is run as well.</span><span class="sxs-lookup"><span data-stu-id="53281-133">If any additional custom build process is configured, it is run as well.</span></span> <span data-ttu-id="53281-134">For more information, see [Kudu documentation](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).</span><span class="sxs-lookup"><span data-stu-id="53281-134">For more information, see [Kudu documentation](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).</span></span>

[!INCLUDE [app-service-deploy-zip-push-rest](../../includes/app-service-deploy-zip-push-rest.md)]  

## <a name="deploy-war-file"></a><span data-ttu-id="53281-135">Deploy WAR file</span><span class="sxs-lookup"><span data-stu-id="53281-135">Deploy WAR file</span></span>

<span data-ttu-id="53281-136">To deploy a WAR file to App Service, send a POST request to https://<app_name>.scm.azurewebsites.net/api/wardeploy.</span><span class="sxs-lookup"><span data-stu-id="53281-136">To deploy a WAR file to App Service, send a POST request to https://<app_name>.scm.azurewebsites.net/api/wardeploy.</span></span> <span data-ttu-id="53281-137">The POST request must contain the .war file in the message body.</span><span class="sxs-lookup"><span data-stu-id="53281-137">The POST request must contain the .war file in the message body.</span></span> <span data-ttu-id="53281-138">The deployment credentials for your app are provided in the request by using HTTP BASIC authentication.</span><span class="sxs-lookup"><span data-stu-id="53281-138">The deployment credentials for your app are provided in the request by using HTTP BASIC authentication.</span></span> 

<span data-ttu-id="53281-139">For the HTTP BASIC authentication, you need your App Service deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="53281-139">For the HTTP BASIC authentication, you need your App Service deployment credentials.</span></span> <span data-ttu-id="53281-140">To see how to set your deployment credentials, see [Set and reset user-level credentials](app-service-deployment-credentials.md#userscope).</span><span class="sxs-lookup"><span data-stu-id="53281-140">To see how to set your deployment credentials, see [Set and reset user-level credentials](app-service-deployment-credentials.md#userscope).</span></span>

### <a name="with-curl"></a><span data-ttu-id="53281-141">With cURL</span><span class="sxs-lookup"><span data-stu-id="53281-141">With cURL</span></span>

<span data-ttu-id="53281-142">The following example uses the cURL tool to deploy a .war file.</span><span class="sxs-lookup"><span data-stu-id="53281-142">The following example uses the cURL tool to deploy a .war file.</span></span> <span data-ttu-id="53281-143">Replace the placeholders `<username>`, `<war_file_path>`, and `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="53281-143">Replace the placeholders `<username>`, `<war_file_path>`, and `<app_name>`.</span></span> <span data-ttu-id="53281-144">When prompted by cURL, type in the password.</span><span class="sxs-lookup"><span data-stu-id="53281-144">When prompted by cURL, type in the password.</span></span>

```bash
curl -X POST -u <username> --data-binary @"<war_file_path>" https://<app_name>.scm.azurewebsites.net/api/wardeploy
```

### <a name="with-powershell"></a><span data-ttu-id="53281-145">With PowerShell</span><span class="sxs-lookup"><span data-stu-id="53281-145">With PowerShell</span></span>

<span data-ttu-id="53281-146">The following example uses [Invoke-RestMethod](/powershell/module/microsoft.powershell.utility/invoke-restmethod) to send a request that contains the .war file.</span><span class="sxs-lookup"><span data-stu-id="53281-146">The following example uses [Invoke-RestMethod](/powershell/module/microsoft.powershell.utility/invoke-restmethod) to send a request that contains the .war file.</span></span> <span data-ttu-id="53281-147">Replace the placeholders `<deployment_user>`, `<deployment_password>`, `<zip_file_path>`, and `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="53281-147">Replace the placeholders `<deployment_user>`, `<deployment_password>`, `<zip_file_path>`, and `<app_name>`.</span></span>

```PowerShell
$username = "<deployment_user>"
$password = "<deployment_password>"
$filePath = "<war_file_path>"
$apiUrl = "https://<app_name>.scm.azurewebsites.net/api/wardeploy"
$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $username, $password)))
Invoke-RestMethod -Uri $apiUrl -Headers @{Authorization=("Basic {0}" -f $base64AuthInfo)} -Method POST -InFile $filePath -ContentType "multipart/form-data"
```

[!INCLUDE [What happens to my app during deployment?](../../includes/app-service-deploy-atomicity.md)]

## <a name="next-steps"></a><span data-ttu-id="53281-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="53281-148">Next steps</span></span>

<span data-ttu-id="53281-149">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="53281-149">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="53281-150">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span><span class="sxs-lookup"><span data-stu-id="53281-150">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="53281-151">More resources</span><span class="sxs-lookup"><span data-stu-id="53281-151">More resources</span></span>

* [<span data-ttu-id="53281-152">Kudu: Deploying from a zip file</span><span class="sxs-lookup"><span data-stu-id="53281-152">Kudu: Deploying from a zip file</span></span>](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file)
* [<span data-ttu-id="53281-153">Azure App Service Deployment Credentials</span><span class="sxs-lookup"><span data-stu-id="53281-153">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
