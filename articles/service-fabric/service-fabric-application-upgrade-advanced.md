---
title: Advanced Application Upgrade Topics | Microsoft Docs
description: This article covers some advanced topics pertaining to upgrading a Service Fabric application.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar;chackdan
ms.openlocfilehash: c915ab9ed062099ac50491f56bd42c6575da5686
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555889"
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="01b10-103">Service Fabric application upgrade: advanced topics</span><span class="sxs-lookup"><span data-stu-id="01b10-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="01b10-104">Adding or removing services during an application upgrade</span><span class="sxs-lookup"><span data-stu-id="01b10-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="01b10-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span><span class="sxs-lookup"><span data-stu-id="01b10-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="01b10-106">Such an upgrade does not affect any of the services that were already part of the application.</span><span class="sxs-lookup"><span data-stu-id="01b10-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="01b10-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="01b10-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="01b10-108">Services can also be removed from an application as part of an upgrade.</span><span class="sxs-lookup"><span data-stu-id="01b10-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="01b10-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="01b10-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="01b10-110">Manual upgrade mode</span><span class="sxs-lookup"><span data-stu-id="01b10-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="01b10-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span><span class="sxs-lookup"><span data-stu-id="01b10-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="01b10-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span><span class="sxs-lookup"><span data-stu-id="01b10-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="01b10-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span><span class="sxs-lookup"><span data-stu-id="01b10-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="01b10-114">Deployment options chosen may be different for different environments.</span><span class="sxs-lookup"><span data-stu-id="01b10-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="01b10-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span><span class="sxs-lookup"><span data-stu-id="01b10-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="01b10-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span><span class="sxs-lookup"><span data-stu-id="01b10-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="01b10-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="01b10-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="01b10-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span><span class="sxs-lookup"><span data-stu-id="01b10-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="01b10-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span><span class="sxs-lookup"><span data-stu-id="01b10-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="01b10-120">Change to manual upgrade mode</span><span class="sxs-lookup"><span data-stu-id="01b10-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="01b10-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span><span class="sxs-lookup"><span data-stu-id="01b10-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="01b10-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span><span class="sxs-lookup"><span data-stu-id="01b10-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="01b10-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span><span class="sxs-lookup"><span data-stu-id="01b10-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="01b10-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span><span class="sxs-lookup"><span data-stu-id="01b10-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="01b10-125">Upgrade with a diff package</span><span class="sxs-lookup"><span data-stu-id="01b10-125">Upgrade with a diff package</span></span>
<span data-ttu-id="01b10-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span><span class="sxs-lookup"><span data-stu-id="01b10-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="01b10-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span><span class="sxs-lookup"><span data-stu-id="01b10-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="01b10-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="01b10-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="01b10-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span><span class="sxs-lookup"><span data-stu-id="01b10-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="01b10-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span><span class="sxs-lookup"><span data-stu-id="01b10-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="01b10-131">Full application packages are required for the first installation of an application to the cluster.</span><span class="sxs-lookup"><span data-stu-id="01b10-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="01b10-132">Subsequent updates can be either a full application package or a diff package.</span><span class="sxs-lookup"><span data-stu-id="01b10-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="01b10-133">Occasions when using a diff package would be a good choice:</span><span class="sxs-lookup"><span data-stu-id="01b10-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="01b10-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span><span class="sxs-lookup"><span data-stu-id="01b10-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="01b10-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span><span class="sxs-lookup"><span data-stu-id="01b10-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="01b10-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span><span class="sxs-lookup"><span data-stu-id="01b10-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="01b10-137">Using a full application package would require you to update the version on all code packages.</span><span class="sxs-lookup"><span data-stu-id="01b10-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="01b10-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span><span class="sxs-lookup"><span data-stu-id="01b10-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="01b10-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span><span class="sxs-lookup"><span data-stu-id="01b10-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="01b10-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span><span class="sxs-lookup"><span data-stu-id="01b10-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="01b10-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span><span class="sxs-lookup"><span data-stu-id="01b10-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="01b10-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01b10-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="01b10-143">Now, your updated application has the following folder structure:</span><span class="sxs-lookup"><span data-stu-id="01b10-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="01b10-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span><span class="sxs-lookup"><span data-stu-id="01b10-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="01b10-145">The folder for your application package would have the following structure:</span><span class="sxs-lookup"><span data-stu-id="01b10-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="01b10-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="01b10-146">Next steps</span></span>
<span data-ttu-id="01b10-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01b10-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="01b10-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01b10-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="01b10-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="01b10-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="01b10-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="01b10-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="01b10-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="01b10-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
