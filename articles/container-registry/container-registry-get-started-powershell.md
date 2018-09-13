---
title: Quickstart - Create a private Docker registry in Azure with PowerShell
description: Quickly learn to create a private Docker container registry in Azure with PowerShell.
services: container-registry
author: marsma
manager: jeconnoc
ms.service: container-registry
ms.topic: quickstart
ms.date: 05/08/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: e6c3330519692eb829803af2582b711be2fb3efe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865011"
---
# <a name="quickstart-create-an-azure-container-registry-using-powershell"></a><span data-ttu-id="70874-103">Quickstart: Create an Azure Container Registry using PowerShell</span><span class="sxs-lookup"><span data-stu-id="70874-103">Quickstart: Create an Azure Container Registry using PowerShell</span></span>

<span data-ttu-id="70874-104">Azure Container Registry is a managed, private Docker container registry service for building, storing, and serving Docker container images.</span><span class="sxs-lookup"><span data-stu-id="70874-104">Azure Container Registry is a managed, private Docker container registry service for building, storing, and serving Docker container images.</span></span> <span data-ttu-id="70874-105">In this quickstart, you learn how to create an Azure container registry using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70874-105">In this quickstart, you learn how to create an Azure container registry using PowerShell.</span></span> <span data-ttu-id="70874-106">After you create the registry, you push a container image to it, then deploy the container from your registry into Azure Container Instances (ACI).</span><span class="sxs-lookup"><span data-stu-id="70874-106">After you create the registry, you push a container image to it, then deploy the container from your registry into Azure Container Instances (ACI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70874-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="70874-107">Prerequisites</span></span>

<span data-ttu-id="70874-108">This quickstart requires Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="70874-108">This quickstart requires Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="70874-109">Run `Get-Module -ListAvailable AzureRM` to determine your installed version.</span><span class="sxs-lookup"><span data-stu-id="70874-109">Run `Get-Module -ListAvailable AzureRM` to determine your installed version.</span></span> <span data-ttu-id="70874-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="70874-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="70874-111">You must also have Docker installed locally.</span><span class="sxs-lookup"><span data-stu-id="70874-111">You must also have Docker installed locally.</span></span> <span data-ttu-id="70874-112">Docker provides packages for [macOS][docker-mac], [Windows][docker-windows], and [Linux][docker-linux] systems.</span><span class="sxs-lookup"><span data-stu-id="70874-112">Docker provides packages for [macOS][docker-mac], [Windows][docker-windows], and [Linux][docker-linux] systems.</span></span>

<span data-ttu-id="70874-113">Because the Azure Cloud Shell doesn't include all required Docker components (the `dockerd` daemon), you can't use the Cloud Shell for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="70874-113">Because the Azure Cloud Shell doesn't include all required Docker components (the `dockerd` daemon), you can't use the Cloud Shell for this quickstart.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="70874-114">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="70874-114">Sign in to Azure</span></span>

<span data-ttu-id="70874-115">Sign in to your Azure subscription with the [Connect-AzureRmAccount][Connect-AzureRmAccount] command, and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="70874-115">Sign in to your Azure subscription with the [Connect-AzureRmAccount][Connect-AzureRmAccount] command, and follow the on-screen directions.</span></span>

