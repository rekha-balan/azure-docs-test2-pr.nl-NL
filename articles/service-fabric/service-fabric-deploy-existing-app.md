---
title: Deploy an existing executable to Azure Service Fabric | Microsoft Docs
description: Walkthrough on how to package an existing application as a guest executable, so it can be deployed to a Service Fabric cluster
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/07/2016
ms.author: mfussell;mikhegn
ms.openlocfilehash: dec3c658155efc3cac7a2cf12fe1b6e3784f987c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556736"
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="4cd75-103">Deploy a guest executable to Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4cd75-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="4cd75-104">You can run any type of application, such as Node.js, Java, or native applications in Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cd75-104">You can run any type of application, such as Node.js, Java, or native applications in Azure Service Fabric.</span></span> <span data-ttu-id="4cd75-105">Service Fabric refers to these types of applications as guest executables.</span><span class="sxs-lookup"><span data-stu-id="4cd75-105">Service Fabric refers to these types of applications as guest executables.</span></span>
<span data-ttu-id="4cd75-106">Guest executables are treated by Service Fabric like stateless services.</span><span class="sxs-lookup"><span data-stu-id="4cd75-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="4cd75-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span><span class="sxs-lookup"><span data-stu-id="4cd75-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="4cd75-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span><span class="sxs-lookup"><span data-stu-id="4cd75-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="4cd75-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cd75-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="4cd75-110">Benefits of running a guest executable in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4cd75-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="4cd75-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span><span class="sxs-lookup"><span data-stu-id="4cd75-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="4cd75-112">High availability.</span><span class="sxs-lookup"><span data-stu-id="4cd75-112">High availability.</span></span> <span data-ttu-id="4cd75-113">Applications that run in Service Fabric are made highly available.</span><span class="sxs-lookup"><span data-stu-id="4cd75-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="4cd75-114">Service Fabric ensures that instances of an application are running.</span><span class="sxs-lookup"><span data-stu-id="4cd75-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="4cd75-115">Health monitoring.</span><span class="sxs-lookup"><span data-stu-id="4cd75-115">Health monitoring.</span></span> <span data-ttu-id="4cd75-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span><span class="sxs-lookup"><span data-stu-id="4cd75-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="4cd75-117">Application lifecycle management.</span><span class="sxs-lookup"><span data-stu-id="4cd75-117">Application lifecycle management.</span></span> <span data-ttu-id="4cd75-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span><span class="sxs-lookup"><span data-stu-id="4cd75-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="4cd75-119">Density.</span><span class="sxs-lookup"><span data-stu-id="4cd75-119">Density.</span></span> <span data-ttu-id="4cd75-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span><span class="sxs-lookup"><span data-stu-id="4cd75-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>

