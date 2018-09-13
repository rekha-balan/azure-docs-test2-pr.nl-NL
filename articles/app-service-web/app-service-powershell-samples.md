---
title: Azure PowerShell Samples - App Service | Microsoft Docs
description: Azure PowerShell Samples - App Service
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.openlocfilehash: e35cea1a057b9c5f86325bfb6cf6e0e27f4ce203
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552615"
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="a14e0-103">Azure PowerShell Samples</span><span class="sxs-lookup"><span data-stu-id="a14e0-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="a14e0-104">The following table includes links to bash scripts built using the Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a14e0-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="a14e0-105">**Create app**</span><span class="sxs-lookup"><span data-stu-id="a14e0-105">**Create app**</span></span>||
| [<span data-ttu-id="a14e0-106">Create a web app with deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="a14e0-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a14e0-107">Creates an Azure web app which pulls code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="a14e0-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="a14e0-108">Create a web app with continuous deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="a14e0-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a14e0-109">Creates an Azure web app which continuously deploys code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="a14e0-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="a14e0-110">Create a web app and deploy code with FTP</span><span class="sxs-lookup"><span data-stu-id="a14e0-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a14e0-111">Creates an Azure web app and upload files from a local directory using FTP.</span><span class="sxs-lookup"><span data-stu-id="a14e0-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="a14e0-112">Create a web app and deploy code from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="a14e0-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a14e0-113">Creates an Azure web app and configures code push from a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="a14e0-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="a14e0-114">Create a web app and deploy code to a staging environment</span><span class="sxs-lookup"><span data-stu-id="a14e0-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a14e0-115">Creates an Azure web app with a deployment slot for staging code changes.</span><span class="sxs-lookup"><span data-stu-id="a14e0-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="a14e0-116">**Configure app**</span><span class="sxs-lookup"><span data-stu-id="a14e0-116">**Configure app**</span></span>||
| [<span data-ttu-id="a14e0-117">Map a custom domain to a web app</span><span class="sxs-lookup"><span data-stu-id="a14e0-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a14e0-118">Creates an Azure web app and maps a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="a14e0-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="a14e0-119">Bind a custom SSL certificate to a web app</span><span class="sxs-lookup"><span data-stu-id="a14e0-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a14e0-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="a14e0-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="a14e0-121">**Scale app**</span><span class="sxs-lookup"><span data-stu-id="a14e0-121">**Scale app**</span></span>||
| [<span data-ttu-id="a14e0-122">Scale a web app manually</span><span class="sxs-lookup"><span data-stu-id="a14e0-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a14e0-123">Creates an Azure web app and scales it across 2 instances.</span><span class="sxs-lookup"><span data-stu-id="a14e0-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="a14e0-124">Scale a web app worldwide with a high-availability architecture</span><span class="sxs-lookup"><span data-stu-id="a14e0-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a14e0-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="a14e0-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="a14e0-126">**Connect app to resources**</span><span class="sxs-lookup"><span data-stu-id="a14e0-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="a14e0-127">Connect a web app to a SQL Database</span><span class="sxs-lookup"><span data-stu-id="a14e0-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a14e0-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span><span class="sxs-lookup"><span data-stu-id="a14e0-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="a14e0-129">Connect a web app to a storage account</span><span class="sxs-lookup"><span data-stu-id="a14e0-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="a14e0-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span><span class="sxs-lookup"><span data-stu-id="a14e0-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="a14e0-131">**Monitor app**</span><span class="sxs-lookup"><span data-stu-id="a14e0-131">**Monitor app**</span></span>||
| [<span data-ttu-id="a14e0-132">Monitor a web app with web server logs</span><span class="sxs-lookup"><span data-stu-id="a14e0-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="a14e0-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span><span class="sxs-lookup"><span data-stu-id="a14e0-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
