---
title: Service Fabric application deployment | Microsoft Docs
description: How to deploy and remove applications in Service Fabric
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/23/2017
ms.author: ryanwi
ms.openlocfilehash: 3dd7f6db58bbb8704b7811b2fd19619e5e1ec0d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563877"
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="88236-103">Deploy and remove applications using PowerShell</span><span class="sxs-lookup"><span data-stu-id="88236-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient APIs](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="88236-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="88236-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="88236-108">Deployment involves the following three steps:</span><span class="sxs-lookup"><span data-stu-id="88236-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="88236-109">Upload the application package to the image store</span><span class="sxs-lookup"><span data-stu-id="88236-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="88236-110">Register the application type</span><span class="sxs-lookup"><span data-stu-id="88236-110">Register the application type</span></span>
3. <span data-ttu-id="88236-111">Create the application instance</span><span class="sxs-lookup"><span data-stu-id="88236-111">Create the application instance</span></span>

<span data-ttu-id="88236-112">After an app is deployed and an instance is running in the cluster, you can delete the app instance and its application type.</span><span class="sxs-lookup"><span data-stu-id="88236-112">After an app is deployed and an instance is running in the cluster, you can delete the app instance and its application type.</span></span> <span data-ttu-id="88236-113">To completely remove an app from the cluster involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="88236-113">To completely remove an app from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="88236-114">Remove (or delete) the running application instance</span><span class="sxs-lookup"><span data-stu-id="88236-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="88236-115">Unregister the application type if you no longer need it</span><span class="sxs-lookup"><span data-stu-id="88236-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="88236-116">Remove the application package from the image store</span><span class="sxs-lookup"><span data-stu-id="88236-116">Remove the application package from the image store</span></span>

<span data-ttu-id="88236-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="88236-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="88236-118">This script is found in the *Scripts* folder of the application project.</span><span class="sxs-lookup"><span data-stu-id="88236-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="88236-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88236-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="88236-120">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="88236-120">Connect to the cluster</span></span>
<span data-ttu-id="88236-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/servicefabric/vlatest/connect-servicefabriccluster) to connect to the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="88236-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/servicefabric/vlatest/connect-servicefabriccluster) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="88236-122">To connect to the local development cluster, run the following:</span><span class="sxs-lookup"><span data-stu-id="88236-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="88236-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="88236-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="88236-124">Upload the application package</span><span class="sxs-lookup"><span data-stu-id="88236-124">Upload the application package</span></span>
<span data-ttu-id="88236-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span><span class="sxs-lookup"><span data-stu-id="88236-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="88236-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88236-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.</span></span>

<span data-ttu-id="88236-127">The [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command uploads the application package to the cluster image store.</span><span class="sxs-lookup"><span data-stu-id="88236-127">The [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="88236-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span><span class="sxs-lookup"><span data-stu-id="88236-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="88236-129">To import the SDK module, run:</span><span class="sxs-lookup"><span data-stu-id="88236-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="88236-130">Suppose you build and package an app named *MyApplication* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88236-130">Suppose you build and package an app named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="88236-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="88236-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="88236-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="88236-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="88236-133">The following command lists the contents of the application package:</span><span class="sxs-lookup"><span data-stu-id="88236-133">The following command lists the contents of the application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\user\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="88236-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="88236-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="88236-135">The compression reduces the size and the number of files.</span><span class="sxs-lookup"><span data-stu-id="88236-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="88236-136">The side effect is that registering and un-registering the application type are faster.</span><span class="sxs-lookup"><span data-stu-id="88236-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="88236-137">Upload time may be slower currently, especially if you include the time to compress the package.</span><span class="sxs-lookup"><span data-stu-id="88236-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="88236-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command.</span><span class="sxs-lookup"><span data-stu-id="88236-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command.</span></span> <span data-ttu-id="88236-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span><span class="sxs-lookup"><span data-stu-id="88236-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="88236-140">Applying compression on a compressed package is no-op.</span><span class="sxs-lookup"><span data-stu-id="88236-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="88236-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command with the `UncompressPackage` switch.</span><span class="sxs-lookup"><span data-stu-id="88236-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="88236-142">The following cmdlet compresses the package without copying it to the image store.</span><span class="sxs-lookup"><span data-stu-id="88236-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="88236-143">The package now includes zipped files for the `Code` and `Config` packages.</span><span class="sxs-lookup"><span data-stu-id="88236-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="88236-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span><span class="sxs-lookup"><span data-stu-id="88236-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="88236-145">Zipping the manifests would make these operations inefficient.</span><span class="sxs-lookup"><span data-stu-id="88236-145">Zipping the manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="88236-146">For large application packages, the compression takes time.</span><span class="sxs-lookup"><span data-stu-id="88236-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="88236-147">For best results, use a fast SSD drive.</span><span class="sxs-lookup"><span data-stu-id="88236-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="88236-148">The compression times and the size of the compressed package also differ based on the package content.</span><span class="sxs-lookup"><span data-stu-id="88236-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="88236-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span><span class="sxs-lookup"><span data-stu-id="88236-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="88236-150">Initial size (MB)</span><span class="sxs-lookup"><span data-stu-id="88236-150">Initial size (MB)</span></span>|<span data-ttu-id="88236-151">File count</span><span class="sxs-lookup"><span data-stu-id="88236-151">File count</span></span>|<span data-ttu-id="88236-152">Compression Time</span><span class="sxs-lookup"><span data-stu-id="88236-152">Compression Time</span></span>|<span data-ttu-id="88236-153">Compressed package size (MB)</span><span class="sxs-lookup"><span data-stu-id="88236-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="88236-154">100</span><span class="sxs-lookup"><span data-stu-id="88236-154">100</span></span>|<span data-ttu-id="88236-155">100</span><span class="sxs-lookup"><span data-stu-id="88236-155">100</span></span>|<span data-ttu-id="88236-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="88236-156">00:00:03.3547592</span></span>|<span data-ttu-id="88236-157">60</span><span class="sxs-lookup"><span data-stu-id="88236-157">60</span></span>|
|<span data-ttu-id="88236-158">512</span><span class="sxs-lookup"><span data-stu-id="88236-158">512</span></span>|<span data-ttu-id="88236-159">100</span><span class="sxs-lookup"><span data-stu-id="88236-159">100</span></span>|<span data-ttu-id="88236-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="88236-160">00:00:16.3850303</span></span>|<span data-ttu-id="88236-161">307</span><span class="sxs-lookup"><span data-stu-id="88236-161">307</span></span>|
|<span data-ttu-id="88236-162">1024</span><span class="sxs-lookup"><span data-stu-id="88236-162">1024</span></span>|<span data-ttu-id="88236-163">500</span><span class="sxs-lookup"><span data-stu-id="88236-163">500</span></span>|<span data-ttu-id="88236-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="88236-164">00:00:32.5907950</span></span>|<span data-ttu-id="88236-165">615</span><span class="sxs-lookup"><span data-stu-id="88236-165">615</span></span>|
|<span data-ttu-id="88236-166">2048</span><span class="sxs-lookup"><span data-stu-id="88236-166">2048</span></span>|<span data-ttu-id="88236-167">1000</span><span class="sxs-lookup"><span data-stu-id="88236-167">1000</span></span>|<span data-ttu-id="88236-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="88236-168">00:01:04.3775554</span></span>|<span data-ttu-id="88236-169">1231</span><span class="sxs-lookup"><span data-stu-id="88236-169">1231</span></span>|
|<span data-ttu-id="88236-170">5012</span><span class="sxs-lookup"><span data-stu-id="88236-170">5012</span></span>|<span data-ttu-id="88236-171">100</span><span class="sxs-lookup"><span data-stu-id="88236-171">100</span></span>|<span data-ttu-id="88236-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="88236-172">00:02:45.2951288</span></span>|<span data-ttu-id="88236-173">3074</span><span class="sxs-lookup"><span data-stu-id="88236-173">3074</span></span>|

<span data-ttu-id="88236-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span><span class="sxs-lookup"><span data-stu-id="88236-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="88236-175">The deploy mechanism is same for compressed and uncompressed packages.</span><span class="sxs-lookup"><span data-stu-id="88236-175">The deploy mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="88236-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span><span class="sxs-lookup"><span data-stu-id="88236-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="88236-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="88236-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="88236-178">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the app package is copied into the "Debug" folder in the image store.</span><span class="sxs-lookup"><span data-stu-id="88236-178">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the app package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="88236-179">The time it takes to upload a package differs depending on multiple factors.</span><span class="sxs-lookup"><span data-stu-id="88236-179">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="88236-180">Some of these factors are the number of files in the package, the package size, and the file sizes.</span><span class="sxs-lookup"><span data-stu-id="88236-180">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="88236-181">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span><span class="sxs-lookup"><span data-stu-id="88236-181">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="88236-182">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) is 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="88236-182">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) is 30 minutes.</span></span>
<span data-ttu-id="88236-183">Depending on the described factors, you may have to increase the timeout.</span><span class="sxs-lookup"><span data-stu-id="88236-183">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="88236-184">If you are compressing the package in the copy call, you need to also consider the compression time.</span><span class="sxs-lookup"><span data-stu-id="88236-184">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="88236-185">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span><span class="sxs-lookup"><span data-stu-id="88236-185">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="88236-186">Register the application package</span><span class="sxs-lookup"><span data-stu-id="88236-186">Register the application package</span></span>
<span data-ttu-id="88236-187">The application type and version declared in the application manifest become available for use when the app package is registered.</span><span class="sxs-lookup"><span data-stu-id="88236-187">The application type and version declared in the application manifest become available for use when the app package is registered.</span></span> <span data-ttu-id="88236-188">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span><span class="sxs-lookup"><span data-stu-id="88236-188">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="88236-189">Run the [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet to register the application type in the cluster and make it available for deployment:</span><span class="sxs-lookup"><span data-stu-id="88236-189">Run the [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="88236-190">"MyApplicationV1" is the folder in the image store where the app package is located.</span><span class="sxs-lookup"><span data-stu-id="88236-190">"MyApplicationV1" is the folder in the image store where the app package is located.</span></span> <span data-ttu-id="88236-191">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span><span class="sxs-lookup"><span data-stu-id="88236-191">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="88236-192">The [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) command returns only after the system has successfully registered the application package.</span><span class="sxs-lookup"><span data-stu-id="88236-192">The [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="88236-193">How long registration takes depends on the size and contents of the application package.</span><span class="sxs-lookup"><span data-stu-id="88236-193">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="88236-194">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span><span class="sxs-lookup"><span data-stu-id="88236-194">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="88236-195">If you have a large app package or if you are experiencing timeouts, use the **-Async** parameter.</span><span class="sxs-lookup"><span data-stu-id="88236-195">If you have a large app package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="88236-196">The command returns when the cluster accepts the register command, and the processing continues as needed.</span><span class="sxs-lookup"><span data-stu-id="88236-196">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="88236-197">The [Get-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/get-servicefabricapplicationtype) command lists all successfully registered application type versions and their registration status.</span><span class="sxs-lookup"><span data-stu-id="88236-197">The [Get-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/get-servicefabricapplicationtype) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="88236-198">You can use this command to determine when the registration is done.</span><span class="sxs-lookup"><span data-stu-id="88236-198">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="88236-199">Create the application</span><span class="sxs-lookup"><span data-stu-id="88236-199">Create the application</span></span>
<span data-ttu-id="88236-200">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/servicefabric/vlatest/new-servicefabricapplication) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88236-200">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/servicefabric/vlatest/new-servicefabricapplication) cmdlet.</span></span> <span data-ttu-id="88236-201">The name of each application must start with the *fabric:* scheme and be unique for each application instance.</span><span class="sxs-lookup"><span data-stu-id="88236-201">The name of each application must start with the *fabric:* scheme and be unique for each application instance.</span></span> <span data-ttu-id="88236-202">Any default services defined in the application manifest of the target application type are also created.</span><span class="sxs-lookup"><span data-stu-id="88236-202">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="88236-203">Multiple application instances can be created for any given version of a registered application type.</span><span class="sxs-lookup"><span data-stu-id="88236-203">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="88236-204">Each application instance runs in isolation, with its own work directory and process.</span><span class="sxs-lookup"><span data-stu-id="88236-204">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="88236-205">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/servicefabric/vlatest/get-servicefabricservice) cmdlets:</span><span class="sxs-lookup"><span data-stu-id="88236-205">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/servicefabric/vlatest/get-servicefabricservice) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="88236-206">Remove an application</span><span class="sxs-lookup"><span data-stu-id="88236-206">Remove an application</span></span>
<span data-ttu-id="88236-207">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/servicefabric/vlatest/remove-servicefabricapplication) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88236-207">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/servicefabric/vlatest/remove-servicefabricapplication) cmdlet.</span></span> <span data-ttu-id="88236-208">[Remove-ServiceFabricApplication](/powershell/servicefabric/vlatest/remove-servicefabricapplication) automatically removes all services that belong to the application as well, permanently removing all service state.</span><span class="sxs-lookup"><span data-stu-id="88236-208">[Remove-ServiceFabricApplication](/powershell/servicefabric/vlatest/remove-servicefabricapplication) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> <span data-ttu-id="88236-209">This operation cannot be reversed, and application state cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="88236-209">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="88236-210">Unregister an application type</span><span class="sxs-lookup"><span data-stu-id="88236-210">Unregister an application type</span></span>
<span data-ttu-id="88236-211">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88236-211">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype) cmdlet.</span></span> <span data-ttu-id="88236-212">Unregistering unused application types releases storage space used by the image store.</span><span class="sxs-lookup"><span data-stu-id="88236-212">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="88236-213">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span><span class="sxs-lookup"><span data-stu-id="88236-213">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="88236-214">Run [Get-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/get-servicefabricapplicationtype) to see the application types currently registered in the cluster:</span><span class="sxs-lookup"><span data-stu-id="88236-214">Run [Get-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/get-servicefabricapplicationtype) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="88236-215">Run [Unregister-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype) to unregister a specific application type:</span><span class="sxs-lookup"><span data-stu-id="88236-215">Run [Unregister-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="88236-216">Remove an application package from the image store</span><span class="sxs-lookup"><span data-stu-id="88236-216">Remove an application package from the image store</span></span>
<span data-ttu-id="88236-217">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span><span class="sxs-lookup"><span data-stu-id="88236-217">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="88236-218">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="88236-218">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="88236-219">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="88236-219">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="88236-220">The Service Fabric SDK environment should already have the correct defaults set up.</span><span class="sxs-lookup"><span data-stu-id="88236-220">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="88236-221">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span><span class="sxs-lookup"><span data-stu-id="88236-221">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="88236-222">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/servicefabric/vlatest/get-servicefabricclustermanifest) commanC:</span><span class="sxs-lookup"><span data-stu-id="88236-222">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/servicefabric/vlatest/get-servicefabricclustermanifest) commanC:</span></span>

```powershell
PS C:\> Get-ServiceFabricClusterManifest
```

<span data-ttu-id="88236-223">The ImageStoreConnectionString is found in the cluster manifest:</span><span class="sxs-lookup"><span data-stu-id="88236-223">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="88236-224">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span><span class="sxs-lookup"><span data-stu-id="88236-224">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="88236-225">Deploy large application package</span><span class="sxs-lookup"><span data-stu-id="88236-225">Deploy large application package</span></span>
<span data-ttu-id="88236-226">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) times out for a large application package (order of GB).</span><span class="sxs-lookup"><span data-stu-id="88236-226">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="88236-227">Try:</span><span class="sxs-lookup"><span data-stu-id="88236-227">Try:</span></span>
- <span data-ttu-id="88236-228">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command, with `TimeoutSec` parameter.</span><span class="sxs-lookup"><span data-stu-id="88236-228">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="88236-229">By default, the timeout is 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="88236-229">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="88236-230">Check the network connection between your source machine and cluster.</span><span class="sxs-lookup"><span data-stu-id="88236-230">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="88236-231">If the connection is slow, consider using a machine with a better network connection.</span><span class="sxs-lookup"><span data-stu-id="88236-231">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="88236-232">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span><span class="sxs-lookup"><span data-stu-id="88236-232">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="88236-233">Check if you are hitting external throttling.</span><span class="sxs-lookup"><span data-stu-id="88236-233">Check if you are hitting external throttling.</span></span> <span data-ttu-id="88236-234">For example, when the image store is configured to use azure storage, upload may be throttled.</span><span class="sxs-lookup"><span data-stu-id="88236-234">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="88236-235">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) times out. Try:</span><span class="sxs-lookup"><span data-stu-id="88236-235">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) times out. Try:</span></span>
- <span data-ttu-id="88236-236">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span><span class="sxs-lookup"><span data-stu-id="88236-236">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="88236-237">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span><span class="sxs-lookup"><span data-stu-id="88236-237">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="88236-238">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span><span class="sxs-lookup"><span data-stu-id="88236-238">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="88236-239">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) with `TimeoutSec` parameter.</span><span class="sxs-lookup"><span data-stu-id="88236-239">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="88236-240">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype).</span><span class="sxs-lookup"><span data-stu-id="88236-240">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype).</span></span> <span data-ttu-id="88236-241">The command returns when the cluster accepts the command and the provision continues async.</span><span class="sxs-lookup"><span data-stu-id="88236-241">The command returns when the cluster accepts the command and the provision continues async.</span></span>
<span data-ttu-id="88236-242">For this reason, there is no need to specify a higher timeout in this case.</span><span class="sxs-lookup"><span data-stu-id="88236-242">For this reason, there is no need to specify a higher timeout in this case.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="88236-243">Deploy application package with many files</span><span class="sxs-lookup"><span data-stu-id="88236-243">Deploy application package with many files</span></span>
<span data-ttu-id="88236-244">Issue: [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) times out for an application package with many files (order of thousands).</span><span class="sxs-lookup"><span data-stu-id="88236-244">Issue: [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="88236-245">Try:</span><span class="sxs-lookup"><span data-stu-id="88236-245">Try:</span></span>
- <span data-ttu-id="88236-246">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span><span class="sxs-lookup"><span data-stu-id="88236-246">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="88236-247">The compression reduces the number of files.</span><span class="sxs-lookup"><span data-stu-id="88236-247">The compression reduces the number of files.</span></span>
- <span data-ttu-id="88236-248">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) with `TimeoutSec` parameter.</span><span class="sxs-lookup"><span data-stu-id="88236-248">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="88236-249">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype).</span><span class="sxs-lookup"><span data-stu-id="88236-249">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype).</span></span> <span data-ttu-id="88236-250">The command returns when the cluster accepts the command and the provision continues async.</span><span class="sxs-lookup"><span data-stu-id="88236-250">The command returns when the cluster accepts the command and the provision continues async.</span></span>
<span data-ttu-id="88236-251">For this reason, there is no need to specify a higher timeout in this case.</span><span class="sxs-lookup"><span data-stu-id="88236-251">For this reason, there is no need to specify a higher timeout in this case.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="88236-252">Next steps</span><span class="sxs-lookup"><span data-stu-id="88236-252">Next steps</span></span>
[<span data-ttu-id="88236-253">Service Fabric application upgrade</span><span class="sxs-lookup"><span data-stu-id="88236-253">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="88236-254">Service Fabric health introduction</span><span class="sxs-lookup"><span data-stu-id="88236-254">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="88236-255">Diagnose and troubleshoot a Service Fabric service</span><span class="sxs-lookup"><span data-stu-id="88236-255">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="88236-256">Model an application in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="88236-256">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
