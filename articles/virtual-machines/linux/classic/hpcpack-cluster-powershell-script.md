---
title: PowerShell script to deploy Linux HPC cluster | Microsoft Docs
description: Run a PowerShell script to deploy a Linux HPC Pack 2012 R2 cluster in Azure virtual machines
services: virtual-machines-linux
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 66affb47190ba0c6fccaae8e8267b310682aee46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774442"
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="21836-103">Create a Linux high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span><span class="sxs-lookup"><span data-stu-id="21836-103">Create a Linux high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="21836-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="21836-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="21836-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of the Linux distributions supported by HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="21836-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of the Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="21836-106">If you want to deploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="21836-106">If you want to deploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="21836-107">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="21836-107">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="21836-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="21836-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="21836-109">In addition, the script described in this article does not support HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="21836-109">In addition, the script described in this article does not support HPC Pack 2016.</span></span> <span data-ttu-id="21836-110">For information about Resource Manager templates for HPC Pack 2012 R2 and HPC Pack 2016, see the [HPC Pack cluster deployment options in Azure](../hpcpack-cluster-options.md).</span><span class="sxs-lookup"><span data-stu-id="21836-110">For information about Resource Manager templates for HPC Pack 2012 R2 and HPC Pack 2016, see the [HPC Pack cluster deployment options in Azure](../hpcpack-cluster-options.md).</span></span>


[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="21836-111">Example configuration file</span><span class="sxs-lookup"><span data-stu-id="21836-111">Example configuration file</span></span>
<span data-ttu-id="21836-112">The following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="21836-112">The following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="21836-113">All the cloud services are created directly in the East Asia location.</span><span class="sxs-lookup"><span data-stu-id="21836-113">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="21836-114">The Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span><span class="sxs-lookup"><span data-stu-id="21836-114">The Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="21836-115">The compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span><span class="sxs-lookup"><span data-stu-id="21836-115">The compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="21836-116">Substitute your own values for your subscription name and the account and service names.</span><span class="sxs-lookup"><span data-stu-id="21836-116">Substitute your own values for your subscription name and the account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="21836-117">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="21836-117">Troubleshooting</span></span>
* <span data-ttu-id="21836-118">**“VNet doesn’t exist” error**.</span><span class="sxs-lookup"><span data-stu-id="21836-118">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="21836-119">If you run the HPC Pack IaaS deployment script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span><span class="sxs-lookup"><span data-stu-id="21836-119">If you run the HPC Pack IaaS deployment script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="21836-120">If this error occurs, rerun the script for the failed deployment.</span><span class="sxs-lookup"><span data-stu-id="21836-120">If this error occurs, rerun the script for the failed deployment.</span></span>
* <span data-ttu-id="21836-121">**Problem accessing the Internet from the Azure virtual network**.</span><span class="sxs-lookup"><span data-stu-id="21836-121">**Problem accessing the Internet from the Azure virtual network**.</span></span> <span data-ttu-id="21836-122">If you create an HPC Pack cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs in the Azure virtual network to the Internet.</span><span class="sxs-lookup"><span data-stu-id="21836-122">If you create an HPC Pack cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs in the Azure virtual network to the Internet.</span></span> <span data-ttu-id="21836-123">This can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span><span class="sxs-lookup"><span data-stu-id="21836-123">This can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="21836-124">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span><span class="sxs-lookup"><span data-stu-id="21836-124">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="21836-125">To do this, in Server Manager click **Tools** > **DNS** to open DNS Manager, and then double-click **Forwarders**.</span><span class="sxs-lookup"><span data-stu-id="21836-125">To do this, in Server Manager click **Tools** > **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21836-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="21836-126">Next steps</span></span>
* <span data-ttu-id="21836-127">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs to an HPC Pack cluster with Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="21836-127">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs to an HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="21836-128">For tutorials that use the script to create a cluster and run a Linux HPC workload, see:</span><span class="sxs-lookup"><span data-stu-id="21836-128">For tutorials that use the script to create a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="21836-129">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="21836-129">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="21836-130">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="21836-130">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="21836-131">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="21836-131">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

