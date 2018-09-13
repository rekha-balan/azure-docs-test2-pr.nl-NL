---
title: Service Fabric and Deploying Containers in Linux | Microsoft Docs
description: Service Fabric and the use of Docker containers to deploy microservice applications. This article describes the capabilities that Service Fabric provides for containers and how to deploy a Docker container image into a cluster
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: ''
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 3/24/2017
ms.author: msfussell
ms.openlocfilehash: 149070274ef7da698f6629b87316b4592431eeb3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556475"
---
# <a name="deploy-a-docker-container-to-service-fabric"></a><span data-ttu-id="93bc6-104">Deploy a Docker container to Service Fabric</span><span class="sxs-lookup"><span data-stu-id="93bc6-104">Deploy a Docker container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [Deploy Windows Container](service-fabric-deploy-container.md)
> * [Deploy Docker Container](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="93bc6-107">This article walks you through building containerized services in Docker containers on Linux.</span><span class="sxs-lookup"><span data-stu-id="93bc6-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="93bc6-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span><span class="sxs-lookup"><span data-stu-id="93bc6-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="93bc6-109">These services are called containerized services.</span><span class="sxs-lookup"><span data-stu-id="93bc6-109">These services are called containerized services.</span></span>

<span data-ttu-id="93bc6-110">The capabilities include;</span><span class="sxs-lookup"><span data-stu-id="93bc6-110">The capabilities include;</span></span>

* <span data-ttu-id="93bc6-111">Container image deployment and activation</span><span class="sxs-lookup"><span data-stu-id="93bc6-111">Container image deployment and activation</span></span>
* <span data-ttu-id="93bc6-112">Resource governance</span><span class="sxs-lookup"><span data-stu-id="93bc6-112">Resource governance</span></span>
* <span data-ttu-id="93bc6-113">Repository authentication</span><span class="sxs-lookup"><span data-stu-id="93bc6-113">Repository authentication</span></span>
* <span data-ttu-id="93bc6-114">Container port to host port mapping</span><span class="sxs-lookup"><span data-stu-id="93bc6-114">Container port to host port mapping</span></span>
* <span data-ttu-id="93bc6-115">Container-to-container discovery and communication</span><span class="sxs-lookup"><span data-stu-id="93bc6-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="93bc6-116">Ability to configure and set environment variables</span><span class="sxs-lookup"><span data-stu-id="93bc6-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="93bc6-117">Packaging a docker container with yeoman</span><span class="sxs-lookup"><span data-stu-id="93bc6-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="93bc6-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span><span class="sxs-lookup"><span data-stu-id="93bc6-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="93bc6-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="93bc6-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="93bc6-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span><span class="sxs-lookup"><span data-stu-id="93bc6-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="93bc6-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="93bc6-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="93bc6-122">You can add more services later by editing the generated manifest files.</span><span class="sxs-lookup"><span data-stu-id="93bc6-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="93bc6-123">Install Docker on your development box</span><span class="sxs-lookup"><span data-stu-id="93bc6-123">Install Docker on your development box</span></span>

<span data-ttu-id="93bc6-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span><span class="sxs-lookup"><span data-stu-id="93bc6-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="93bc6-125">Create the application</span><span class="sxs-lookup"><span data-stu-id="93bc6-125">Create the application</span></span>
1. <span data-ttu-id="93bc6-126">In a terminal, type `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="93bc6-126">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="93bc6-127">For the framework, choose **Container**.</span><span class="sxs-lookup"><span data-stu-id="93bc6-127">For the framework, choose **Container**.</span></span>
3. <span data-ttu-id="93bc6-128">Name your application - for example, SimpleContainerApp</span><span class="sxs-lookup"><span data-stu-id="93bc6-128">Name your application - for example, SimpleContainerApp</span></span>
4. <span data-ttu-id="93bc6-129">Provide the URL for the container image from a DockerHub repo.</span><span class="sxs-lookup"><span data-stu-id="93bc6-129">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="93bc6-130">The image parameter takes the form [repo]/[image name]</span><span class="sxs-lookup"><span data-stu-id="93bc6-130">The image parameter takes the form [repo]/[image name]</span></span>

![Service Fabric Yeoman generator for containers][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="93bc6-132">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="93bc6-132">Deploy the application</span></span>
<span data-ttu-id="93bc6-133">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="93bc6-133">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="93bc6-134">Connect to the local Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="93bc6-134">Connect to the local Service Fabric cluster.</span></span>

```bash
    azure servicefabric cluster connect
```

2. <span data-ttu-id="93bc6-135">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="93bc6-135">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

```bash
    ./install.sh
```

3. <span data-ttu-id="93bc6-136">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="93bc6-136">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="93bc6-137">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span><span class="sxs-lookup"><span data-stu-id="93bc6-137">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="93bc6-138">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span><span class="sxs-lookup"><span data-stu-id="93bc6-138">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

```bash
    ./uninstall.sh
```

<span data-ttu-id="93bc6-139">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="93bc6-139">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="93bc6-140">Adding more services to an existing application</span><span class="sxs-lookup"><span data-stu-id="93bc6-140">Adding more services to an existing application</span></span>

<span data-ttu-id="93bc6-141">To add another container service to an application already created using `yo`, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="93bc6-141">To add another container service to an application already created using `yo`, perform the following steps:</span></span> 

1. <span data-ttu-id="93bc6-142">Change directory to the root of the existing application.</span><span class="sxs-lookup"><span data-stu-id="93bc6-142">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="93bc6-143">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span><span class="sxs-lookup"><span data-stu-id="93bc6-143">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="93bc6-144">Run `yo azuresfguest:AddService`</span><span class="sxs-lookup"><span data-stu-id="93bc6-144">Run `yo azuresfguest:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="93bc6-145">Manually package and deploy a container image</span><span class="sxs-lookup"><span data-stu-id="93bc6-145">Manually package and deploy a container image</span></span>
<span data-ttu-id="93bc6-146">The process of manually packaging a containerized service is based on the following steps:</span><span class="sxs-lookup"><span data-stu-id="93bc6-146">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="93bc6-147">Publish the containers to your repository.</span><span class="sxs-lookup"><span data-stu-id="93bc6-147">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="93bc6-148">Create the package directory structure.</span><span class="sxs-lookup"><span data-stu-id="93bc6-148">Create the package directory structure.</span></span>
3. <span data-ttu-id="93bc6-149">Edit the service manifest file.</span><span class="sxs-lookup"><span data-stu-id="93bc6-149">Edit the service manifest file.</span></span>
4. <span data-ttu-id="93bc6-150">Edit the application manifest file.</span><span class="sxs-lookup"><span data-stu-id="93bc6-150">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="93bc6-151">Deploy and activate a container image</span><span class="sxs-lookup"><span data-stu-id="93bc6-151">Deploy and activate a container image</span></span>
<span data-ttu-id="93bc6-152">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span><span class="sxs-lookup"><span data-stu-id="93bc6-152">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="93bc6-153">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span><span class="sxs-lookup"><span data-stu-id="93bc6-153">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="93bc6-154">In the service manifest, add a `ContainerHost` for the entry point.</span><span class="sxs-lookup"><span data-stu-id="93bc6-154">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="93bc6-155">Then set the `ImageName` to be the name of the container repository and image.</span><span class="sxs-lookup"><span data-stu-id="93bc6-155">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="93bc6-156">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="93bc6-156">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="93bc6-157">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span><span class="sxs-lookup"><span data-stu-id="93bc6-157">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="93bc6-158">Understand resource governance</span><span class="sxs-lookup"><span data-stu-id="93bc6-158">Understand resource governance</span></span>
<span data-ttu-id="93bc6-159">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span><span class="sxs-lookup"><span data-stu-id="93bc6-159">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="93bc6-160">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span><span class="sxs-lookup"><span data-stu-id="93bc6-160">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="93bc6-161">Resource limits can be set for the following resources:</span><span class="sxs-lookup"><span data-stu-id="93bc6-161">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="93bc6-162">Memory</span><span class="sxs-lookup"><span data-stu-id="93bc6-162">Memory</span></span>
* <span data-ttu-id="93bc6-163">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="93bc6-163">MemorySwap</span></span>
* <span data-ttu-id="93bc6-164">CpuShares (CPU relative weight)</span><span class="sxs-lookup"><span data-stu-id="93bc6-164">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="93bc6-165">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="93bc6-165">MemoryReservationInMB</span></span>  
* <span data-ttu-id="93bc6-166">BlkioWeight (BlockIO relative weight).</span><span class="sxs-lookup"><span data-stu-id="93bc6-166">BlkioWeight (BlockIO relative weight).</span></span>

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

## <a name="authenticate-a-repository"></a><span data-ttu-id="93bc6-168">Authenticate a repository</span><span class="sxs-lookup"><span data-stu-id="93bc6-168">Authenticate a repository</span></span>
<span data-ttu-id="93bc6-169">To download a container, you might have to provide sign-in credentials to the container repository.</span><span class="sxs-lookup"><span data-stu-id="93bc6-169">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="93bc6-170">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span><span class="sxs-lookup"><span data-stu-id="93bc6-170">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="93bc6-171">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span><span class="sxs-lookup"><span data-stu-id="93bc6-171">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="93bc6-172">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span><span class="sxs-lookup"><span data-stu-id="93bc6-172">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="93bc6-173">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="93bc6-173">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="93bc6-174">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span><span class="sxs-lookup"><span data-stu-id="93bc6-174">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="93bc6-175">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="93bc6-175">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="93bc6-176">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span><span class="sxs-lookup"><span data-stu-id="93bc6-176">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="93bc6-177">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span><span class="sxs-lookup"><span data-stu-id="93bc6-177">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="93bc6-178">By using the secret along with the account name, it can then authenticate with the container repository.</span><span class="sxs-lookup"><span data-stu-id="93bc6-178">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="93bc6-179">Configure container port-to-host port mapping</span><span class="sxs-lookup"><span data-stu-id="93bc6-179">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="93bc6-180">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span><span class="sxs-lookup"><span data-stu-id="93bc6-180">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="93bc6-181">The port binding maps the port to which the service is listening inside the container to a port on the host.</span><span class="sxs-lookup"><span data-stu-id="93bc6-181">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="93bc6-182">Configure container-to-container discovery and communication</span><span class="sxs-lookup"><span data-stu-id="93bc6-182">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="93bc6-183">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span><span class="sxs-lookup"><span data-stu-id="93bc6-183">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="93bc6-184">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span><span class="sxs-lookup"><span data-stu-id="93bc6-184">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="93bc6-185">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span><span class="sxs-lookup"><span data-stu-id="93bc6-185">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="93bc6-186">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span><span class="sxs-lookup"><span data-stu-id="93bc6-186">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="93bc6-187">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span><span class="sxs-lookup"><span data-stu-id="93bc6-187">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="93bc6-188">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="93bc6-188">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="93bc6-189">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span><span class="sxs-lookup"><span data-stu-id="93bc6-189">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="93bc6-190">For more information, see the next section.</span><span class="sxs-lookup"><span data-stu-id="93bc6-190">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="93bc6-191">Configure and set environment variables</span><span class="sxs-lookup"><span data-stu-id="93bc6-191">Configure and set environment variables</span></span>
<span data-ttu-id="93bc6-192">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span><span class="sxs-lookup"><span data-stu-id="93bc6-192">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="93bc6-193">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span><span class="sxs-lookup"><span data-stu-id="93bc6-193">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="93bc6-194">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span><span class="sxs-lookup"><span data-stu-id="93bc6-194">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="93bc6-195">These environment variables can be overridden at the application manifest level:</span><span class="sxs-lookup"><span data-stu-id="93bc6-195">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="93bc6-196">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span><span class="sxs-lookup"><span data-stu-id="93bc6-196">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="93bc6-197">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span><span class="sxs-lookup"><span data-stu-id="93bc6-197">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="93bc6-198">Complete examples for application and service manifest</span><span class="sxs-lookup"><span data-stu-id="93bc6-198">Complete examples for application and service manifest</span></span>

<span data-ttu-id="93bc6-199">An example application manifest follows:</span><span class="sxs-lookup"><span data-stu-id="93bc6-199">An example application manifest follows:</span></span>

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

<span data-ttu-id="93bc6-200">An example service manifest (specified in the preceding application manifest) follows:</span><span class="sxs-lookup"><span data-stu-id="93bc6-200">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="93bc6-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="93bc6-201">Next steps</span></span>
<span data-ttu-id="93bc6-202">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="93bc6-202">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="93bc6-203">Overview of Service Fabric and containers</span><span class="sxs-lookup"><span data-stu-id="93bc6-203">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="93bc6-204">Interacting with Service Fabric clusters using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93bc6-204">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

