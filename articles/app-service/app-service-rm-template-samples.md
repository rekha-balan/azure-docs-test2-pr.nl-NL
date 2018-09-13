---
title: Azure Resource Manager template samples - App Service | Microsoft Docs
description: Azure Resource Manager template samples for the Web Apps feature of App Service
services: app-service
documentationcenter: app-service
author: tfitzmac
manager: timlt
editor: ggailey777
tags: azure-service-management
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 02/26/2018
ms.author: tomfitz
ms.custom: mvc
ms.openlocfilehash: 155b47fc4c664701ec0f21bdc5ae34f3d7f666ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869366"
---
# <a name="azure-resource-manager-templates-for-web-apps"></a><span data-ttu-id="4de3d-103">Azure Resource Manager templates for Web Apps</span><span class="sxs-lookup"><span data-stu-id="4de3d-103">Azure Resource Manager templates for Web Apps</span></span>

<span data-ttu-id="4de3d-104">The following table includes links to Azure Resource Manager templates for the Web Apps feature of Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4de3d-104">The following table includes links to Azure Resource Manager templates for the Web Apps feature of Azure App Service.</span></span> <span data-ttu-id="4de3d-105">For recommendations about avoiding common errors when you're creating web app templates, see [Guidance on deploying web apps with Azure Resource Manager templates](web-sites-rm-template-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="4de3d-105">For recommendations about avoiding common errors when you're creating web app templates, see [Guidance on deploying web apps with Azure Resource Manager templates](web-sites-rm-template-guidance.md).</span></span>

