---
title: Linux compute VMs in an HPC Pack cluster | Microsoft Docs
description: Learn how to create and use an HPC Pack cluster in Azure for Linux high performance computing (HPC) workloads
services: virtual-machines-linux
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 0dd09540fe56efe0f6b463f3410740b87ad8f87b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563459"
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="606a5-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="606a5-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="606a5-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="606a5-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="606a5-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="606a5-106">Learn how to submit Linux HPC jobs to the cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="606a5-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span><span class="sxs-lookup"><span data-stu-id="606a5-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![HPC Pack cluster with Linux nodes][scenario]

<span data-ttu-id="606a5-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="606a5-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="606a5-110">Deploy an HPC Pack cluster with Linux compute nodes</span><span class="sxs-lookup"><span data-stu-id="606a5-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="606a5-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="606a5-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span><span class="sxs-lookup"><span data-stu-id="606a5-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="606a5-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="606a5-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="606a5-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span><span class="sxs-lookup"><span data-stu-id="606a5-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="606a5-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="606a5-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="606a5-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="606a5-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="606a5-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="606a5-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="606a5-118">Prerequisites</span></span>
* <span data-ttu-id="606a5-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span><span class="sxs-lookup"><span data-stu-id="606a5-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="606a5-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="606a5-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="606a5-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span><span class="sxs-lookup"><span data-stu-id="606a5-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="606a5-122">To increase a quota, open an online customer support request at no charge.</span><span class="sxs-lookup"><span data-stu-id="606a5-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="606a5-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="606a5-124">You can use Marketplace versions of these distributions where available, or supply your own.</span><span class="sxs-lookup"><span data-stu-id="606a5-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="606a5-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="606a5-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="606a5-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="606a5-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="606a5-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="606a5-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="606a5-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="606a5-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="606a5-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="606a5-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="606a5-130">For more information, see [About H-series and compute-intensive A-series VMs](../a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="606a5-130">For more information, see [About H-series and compute-intensive A-series VMs](../a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="606a5-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span><span class="sxs-lookup"><span data-stu-id="606a5-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="606a5-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span><span class="sxs-lookup"><span data-stu-id="606a5-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="606a5-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (version 0.8.10 or later) on your client computer.</span><span class="sxs-lookup"><span data-stu-id="606a5-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="606a5-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="606a5-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="606a5-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="606a5-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="606a5-136">This article is based on version 4.4.1 or later of the script.</span><span class="sxs-lookup"><span data-stu-id="606a5-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="606a5-137">Deployment option 1.</span><span class="sxs-lookup"><span data-stu-id="606a5-137">Deployment option 1.</span></span> <span data-ttu-id="606a5-138">Use a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="606a5-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="606a5-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="606a5-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="606a5-140">In the Azure portal, review the information and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="606a5-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![Portal creation][portal]
3. <span data-ttu-id="606a5-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span><span class="sxs-lookup"><span data-stu-id="606a5-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="606a5-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span><span class="sxs-lookup"><span data-stu-id="606a5-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="606a5-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="606a5-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="606a5-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span><span class="sxs-lookup"><span data-stu-id="606a5-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="606a5-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span><span class="sxs-lookup"><span data-stu-id="606a5-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="606a5-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span><span class="sxs-lookup"><span data-stu-id="606a5-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="606a5-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span><span class="sxs-lookup"><span data-stu-id="606a5-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="606a5-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span><span class="sxs-lookup"><span data-stu-id="606a5-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="606a5-150">After the validation tests run and you review the terms of use, click **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="606a5-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="606a5-151">Deployment option 2.</span><span class="sxs-lookup"><span data-stu-id="606a5-151">Deployment option 2.</span></span> <span data-ttu-id="606a5-152">Use the IaaS deployment script</span><span class="sxs-lookup"><span data-stu-id="606a5-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="606a5-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span><span class="sxs-lookup"><span data-stu-id="606a5-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="606a5-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span><span class="sxs-lookup"><span data-stu-id="606a5-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="606a5-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (version 0.8.10 or later) on your client computer.</span><span class="sxs-lookup"><span data-stu-id="606a5-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="606a5-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="606a5-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="606a5-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="606a5-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="606a5-158">This article is based on version 4.4.1 or later of the script.</span><span class="sxs-lookup"><span data-stu-id="606a5-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="606a5-159">**XML configuration file**</span><span class="sxs-lookup"><span data-stu-id="606a5-159">**XML configuration file**</span></span>

