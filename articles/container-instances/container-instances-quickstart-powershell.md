---
title: Quickstart - Create your first Azure Container Instances container with PowerShell
description: In this quickstart, you use Azure PowerShell to deploy a Windows container in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: quickstart
ms.date: 05/11/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 4a1d338304dbd5e2845768b7bf0273eed23af0ec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870501"
---
# <a name="quickstart-create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="80543-103">Quickstart: Create your first container in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="80543-103">Quickstart: Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="80543-104">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span><span class="sxs-lookup"><span data-stu-id="80543-104">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span></span> <span data-ttu-id="80543-105">In this quickstart, you create a Windows container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="80543-105">In this quickstart, you create a Windows container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="80543-106">This operation is completed in a single command.</span><span class="sxs-lookup"><span data-stu-id="80543-106">This operation is completed in a single command.</span></span> <span data-ttu-id="80543-107">Within just a few moments, you can see the running application in your browser:</span><span class="sxs-lookup"><span data-stu-id="80543-107">Within just a few moments, you can see the running application in your browser:</span></span>

![App deployed using Azure Container Instances viewed in browser][qs-powershell-01]

<span data-ttu-id="80543-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="80543-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="80543-110">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.5 or later.</span><span class="sxs-lookup"><span data-stu-id="80543-110">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.5 or later.</span></span> <span data-ttu-id="80543-111">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="80543-111">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="80543-112">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="80543-112">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="80543-113">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="80543-113">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="80543-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="80543-114">Create a resource group</span></span>

<span data-ttu-id="80543-115">Create an Azure resource group with [New-AzureRmResourceGroup][New-AzureRmResourceGroup].</span><span class="sxs-lookup"><span data-stu-id="80543-115">Create an Azure resource group with [New-AzureRmResourceGroup][New-AzureRmResourceGroup].</span></span> <span data-ttu-id="80543-116">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="80543-116">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

 ```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-a-container"></a><span data-ttu-id="80543-117">Create a container</span><span class="sxs-lookup"><span data-stu-id="80543-117">Create a container</span></span>

<span data-ttu-id="80543-118">You can create a container by providing a name, a Docker image, and an Azure resource group to the [New-AzureRmContainerGroup][New-AzureRmContainerGroup] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="80543-118">You can create a container by providing a name, a Docker image, and an Azure resource group to the [New-AzureRmContainerGroup][New-AzureRmContainerGroup] cmdlet.</span></span> <span data-ttu-id="80543-119">You can optionally expose the container to the internet with a DNS name label.</span><span class="sxs-lookup"><span data-stu-id="80543-119">You can optionally expose the container to the internet with a DNS name label.</span></span>

<span data-ttu-id="80543-120">Execute the following command to launch a Nano Server container running Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="80543-120">Execute the following command to launch a Nano Server container running Internet Information Services (IIS).</span></span> <span data-ttu-id="80543-121">The `-DnsNameLabel` value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness.</span><span class="sxs-lookup"><span data-stu-id="80543-121">The `-DnsNameLabel` value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness.</span></span>

 ```azurepowershell-interactive
New-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer -Image microsoft/iis:nanoserver -OsType Windows -DnsNameLabel aci-demo-win
```

<span data-ttu-id="80543-122">Within a few seconds, you should receive a response to your request.</span><span class="sxs-lookup"><span data-stu-id="80543-122">Within a few seconds, you should receive a response to your request.</span></span> <span data-ttu-id="80543-123">The container is initially in the **Creating** state, but it should start within a minute or two.</span><span class="sxs-lookup"><span data-stu-id="80543-123">The container is initially in the **Creating** state, but it should start within a minute or two.</span></span> <span data-ttu-id="80543-124">You can check the deployment status by using the [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup] cmdlet:</span><span class="sxs-lookup"><span data-stu-id="80543-124">You can check the deployment status by using the [Get-AzureRmContainerGroup][Get-AzureRmContainerGroup] cmdlet:</span></span>

 ```azurepowershell-interactive
Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer
```

<span data-ttu-id="80543-125">The container's provisioning state, fully qualified domain name (FQDN), and IP address appear in the cmdlet's output:</span><span class="sxs-lookup"><span data-stu-id="80543-125">The container's provisioning state, fully qualified domain name (FQDN), and IP address appear in the cmdlet's output:</span></span>

```console
PS Azure:\> Get-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer


ResourceGroupName        : myResourceGroup
Id                       : /subscriptions/<Subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerInstance/containerGroups/mycontainer
Name                     : mycontainer
Type                     : Microsoft.ContainerInstance/containerGroups
Location                 : eastus
Tags                     :
ProvisioningState        : Creating
Containers               : {mycontainer}
ImageRegistryCredentials :
RestartPolicy            : Always
IpAddress                : 52.226.19.87
DnsNameLabel             : aci-demo-win
Fqdn                     : aci-demo-win.eastus.azurecontainer.io
Ports                    : {80}
OsType                   : Windows
Volumes                  :
State                    : Pending
Events                   : {}
```

<span data-ttu-id="80543-126">Once the container **ProvisioningState** moves to `Succeeded`, navigate to its `Fqdn` in your browser:</span><span class="sxs-lookup"><span data-stu-id="80543-126">Once the container **ProvisioningState** moves to `Succeeded`, navigate to its `Fqdn` in your browser:</span></span>

![IIS deployed using Azure Container Instances viewed in browser][qs-powershell-01]

## <a name="clean-up-resources"></a><span data-ttu-id="80543-128">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="80543-128">Clean up resources</span></span>

<span data-ttu-id="80543-129">When you're done with the container, remove it with the [Remove-AzureRmContainerGroup][Remove-AzureRmContainerGroup] cmdlet:</span><span class="sxs-lookup"><span data-stu-id="80543-129">When you're done with the container, remove it with the [Remove-AzureRmContainerGroup][Remove-AzureRmContainerGroup] cmdlet:</span></span>

 ```azurepowershell-interactive
Remove-AzureRmContainerGroup -ResourceGroupName myResourceGroup -Name mycontainer
```

## <a name="next-steps"></a><span data-ttu-id="80543-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="80543-130">Next steps</span></span>

<span data-ttu-id="80543-131">In this quickstart, you created an Azure container instance from an image in the public Docker Hub registry.</span><span class="sxs-lookup"><span data-stu-id="80543-131">In this quickstart, you created an Azure container instance from an image in the public Docker Hub registry.</span></span> <span data-ttu-id="80543-132">If you'd like to build a container image yourself and deploy it to Azure Container Instances from a private Azure container registry, continue to the Azure Container Instances tutorial.</span><span class="sxs-lookup"><span data-stu-id="80543-132">If you'd like to build a container image yourself and deploy it to Azure Container Instances from a private Azure container registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="80543-133">Azure Container Instances tutorial</span><span class="sxs-lookup"><span data-stu-id="80543-133">Azure Container Instances tutorial</span></span>](./container-instances-tutorial-prepare-app.md)

<!-- IMAGES -->
[qs-powershell-01]: ./media/container-instances-quickstart-powershell/qs-powershell-01.png

<!-- LINKS -->
[New-AzureRmResourceGroup]: /powershell/module/azurerm.resources/new-azurermresourcegroup
[New-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/new-azurermcontainergroup
[Get-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/get-azurermcontainergroup
[Remove-AzureRmContainerGroup]: /powershell/module/azurerm.containerinstance/remove-azurermcontainergroup