| | |
|-|-|
|<span data-ttu-id="4de3d-106">**Deploying a web app**</span><span class="sxs-lookup"><span data-stu-id="4de3d-106">**Deploying a web app**</span></span>||
| [<span data-ttu-id="4de3d-107">Web app linked to a GitHub repository</span><span class="sxs-lookup"><span data-stu-id="4de3d-107">Web app linked to a GitHub repository</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-github-deploy)| <span data-ttu-id="4de3d-108">Deploys an Azure web app that pulls code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="4de3d-108">Deploys an Azure web app that pulls code from GitHub.</span></span> |
| [<span data-ttu-id="4de3d-109">Web app with custom deployment slots</span><span class="sxs-lookup"><span data-stu-id="4de3d-109">Web app with custom deployment slots</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webapp-custom-deployment-slots)| <span data-ttu-id="4de3d-110">Deploys an Azure web app with custom deployment slots/environments.</span><span class="sxs-lookup"><span data-stu-id="4de3d-110">Deploys an Azure web app with custom deployment slots/environments.</span></span> |
|<span data-ttu-id="4de3d-111">**Configuring a web app**</span><span class="sxs-lookup"><span data-stu-id="4de3d-111">**Configuring a web app**</span></span>||
| [<span data-ttu-id="4de3d-112">Web app certificate from Key Vault</span><span class="sxs-lookup"><span data-stu-id="4de3d-112">Web app certificate from Key Vault</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-certificate-from-key-vault)| <span data-ttu-id="4de3d-113">Deploys an Azure web app certificate from an Azure Key Vault secret and uses it for SSL binding.</span><span class="sxs-lookup"><span data-stu-id="4de3d-113">Deploys an Azure web app certificate from an Azure Key Vault secret and uses it for SSL binding.</span></span> |
| [<span data-ttu-id="4de3d-114">Web app with a custom domain</span><span class="sxs-lookup"><span data-stu-id="4de3d-114">Web app with a custom domain</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-custom-domain)| <span data-ttu-id="4de3d-115">Deploys an Azure web app with a custom host name.</span><span class="sxs-lookup"><span data-stu-id="4de3d-115">Deploys an Azure web app with a custom host name.</span></span> |
| [<span data-ttu-id="4de3d-116">Web app with a custom domain and SSL</span><span class="sxs-lookup"><span data-stu-id="4de3d-116">Web app with a custom domain and SSL</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-custom-domain-and-ssl)| <span data-ttu-id="4de3d-117">Deploys an Azure web app with a custom host name, and gets a web app certificate from Key Vault for SSL binding.</span><span class="sxs-lookup"><span data-stu-id="4de3d-117">Deploys an Azure web app with a custom host name, and gets a web app certificate from Key Vault for SSL binding.</span></span> |
| [<span data-ttu-id="4de3d-118">Web app with a GoLang extension</span><span class="sxs-lookup"><span data-stu-id="4de3d-118">Web app with a GoLang extension</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webapp-with-golang)| <span data-ttu-id="4de3d-119">Deploys an Azure web app with the GoLang site extension.</span><span class="sxs-lookup"><span data-stu-id="4de3d-119">Deploys an Azure web app with the GoLang site extension.</span></span> <span data-ttu-id="4de3d-120">You can then run web applications developed on GoLang on Azure.</span><span class="sxs-lookup"><span data-stu-id="4de3d-120">You can then run web applications developed on GoLang on Azure.</span></span> |
| [<span data-ttu-id="4de3d-121">Web app with Java 8 and Tomcat 8</span><span class="sxs-lookup"><span data-stu-id="4de3d-121">Web app with Java 8 and Tomcat 8</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-java-tomcat)| <span data-ttu-id="4de3d-122">Deploys an Azure web app with Java 8 and Tomcat 8 enabled.</span><span class="sxs-lookup"><span data-stu-id="4de3d-122">Deploys an Azure web app with Java 8 and Tomcat 8 enabled.</span></span> <span data-ttu-id="4de3d-123">You can then run Java applications in Azure.</span><span class="sxs-lookup"><span data-stu-id="4de3d-123">You can then run Java applications in Azure.</span></span> |
|<span data-ttu-id="4de3d-124">**Linux web app**</span><span class="sxs-lookup"><span data-stu-id="4de3d-124">**Linux web app**</span></span>||
| [<span data-ttu-id="4de3d-125">Web app on Linux with MySQL</span><span class="sxs-lookup"><span data-stu-id="4de3d-125">Web app on Linux with MySQL</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webapp-linux-managed-mysql) | <span data-ttu-id="4de3d-126">Deploys an Azure web app on Linux with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4de3d-126">Deploys an Azure web app on Linux with Azure Database for MySQL.</span></span> |
| [<span data-ttu-id="4de3d-127">Web app on Linux with PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4de3d-127">Web app on Linux with PostgreSQL</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webapp-linux-managed-postgresql) | <span data-ttu-id="4de3d-128">Deploys an Azure web app on Linux with Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4de3d-128">Deploys an Azure web app on Linux with Azure Database for PostgreSQL.</span></span> |
|<span data-ttu-id="4de3d-129">**Web app with connected resources**</span><span class="sxs-lookup"><span data-stu-id="4de3d-129">**Web app with connected resources**</span></span>||
| [<span data-ttu-id="4de3d-130">Web app with MySQL</span><span class="sxs-lookup"><span data-stu-id="4de3d-130">Web app with MySQL</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webapp-managed-mysql)| <span data-ttu-id="4de3d-131">Deploys an Azure web app on Windows with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4de3d-131">Deploys an Azure web app on Windows with Azure Database for MySQL.</span></span> |
| [<span data-ttu-id="4de3d-132">Web app with PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4de3d-132">Web app with PostgreSQL</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webapp-managed-postgresql)| <span data-ttu-id="4de3d-133">Deploys an Azure web app on Windows with Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="4de3d-133">Deploys an Azure web app on Windows with Azure Database for PostgreSQL.</span></span> |
| [<span data-ttu-id="4de3d-134">Web app with a SQL database</span><span class="sxs-lookup"><span data-stu-id="4de3d-134">Web app with a SQL database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-sql-database)| <span data-ttu-id="4de3d-135">Deploys an Azure web app and a SQL database at the Basic service level.</span><span class="sxs-lookup"><span data-stu-id="4de3d-135">Deploys an Azure web app and a SQL database at the Basic service level.</span></span> |
| [<span data-ttu-id="4de3d-136">Web app with a Blob storage connection</span><span class="sxs-lookup"><span data-stu-id="4de3d-136">Web app with a Blob storage connection</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-blob-connection)| <span data-ttu-id="4de3d-137">Deploys an Azure web app with an Azure Blob storage connection string.</span><span class="sxs-lookup"><span data-stu-id="4de3d-137">Deploys an Azure web app with an Azure Blob storage connection string.</span></span> <span data-ttu-id="4de3d-138">You can then use Blob storage from the web app.</span><span class="sxs-lookup"><span data-stu-id="4de3d-138">You can then use Blob storage from the web app.</span></span> |
| [<span data-ttu-id="4de3d-139">Web app with a Redis cache</span><span class="sxs-lookup"><span data-stu-id="4de3d-139">Web app with a Redis cache</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-with-redis-cache)| <span data-ttu-id="4de3d-140">Deploys an Azure web app with a Redis cache.</span><span class="sxs-lookup"><span data-stu-id="4de3d-140">Deploys an Azure web app with a Redis cache.</span></span> |
|<span data-ttu-id="4de3d-141">**App Service Environment for PowerApps**</span><span class="sxs-lookup"><span data-stu-id="4de3d-141">**App Service Environment for PowerApps**</span></span>||
| [<span data-ttu-id="4de3d-142">Create an App Service environment v2</span><span class="sxs-lookup"><span data-stu-id="4de3d-142">Create an App Service environment v2</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-asev2-create) | <span data-ttu-id="4de3d-143">Creates an App Service environment v2 in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="4de3d-143">Creates an App Service environment v2 in your virtual network.</span></span> |
| [<span data-ttu-id="4de3d-144">Create an App Service environment v2 with an ILB address</span><span class="sxs-lookup"><span data-stu-id="4de3d-144">Create an App Service environment v2 with an ILB address</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-asev2-ilb-create/) | <span data-ttu-id="4de3d-145">Creates an App Service environment v2 in your virtual network with a private internal load balancer address.</span><span class="sxs-lookup"><span data-stu-id="4de3d-145">Creates an App Service environment v2 in your virtual network with a private internal load balancer address.</span></span> |
| [<span data-ttu-id="4de3d-146">Configure the default SSL certificate for an ILB App Service environment or an ILB App Service environment v2</span><span class="sxs-lookup"><span data-stu-id="4de3d-146">Configure the default SSL certificate for an ILB App Service environment or an ILB App Service environment v2</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-ase-ilb-configure-default-ssl) | <span data-ttu-id="4de3d-147">Configures the default SSL certificate for an ILB App Service environment or an ILB App Service environment v2.</span><span class="sxs-lookup"><span data-stu-id="4de3d-147">Configures the default SSL certificate for an ILB App Service environment or an ILB App Service environment v2.</span></span> |
| | |