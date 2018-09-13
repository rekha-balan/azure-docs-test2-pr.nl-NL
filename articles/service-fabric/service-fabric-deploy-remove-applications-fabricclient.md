---
title: Azure Service Fabric application deployment | Microsoft Docs
description: Use the FabricClient APIs to deploy and remove applications in Service Fabric.
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
ms.date: 04/10/2017
ms.author: ryanwi
ms.openlocfilehash: 4c7a92352d4fef6a0e55b608bf5c957cd2c40332
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661179"
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="4916c-103">Deploy and remove applications using FabricClient</span><span class="sxs-lookup"><span data-stu-id="4916c-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient APIs](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="4916c-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="4916c-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="4916c-108">Deployment involves the following three steps:</span><span class="sxs-lookup"><span data-stu-id="4916c-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="4916c-109">Upload the application package to the image store</span><span class="sxs-lookup"><span data-stu-id="4916c-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="4916c-110">Register the application type</span><span class="sxs-lookup"><span data-stu-id="4916c-110">Register the application type</span></span>
3. <span data-ttu-id="4916c-111">Create the application instance</span><span class="sxs-lookup"><span data-stu-id="4916c-111">Create the application instance</span></span>

<span data-ttu-id="4916c-112">After an app is deployed and an instance is running in the cluster, you can delete the app instance and its application type.</span><span class="sxs-lookup"><span data-stu-id="4916c-112">After an app is deployed and an instance is running in the cluster, you can delete the app instance and its application type.</span></span> <span data-ttu-id="4916c-113">To completely remove an app from the cluster involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="4916c-113">To completely remove an app from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="4916c-114">Remove (or delete) the running application instance</span><span class="sxs-lookup"><span data-stu-id="4916c-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="4916c-115">Unregister the application type if you no longer need it</span><span class="sxs-lookup"><span data-stu-id="4916c-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="4916c-116">Remove the application package from the image store</span><span class="sxs-lookup"><span data-stu-id="4916c-116">Remove the application package from the image store</span></span>

<span data-ttu-id="4916c-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="4916c-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="4916c-118">This script is found in the *Scripts* folder of the application project.</span><span class="sxs-lookup"><span data-stu-id="4916c-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="4916c-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4916c-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="4916c-120">Connect to the cluster</span><span class="sxs-lookup"><span data-stu-id="4916c-120">Connect to the cluster</span></span>
<span data-ttu-id="4916c-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span><span class="sxs-lookup"><span data-stu-id="4916c-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="4916c-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="4916c-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span>  <span data-ttu-id="4916c-123">To connect to the local development cluster, run the following:</span><span class="sxs-lookup"><span data-stu-id="4916c-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="4916c-124">Upload the application package</span><span class="sxs-lookup"><span data-stu-id="4916c-124">Upload the application package</span></span>
<span data-ttu-id="4916c-125">Suppose you build and package an app named *MyApplication* in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4916c-125">Suppose you build and package an app named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="4916c-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="4916c-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="4916c-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="4916c-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="4916c-128">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span><span class="sxs-lookup"><span data-stu-id="4916c-128">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="4916c-129">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4916c-129">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet.</span></span>

