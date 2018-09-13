---
title: Run STAR-CCM+ with HPC Pack on Linux VMs | Microsoft Docs
description: Deploy a Microsoft HPC Pack cluster on Azure and run an STAR-CCM+ job on multiple Linux compute nodes across an RDMA network.
services: virtual-machines-linux
documentationcenter: ''
author: xpillons
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: aa7e5935703e0707b6b32cab063f22860e0aed6b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555839"
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="a105e-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="a105e-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="a105e-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="a105e-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a105e-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a105e-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="a105e-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="a105e-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="a105e-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a105e-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="a105e-108">Set up an HPC Pack cluster</span><span class="sxs-lookup"><span data-stu-id="a105e-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="a105e-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span><span class="sxs-lookup"><span data-stu-id="a105e-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="a105e-110">Azure PowerShell is a prerequisite.</span><span class="sxs-lookup"><span data-stu-id="a105e-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="a105e-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a105e-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="a105e-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="a105e-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="a105e-113">This article is based on the usage of SLES 12.</span><span class="sxs-lookup"><span data-stu-id="a105e-113">This article is based on the usage of SLES 12.</span></span> <span data-ttu-id="a105e-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="a105e-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="a105e-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span><span class="sxs-lookup"><span data-stu-id="a105e-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span></span>

<span data-ttu-id="a105e-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span><span class="sxs-lookup"><span data-stu-id="a105e-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span></span> <span data-ttu-id="a105e-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span><span class="sxs-lookup"><span data-stu-id="a105e-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span></span>

<span data-ttu-id="a105e-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span><span class="sxs-lookup"><span data-stu-id="a105e-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="a105e-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span><span class="sxs-lookup"><span data-stu-id="a105e-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="a105e-120">After 20 to 30 minutes, the head node should be ready.</span><span class="sxs-lookup"><span data-stu-id="a105e-120">After 20 to 30 minutes, the head node should be ready.</span></span> <span data-ttu-id="a105e-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a105e-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span></span>

<span data-ttu-id="a105e-122">You might eventually have to fix the DNS forwarder.</span><span class="sxs-lookup"><span data-stu-id="a105e-122">You might eventually have to fix the DNS forwarder.</span></span> <span data-ttu-id="a105e-123">To do so, start DNS Manager.</span><span class="sxs-lookup"><span data-stu-id="a105e-123">To do so, start DNS Manager.</span></span>

1. <span data-ttu-id="a105e-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span><span class="sxs-lookup"><span data-stu-id="a105e-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span></span>
2. <span data-ttu-id="a105e-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a105e-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="a105e-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a105e-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="a105e-127">Set up Linux compute nodes</span><span class="sxs-lookup"><span data-stu-id="a105e-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="a105e-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span><span class="sxs-lookup"><span data-stu-id="a105e-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span></span>

<span data-ttu-id="a105e-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span><span class="sxs-lookup"><span data-stu-id="a105e-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span></span> <span data-ttu-id="a105e-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a105e-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="a105e-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span><span class="sxs-lookup"><span data-stu-id="a105e-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span></span>

<span data-ttu-id="a105e-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span><span class="sxs-lookup"><span data-stu-id="a105e-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="a105e-133">Run the following Azure PowerShell commands in an elevated command prompt:</span><span class="sxs-lookup"><span data-stu-id="a105e-133">Run the following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="a105e-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a105e-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span></span>
2. <span data-ttu-id="a105e-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span><span class="sxs-lookup"><span data-stu-id="a105e-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span></span>
3. <span data-ttu-id="a105e-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span><span class="sxs-lookup"><span data-stu-id="a105e-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="a105e-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="a105e-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span></span>
   
   ![Head-node deployment in action][hndeploy]

<span data-ttu-id="a105e-139">Open the HPC Pack Cluster Manager tool.</span><span class="sxs-lookup"><span data-stu-id="a105e-139">Open the HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="a105e-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span><span class="sxs-lookup"><span data-stu-id="a105e-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="a105e-141">With the classic deployment mode, IaaS VMs are created sequentially.</span><span class="sxs-lookup"><span data-stu-id="a105e-141">With the classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="a105e-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span><span class="sxs-lookup"><span data-stu-id="a105e-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Linux nodes in HPC Pack Cluster Manager][clustermanager]

