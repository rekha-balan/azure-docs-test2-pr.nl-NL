---
title: Getting Started with Cloud Foundry on Microsoft Azure | Microsoft Docs
description: Run OSS or Pivotal Cloud Foundry on Microsoft Azure
services: virtual-machines-linux
documentationcenter: ''
author: seanmck
manager: timlt
editor: ''
tags: ''
keywords: ''
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 32e2d6f18321a0e4599df0fe0bdfc7336db2948b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556652"
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="ff7f2-103">Cloud Foundry on Azure</span><span class="sxs-lookup"><span data-stu-id="ff7f2-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="ff7f2-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in a variety of languages and frameworks.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in a variety of languages and frameworks.</span></span> <span data-ttu-id="ff7f2-105">This document describes the options you have for running Cloud Foundry on Azure and how you can get started.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-105">This document describes the options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="ff7f2-106">Cloud Foundry offerings</span><span class="sxs-lookup"><span data-stu-id="ff7f2-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="ff7f2-107">There are two forms of Cloud Foundry available to run on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span><span class="sxs-lookup"><span data-stu-id="ff7f2-107">There are two forms of Cloud Foundry available to run on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="ff7f2-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by the Cloud Foundry Foundation.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by the Cloud Foundry Foundation.</span></span> <span data-ttu-id="ff7f2-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of the differences between the two offerings.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of the differences between the two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="ff7f2-110">Open-source Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ff7f2-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="ff7f2-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using the [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span><span class="sxs-lookup"><span data-stu-id="ff7f2-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using the [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="ff7f2-112">To learn more about using OSS CF, see the [documentation](https://docs.cloudfoundry.org/) provided by the Cloud Foundry Foundation.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-112">To learn more about using OSS CF, see the [documentation](https://docs.cloudfoundry.org/) provided by the Cloud Foundry Foundation.</span></span>

<span data-ttu-id="ff7f2-113">Microsoft provides best-effort support for OSS CF through the following community channels:</span><span class="sxs-lookup"><span data-stu-id="ff7f2-113">Microsoft provides best-effort support for OSS CF through the following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="ff7f2-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span><span class="sxs-lookup"><span data-stu-id="ff7f2-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="ff7f2-115">cf-bosh mailing list</span><span class="sxs-lookup"><span data-stu-id="ff7f2-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="ff7f2-116">GitHub issues for the [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span><span class="sxs-lookup"><span data-stu-id="ff7f2-116">GitHub issues for the [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="ff7f2-117">The level of support for your Azure resources, such as the virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-117">The level of support for your Azure resources, such as the virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="ff7f2-118">Best-effort community support only applies to the Cloud Foundry-specific components.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-118">Best-effort community support only applies to the Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="ff7f2-119">Pivotal Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="ff7f2-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="ff7f2-120">Pivotal Cloud Foundry includes the same core platform as the OSS distribution, along with a set of proprietary management tools and enterprise support.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-120">Pivotal Cloud Foundry includes the same core platform as the OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="ff7f2-121">In order to run PCF on Azure, you must to acquire a license from Pivotal.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-121">In order to run PCF on Azure, you must to acquire a license from Pivotal.</span></span> <span data-ttu-id="ff7f2-122">The PCF offer from the Azure marketplace includes a 90-day trial license.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-122">The PCF offer from the Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="ff7f2-123">The tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-123">The tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="ff7f2-124">In addition to the support channels listed for OSS CF above, a PCF license entitles you to contact Pivotal for support.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-124">In addition to the support channels listed for OSS CF above, a PCF license entitles you to contact Pivotal for support.</span></span> <span data-ttu-id="ff7f2-125">Microsoft and Pivotal have also enabled support workflows that allow you to contact either party for assistance and have your inquiry routed appropriately depending on where the issue lies.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-125">Microsoft and Pivotal have also enabled support workflows that allow you to contact either party for assistance and have your inquiry routed appropriately depending on where the issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="ff7f2-126">Azure Service Broker</span><span class="sxs-lookup"><span data-stu-id="ff7f2-126">Azure Service Broker</span></span>

<span data-ttu-id="ff7f2-127">Cloud Foundry encourages the ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-127">Cloud Foundry encourages the ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="ff7f2-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way to provision and bind backing services to applications.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way to provision and bind backing services to applications.</span></span> <span data-ttu-id="ff7f2-129">The [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of the key Azure services through this channel, including Azure storage and Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-129">The [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of the key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="ff7f2-130">If you are using Pivotal Cloud Foundry, the service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from the Pivotal Network.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-130">If you are using Pivotal Cloud Foundry, the service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from the Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="ff7f2-131">Related resources</span><span class="sxs-lookup"><span data-stu-id="ff7f2-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="ff7f2-132">Visual Studio Team Services plugin</span><span class="sxs-lookup"><span data-stu-id="ff7f2-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="ff7f2-133">Cloud Foundry is well suited to agile software development, including the use of continuous integration (CI) and continuous delivery (CD).</span><span class="sxs-lookup"><span data-stu-id="ff7f2-133">Cloud Foundry is well suited to agile software development, including the use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="ff7f2-134">If you use Visual Studio Team Services (VSTS) to manage your projects and would like to set up a CI/CD pipeline targeting Cloud Foundry, you can use the [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span><span class="sxs-lookup"><span data-stu-id="ff7f2-134">If you use Visual Studio Team Services (VSTS) to manage your projects and would like to set up a CI/CD pipeline targeting Cloud Foundry, you can use the [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="ff7f2-135">The plugin makes it simple to configure and automate deployments to Cloud Foundry, whether running in Azure or another environment.</span><span class="sxs-lookup"><span data-stu-id="ff7f2-135">The plugin makes it simple to configure and automate deployments to Cloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff7f2-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff7f2-136">Next steps</span></span>

- [<span data-ttu-id="ff7f2-137">Deploy Pivotal Cloud Foundry from the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ff7f2-137">Deploy Pivotal Cloud Foundry from the Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
