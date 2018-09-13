---
title: Deploy your app to Azure App Service using FTP/S | Microsoft Docs
description: Learn how to deploy your app to Azure App Service using FTP or FTPS.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 2ac86d23d56a6130d5a65a6e004d983aea54a649
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556688"
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="3ce4f-103">Deploy your app to Azure App Service using FTP/S</span><span class="sxs-lookup"><span data-stu-id="3ce4f-103">Deploy your app to Azure App Service using FTP/S</span></span>
<span data-ttu-id="3ce4f-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="3ce4f-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="3ce4f-105">The FTP/S endpoint for your app is already active.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="3ce4f-106">No configuration is necessary to enable FTP/S deployment.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-106">No configuration is necessary to enable FTP/S deployment.</span></span> 

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="3ce4f-107">Step 1: Set deployment credentials</span><span class="sxs-lookup"><span data-stu-id="3ce4f-107">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="3ce4f-108">To access the FTP server for your app, you first need deployment credentials.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-108">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="3ce4f-109">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="3ce4f-109">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="3ce4f-110">This tutorial demonstrates the use of user-level credentials.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-110">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="3ce4f-111">Step 2: Get FTP connection information</span><span class="sxs-lookup"><span data-stu-id="3ce4f-111">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="3ce4f-112">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="3ce4f-112">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="3ce4f-113">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-113">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![FTP Connection Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="3ce4f-115">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-115">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="3ce4f-116">You can find the same information when you select **Properties** in the left menu.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-116">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="3ce4f-117">Also, the deployment password is never shown.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-117">Also, the deployment password is never shown.</span></span> <span data-ttu-id="3ce4f-118">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-118">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="3ce4f-119">Step 3: Deploy files to Azure</span><span class="sxs-lookup"><span data-stu-id="3ce4f-119">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="3ce4f-120">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-120">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="3ce4f-121">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span><span class="sxs-lookup"><span data-stu-id="3ce4f-121">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="3ce4f-122">Browse to your app's URL to verify the app is running properly.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-122">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="3ce4f-123">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span><span class="sxs-lookup"><span data-stu-id="3ce4f-123">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="3ce4f-124">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span><span class="sxs-lookup"><span data-stu-id="3ce4f-124">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="3ce4f-125">compilation of .NET binaries</span><span class="sxs-lookup"><span data-stu-id="3ce4f-125">compilation of .NET binaries</span></span>
> - <span data-ttu-id="3ce4f-126">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="3ce4f-126">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="3ce4f-127">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-127">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3ce4f-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ce4f-128">Next steps</span></span>

<span data-ttu-id="3ce4f-129">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="3ce4f-129">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="3ce4f-130">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span><span class="sxs-lookup"><span data-stu-id="3ce4f-130">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="3ce4f-131">More Resources</span><span class="sxs-lookup"><span data-stu-id="3ce4f-131">More Resources</span></span>

* <span data-ttu-id="3ce4f-132">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="3ce4f-132">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="3ce4f-133">Azure App Service Deployment Credentials</span><span class="sxs-lookup"><span data-stu-id="3ce4f-133">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)

