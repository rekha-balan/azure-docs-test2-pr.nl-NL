---
title: Manage applications for multiple environments in Azure Service Fabric | Microsoft Docs
description: Azure Service Fabric applications can be run on clusters that range in size from one machine to thousands of machines. In some cases, you will want to configure your application differently for those varied environments. This article covers how to define different application parameters per environment.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: ''
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/23/2018
ms.author: mikhegn
ms.openlocfilehash: 78b3e9634981f5ec0cfcdaa85608314be1335138
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44801234"
---
# <a name="manage-applications-for-multiple-environments"></a><span data-ttu-id="35f3f-105">Manage applications for multiple environments</span><span class="sxs-lookup"><span data-stu-id="35f3f-105">Manage applications for multiple environments</span></span>

<span data-ttu-id="35f3f-106">Azure Service Fabric clusters enable you to create clusters using anywhere from one to many thousands machines.</span><span class="sxs-lookup"><span data-stu-id="35f3f-106">Azure Service Fabric clusters enable you to create clusters using anywhere from one to many thousands machines.</span></span> <span data-ttu-id="35f3f-107">In most cases, you find yourself having to deploy your application across multiple cluster configurations: your local development cluster, a shared development cluster and your production cluster.</span><span class="sxs-lookup"><span data-stu-id="35f3f-107">In most cases, you find yourself having to deploy your application across multiple cluster configurations: your local development cluster, a shared development cluster and your production cluster.</span></span> <span data-ttu-id="35f3f-108">All of these clusters are considered different environments your code has to run in.</span><span class="sxs-lookup"><span data-stu-id="35f3f-108">All of these clusters are considered different environments your code has to run in.</span></span> <span data-ttu-id="35f3f-109">Application binaries can run without modification across this wide spectrum, but you often want to configure the application differently.</span><span class="sxs-lookup"><span data-stu-id="35f3f-109">Application binaries can run without modification across this wide spectrum, but you often want to configure the application differently.</span></span>

<span data-ttu-id="35f3f-110">Consider two simple examples:</span><span class="sxs-lookup"><span data-stu-id="35f3f-110">Consider two simple examples:</span></span>
  - <span data-ttu-id="35f3f-111">your service listens on a defined port, but you need that port to be different across the environments</span><span class="sxs-lookup"><span data-stu-id="35f3f-111">your service listens on a defined port, but you need that port to be different across the environments</span></span>
  - <span data-ttu-id="35f3f-112">you need to provide different binding credentials for a database across the environments</span><span class="sxs-lookup"><span data-stu-id="35f3f-112">you need to provide different binding credentials for a database across the environments</span></span>

## <a name="specifying-configuration"></a><span data-ttu-id="35f3f-113">Specifying configuration</span><span class="sxs-lookup"><span data-stu-id="35f3f-113">Specifying configuration</span></span>

<span data-ttu-id="35f3f-114">The configuration you provide can be divided in two categories:</span><span class="sxs-lookup"><span data-stu-id="35f3f-114">The configuration you provide can be divided in two categories:</span></span>

- <span data-ttu-id="35f3f-115">Configuration that applies to how your services are run</span><span class="sxs-lookup"><span data-stu-id="35f3f-115">Configuration that applies to how your services are run</span></span>
  - <span data-ttu-id="35f3f-116">For example, the port number for an endpoint or the number of instances of a service</span><span class="sxs-lookup"><span data-stu-id="35f3f-116">For example, the port number for an endpoint or the number of instances of a service</span></span>
  - <span data-ttu-id="35f3f-117">This configuration is specified in the application or service manifest file</span><span class="sxs-lookup"><span data-stu-id="35f3f-117">This configuration is specified in the application or service manifest file</span></span>
- <span data-ttu-id="35f3f-118">Configuration that applies to your application code</span><span class="sxs-lookup"><span data-stu-id="35f3f-118">Configuration that applies to your application code</span></span>
  - <span data-ttu-id="35f3f-119">For example, binding information for a database</span><span class="sxs-lookup"><span data-stu-id="35f3f-119">For example, binding information for a database</span></span>
  - <span data-ttu-id="35f3f-120">This configuration can be provided either through configuration files or environment variables</span><span class="sxs-lookup"><span data-stu-id="35f3f-120">This configuration can be provided either through configuration files or environment variables</span></span>