```powershell
Connect-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="70874-116">Create resource group</span><span class="sxs-lookup"><span data-stu-id="70874-116">Create resource group</span></span>

<span data-ttu-id="70874-117">Once you're authenticated with Azure, create a resource group with [New-AzureRmResourceGroup][New-AzureRmResourceGroup].</span><span class="sxs-lookup"><span data-stu-id="70874-117">Once you're authenticated with Azure, create a resource group with [New-AzureRmResourceGroup][New-AzureRmResourceGroup].</span></span> <span data-ttu-id="70874-118">A resource group is a logical container in which you deploy and manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="70874-118">A resource group is a logical container in which you deploy and manage your Azure resources.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-container-registry"></a><span data-ttu-id="70874-119">Create container registry</span><span class="sxs-lookup"><span data-stu-id="70874-119">Create container registry</span></span>

<span data-ttu-id="70874-120">Next, create a container registry in your new resource group with the [New-AzureRMContainerRegistry][New-AzureRMContainerRegistry] command.</span><span class="sxs-lookup"><span data-stu-id="70874-120">Next, create a container registry in your new resource group with the [New-AzureRMContainerRegistry][New-AzureRMContainerRegistry] command.</span></span>

<span data-ttu-id="70874-121">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="70874-121">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="70874-122">The following example creates a registry named "myContainerRegistry007."</span><span class="sxs-lookup"><span data-stu-id="70874-122">The following example creates a registry named "myContainerRegistry007."</span></span> <span data-ttu-id="70874-123">Replace *myContainerRegistry007* in the following command, then run it to create the registry:</span><span class="sxs-lookup"><span data-stu-id="70874-123">Replace *myContainerRegistry007* in the following command, then run it to create the registry:</span></span>

```powershell
$registry = New-AzureRMContainerRegistry -ResourceGroupName "myResourceGroup" -Name "myContainerRegistry007" -EnableAdminUser -Sku Basic
```

## <a name="log-in-to-registry"></a><span data-ttu-id="70874-124">Log in to registry</span><span class="sxs-lookup"><span data-stu-id="70874-124">Log in to registry</span></span>

<span data-ttu-id="70874-125">Before pushing and pulling container images, you must log in to your registry.</span><span class="sxs-lookup"><span data-stu-id="70874-125">Before pushing and pulling container images, you must log in to your registry.</span></span> <span data-ttu-id="70874-126">Use the [Get-AzureRmContainerRegistryCredential][Get-AzureRmContainerRegistryCredential] command to first get the admin credentials for the registry:</span><span class="sxs-lookup"><span data-stu-id="70874-126">Use the [Get-AzureRmContainerRegistryCredential][Get-AzureRmContainerRegistryCredential] command to first get the admin credentials for the registry:</span></span>

```powershell
$creds = Get-AzureRmContainerRegistryCredential -Registry $registry
```

<span data-ttu-id="70874-127">Next, run [docker login][docker-login] to log in:</span><span class="sxs-lookup"><span data-stu-id="70874-127">Next, run [docker login][docker-login] to log in:</span></span>

```powershell
$creds.Password | docker login $registry.LoginServer -u $creds.Username --password-stdin
```

<span data-ttu-id="70874-128">A successful login returns `Login Succeeded`:</span><span class="sxs-lookup"><span data-stu-id="70874-128">A successful login returns `Login Succeeded`:</span></span>

```console
PS Azure:\> $creds.Password | docker login $registry.LoginServer -u $creds.Username --password-stdin
Login Succeeded
```

## <a name="push-image-to-registry"></a><span data-ttu-id="70874-129">Push image to registry</span><span class="sxs-lookup"><span data-stu-id="70874-129">Push image to registry</span></span>

<span data-ttu-id="70874-130">Now that you're logged in to the registry, you can push container images to it.</span><span class="sxs-lookup"><span data-stu-id="70874-130">Now that you're logged in to the registry, you can push container images to it.</span></span> <span data-ttu-id="70874-131">To get an image you can push to your registry, pull the public [aci-helloworld][aci-helloworld-image] image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="70874-131">To get an image you can push to your registry, pull the public [aci-helloworld][aci-helloworld-image] image from Docker Hub.</span></span> <span data-ttu-id="70874-132">The [aci-helloworld][aci-helloworld-github] image is a small Node.js application that serves a static HTML page showing the Azure Container Instances logo.</span><span class="sxs-lookup"><span data-stu-id="70874-132">The [aci-helloworld][aci-helloworld-github] image is a small Node.js application that serves a static HTML page showing the Azure Container Instances logo.</span></span>

```powershell
docker pull microsoft/aci-helloworld
```

<span data-ttu-id="70874-133">As the image is pulled, output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="70874-133">As the image is pulled, output is similar to the following:</span></span>

```console
PS Azure:\> docker pull microsoft/aci-helloworld
Using default tag: latest
latest: Pulling from microsoft/aci-helloworld
88286f41530e: Pull complete
84f3a4bf8410: Pull complete
d0d9b2214720: Pull complete
3be0618266da: Pull complete
9e232827e52f: Pull complete
b53c152f538f: Pull complete
Digest: sha256:a3b2eb140e6881ca2c4df4d9c97bedda7468a5c17240d7c5d30a32850a2bc573
Status: Downloaded newer image for microsoft/aci-helloworld:latest
```

<span data-ttu-id="70874-134">Before you can push an image to your Azure container registry, you must tag it with the fully qualified domain name (FQDN) of your registry.</span><span class="sxs-lookup"><span data-stu-id="70874-134">Before you can push an image to your Azure container registry, you must tag it with the fully qualified domain name (FQDN) of your registry.</span></span> <span data-ttu-id="70874-135">The FQDN of Azure container registries are in the format *\<registry-name\>.azurecr.io*.</span><span class="sxs-lookup"><span data-stu-id="70874-135">The FQDN of Azure container registries are in the format *\<registry-name\>.azurecr.io*.</span></span>

<span data-ttu-id="70874-136">Populate a variable with the full image tag.</span><span class="sxs-lookup"><span data-stu-id="70874-136">Populate a variable with the full image tag.</span></span> <span data-ttu-id="70874-137">Include the login server, repository name ("aci-helloworld"), and image version ("v1"):</span><span class="sxs-lookup"><span data-stu-id="70874-137">Include the login server, repository name ("aci-helloworld"), and image version ("v1"):</span></span>

```powershell
$image = $registry.LoginServer + "/aci-helloworld:v1"
```

<span data-ttu-id="70874-138">Now, tag the image with [docker tag][docker-tag]:</span><span class="sxs-lookup"><span data-stu-id="70874-138">Now, tag the image with [docker tag][docker-tag]:</span></span>

```powershell
docker tag microsoft/aci-helloworld $image
```

<span data-ttu-id="70874-139">And finally, [docker push][docker-push] it to your registry:</span><span class="sxs-lookup"><span data-stu-id="70874-139">And finally, [docker push][docker-push] it to your registry:</span></span>

```powershell
docker push $image
```

<span data-ttu-id="70874-140">As the Docker client pushes your image, output should be similar to:</span><span class="sxs-lookup"><span data-stu-id="70874-140">As the Docker client pushes your image, output should be similar to:</span></span>

```console
PS Azure:\> docker push $image
The push refers to repository [myContainerRegistry007.azurecr.io/aci-helloworld]
31ba1ebd9cf5: Pushed
cd07853fe8be: Pushed
73f25249687f: Pushed
d8fbd47558a8: Pushed
44ab46125c35: Pushed
5bef08742407: Pushed
v1: digest: sha256:565dba8ce20ca1a311c2d9485089d7ddc935dd50140510050345a1b0ea4ffa6e size: 1576
```

<span data-ttu-id="70874-141">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="70874-141">Congratulations!</span></span> <span data-ttu-id="70874-142">You've just pushed your first container image to your registry.</span><span class="sxs-lookup"><span data-stu-id="70874-142">You've just pushed your first container image to your registry.</span></span>

## <a name="deploy-image-to-aci"></a><span data-ttu-id="70874-143">Deploy image to ACI</span><span class="sxs-lookup"><span data-stu-id="70874-143">Deploy image to ACI</span></span>

<span data-ttu-id="70874-144">With the image now in your registry, deploy a container directly to Azure Container Instances to see it running in Azure.</span><span class="sxs-lookup"><span data-stu-id="70874-144">With the image now in your registry, deploy a container directly to Azure Container Instances to see it running in Azure.</span></span>

<span data-ttu-id="70874-145">First, convert the registry credential to a *PSCredential*.</span><span class="sxs-lookup"><span data-stu-id="70874-145">First, convert the registry credential to a *PSCredential*.</span></span> <span data-ttu-id="70874-146">The `New-AzureRmContainerGroup` command, which you use to create the container instance, requires it in this format.</span><span class="sxs-lookup"><span data-stu-id="70874-146">The `New-AzureRmContainerGroup` command, which you use to create the container instance, requires it in this format.</span></span>

```powershell
$secpasswd = ConvertTo-SecureString $creds.Password -AsPlainText -Force
$pscred = New-Object System.Management.Automation.PSCredential($creds.Username, $secpasswd)
```

<span data-ttu-id="70874-147">Additionally, the DNS name label for your container must be unique within the Azure region you create it.</span><span class="sxs-lookup"><span data-stu-id="70874-147">Additionally, the DNS name label for your container must be unique within the Azure region you create it.</span></span> <span data-ttu-id="70874-148">Execute the following command to populate a variable with a generated name:</span><span class="sxs-lookup"><span data-stu-id="70874-148">Execute the following command to populate a variable with a generated name:</span></span>

```powershell
$dnsname = "aci-demo-" + (Get-Random -Maximum 9999)
```

<span data-ttu-id="70874-149">Finally, run [New-AzureRmContainerGroup][New-AzureRmContainerGroup] to deploy a container from the image in your registry with 1 CPU core and 1 GB of memory:</span><span class="sxs-lookup"><span data-stu-id="70874-149">Finally, run [New-AzureRmContainerGroup][New-AzureRmContainerGroup] to deploy a container from the image in your registry with 1 CPU core and 1 GB of memory:</span></span>

```powershell
New-AzureRmContainerGroup -ResourceGroup myResourceGroup -Name "mycontainer" -Image $image -RegistryCredential $pscred -Cpu 1 -MemoryInGB 1 -DnsNameLabel $dnsname
```

<span data-ttu-id="70874-150">You should get an initial response from Azure with details on your container, and its state is at first "Pending":</span><span class="sxs-lookup"><span data-stu-id="70874-150">You should get an initial response from Azure with details on your container, and its state is at first "Pending":</span></span>

```console
PS Azure:\> New-AzureRmContainerGroup -ResourceGroup myResourceGroup -Name "mycontainer" -Image $image -RegistryCredential $pscred -Cpu 1 -MemoryInGB 1 -DnsNameLabel $dnsname
ResourceGroupName        : myResourceGroup
Id                       : /subscriptions/<subscriptionID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerInstance/containerGroups/mycontainer
Name                     : mycontainer
Type                     : Microsoft.ContainerInstance/containerGroups
Location                 : eastus
Tags                     :
ProvisioningState        : Creating
Containers               : {mycontainer}
ImageRegistryCredentials : {myContainerRegistry007}
RestartPolicy            : Always
IpAddress                : 40.117.255.198
DnsNameLabel             : aci-demo-8751
Fqdn                     : aci-demo-8751.eastus.azurecontainer.io
Ports                    : {80}
OsType                   : Linux
Volumes                  :
State                    : Pending
Events                   : {}
```

<span data-ttu-id="70874-151">To monitor its status and determine when it's running, run the [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup] command a few times.</span><span class="sxs-lookup"><span data-stu-id="70874-151">To monitor its status and determine when it's running, run the [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup] command a few times.</span></span> <span data-ttu-id="70874-152">It should take less than a minute for the container to start.</span><span class="sxs-lookup"><span data-stu-id="70874-152">It should take less than a minute for the container to start.</span></span>

```powershell
(Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer).ProvisioningState
```

<span data-ttu-id="70874-153">Here, you can see the container's ProvisioningState is at first *Creating*, and then moves to the *Succeeded* state once it's up and running:</span><span class="sxs-lookup"><span data-stu-id="70874-153">Here, you can see the container's ProvisioningState is at first *Creating*, and then moves to the *Succeeded* state once it's up and running:</span></span>

```console
PS Azure:\> (Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer).ProvisioningState
Creating
PS Azure:\> (Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer).ProvisioningState
Succeeded
```

## <a name="view-running-application"></a><span data-ttu-id="70874-154">View running application</span><span class="sxs-lookup"><span data-stu-id="70874-154">View running application</span></span>

<span data-ttu-id="70874-155">Once the deployment to ACI has succeeded and your container is up and running, navigate to its fully qualified domain name (FQDN) in your browser to see the app running in Azure.</span><span class="sxs-lookup"><span data-stu-id="70874-155">Once the deployment to ACI has succeeded and your container is up and running, navigate to its fully qualified domain name (FQDN) in your browser to see the app running in Azure.</span></span>

<span data-ttu-id="70874-156">Get the FQDN for your container with [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup]:</span><span class="sxs-lookup"><span data-stu-id="70874-156">Get the FQDN for your container with [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup]:</span></span>


```powershell
(Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer).Fqdn
```

<span data-ttu-id="70874-157">The output of the command is the FQDN of your container instance:</span><span class="sxs-lookup"><span data-stu-id="70874-157">The output of the command is the FQDN of your container instance:</span></span>

```console
PS Azure:\> (Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer).Fqdn
aci-demo-8571.eastus.azurecontainer.io
```

<span data-ttu-id="70874-158">With the FQDN in hand, navigate to it in your browser:</span><span class="sxs-lookup"><span data-stu-id="70874-158">With the FQDN in hand, navigate to it in your browser:</span></span>

![Hello world app in the browser][qs-psh-01-running-app]

<span data-ttu-id="70874-160">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="70874-160">Congratulations!</span></span> <span data-ttu-id="70874-161">You've got a container running an application in Azure, deployed directly from a container image in your private Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="70874-161">You've got a container running an application in Azure, deployed directly from a container image in your private Azure container registry.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="70874-162">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="70874-162">Clean up resources</span></span>

<span data-ttu-id="70874-163">Once you're done working with the resources you created in this quickstart, use the [Remove-AzureRmResourceGroup][Remove-AzureRmResourceGroup] command to remove the resource group, the container registry, and the container instance:</span><span class="sxs-lookup"><span data-stu-id="70874-163">Once you're done working with the resources you created in this quickstart, use the [Remove-AzureRmResourceGroup][Remove-AzureRmResourceGroup] command to remove the resource group, the container registry, and the container instance:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="70874-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="70874-164">Next steps</span></span>

<span data-ttu-id="70874-165">In this quickstart, you created an Azure Container Registry with the Azure CLI, and launched an instance of it in Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="70874-165">In this quickstart, you created an Azure Container Registry with the Azure CLI, and launched an instance of it in Azure Container Instances.</span></span> <span data-ttu-id="70874-166">Continue to the Azure Container Instances tutorial for a deeper look at ACI.</span><span class="sxs-lookup"><span data-stu-id="70874-166">Continue to the Azure Container Instances tutorial for a deeper look at ACI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70874-167">Azure Container Instances tutorial</span><span class="sxs-lookup"><span data-stu-id="70874-167">Azure Container Instances tutorial</span></span>](../container-instances/container-instances-tutorial-prepare-app.md)

<!-- LINKS - external -->
[aci-helloworld-github]: https://github.com/Azure-Samples/aci-helloworld
[aci-helloworld-image]: https://hub.docker.com/r/microsoft/aci-helloworld/
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/

<!-- Links - internal -->
[Connect-AzureRmAccount]: /powershell/module/azurerm.profile/connect-azurermaccount
[Get-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/get-azurermcontainergroup
[Get-AzureRmContainerRegistryCredential]: /powershell/module/azurerm.containerregistry/get-azurermcontainerregistrycredential
[Get-Module]: /powershell/module/microsoft.powershell.core/get-module
[New-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/new-azurermcontainergroup
[New-AzureRMContainerRegistry]: /powershell/module/azurerm.containerregistry/New-AzureRMContainerRegistry
[New-AzureRmResourceGroup]: /powershell/module/azurerm.resources/new-azurermresourcegroup
[Remove-AzureRmResourceGroup]: /powershell/module/azurerm.resources/remove-azurermresourcegroup

<!-- IMAGES> -->
[qs-psh-01-running-app]: ./media/container-registry-get-started-powershell/qs-psh-01-running-app.png