## <a name="samples"></a><span data-ttu-id="4cd75-121">Samples</span><span class="sxs-lookup"><span data-stu-id="4cd75-121">Samples</span></span>
* [<span data-ttu-id="4cd75-122">Sample for packaging and deploying a guest executable</span><span class="sxs-lookup"><span data-stu-id="4cd75-122">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="4cd75-123">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span><span class="sxs-lookup"><span data-stu-id="4cd75-123">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="4cd75-124">Overview of application and service manifest files</span><span class="sxs-lookup"><span data-stu-id="4cd75-124">Overview of application and service manifest files</span></span>
<span data-ttu-id="4cd75-125">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="4cd75-125">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="4cd75-126">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span><span class="sxs-lookup"><span data-stu-id="4cd75-126">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="4cd75-127">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="4cd75-127">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="4cd75-128">**Application manifest** The application manifest is used to describe the application.</span><span class="sxs-lookup"><span data-stu-id="4cd75-128">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="4cd75-129">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span><span class="sxs-lookup"><span data-stu-id="4cd75-129">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>
  
  <span data-ttu-id="4cd75-130">In Service Fabric, an application is a unit of deployment and upgrade.</span><span class="sxs-lookup"><span data-stu-id="4cd75-130">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="4cd75-131">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span><span class="sxs-lookup"><span data-stu-id="4cd75-131">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="4cd75-132">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span><span class="sxs-lookup"><span data-stu-id="4cd75-132">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="4cd75-133">**Service manifest** The service manifest describes the components of a service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-133">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="4cd75-134">It includes data, such as the name and type of service, and its code and configuration.</span><span class="sxs-lookup"><span data-stu-id="4cd75-134">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="4cd75-135">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span><span class="sxs-lookup"><span data-stu-id="4cd75-135">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="4cd75-136">Application package file structure</span><span class="sxs-lookup"><span data-stu-id="4cd75-136">Application package file structure</span></span>
<span data-ttu-id="4cd75-137">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span><span class="sxs-lookup"><span data-stu-id="4cd75-137">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="4cd75-138">The following is an example of that structure.</span><span class="sxs-lookup"><span data-stu-id="4cd75-138">The following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="4cd75-139">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span><span class="sxs-lookup"><span data-stu-id="4cd75-139">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="4cd75-140">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span><span class="sxs-lookup"><span data-stu-id="4cd75-140">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="4cd75-141">These subdirectories are the ServiceManifest.xml and, typically, the following:</span><span class="sxs-lookup"><span data-stu-id="4cd75-141">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="4cd75-142">*Code*.</span><span class="sxs-lookup"><span data-stu-id="4cd75-142">*Code*.</span></span> <span data-ttu-id="4cd75-143">This directory contains the service code.</span><span class="sxs-lookup"><span data-stu-id="4cd75-143">This directory contains the service code.</span></span>
* <span data-ttu-id="4cd75-144">*Config*. This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span><span class="sxs-lookup"><span data-stu-id="4cd75-144">*Config*. This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="4cd75-145">*Data*.</span><span class="sxs-lookup"><span data-stu-id="4cd75-145">*Data*.</span></span> <span data-ttu-id="4cd75-146">This is an additional directory to store additional local data that the service may need.</span><span class="sxs-lookup"><span data-stu-id="4cd75-146">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="4cd75-147">Data should be used to store only ephemeral data.</span><span class="sxs-lookup"><span data-stu-id="4cd75-147">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="4cd75-148">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span><span class="sxs-lookup"><span data-stu-id="4cd75-148">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="4cd75-149">You don't have to create the `config` and `data` directories if you don't need them.</span><span class="sxs-lookup"><span data-stu-id="4cd75-149">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
> 
> 

## <a name="package-an-existing-executable"></a><span data-ttu-id="4cd75-150">Package an existing executable</span><span class="sxs-lookup"><span data-stu-id="4cd75-150">Package an existing executable</span></span>
<span data-ttu-id="4cd75-151">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span><span class="sxs-lookup"><span data-stu-id="4cd75-151">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="4cd75-152">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span><span class="sxs-lookup"><span data-stu-id="4cd75-152">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="4cd75-153">The easiest way to package an existing Windows executable into a service is to use Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4cd75-153">The easiest way to package an existing Windows executable into a service is to use Visual Studio.</span></span>
> 
> 

## <a name="use-visual-studio-to-package-an-existing-executable"></a><span data-ttu-id="4cd75-154">Use Visual Studio to package an existing executable</span><span class="sxs-lookup"><span data-stu-id="4cd75-154">Use Visual Studio to package an existing executable</span></span>
<span data-ttu-id="4cd75-155">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-155">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="4cd75-156">Choose **File** > **New Project**, and create a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="4cd75-156">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="4cd75-157">Choose **Guest Executable** as the service template.</span><span class="sxs-lookup"><span data-stu-id="4cd75-157">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="4cd75-158">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-158">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="4cd75-159">*Code Package Behavior*.</span><span class="sxs-lookup"><span data-stu-id="4cd75-159">*Code Package Behavior*.</span></span> <span data-ttu-id="4cd75-160">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span><span class="sxs-lookup"><span data-stu-id="4cd75-160">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="4cd75-161">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span><span class="sxs-lookup"><span data-stu-id="4cd75-161">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="4cd75-162">Note that you can use linked folders when creating the application project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4cd75-162">Note that you can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="4cd75-163">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span><span class="sxs-lookup"><span data-stu-id="4cd75-163">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="4cd75-164">Those updates become part of the application package on build.</span><span class="sxs-lookup"><span data-stu-id="4cd75-164">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="4cd75-165">*Program* specifies the executable that should be run to start the service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-165">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="4cd75-166">*Arguments* specifies the arguments that should be passed to the executable.</span><span class="sxs-lookup"><span data-stu-id="4cd75-166">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="4cd75-167">It can be a list of parameters with arguments.</span><span class="sxs-lookup"><span data-stu-id="4cd75-167">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="4cd75-168">*WorkingFolder* specifies the working directory for the process that is going to be started.</span><span class="sxs-lookup"><span data-stu-id="4cd75-168">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="4cd75-169">You can specify three values:</span><span class="sxs-lookup"><span data-stu-id="4cd75-169">You can specify three values:</span></span>
     * <span data-ttu-id="4cd75-170">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span><span class="sxs-lookup"><span data-stu-id="4cd75-170">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="4cd75-171">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span><span class="sxs-lookup"><span data-stu-id="4cd75-171">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="4cd75-172">`Work` specifies that the files are placed in a subdirectory called work.</span><span class="sxs-lookup"><span data-stu-id="4cd75-172">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="4cd75-173">Give your service a name, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4cd75-173">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="4cd75-174">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span><span class="sxs-lookup"><span data-stu-id="4cd75-174">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="4cd75-175">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-175">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="4cd75-176">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4cd75-176">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="4cd75-177">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span><span class="sxs-lookup"><span data-stu-id="4cd75-177">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="4cd75-178">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4cd75-178">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="4cd75-179">Manually package and deploy an existing executable</span><span class="sxs-lookup"><span data-stu-id="4cd75-179">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="4cd75-180">The process of manually packaging a guest executable is based on the following general steps:</span><span class="sxs-lookup"><span data-stu-id="4cd75-180">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="4cd75-181">Create the package directory structure.</span><span class="sxs-lookup"><span data-stu-id="4cd75-181">Create the package directory structure.</span></span>
2. <span data-ttu-id="4cd75-182">Add the application's code and configuration files.</span><span class="sxs-lookup"><span data-stu-id="4cd75-182">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="4cd75-183">Edit the service manifest file.</span><span class="sxs-lookup"><span data-stu-id="4cd75-183">Edit the service manifest file.</span></span>
4. <span data-ttu-id="4cd75-184">Edit the application manifest file.</span><span class="sxs-lookup"><span data-stu-id="4cd75-184">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="4cd75-185">Create the package directory structure</span><span class="sxs-lookup"><span data-stu-id="4cd75-185">Create the package directory structure</span></span>
<span data-ttu-id="4cd75-186">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span><span class="sxs-lookup"><span data-stu-id="4cd75-186">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="4cd75-187">Add the application's code and configuration files</span><span class="sxs-lookup"><span data-stu-id="4cd75-187">Add the application's code and configuration files</span></span>
<span data-ttu-id="4cd75-188">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span><span class="sxs-lookup"><span data-stu-id="4cd75-188">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="4cd75-189">You can also create additional directories or subdirectories under the code or config directories.</span><span class="sxs-lookup"><span data-stu-id="4cd75-189">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="4cd75-190">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span><span class="sxs-lookup"><span data-stu-id="4cd75-190">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="4cd75-191">(You can pick different names if you want.</span><span class="sxs-lookup"><span data-stu-id="4cd75-191">(You can pick different names if you want.</span></span> <span data-ttu-id="4cd75-192">More details are in the next section.)</span><span class="sxs-lookup"><span data-stu-id="4cd75-192">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="4cd75-193">Make sure that you include all the files and dependencies that the application needs.</span><span class="sxs-lookup"><span data-stu-id="4cd75-193">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="4cd75-194">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span><span class="sxs-lookup"><span data-stu-id="4cd75-194">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="4cd75-195">The package should contain all the code that the application needs to run.</span><span class="sxs-lookup"><span data-stu-id="4cd75-195">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="4cd75-196">Do not assume that the dependencies are already installed.</span><span class="sxs-lookup"><span data-stu-id="4cd75-196">Do not assume that the dependencies are already installed.</span></span>
> 
> 

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="4cd75-197">Edit the service manifest file</span><span class="sxs-lookup"><span data-stu-id="4cd75-197">Edit the service manifest file</span></span>
<span data-ttu-id="4cd75-198">The next step is to edit the service manifest file to include the following information:</span><span class="sxs-lookup"><span data-stu-id="4cd75-198">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="4cd75-199">The name of the service type.</span><span class="sxs-lookup"><span data-stu-id="4cd75-199">The name of the service type.</span></span> <span data-ttu-id="4cd75-200">This is an ID that Service Fabric uses to identify a service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-200">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="4cd75-201">The command to use to launch the application (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="4cd75-201">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="4cd75-202">Any script that needs to be run to set up the application (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="4cd75-202">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="4cd75-203">The following is an example of a `ServiceManifest.xml` file:</span><span class="sxs-lookup"><span data-stu-id="4cd75-203">The following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="4cd75-204">The following sections go over the different parts of the file that you need to update.</span><span class="sxs-lookup"><span data-stu-id="4cd75-204">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="4cd75-205">Update ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="4cd75-205">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="4cd75-206">You can pick any name that you want for `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-206">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="4cd75-207">The value is used in the `ApplicationManifest.xml` file to identify the service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-207">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="4cd75-208">Specify `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-208">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="4cd75-209">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span><span class="sxs-lookup"><span data-stu-id="4cd75-209">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="4cd75-210">Update CodePackage</span><span class="sxs-lookup"><span data-stu-id="4cd75-210">Update CodePackage</span></span>
<span data-ttu-id="4cd75-211">The CodePackage element specifies the location (and version) of the service's code.</span><span class="sxs-lookup"><span data-stu-id="4cd75-211">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="4cd75-212">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span><span class="sxs-lookup"><span data-stu-id="4cd75-212">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="4cd75-213">`CodePackage` also has the `version` attribute.</span><span class="sxs-lookup"><span data-stu-id="4cd75-213">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="4cd75-214">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cd75-214">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="4cd75-215">Optional: Update SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="4cd75-215">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="4cd75-216">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span><span class="sxs-lookup"><span data-stu-id="4cd75-216">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="4cd75-217">It is an optional step, so it does not need to be included if there is no initialization required.</span><span class="sxs-lookup"><span data-stu-id="4cd75-217">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="4cd75-218">The SetupEntryPoint is executed every time the service is restarted.</span><span class="sxs-lookup"><span data-stu-id="4cd75-218">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="4cd75-219">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span><span class="sxs-lookup"><span data-stu-id="4cd75-219">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="4cd75-220">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4cd75-220">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="4cd75-221">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="4cd75-221">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="4cd75-222">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span><span class="sxs-lookup"><span data-stu-id="4cd75-222">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="4cd75-223">Update EntryPoint</span><span class="sxs-lookup"><span data-stu-id="4cd75-223">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="4cd75-224">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-224">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="4cd75-225">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-225">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="4cd75-226">`Program` specifies the name of the executable that should start the service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-226">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="4cd75-227">`Arguments` specifies the arguments that should be passed to the executable.</span><span class="sxs-lookup"><span data-stu-id="4cd75-227">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="4cd75-228">It can be a list of parameters with arguments.</span><span class="sxs-lookup"><span data-stu-id="4cd75-228">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="4cd75-229">`WorkingFolder` specifies the working directory for the process that is going to be started.</span><span class="sxs-lookup"><span data-stu-id="4cd75-229">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="4cd75-230">You can specify three values:</span><span class="sxs-lookup"><span data-stu-id="4cd75-230">You can specify three values:</span></span>
  * <span data-ttu-id="4cd75-231">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span><span class="sxs-lookup"><span data-stu-id="4cd75-231">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="4cd75-232">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span><span class="sxs-lookup"><span data-stu-id="4cd75-232">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="4cd75-233">`Work` specifies that the files are placed in a subdirectory called work.</span><span class="sxs-lookup"><span data-stu-id="4cd75-233">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="4cd75-234">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span><span class="sxs-lookup"><span data-stu-id="4cd75-234">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="4cd75-235">Update Endpoints and register with Naming Service for communication</span><span class="sxs-lookup"><span data-stu-id="4cd75-235">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="4cd75-236">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span><span class="sxs-lookup"><span data-stu-id="4cd75-236">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="4cd75-237">In this example, the Node.js application listens on http on port 3000.</span><span class="sxs-lookup"><span data-stu-id="4cd75-237">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="4cd75-238">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-238">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="4cd75-239">This enables you to be able to communicate between services that are guest executables.</span><span class="sxs-lookup"><span data-stu-id="4cd75-239">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="4cd75-240">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-240">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="4cd75-241">`UriScheme` and `PathSuffix` are optional attributes.</span><span class="sxs-lookup"><span data-stu-id="4cd75-241">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="4cd75-242">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span><span class="sxs-lookup"><span data-stu-id="4cd75-242">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="4cd75-243">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span><span class="sxs-lookup"><span data-stu-id="4cd75-243">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="4cd75-244">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-244">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="4cd75-245">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span><span class="sxs-lookup"><span data-stu-id="4cd75-245">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="4cd75-246">Edit the application manifest file</span><span class="sxs-lookup"><span data-stu-id="4cd75-246">Edit the application manifest file</span></span>
<span data-ttu-id="4cd75-247">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span><span class="sxs-lookup"><span data-stu-id="4cd75-247">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="4cd75-248">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="4cd75-248">ServiceManifestImport</span></span>
<span data-ttu-id="4cd75-249">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span><span class="sxs-lookup"><span data-stu-id="4cd75-249">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="4cd75-250">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span><span class="sxs-lookup"><span data-stu-id="4cd75-250">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="4cd75-251">Set up logging</span><span class="sxs-lookup"><span data-stu-id="4cd75-251">Set up logging</span></span>
<span data-ttu-id="4cd75-252">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span><span class="sxs-lookup"><span data-stu-id="4cd75-252">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="4cd75-253">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span><span class="sxs-lookup"><span data-stu-id="4cd75-253">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="4cd75-254">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span><span class="sxs-lookup"><span data-stu-id="4cd75-254">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="4cd75-255">*Only* use this for local development and debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="4cd75-255">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="4cd75-256">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span><span class="sxs-lookup"><span data-stu-id="4cd75-256">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="4cd75-257">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-257">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="4cd75-258">`FileRetentionCount` determines how many files are saved in the working directory.</span><span class="sxs-lookup"><span data-stu-id="4cd75-258">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="4cd75-259">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span><span class="sxs-lookup"><span data-stu-id="4cd75-259">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="4cd75-260">`FileMaxSizeInKb` specifies the maximum size of the log files.</span><span class="sxs-lookup"><span data-stu-id="4cd75-260">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="4cd75-261">Log files are saved in one of the service's working directories.</span><span class="sxs-lookup"><span data-stu-id="4cd75-261">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="4cd75-262">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span><span class="sxs-lookup"><span data-stu-id="4cd75-262">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="4cd75-263">This process is covered later in this article.</span><span class="sxs-lookup"><span data-stu-id="4cd75-263">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="4cd75-264">Deployment</span><span class="sxs-lookup"><span data-stu-id="4cd75-264">Deployment</span></span>
<span data-ttu-id="4cd75-265">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4cd75-265">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="4cd75-266">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span><span class="sxs-lookup"><span data-stu-id="4cd75-266">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="4cd75-267">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span><span class="sxs-lookup"><span data-stu-id="4cd75-267">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="4cd75-268">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="4cd75-268">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="4cd75-269">A Service Fabric service can be deployed in various "configurations."</span><span class="sxs-lookup"><span data-stu-id="4cd75-269">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="4cd75-270">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-270">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="4cd75-271">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-271">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="4cd75-272">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span><span class="sxs-lookup"><span data-stu-id="4cd75-272">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="4cd75-273">The two most common scenarios are:</span><span class="sxs-lookup"><span data-stu-id="4cd75-273">The two most common scenarios are:</span></span>

* <span data-ttu-id="4cd75-274">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-274">`InstanceCount = "1"`.</span></span> <span data-ttu-id="4cd75-275">In this case, only one instance of the service is deployed in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-275">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="4cd75-276">Service Fabric's scheduler determines which node the service is going to be deployed on.</span><span class="sxs-lookup"><span data-stu-id="4cd75-276">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="4cd75-277">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-277">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="4cd75-278">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-278">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="4cd75-279">The result is having one (and only one) instance of the service for each node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-279">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="4cd75-280">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span><span class="sxs-lookup"><span data-stu-id="4cd75-280">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="4cd75-281">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span><span class="sxs-lookup"><span data-stu-id="4cd75-281">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="4cd75-282">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="4cd75-282">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="4cd75-283">Check your running application</span><span class="sxs-lookup"><span data-stu-id="4cd75-283">Check your running application</span></span>
<span data-ttu-id="4cd75-284">In Service Fabric Explorer, identify the node where the service is running.</span><span class="sxs-lookup"><span data-stu-id="4cd75-284">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="4cd75-285">In this example, it runs on Node1:</span><span class="sxs-lookup"><span data-stu-id="4cd75-285">In this example, it runs on Node1:</span></span>

![Node where service is running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="4cd75-287">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span><span class="sxs-lookup"><span data-stu-id="4cd75-287">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![Location on disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="4cd75-289">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="4cd75-289">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot.</span></span>

![Location of log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="creating-a-guest-executable-using-yeoman-for-service-fabric-on-linux"></a><span data-ttu-id="4cd75-291">Creating a guest executable using Yeoman for Service Fabric on Linux</span><span class="sxs-lookup"><span data-stu-id="4cd75-291">Creating a guest executable using Yeoman for Service Fabric on Linux</span></span>

<span data-ttu-id="4cd75-292">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span><span class="sxs-lookup"><span data-stu-id="4cd75-292">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span> 

1. <span data-ttu-id="4cd75-293">In a terminal, type `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="4cd75-293">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="4cd75-294">Name your application.</span><span class="sxs-lookup"><span data-stu-id="4cd75-294">Name your application.</span></span>
3. <span data-ttu-id="4cd75-295">Choose the type of your first service and name it.</span><span class="sxs-lookup"><span data-stu-id="4cd75-295">Choose the type of your first service and name it.</span></span> <span data-ttu-id="4cd75-296">Choose **Guest Binary** for a guest executable (and **Guest Container** for a container), and provide the details including path of the executable and the parameters it must be invoked with.</span><span class="sxs-lookup"><span data-stu-id="4cd75-296">Choose **Guest Binary** for a guest executable (and **Guest Container** for a container), and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="4cd75-297">Yeoman would have created an application package with the appropriate application and manifest files along with install and uninstall scripts.</span><span class="sxs-lookup"><span data-stu-id="4cd75-297">Yeoman would have created an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cd75-298">Next steps</span><span class="sxs-lookup"><span data-stu-id="4cd75-298">Next steps</span></span>
<span data-ttu-id="4cd75-299">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4cd75-299">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="4cd75-300">See the following articles for related information and tasks.</span><span class="sxs-lookup"><span data-stu-id="4cd75-300">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="4cd75-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span><span class="sxs-lookup"><span data-stu-id="4cd75-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="4cd75-302">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span><span class="sxs-lookup"><span data-stu-id="4cd75-302">Sample of two guest exectuables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="4cd75-303">Deploy multiple guest executables</span><span class="sxs-lookup"><span data-stu-id="4cd75-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="4cd75-304">Create your first Service Fabric application using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4cd75-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)




