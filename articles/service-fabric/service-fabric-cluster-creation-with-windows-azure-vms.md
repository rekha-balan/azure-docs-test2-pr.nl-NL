---
title: Create a standalone cluster with Azure VMs running Windows| Microsoft Docs
description: Learn how to create and manage an Azure Service Fabric cluster on Azure virtual machines running Windows Server.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/24/2017
ms.author: ryanwi;chackdan
ms.openlocfilehash: 6640cd714d6860d1c4aa9558cb86871d45cf899f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671437"
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="3db49-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span><span class="sxs-lookup"><span data-stu-id="3db49-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="3db49-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3db49-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="3db49-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3db49-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="3db49-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span><span class="sxs-lookup"><span data-stu-id="3db49-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="3db49-107">Steps to create the standalone cluster</span><span class="sxs-lookup"><span data-stu-id="3db49-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="3db49-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span><span class="sxs-lookup"><span data-stu-id="3db49-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="3db49-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span><span class="sxs-lookup"><span data-stu-id="3db49-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="3db49-110">Add a couple more VMs to the same resource group.</span><span class="sxs-lookup"><span data-stu-id="3db49-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="3db49-111">Ensure that each of the VMs has the same administrator user name and password when created.</span><span class="sxs-lookup"><span data-stu-id="3db49-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="3db49-112">Once created you should see all three VMs in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="3db49-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="3db49-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="3db49-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="3db49-114">This ensures that the network traffic can communicate between the machines.</span><span class="sxs-lookup"><span data-stu-id="3db49-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="3db49-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="3db49-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="3db49-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span><span class="sxs-lookup"><span data-stu-id="3db49-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="3db49-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span><span class="sxs-lookup"><span data-stu-id="3db49-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="3db49-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span><span class="sxs-lookup"><span data-stu-id="3db49-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="3db49-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span><span class="sxs-lookup"><span data-stu-id="3db49-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="3db49-120">Change the cluster name at the top and save the file.</span><span class="sxs-lookup"><span data-stu-id="3db49-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="3db49-121">A partial example of the cluster manifest is shown below.</span><span class="sxs-lookup"><span data-stu-id="3db49-121">A partial example of the cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="3db49-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="3db49-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="3db49-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3db49-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="3db49-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span><span class="sxs-lookup"><span data-stu-id="3db49-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="3db49-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="3db49-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="3db49-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span><span class="sxs-lookup"><span data-stu-id="3db49-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="3db49-127">Run the following PowerShell command to deploy the cluster:</span><span class="sxs-lookup"><span data-stu-id="3db49-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="3db49-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span><span class="sxs-lookup"><span data-stu-id="3db49-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="3db49-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="3db49-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3db49-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="3db49-130">Next steps</span></span>
* [<span data-ttu-id="3db49-131">Create standalone Service Fabric clusters on Windows Server or Linux</span><span class="sxs-lookup"><span data-stu-id="3db49-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="3db49-132">Add or remove nodes to a standalone Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="3db49-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="3db49-133">Configuration settings for standalone Windows cluster</span><span class="sxs-lookup"><span data-stu-id="3db49-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="3db49-134">Secure a standalone cluster on Windows using Windows security</span><span class="sxs-lookup"><span data-stu-id="3db49-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="3db49-135">Secure a standalone cluster on Windows using X509 certificates</span><span class="sxs-lookup"><span data-stu-id="3db49-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