> [!NOTE]
> <span data-ttu-id="35f3f-121">Not all attributes in the application and service manifest file support parameters.</span><span class="sxs-lookup"><span data-stu-id="35f3f-121">Not all attributes in the application and service manifest file support parameters.</span></span>
> <span data-ttu-id="35f3f-122">In those cases, you have to rely on substituting strings as part of your deployment workflow.</span><span class="sxs-lookup"><span data-stu-id="35f3f-122">In those cases, you have to rely on substituting strings as part of your deployment workflow.</span></span> <span data-ttu-id="35f3f-123">In Azure DevOps you can use an extension like Replace Tokens: https://marketplace.visualstudio.com/items?itemName=qetza.replacetokens or in Jenkins you could run a script task to replace the values.</span><span class="sxs-lookup"><span data-stu-id="35f3f-123">In Azure DevOps you can use an extension like Replace Tokens: https://marketplace.visualstudio.com/items?itemName=qetza.replacetokens or in Jenkins you could run a script task to replace the values.</span></span>
>

## <a name="specifying-parameters-during-application-creation"></a><span data-ttu-id="35f3f-124">Specifying parameters during application creation</span><span class="sxs-lookup"><span data-stu-id="35f3f-124">Specifying parameters during application creation</span></span>

<span data-ttu-id="35f3f-125">When creating a named application instances in Service Fabric, you have the option to pass in parameters.</span><span class="sxs-lookup"><span data-stu-id="35f3f-125">When creating a named application instances in Service Fabric, you have the option to pass in parameters.</span></span> <span data-ttu-id="35f3f-126">The way you do it depends on how you create the application instance.</span><span class="sxs-lookup"><span data-stu-id="35f3f-126">The way you do it depends on how you create the application instance.</span></span>

  - <span data-ttu-id="35f3f-127">In PowerShell, the [`New-ServiceFabricApplication`](https://docs.microsoft.com/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet takes the application parameters as a hashtable.</span><span class="sxs-lookup"><span data-stu-id="35f3f-127">In PowerShell, the [`New-ServiceFabricApplication`](https://docs.microsoft.com/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet takes the application parameters as a hashtable.</span></span>
  - <span data-ttu-id="35f3f-128">Using sfctl, The [`sfctl application create`](https://docs.microsoft.com/azure/service-fabric/service-fabric-sfctl-application#sfctl-application-create) command takes parameters as a JSON string.</span><span class="sxs-lookup"><span data-stu-id="35f3f-128">Using sfctl, The [`sfctl application create`](https://docs.microsoft.com/azure/service-fabric/service-fabric-sfctl-application#sfctl-application-create) command takes parameters as a JSON string.</span></span> <span data-ttu-id="35f3f-129">The install.sh script uses sfctl.</span><span class="sxs-lookup"><span data-stu-id="35f3f-129">The install.sh script uses sfctl.</span></span>
  - <span data-ttu-id="35f3f-130">Visual Studio provides you with a set of parameter files in the Parameters folder in the application project.</span><span class="sxs-lookup"><span data-stu-id="35f3f-130">Visual Studio provides you with a set of parameter files in the Parameters folder in the application project.</span></span> <span data-ttu-id="35f3f-131">These parameter files are used when publishing from Visual Studio, using Azure DevOps Services or Team Foundation Server.</span><span class="sxs-lookup"><span data-stu-id="35f3f-131">These parameter files are used when publishing from Visual Studio, using Azure DevOps Services or Team Foundation Server.</span></span> <span data-ttu-id="35f3f-132">In Visual Studio, the parameter files are being passed on to the Deploy-FabricApplication.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="35f3f-132">In Visual Studio, the parameter files are being passed on to the Deploy-FabricApplication.ps1 script.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35f3f-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="35f3f-133">Next steps</span></span>
<span data-ttu-id="35f3f-134">The following articles show you how to use some of the concepts described here:</span><span class="sxs-lookup"><span data-stu-id="35f3f-134">The following articles show you how to use some of the concepts described here:</span></span>

- [<span data-ttu-id="35f3f-135">How to specify environment variables for services in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="35f3f-135">How to specify environment variables for services in Service Fabric</span></span>](service-fabric-how-to-specify-environment-variables.md)
- [<span data-ttu-id="35f3f-136">How to specify the port number of a service using parameters in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="35f3f-136">How to specify the port number of a service using parameters in Service Fabric</span></span>](service-fabric-how-to-specify-port-number-using-parameters.md)
- [<span data-ttu-id="35f3f-137">How to parameterize configuration files</span><span class="sxs-lookup"><span data-stu-id="35f3f-137">How to parameterize configuration files</span></span>](service-fabric-how-to-parameterize-configuration-files.md)

- [<span data-ttu-id="35f3f-138">Environment variable reference</span><span class="sxs-lookup"><span data-stu-id="35f3f-138">Environment variable reference</span></span>](service-fabric-environment-variables-reference.md)