<span data-ttu-id="4916c-130">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method uploads the application package to the cluster image store.</span><span class="sxs-lookup"><span data-stu-id="4916c-130">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="4916c-131">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the imagestore using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4916c-131">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the imagestore using PowerShell.</span></span> <span data-ttu-id="4916c-132">The compression reduces the size and the number of files.</span><span class="sxs-lookup"><span data-stu-id="4916c-132">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="4916c-133">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span><span class="sxs-lookup"><span data-stu-id="4916c-133">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="4916c-134">Register the application package</span><span class="sxs-lookup"><span data-stu-id="4916c-134">Register the application package</span></span>
<span data-ttu-id="4916c-135">The application type and version declared in the application manifest become available for use when the app package is registered.</span><span class="sxs-lookup"><span data-stu-id="4916c-135">The application type and version declared in the application manifest become available for use when the app package is registered.</span></span> <span data-ttu-id="4916c-136">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span><span class="sxs-lookup"><span data-stu-id="4916c-136">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="4916c-137">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method registers the application type in the cluster and make it available for deployment.</span><span class="sxs-lookup"><span data-stu-id="4916c-137">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="4916c-138">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) method lists all successfully registered application type versions and their registration status.</span><span class="sxs-lookup"><span data-stu-id="4916c-138">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) method lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4916c-139">You can use this command to determine when the registration is done.</span><span class="sxs-lookup"><span data-stu-id="4916c-139">You can use this command to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="4916c-140">Create an application instance</span><span class="sxs-lookup"><span data-stu-id="4916c-140">Create an application instance</span></span>
<span data-ttu-id="4916c-141">You can instantiate an application from any application type version that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-141">You can instantiate an application from any application type version that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) method.</span></span> <span data-ttu-id="4916c-142">The name of each application must start with the *fabric:* scheme and be unique for each application instance.</span><span class="sxs-lookup"><span data-stu-id="4916c-142">The name of each application must start with the *fabric:* scheme and be unique for each application instance.</span></span> <span data-ttu-id="4916c-143">Any default services defined in the application manifest of the target application type are also created.</span><span class="sxs-lookup"><span data-stu-id="4916c-143">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="4916c-144">Multiple application instances can be created for any given version of a registered application type.</span><span class="sxs-lookup"><span data-stu-id="4916c-144">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="4916c-145">Each application instance runs in isolation, with its own work directory and process.</span><span class="sxs-lookup"><span data-stu-id="4916c-145">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="4916c-146">To see which named apps and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) methods.</span><span class="sxs-lookup"><span data-stu-id="4916c-146">To see which named apps and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) methods.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="4916c-147">Create a service instance</span><span class="sxs-lookup"><span data-stu-id="4916c-147">Create a service instance</span></span>
<span data-ttu-id="4916c-148">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-148">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) method.</span></span>  <span data-ttu-id="4916c-149">If the service is declared as a default service in the application manifest, the service is instantiated with the application is instantiated.</span><span class="sxs-lookup"><span data-stu-id="4916c-149">If the service is declared as a default service in the application manifest, the service is instantiated with the application is instantiated.</span></span>  <span data-ttu-id="4916c-150">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) method for a service that is already instantiated will return an exception.</span><span class="sxs-lookup"><span data-stu-id="4916c-150">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) method for a service that is already instantiated will return an exception.</span></span> 

## <a name="remove-a-service-instance"></a><span data-ttu-id="4916c-151">Remove a service instance</span><span class="sxs-lookup"><span data-stu-id="4916c-151">Remove a service instance</span></span>
<span data-ttu-id="4916c-152">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-152">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) method.</span></span>  <span data-ttu-id="4916c-153">This operation cannot be reversed, and service state cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="4916c-153">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="4916c-154">Remove an application instance</span><span class="sxs-lookup"><span data-stu-id="4916c-154">Remove an application instance</span></span>
<span data-ttu-id="4916c-155">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-155">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) method.</span></span> <span data-ttu-id="4916c-156">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span><span class="sxs-lookup"><span data-stu-id="4916c-156">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> <span data-ttu-id="4916c-157">This operation cannot be reversed, and application state cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="4916c-157">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="4916c-158">Unregister an application type</span><span class="sxs-lookup"><span data-stu-id="4916c-158">Unregister an application type</span></span>
<span data-ttu-id="4916c-159">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-159">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) method.</span></span> <span data-ttu-id="4916c-160">Unregistering unused application types releases storage space used by the image store.</span><span class="sxs-lookup"><span data-stu-id="4916c-160">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="4916c-161">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span><span class="sxs-lookup"><span data-stu-id="4916c-161">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="4916c-162">Remove an application package from the image store</span><span class="sxs-lookup"><span data-stu-id="4916c-162">Remove an application package from the image store</span></span>
<span data-ttu-id="4916c-163">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-163">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) method.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4916c-164">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="4916c-164">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="4916c-165">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="4916c-165">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="4916c-166">The Service Fabric SDK environment should already have the correct defaults set up.</span><span class="sxs-lookup"><span data-stu-id="4916c-166">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="4916c-167">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span><span class="sxs-lookup"><span data-stu-id="4916c-167">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="4916c-168">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/dotnet/api/system.fabric.fabricclient.clustermanagementclient.getclustermanifestasync) method.</span><span class="sxs-lookup"><span data-stu-id="4916c-168">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/dotnet/api/system.fabric.fabricclient.clustermanagementclient.getclustermanifestasync) method.</span></span>

<span data-ttu-id="4916c-169">The ImageStoreConnectionString is found in the cluster manifest:</span><span class="sxs-lookup"><span data-stu-id="4916c-169">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="4916c-170">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span><span class="sxs-lookup"><span data-stu-id="4916c-170">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="4916c-171">Deploy large application package</span><span class="sxs-lookup"><span data-stu-id="4916c-171">Deploy large application package</span></span>
<span data-ttu-id="4916c-172">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method times out for a large application package (order of GB).</span><span class="sxs-lookup"><span data-stu-id="4916c-172">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method times out for a large application package (order of GB).</span></span>
<span data-ttu-id="4916c-173">Try:</span><span class="sxs-lookup"><span data-stu-id="4916c-173">Try:</span></span>
- <span data-ttu-id="4916c-174">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span><span class="sxs-lookup"><span data-stu-id="4916c-174">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="4916c-175">By default, the timeout is 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="4916c-175">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="4916c-176">Check the network connection between your source machine and cluster.</span><span class="sxs-lookup"><span data-stu-id="4916c-176">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="4916c-177">If the connection is slow, consider using a machine with a better network connection.</span><span class="sxs-lookup"><span data-stu-id="4916c-177">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="4916c-178">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span><span class="sxs-lookup"><span data-stu-id="4916c-178">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="4916c-179">Check if you are hitting external throttling.</span><span class="sxs-lookup"><span data-stu-id="4916c-179">Check if you are hitting external throttling.</span></span> <span data-ttu-id="4916c-180">For example, when the image store is configured to use azure storage, upload may be throttled.</span><span class="sxs-lookup"><span data-stu-id="4916c-180">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="4916c-181">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method times out. Try:</span><span class="sxs-lookup"><span data-stu-id="4916c-181">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method times out. Try:</span></span>
- <span data-ttu-id="4916c-182">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span><span class="sxs-lookup"><span data-stu-id="4916c-182">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="4916c-183">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span><span class="sxs-lookup"><span data-stu-id="4916c-183">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="4916c-184">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span><span class="sxs-lookup"><span data-stu-id="4916c-184">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="4916c-185">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method with `timeout` parameter.</span><span class="sxs-lookup"><span data-stu-id="4916c-185">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) method with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="4916c-186">Deploy application package with many files</span><span class="sxs-lookup"><span data-stu-id="4916c-186">Deploy application package with many files</span></span>
<span data-ttu-id="4916c-187">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span><span class="sxs-lookup"><span data-stu-id="4916c-187">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="4916c-188">Try:</span><span class="sxs-lookup"><span data-stu-id="4916c-188">Try:</span></span>
- <span data-ttu-id="4916c-189">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span><span class="sxs-lookup"><span data-stu-id="4916c-189">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="4916c-190">The compression reduces the number of files.</span><span class="sxs-lookup"><span data-stu-id="4916c-190">The compression reduces the number of files.</span></span>
- <span data-ttu-id="4916c-191">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span><span class="sxs-lookup"><span data-stu-id="4916c-191">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="4916c-192">Code example</span><span class="sxs-lookup"><span data-stu-id="4916c-192">Code example</span></span>
<span data-ttu-id="4916c-193">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span><span class="sxs-lookup"><span data-stu-id="4916c-193">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\Users\username\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug";
    string serviceType = "Stateless1Type";

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the app package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create the application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from the application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision the application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete the application package from a location in the image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="4916c-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="4916c-194">Next steps</span></span>
[<span data-ttu-id="4916c-195">Service Fabric application upgrade</span><span class="sxs-lookup"><span data-stu-id="4916c-195">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="4916c-196">Service Fabric health introduction</span><span class="sxs-lookup"><span data-stu-id="4916c-196">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="4916c-197">Diagnose and troubleshoot a Service Fabric service</span><span class="sxs-lookup"><span data-stu-id="4916c-197">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="4916c-198">Model an application in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4916c-198">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