<span data-ttu-id="606a5-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="606a5-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="606a5-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="606a5-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="606a5-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span><span class="sxs-lookup"><span data-stu-id="606a5-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="606a5-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="606a5-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="606a5-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="606a5-166">**To run the HPC Pack IaaS deployment script**</span><span class="sxs-lookup"><span data-stu-id="606a5-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="606a5-167">Open Windows PowerShell on the client computer as an administrator.</span><span class="sxs-lookup"><span data-stu-id="606a5-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="606a5-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span><span class="sxs-lookup"><span data-stu-id="606a5-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="606a5-169">Run the following command to deploy the HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="606a5-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="606a5-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="606a5-171">a.</span><span class="sxs-lookup"><span data-stu-id="606a5-171">a.</span></span> <span data-ttu-id="606a5-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="606a5-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="606a5-173">b.</span><span class="sxs-lookup"><span data-stu-id="606a5-173">b.</span></span> <span data-ttu-id="606a5-174">The script then starts to validate the configuration file.</span><span class="sxs-lookup"><span data-stu-id="606a5-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="606a5-175">It can take up to several minutes depending on the network connection.</span><span class="sxs-lookup"><span data-stu-id="606a5-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![Validation][validate]
   
    <span data-ttu-id="606a5-177">c.</span><span class="sxs-lookup"><span data-stu-id="606a5-177">c.</span></span> <span data-ttu-id="606a5-178">After validations pass, the script lists the cluster resources to create.</span><span class="sxs-lookup"><span data-stu-id="606a5-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="606a5-179">Enter *Y* to continue.</span><span class="sxs-lookup"><span data-stu-id="606a5-179">Enter *Y* to continue.</span></span>
   
    ![Resources][resources]
   
    <span data-ttu-id="606a5-181">d.</span><span class="sxs-lookup"><span data-stu-id="606a5-181">d.</span></span> <span data-ttu-id="606a5-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span><span class="sxs-lookup"><span data-stu-id="606a5-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="606a5-183">The script can run for several minutes.</span><span class="sxs-lookup"><span data-stu-id="606a5-183">The script can run for several minutes.</span></span>
   
    ![Deploy][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="606a5-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span><span class="sxs-lookup"><span data-stu-id="606a5-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="606a5-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span><span class="sxs-lookup"><span data-stu-id="606a5-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="606a5-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span><span class="sxs-lookup"><span data-stu-id="606a5-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="606a5-188">Connect to the head node</span><span class="sxs-lookup"><span data-stu-id="606a5-188">Connect to the head node</span></span>
<span data-ttu-id="606a5-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="606a5-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="606a5-190">You manage the cluster from the head node.</span><span class="sxs-lookup"><span data-stu-id="606a5-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="606a5-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="606a5-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="606a5-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span><span class="sxs-lookup"><span data-stu-id="606a5-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![Node Management][management]

<span data-ttu-id="606a5-195">You also see the Linux nodes in the **Heat Map** view.</span><span class="sxs-lookup"><span data-stu-id="606a5-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![Heat map][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="606a5-197">How to move data in a cluster with Linux nodes</span><span class="sxs-lookup"><span data-stu-id="606a5-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="606a5-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="606a5-199">Here are three common methods, described in more detail in the following sections:</span><span class="sxs-lookup"><span data-stu-id="606a5-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="606a5-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="606a5-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="606a5-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span><span class="sxs-lookup"><span data-stu-id="606a5-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="606a5-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="606a5-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span><span class="sxs-lookup"><span data-stu-id="606a5-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="606a5-204">Azure File storage</span><span class="sxs-lookup"><span data-stu-id="606a5-204">Azure File storage</span></span>
<span data-ttu-id="606a5-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span><span class="sxs-lookup"><span data-stu-id="606a5-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="606a5-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span><span class="sxs-lookup"><span data-stu-id="606a5-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="606a5-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="606a5-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/storage-dotnet-how-to-use-files.md).</span></span> <span data-ttu-id="606a5-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File Storage with Linux](../../../storage/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="606a5-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File Storage with Linux](../../../storage/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="606a5-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="606a5-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="606a5-210">In the following example, create an Azure File share on a storage account.</span><span class="sxs-lookup"><span data-stu-id="606a5-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="606a5-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span><span class="sxs-lookup"><span data-stu-id="606a5-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="606a5-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span><span class="sxs-lookup"><span data-stu-id="606a5-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="606a5-213">The Azure File share is mounted as Z: on the head node.</span><span class="sxs-lookup"><span data-stu-id="606a5-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="606a5-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span><span class="sxs-lookup"><span data-stu-id="606a5-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="606a5-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="606a5-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span><span class="sxs-lookup"><span data-stu-id="606a5-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="606a5-217">Open a Windows PowerShell window and enter the following commands:</span><span class="sxs-lookup"><span data-stu-id="606a5-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="606a5-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span><span class="sxs-lookup"><span data-stu-id="606a5-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="606a5-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span><span class="sxs-lookup"><span data-stu-id="606a5-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="606a5-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span><span class="sxs-lookup"><span data-stu-id="606a5-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="606a5-221">The “\`” symbol in the second command is an escape symbol for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="606a5-221">The “\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="606a5-222">“\`,” means that the “,” (comma character) is a part of the command.</span><span class="sxs-lookup"><span data-stu-id="606a5-222">“\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="606a5-223">Head node share</span><span class="sxs-lookup"><span data-stu-id="606a5-223">Head node share</span></span>
<span data-ttu-id="606a5-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="606a5-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="606a5-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="606a5-226">Here are the steps.</span><span class="sxs-lookup"><span data-stu-id="606a5-226">Here are the steps.</span></span>

1. <span data-ttu-id="606a5-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span><span class="sxs-lookup"><span data-stu-id="606a5-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="606a5-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="606a5-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="606a5-229">Here CentOS7RDMA-HN is the hostname of the head node.</span><span class="sxs-lookup"><span data-stu-id="606a5-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![File share permissions][fileshareperms]
   
    ![File sharing][filesharing]
2. <span data-ttu-id="606a5-232">Open a Windows PowerShell window and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="606a5-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="606a5-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span><span class="sxs-lookup"><span data-stu-id="606a5-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="606a5-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span><span class="sxs-lookup"><span data-stu-id="606a5-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="606a5-235">The username and password in the command should be the username and password of a cluster user on the head node.</span><span class="sxs-lookup"><span data-stu-id="606a5-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="606a5-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="606a5-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="606a5-237">The “\`” symbol in the second command is an escape symbol for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="606a5-237">The “\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="606a5-238">“\`,” means that the “,” (comma character) is a part of the command.</span><span class="sxs-lookup"><span data-stu-id="606a5-238">“\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="606a5-239">NFS server</span><span class="sxs-lookup"><span data-stu-id="606a5-239">NFS server</span></span>
<span data-ttu-id="606a5-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span><span class="sxs-lookup"><span data-stu-id="606a5-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="606a5-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="606a5-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="606a5-242">It provides better compatibility with Linux nodes compared with an SMB share.</span><span class="sxs-lookup"><span data-stu-id="606a5-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="606a5-243">For example, it supports file links.</span><span class="sxs-lookup"><span data-stu-id="606a5-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="606a5-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="606a5-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="606a5-245">For example, create an NFS share named nfs with the following properties:</span><span class="sxs-lookup"><span data-stu-id="606a5-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![NFS authorization][nfsauth]
   
    ![NFS share permissions][nfsshare]
   
    ![NFS NTFS permissions][nfsperm]
   
    ![NFS management properties][nfsmanage]
2. <span data-ttu-id="606a5-250">Open a Windows PowerShell window and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="606a5-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="606a5-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span><span class="sxs-lookup"><span data-stu-id="606a5-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="606a5-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span><span class="sxs-lookup"><span data-stu-id="606a5-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="606a5-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span><span class="sxs-lookup"><span data-stu-id="606a5-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="606a5-254">How to submit jobs</span><span class="sxs-lookup"><span data-stu-id="606a5-254">How to submit jobs</span></span>
<span data-ttu-id="606a5-255">There are several ways to submit jobs to the HPC Pack cluster:</span><span class="sxs-lookup"><span data-stu-id="606a5-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="606a5-256">HPC Cluster Manager or HPC Job Manager GUI</span><span class="sxs-lookup"><span data-stu-id="606a5-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="606a5-257">HPC web portal</span><span class="sxs-lookup"><span data-stu-id="606a5-257">HPC web portal</span></span>
* <span data-ttu-id="606a5-258">REST API</span><span class="sxs-lookup"><span data-stu-id="606a5-258">REST API</span></span>

<span data-ttu-id="606a5-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span><span class="sxs-lookup"><span data-stu-id="606a5-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="606a5-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="606a5-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="606a5-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="606a5-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="606a5-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="606a5-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="606a5-263">Clusrun for Linux nodes</span><span class="sxs-lookup"><span data-stu-id="606a5-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="606a5-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="606a5-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="606a5-265">Following are some basic examples.</span><span class="sxs-lookup"><span data-stu-id="606a5-265">Following are some basic examples.</span></span>

* <span data-ttu-id="606a5-266">Show current user names on all nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="606a5-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="606a5-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="606a5-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span><span class="sxs-lookup"><span data-stu-id="606a5-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="606a5-269">You might need to use certain escape characters in **clusrun** commands.</span><span class="sxs-lookup"><span data-stu-id="606a5-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="606a5-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span><span class="sxs-lookup"><span data-stu-id="606a5-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="606a5-271">Next steps</span><span class="sxs-lookup"><span data-stu-id="606a5-271">Next steps</span></span>
* <span data-ttu-id="606a5-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span><span class="sxs-lookup"><span data-stu-id="606a5-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="606a5-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="606a5-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="606a5-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span><span class="sxs-lookup"><span data-stu-id="606a5-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="606a5-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="606a5-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="606a5-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="606a5-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/scenario.png
[portal]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/portal.png
[validate]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/validate.png
[resources]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/resources.png
[deploy]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/deploy.png
[management]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/management.png
[heatmap]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/heatmap.png
[fileshareperms]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/fileshare1.png
[filesharing]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/fileshare2.png
[nfsauth]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/nfsauth.png
[nfsshare]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/nfsshare.png
[nfsperm]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/nfsperm.png
[nfsmanage]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster/nfsmanage.png