<span data-ttu-id="a105e-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span><span class="sxs-lookup"><span data-stu-id="a105e-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="a105e-145">Set up an Azure File share for Windows and Linux nodes</span><span class="sxs-lookup"><span data-stu-id="a105e-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="a105e-146">You can use the Azure File service to store scripts, application packages, and data files.</span><span class="sxs-lookup"><span data-stu-id="a105e-146">You can use the Azure File service to store scripts, application packages, and data files.</span></span> <span data-ttu-id="a105e-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span><span class="sxs-lookup"><span data-stu-id="a105e-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="a105e-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span><span class="sxs-lookup"><span data-stu-id="a105e-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="a105e-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="a105e-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="a105e-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span><span class="sxs-lookup"><span data-stu-id="a105e-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span></span>

### <a name="mount-the-azure-file-share-on-the-head-node"></a><span data-ttu-id="a105e-151">Mount the Azure File share on the head node</span><span class="sxs-lookup"><span data-stu-id="a105e-151">Mount the Azure File share on the head node</span></span>
<span data-ttu-id="a105e-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span><span class="sxs-lookup"><span data-stu-id="a105e-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="a105e-153">Then, to mount the Azure File share, run:</span><span class="sxs-lookup"><span data-stu-id="a105e-153">Then, to mount the Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-the-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="a105e-154">Mount the Azure File share on Linux compute nodes</span><span class="sxs-lookup"><span data-stu-id="a105e-154">Mount the Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="a105e-155">One useful tool that comes with HPC Pack is the clusrun tool.</span><span class="sxs-lookup"><span data-stu-id="a105e-155">One useful tool that comes with HPC Pack is the clusrun tool.</span></span> <span data-ttu-id="a105e-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="a105e-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="a105e-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span><span class="sxs-lookup"><span data-stu-id="a105e-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span></span>
<span data-ttu-id="a105e-158">In an elevated command prompt on the head node, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="a105e-158">In an elevated command prompt on the head node, run the following commands.</span></span>

<span data-ttu-id="a105e-159">To create the mount directory:</span><span class="sxs-lookup"><span data-stu-id="a105e-159">To create the mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="a105e-160">To mount the Azure File share:</span><span class="sxs-lookup"><span data-stu-id="a105e-160">To mount the Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="a105e-161">To persist the mount share:</span><span class="sxs-lookup"><span data-stu-id="a105e-161">To persist the mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="a105e-162">Install STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="a105e-162">Install STAR-CCM+</span></span>
<span data-ttu-id="a105e-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span><span class="sxs-lookup"><span data-stu-id="a105e-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="a105e-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a105e-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span></span> <span data-ttu-id="a105e-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span><span class="sxs-lookup"><span data-stu-id="a105e-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="a105e-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span><span class="sxs-lookup"><span data-stu-id="a105e-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="a105e-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="a105e-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="a105e-168">In our case, we used version 11.02.010 in mixed precision.</span><span class="sxs-lookup"><span data-stu-id="a105e-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="a105e-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span><span class="sxs-lookup"><span data-stu-id="a105e-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span></span> <span data-ttu-id="a105e-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span><span class="sxs-lookup"><span data-stu-id="a105e-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="a105e-171">Sample setupstarcm.sh script</span><span class="sxs-lookup"><span data-stu-id="a105e-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh to set up STAR-CCM+ locally

    # Create the CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy the STAR-CCM package from the file share to the local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract the package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without the FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="a105e-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span><span class="sxs-lookup"><span data-stu-id="a105e-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="a105e-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a105e-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span></span> <span data-ttu-id="a105e-174">After few minutes, all nodes should be correctly set up.</span><span class="sxs-lookup"><span data-stu-id="a105e-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="a105e-175">Run STAR-CCM+ jobs</span><span class="sxs-lookup"><span data-stu-id="a105e-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="a105e-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span><span class="sxs-lookup"><span data-stu-id="a105e-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span></span> <span data-ttu-id="a105e-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="a105e-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span></span> <span data-ttu-id="a105e-178">The input data is kept on the Azure File share first for simplicity.</span><span class="sxs-lookup"><span data-stu-id="a105e-178">The input data is kept on the Azure File share first for simplicity.</span></span>

<span data-ttu-id="a105e-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span><span class="sxs-lookup"><span data-stu-id="a105e-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span></span> <span data-ttu-id="a105e-180">It takes three arguments:</span><span class="sxs-lookup"><span data-stu-id="a105e-180">It takes three arguments:</span></span>

* <span data-ttu-id="a105e-181">The model name</span><span class="sxs-lookup"><span data-stu-id="a105e-181">The model name</span></span>
* <span data-ttu-id="a105e-182">The number of nodes to be used</span><span class="sxs-lookup"><span data-stu-id="a105e-182">The number of nodes to be used</span></span>
* <span data-ttu-id="a105e-183">The number of cores on each node to be used</span><span class="sxs-lookup"><span data-stu-id="a105e-183">The number of cores on each node to be used</span></span>

<span data-ttu-id="a105e-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span><span class="sxs-lookup"><span data-stu-id="a105e-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="a105e-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span><span class="sxs-lookup"><span data-stu-id="a105e-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span></span>

<span data-ttu-id="a105e-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span><span class="sxs-lookup"><span data-stu-id="a105e-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span></span> <span data-ttu-id="a105e-187">The job is not started as an MPI job directly.</span><span class="sxs-lookup"><span data-stu-id="a105e-187">The job is not started as an MPI job directly.</span></span> <span data-ttu-id="a105e-188">The **runstarccm.sh** shell script will start the MPI launcher.</span><span class="sxs-lookup"><span data-stu-id="a105e-188">The **runstarccm.sh** shell script will start the MPI launcher.</span></span>

<span data-ttu-id="a105e-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span><span class="sxs-lookup"><span data-stu-id="a105e-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="a105e-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span><span class="sxs-lookup"><span data-stu-id="a105e-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="a105e-191">Sample SubmitStarccmJob.ps1 script</span><span class="sxs-lookup"><span data-stu-id="a105e-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us the job ID that's used to identify the name of the uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit the job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="a105e-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span><span class="sxs-lookup"><span data-stu-id="a105e-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="a105e-193">Sample runstarccm.sh script</span><span class="sxs-lookup"><span data-stu-id="a105e-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # The path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set the mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into the hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with the hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="a105e-194">In our test, we used a Power-On-Demand license token.</span><span class="sxs-lookup"><span data-stu-id="a105e-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="a105e-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span><span class="sxs-lookup"><span data-stu-id="a105e-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span></span>

<span data-ttu-id="a105e-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span><span class="sxs-lookup"><span data-stu-id="a105e-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span></span> <span data-ttu-id="a105e-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span><span class="sxs-lookup"><span data-stu-id="a105e-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span></span>

<span data-ttu-id="a105e-198">The format of **$CCP_NODES_CORES** follows this pattern:</span><span class="sxs-lookup"><span data-stu-id="a105e-198">The format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="a105e-199">Where:</span><span class="sxs-lookup"><span data-stu-id="a105e-199">Where:</span></span>

* <span data-ttu-id="a105e-200">`<Number of nodes>` is the number of nodes allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="a105e-200">`<Number of nodes>` is the number of nodes allocated to this job.</span></span>
* <span data-ttu-id="a105e-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="a105e-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span></span>
* <span data-ttu-id="a105e-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="a105e-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span></span>

<span data-ttu-id="a105e-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="a105e-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="a105e-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span><span class="sxs-lookup"><span data-stu-id="a105e-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="a105e-205">`-mpi intel` to specify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="a105e-205">`-mpi intel` to specify Intel MPI.</span></span>
* <span data-ttu-id="a105e-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span><span class="sxs-lookup"><span data-stu-id="a105e-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="a105e-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="a105e-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="a105e-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span><span class="sxs-lookup"><span data-stu-id="a105e-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span></span>
* <span data-ttu-id="a105e-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span><span class="sxs-lookup"><span data-stu-id="a105e-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="a105e-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a105e-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="a105e-211">Then from a PowerShell command prompt, run this:</span><span class="sxs-lookup"><span data-stu-id="a105e-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="a105e-212">Stop nodes</span><span class="sxs-lookup"><span data-stu-id="a105e-212">Stop nodes</span></span>
<span data-ttu-id="a105e-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span><span class="sxs-lookup"><span data-stu-id="a105e-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="a105e-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="a105e-214">Next steps</span></span>
<span data-ttu-id="a105e-215">Try running other Linux workloads.</span><span class="sxs-lookup"><span data-stu-id="a105e-215">Try running other Linux workloads.</span></span> <span data-ttu-id="a105e-216">For example, see:</span><span class="sxs-lookup"><span data-stu-id="a105e-216">For example, see:</span></span>

* [<span data-ttu-id="a105e-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="a105e-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="a105e-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="a105e-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-starccm/ClusterManager.png


