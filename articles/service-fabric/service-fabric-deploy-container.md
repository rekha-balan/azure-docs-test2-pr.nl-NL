---
title: Service Fabric and deploying containers | Microsoft Docs
description: Service Fabric and the use of containers to deploy microservice applications. This article describes the capabilities that Service Fabric provides for containers and how to deploy a Windows container image into a cluster.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/17/2017
ms.author: msfussell
ms.openlocfilehash: 97b0cb7a5f04f2c5c547cb4b70d87273aa8f2383
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552601"
---
# <a name="preview-deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="2b08b-104">Preview: Deploy a Windows container to Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2b08b-104">Preview: Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [Deploy Windows Container](service-fabric-deploy-container.md)
> * [Deploy Docker Container](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="2b08b-107">This article walks you through the process of building containerized services in Windows containers.</span><span class="sxs-lookup"><span data-stu-id="2b08b-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

> [!NOTE]
> This feature is in preview for Windows Server 2016.
>  

<span data-ttu-id="2b08b-109">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span><span class="sxs-lookup"><span data-stu-id="2b08b-109">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> 

<span data-ttu-id="2b08b-110">The capabilities include:</span><span class="sxs-lookup"><span data-stu-id="2b08b-110">The capabilities include:</span></span>

* <span data-ttu-id="2b08b-111">Container image deployment and activation</span><span class="sxs-lookup"><span data-stu-id="2b08b-111">Container image deployment and activation</span></span>
* <span data-ttu-id="2b08b-112">Resource governance</span><span class="sxs-lookup"><span data-stu-id="2b08b-112">Resource governance</span></span>
* <span data-ttu-id="2b08b-113">Repository authentication</span><span class="sxs-lookup"><span data-stu-id="2b08b-113">Repository authentication</span></span>
* <span data-ttu-id="2b08b-114">Container port-to-host port mapping</span><span class="sxs-lookup"><span data-stu-id="2b08b-114">Container port-to-host port mapping</span></span>
* <span data-ttu-id="2b08b-115">Container-to-container discovery and communication</span><span class="sxs-lookup"><span data-stu-id="2b08b-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="2b08b-116">Ability to configure and set environment variables</span><span class="sxs-lookup"><span data-stu-id="2b08b-116">Ability to configure and set environment variables</span></span>

<span data-ttu-id="2b08b-117">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span><span class="sxs-lookup"><span data-stu-id="2b08b-117">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="2b08b-118">Package a Windows container</span><span class="sxs-lookup"><span data-stu-id="2b08b-118">Package a Windows container</span></span>
<span data-ttu-id="2b08b-119">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span><span class="sxs-lookup"><span data-stu-id="2b08b-119">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="2b08b-120">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span><span class="sxs-lookup"><span data-stu-id="2b08b-120">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> The easiest way to package an existing container image into a service is to use Visual Studio.

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="2b08b-122">Use Visual Studio to package an existing container image</span><span class="sxs-lookup"><span data-stu-id="2b08b-122">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="2b08b-123">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="2b08b-123">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="2b08b-124">Choose **File** > **New Project**, and create a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="2b08b-124">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="2b08b-125">Choose **Guest Container** as the service template.</span><span class="sxs-lookup"><span data-stu-id="2b08b-125">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="2b08b-126">Choose **Image Name** and provide the path to the image in your container repository such as at https://hub.docker.com/ for example myrepo/myimage:v1</span><span class="sxs-lookup"><span data-stu-id="2b08b-126">Choose **Image Name** and provide the path to the image in your container repository such as at https://hub.docker.com/ for example myrepo/myimage:v1</span></span> 
4. <span data-ttu-id="2b08b-127">Give your service a name, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b08b-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="2b08b-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span><span class="sxs-lookup"><span data-stu-id="2b08b-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="2b08b-129">For example:</span><span class="sxs-lookup"><span data-stu-id="2b08b-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="2b08b-130">By providing the `UriScheme` this automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span><span class="sxs-lookup"><span data-stu-id="2b08b-130">By providing the `UriScheme` this automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="2b08b-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated (left blank and a port is allocated from the designated application port range) just as you would with any service.</span><span class="sxs-lookup"><span data-stu-id="2b08b-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated (left blank and a port is allocated from the designated application port range) just as you would with any service.</span></span>
    <span data-ttu-id="2b08b-132">You also need to configure the container port-to-host port mapping by specifying a `PortBinding` policy in the application manifest as described below.</span><span class="sxs-lookup"><span data-stu-id="2b08b-132">You also need to configure the container port-to-host port mapping by specifying a `PortBinding` policy in the application manifest as described below.</span></span>
6. <span data-ttu-id="2b08b-133">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="2b08b-133">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="2b08b-134">If your container needs to authenticate with a private repository then add `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="2b08b-134">If your container needs to authenticate with a private repository then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="2b08b-135">You can now use the package and publish action against your local cluster if this is Windows Server 2016 with container support activated.</span><span class="sxs-lookup"><span data-stu-id="2b08b-135">You can now use the package and publish action against your local cluster if this is Windows Server 2016 with container support activated.</span></span> 
8. <span data-ttu-id="2b08b-136">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span><span class="sxs-lookup"><span data-stu-id="2b08b-136">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="2b08b-137">For an example application [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="2b08b-137">For an example application [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="2b08b-138">Creating a Windows Server 2016 cluster</span><span class="sxs-lookup"><span data-stu-id="2b08b-138">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="2b08b-139">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span><span class="sxs-lookup"><span data-stu-id="2b08b-139">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="2b08b-140">This can either be on your local development machine or deployed via Azure Resource Manager (ARM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b08b-140">This can either be on your local development machine or deployed via Azure Resource Manager (ARM) in Azure.</span></span> 

<span data-ttu-id="2b08b-141">To deploy a cluster using ARM, choose the **Windows Server 2016 with Containers** image option in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b08b-141">To deploy a cluster using ARM, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="2b08b-142">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2b08b-142">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="2b08b-143">Ensure that you use the following ARM settings:</span><span class="sxs-lookup"><span data-stu-id="2b08b-143">Ensure that you use the following ARM settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="2b08b-144">You can also use the [5 Node ARM template here](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="2b08b-144">You can also use the [5 Node ARM template here](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="2b08b-145">Alternatively read [Leok's blog post here](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span><span class="sxs-lookup"><span data-stu-id="2b08b-145">Alternatively read [Leok's blog post here](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="2b08b-146">Manually package and deploy a container image</span><span class="sxs-lookup"><span data-stu-id="2b08b-146">Manually package and deploy a container image</span></span>
<span data-ttu-id="2b08b-147">The process of manually packaging a containerized service is based on the following steps:</span><span class="sxs-lookup"><span data-stu-id="2b08b-147">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="2b08b-148">Publish the containers to your repository.</span><span class="sxs-lookup"><span data-stu-id="2b08b-148">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="2b08b-149">Create the package directory structure.</span><span class="sxs-lookup"><span data-stu-id="2b08b-149">Create the package directory structure.</span></span>
3. <span data-ttu-id="2b08b-150">Edit the service manifest file.</span><span class="sxs-lookup"><span data-stu-id="2b08b-150">Edit the service manifest file.</span></span>
4. <span data-ttu-id="2b08b-151">Edit the application manifest file.</span><span class="sxs-lookup"><span data-stu-id="2b08b-151">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="2b08b-152">Deploy and activate a container image</span><span class="sxs-lookup"><span data-stu-id="2b08b-152">Deploy and activate a container image</span></span>
<span data-ttu-id="2b08b-153">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span><span class="sxs-lookup"><span data-stu-id="2b08b-153">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="2b08b-154">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span><span class="sxs-lookup"><span data-stu-id="2b08b-154">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="2b08b-155">In the service manifest, add a `ContainerHost` for the entry point.</span><span class="sxs-lookup"><span data-stu-id="2b08b-155">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="2b08b-156">Then set the `ImageName` to be the name of the container repository and image.</span><span class="sxs-lookup"><span data-stu-id="2b08b-156">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="2b08b-157">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="2b08b-157">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="2b08b-158">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span><span class="sxs-lookup"><span data-stu-id="2b08b-158">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="2b08b-159">Understand resource governance</span><span class="sxs-lookup"><span data-stu-id="2b08b-159">Understand resource governance</span></span>
<span data-ttu-id="2b08b-160">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span><span class="sxs-lookup"><span data-stu-id="2b08b-160">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="2b08b-161">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span><span class="sxs-lookup"><span data-stu-id="2b08b-161">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="2b08b-162">Resource limits can be set for the following resources:</span><span class="sxs-lookup"><span data-stu-id="2b08b-162">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="2b08b-163">Memory</span><span class="sxs-lookup"><span data-stu-id="2b08b-163">Memory</span></span>
* <span data-ttu-id="2b08b-164">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="2b08b-164">MemorySwap</span></span>
* <span data-ttu-id="2b08b-165">CpuShares (CPU relative weight)</span><span class="sxs-lookup"><span data-stu-id="2b08b-165">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="2b08b-166">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="2b08b-166">MemoryReservationInMB</span></span>  
* <span data-ttu-id="2b08b-167">BlkioWeight (BlockIO relative weight).</span><span class="sxs-lookup"><span data-stu-id="2b08b-167">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="2b08b-169">Authenticate a repository</span><span class="sxs-lookup"><span data-stu-id="2b08b-169">Authenticate a repository</span></span>
<span data-ttu-id="2b08b-170">To download a container, you might have to provide sign-in credentials to the container repository.</span><span class="sxs-lookup"><span data-stu-id="2b08b-170">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="2b08b-171">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span><span class="sxs-lookup"><span data-stu-id="2b08b-171">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="2b08b-172">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span><span class="sxs-lookup"><span data-stu-id="2b08b-172">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="2b08b-173">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span><span class="sxs-lookup"><span data-stu-id="2b08b-173">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="2b08b-174">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="2b08b-174">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="2b08b-175">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span><span class="sxs-lookup"><span data-stu-id="2b08b-175">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="2b08b-176">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="2b08b-176">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="2b08b-177">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span><span class="sxs-lookup"><span data-stu-id="2b08b-177">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="2b08b-178">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span><span class="sxs-lookup"><span data-stu-id="2b08b-178">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="2b08b-179">By using the secret along with the account name, it can then authenticate with the container repository.</span><span class="sxs-lookup"><span data-stu-id="2b08b-179">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="2b08b-180">Configure container port-to-host port mapping</span><span class="sxs-lookup"><span data-stu-id="2b08b-180">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="2b08b-181">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="2b08b-181">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="2b08b-182">The port binding maps the port to which the service is listening inside the container to a port on the host.</span><span class="sxs-lookup"><span data-stu-id="2b08b-182">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="2b08b-183">Configure container-to-container discovery and communication</span><span class="sxs-lookup"><span data-stu-id="2b08b-183">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="2b08b-184">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="2b08b-184">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest as shown in the following example.</span></span> <span data-ttu-id="2b08b-185">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span><span class="sxs-lookup"><span data-stu-id="2b08b-185">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="2b08b-186">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span><span class="sxs-lookup"><span data-stu-id="2b08b-186">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="2b08b-187">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span><span class="sxs-lookup"><span data-stu-id="2b08b-187">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="2b08b-188">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span><span class="sxs-lookup"><span data-stu-id="2b08b-188">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="2b08b-189">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="2b08b-189">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="2b08b-190">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span><span class="sxs-lookup"><span data-stu-id="2b08b-190">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="2b08b-191">For more information, see the next section.</span><span class="sxs-lookup"><span data-stu-id="2b08b-191">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="2b08b-192">Configure and set environment variables</span><span class="sxs-lookup"><span data-stu-id="2b08b-192">Configure and set environment variables</span></span>
<span data-ttu-id="2b08b-193">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span><span class="sxs-lookup"><span data-stu-id="2b08b-193">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="2b08b-194">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span><span class="sxs-lookup"><span data-stu-id="2b08b-194">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="2b08b-195">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span><span class="sxs-lookup"><span data-stu-id="2b08b-195">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="2b08b-196">These environment variables can be overridden at the application manifest level:</span><span class="sxs-lookup"><span data-stu-id="2b08b-196">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="2b08b-197">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span><span class="sxs-lookup"><span data-stu-id="2b08b-197">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="2b08b-198">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span><span class="sxs-lookup"><span data-stu-id="2b08b-198">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="2b08b-199">Complete examples for application and service manifest</span><span class="sxs-lookup"><span data-stu-id="2b08b-199">Complete examples for application and service manifest</span></span>

<span data-ttu-id="2b08b-200">An example application manifest follows:</span><span class="sxs-lookup"><span data-stu-id="2b08b-200">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="2b08b-201">An example service manifest (specified in the preceding application manifest) follows:</span><span class="sxs-lookup"><span data-stu-id="2b08b-201">An example service manifest (specified in the preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="2b08b-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b08b-202">Next steps</span></span>
<span data-ttu-id="2b08b-203">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="2b08b-203">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="2b08b-204">Overview of Service Fabric and containers</span><span class="sxs-lookup"><span data-stu-id="2b08b-204">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="2b08b-205">For an example application [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="2b08b-205">For an example application [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
