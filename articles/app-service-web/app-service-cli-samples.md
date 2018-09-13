---
title: Azure CLI Samples - App Service | Microsoft Docs
description: Azure CLI Samples - App Service
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.openlocfilehash: 5d74f8216edd46fcd36d2b7f8763ec8a69ccad42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550593"
---
# <a name="azure-cli-samples"></a><span data-ttu-id="223e2-103">Azure CLI Samples</span><span class="sxs-lookup"><span data-stu-id="223e2-103">Azure CLI Samples</span></span>

<span data-ttu-id="223e2-104">The following table includes links to bash scripts built using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="223e2-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="223e2-105">**Create app**</span><span class="sxs-lookup"><span data-stu-id="223e2-105">**Create app**</span></span>||
| [<span data-ttu-id="223e2-106">Create a web app and deploy code from GitHub</span><span class="sxs-lookup"><span data-stu-id="223e2-106">Create a web app and deploy code from GitHub</span></span>](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-107">Creates an Azure web app and deploys code from a public GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="223e2-107">Creates an Azure web app and deploys code from a public GitHub repository.</span></span> |
| [<span data-ttu-id="223e2-108">Create a web app with continuous deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="223e2-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-109">Creates an Azure web app with continuous publishing from a GitHub repository you own.</span><span class="sxs-lookup"><span data-stu-id="223e2-109">Creates an Azure web app with continuous publishing from a GitHub repository you own.</span></span> |
| [<span data-ttu-id="223e2-110">Create a web app and deploy code from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="223e2-110">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-111">Creates an Azure web app and configures code push from a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="223e2-111">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="223e2-112">Create a web app and deploy code to a staging environment</span><span class="sxs-lookup"><span data-stu-id="223e2-112">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-113">Creates an Azure web app with a deployment slot for staging code changes.</span><span class="sxs-lookup"><span data-stu-id="223e2-113">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
| [<span data-ttu-id="223e2-114">Create an ASP.NET Core web app in a Docker container</span><span class="sxs-lookup"><span data-stu-id="223e2-114">Create an ASP.NET Core web app in a Docker container</span></span>](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-115">Creates an Azure web app on Linux and loads a Docker image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="223e2-115">Creates an Azure web app on Linux and loads a Docker image from Docker Hub.</span></span> |
|<span data-ttu-id="223e2-116">**Configure app**</span><span class="sxs-lookup"><span data-stu-id="223e2-116">**Configure app**</span></span>||
| [<span data-ttu-id="223e2-117">Map a custom domain to a web app</span><span class="sxs-lookup"><span data-stu-id="223e2-117">Map a custom domain to a web app</span></span>](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-118">Creates an Azure web app and maps a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="223e2-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="223e2-119">Bind a custom SSL certificate to a web app</span><span class="sxs-lookup"><span data-stu-id="223e2-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="223e2-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="223e2-121">**Scale app**</span><span class="sxs-lookup"><span data-stu-id="223e2-121">**Scale app**</span></span>||
| [<span data-ttu-id="223e2-122">Scale a web app manually</span><span class="sxs-lookup"><span data-stu-id="223e2-122">Scale a web app manually</span></span>](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-123">Creates an Azure web app and scales it across 2 instances.</span><span class="sxs-lookup"><span data-stu-id="223e2-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="223e2-124">Scale a web app worldwide with a high-availability architecture</span><span class="sxs-lookup"><span data-stu-id="223e2-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="223e2-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="223e2-126">**Connect app to resources**</span><span class="sxs-lookup"><span data-stu-id="223e2-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="223e2-127">Connect a web app to a SQL Database</span><span class="sxs-lookup"><span data-stu-id="223e2-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span><span class="sxs-lookup"><span data-stu-id="223e2-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="223e2-129">Connect a web app to a storage account</span><span class="sxs-lookup"><span data-stu-id="223e2-129">Connect a web app to a storage account</span></span>](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="223e2-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span><span class="sxs-lookup"><span data-stu-id="223e2-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
| [<span data-ttu-id="223e2-131">Connect a web app to a redis cache</span><span class="sxs-lookup"><span data-stu-id="223e2-131">Connect a web app to a redis cache</span></span>](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-132">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.)</span><span class="sxs-lookup"><span data-stu-id="223e2-132">Creates an Azure web app and a redis cache, then adds the redis connection details to the app settings.)</span></span> |
| [<span data-ttu-id="223e2-133">Connect a web app to a documentdb</span><span class="sxs-lookup"><span data-stu-id="223e2-133">Connect a web app to a documentdb</span></span>](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-134">Creates an Azure web app and a documentdb, then adds the documentdb connection details to the app settings.</span><span class="sxs-lookup"><span data-stu-id="223e2-134">Creates an Azure web app and a documentdb, then adds the documentdb connection details to the app settings.</span></span> |
|<span data-ttu-id="223e2-135">**Monitor app**</span><span class="sxs-lookup"><span data-stu-id="223e2-135">**Monitor app**</span></span>||
| [<span data-ttu-id="223e2-136">Monitor a web app with web server logs</span><span class="sxs-lookup"><span data-stu-id="223e2-136">Monitor a web app with web server logs</span></span>](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="223e2-137">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span><span class="sxs-lookup"><span data-stu-id="223e2-137">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |