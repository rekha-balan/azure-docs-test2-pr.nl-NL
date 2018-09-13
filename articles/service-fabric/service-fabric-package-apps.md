---
title: Package an Azure Service Fabric app | Microsoft Docs
description: How to package a Service Fabric application before deploying to a cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 3/24/2017
ms.author: ryanwi
ms.openlocfilehash: 57e025033457a2906c01545f54c77421c6d8b16d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556384"
---
# <a name="package-an-application"></a><span data-ttu-id="03316-103">Package an application</span><span class="sxs-lookup"><span data-stu-id="03316-103">Package an application</span></span>
<span data-ttu-id="03316-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span><span class="sxs-lookup"><span data-stu-id="03316-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="03316-105">Package layout</span><span class="sxs-lookup"><span data-stu-id="03316-105">Package layout</span></span>
<span data-ttu-id="03316-106">The application manifest, service manifest(s), and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="03316-106">The application manifest, service manifest(s), and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="03316-107">The example manifests in this article would need to be organized in the following directory structure:</span><span class="sxs-lookup"><span data-stu-id="03316-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="03316-108">The folders are named to match the **Name** attributes of each corresponding element.</span><span class="sxs-lookup"><span data-stu-id="03316-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="03316-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span><span class="sxs-lookup"><span data-stu-id="03316-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="03316-110">Use SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="03316-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="03316-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="03316-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="03316-112">For example:</span><span class="sxs-lookup"><span data-stu-id="03316-112">For example:</span></span>

* <span data-ttu-id="03316-113">Setting up and initializing environment variables that the service executable needs.</span><span class="sxs-lookup"><span data-stu-id="03316-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="03316-114">This is not limited to only executables written via the Service Fabric programming models.</span><span class="sxs-lookup"><span data-stu-id="03316-114">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="03316-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span><span class="sxs-lookup"><span data-stu-id="03316-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="03316-116">Setting up access control by installing security certificates.</span><span class="sxs-lookup"><span data-stu-id="03316-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="03316-117">For more details on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="03316-117">For more details on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>  

## <a name="configure"></a><span data-ttu-id="03316-118">Configure</span><span class="sxs-lookup"><span data-stu-id="03316-118">Configure</span></span> 
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="03316-119">Build a package by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="03316-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="03316-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span><span class="sxs-lookup"><span data-stu-id="03316-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="03316-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span><span class="sxs-lookup"><span data-stu-id="03316-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Packaging an application with Visual Studio][vs-package-command]

<span data-ttu-id="03316-123">When packaging is complete, you can find the location of the package in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="03316-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="03316-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03316-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="03316-125">Build a package by command line</span><span class="sxs-lookup"><span data-stu-id="03316-125">Build a package by command line</span></span>
<span data-ttu-id="03316-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="03316-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="03316-127">Under the hood, this is what Visual Studio is running so the output is the same.</span><span class="sxs-lookup"><span data-stu-id="03316-127">Under the hood, this is what Visual Studio is running so the output is the same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="03316-128">Test the package</span><span class="sxs-lookup"><span data-stu-id="03316-128">Test the package</span></span>
<span data-ttu-id="03316-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) command.</span><span class="sxs-lookup"><span data-stu-id="03316-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) command.</span></span>
<span data-ttu-id="03316-130">This command checks for manifest parsing issues and verify all references.</span><span class="sxs-lookup"><span data-stu-id="03316-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="03316-131">This command only verifies the structural correctness of the directories and files in the package.</span><span class="sxs-lookup"><span data-stu-id="03316-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="03316-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span><span class="sxs-lookup"><span data-stu-id="03316-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="03316-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span><span class="sxs-lookup"><span data-stu-id="03316-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="03316-134">After the missing file is added, the application verification passes:</span><span class="sxs-lookup"><span data-stu-id="03316-134">After the missing file is added, the application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="03316-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](https://docs.microsoft.com/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) for proper validation.</span><span class="sxs-lookup"><span data-stu-id="03316-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](https://docs.microsoft.com/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) for proper validation.</span></span>

<span data-ttu-id="03316-136">If you know the cluster where the application will be deployed, it is recommended you pass in the image store connection string.</span><span class="sxs-lookup"><span data-stu-id="03316-136">If you know the cluster where the application will be deployed, it is recommended you pass in the image store connection string.</span></span> <span data-ttu-id="03316-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span><span class="sxs-lookup"><span data-stu-id="03316-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="03316-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span><span class="sxs-lookup"><span data-stu-id="03316-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="03316-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span><span class="sxs-lookup"><span data-stu-id="03316-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span> 

## <a name="compress-a-package"></a><span data-ttu-id="03316-140">Compress a package</span><span class="sxs-lookup"><span data-stu-id="03316-140">Compress a package</span></span>
<span data-ttu-id="03316-141">When a package is large or has many files, you can compress it for faster deployment.</span><span class="sxs-lookup"><span data-stu-id="03316-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="03316-142">Compression reduces the number of files and the package size.</span><span class="sxs-lookup"><span data-stu-id="03316-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="03316-143">[Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer than uploading the uncompressed package, but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) is faster.</span><span class="sxs-lookup"><span data-stu-id="03316-143">[Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer than uploading the uncompressed package, but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) is faster.</span></span>

<span data-ttu-id="03316-144">The deploy mechanism is same for compressed and uncompressed packages.</span><span class="sxs-lookup"><span data-stu-id="03316-144">The deploy mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="03316-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span><span class="sxs-lookup"><span data-stu-id="03316-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="03316-146">The compression replaces the valid Service Fabric package with the compressed version.</span><span class="sxs-lookup"><span data-stu-id="03316-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="03316-147">The folder must allow write permissions.</span><span class="sxs-lookup"><span data-stu-id="03316-147">The folder must allow write permissions.</span></span> <span data-ttu-id="03316-148">Running compression on an already compressed package yields no changes.</span><span class="sxs-lookup"><span data-stu-id="03316-148">Running compression on an already compressed package yields no changes.</span></span> 

<span data-ttu-id="03316-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) with `CompressPackage` switch.</span><span class="sxs-lookup"><span data-stu-id="03316-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) with `CompressPackage` switch.</span></span> <span data-ttu-id="03316-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span><span class="sxs-lookup"><span data-stu-id="03316-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="03316-151">The following command compresses the package without copying it to the image store.</span><span class="sxs-lookup"><span data-stu-id="03316-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="03316-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) without the `SkipCopy` flag.</span><span class="sxs-lookup"><span data-stu-id="03316-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) without the `SkipCopy` flag.</span></span> <span data-ttu-id="03316-153">The package now includes zipped files for the `code`, `config` and `data` packages.</span><span class="sxs-lookup"><span data-stu-id="03316-153">The package now includes zipped files for the `code`, `config` and `data` packages.</span></span> <span data-ttu-id="03316-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span><span class="sxs-lookup"><span data-stu-id="03316-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="03316-155">Zipping the manifests would make these operations inefficient.</span><span class="sxs-lookup"><span data-stu-id="03316-155">Zipping the manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="03316-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) in one step.</span><span class="sxs-lookup"><span data-stu-id="03316-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) in one step.</span></span>
<span data-ttu-id="03316-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span><span class="sxs-lookup"><span data-stu-id="03316-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="03316-158">Internally, Service Fabric computes checksums for the application packages for validation.</span><span class="sxs-lookup"><span data-stu-id="03316-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="03316-159">When using compression, the checksums are computed on the zipped versions of each package.</span><span class="sxs-lookup"><span data-stu-id="03316-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="03316-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config` and `data` packages to avoid checksum mismatch.</span><span class="sxs-lookup"><span data-stu-id="03316-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config` and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="03316-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="03316-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="03316-162">With this option, do not include the unchanged package, just reference it from the service manifest.</span><span class="sxs-lookup"><span data-stu-id="03316-162">With this option, do not include the unchanged package, just reference it from the service manifest.</span></span>

<span data-ttu-id="03316-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span><span class="sxs-lookup"><span data-stu-id="03316-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="03316-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span><span class="sxs-lookup"><span data-stu-id="03316-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03316-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="03316-165">Next steps</span></span>
<span data-ttu-id="03316-166">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span><span class="sxs-lookup"><span data-stu-id="03316-166">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="03316-167">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span><span class="sxs-lookup"><span data-stu-id="03316-167">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="03316-168">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span><span class="sxs-lookup"><span data-stu-id="03316-168">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md

