---
title: Run OpenFOAM with HPC Pack on Linux VMs | Microsoft Docs
description: Deploy a Microsoft HPC Pack cluster on Azure and run an OpenFOAM job on multiple Linux compute nodes across an RDMA network.
services: virtual-machines-linux
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 9032a0b68c4c8789010b0304b64a63d4924521fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814241"
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="b8dde-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="b8dde-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="b8dde-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b8dde-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="b8dde-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="b8dde-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="b8dde-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span><span class="sxs-lookup"><span data-stu-id="b8dde-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="b8dde-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azuremarketplace.microsoft.com/marketplace/apps/cfd-direct.cfd-direct-from-the-cloud), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="b8dde-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azuremarketplace.microsoft.com/marketplace/apps/cfd-direct.cfd-direct-from-the-cloud), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b8dde-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span><span class="sxs-lookup"><span data-stu-id="b8dde-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="b8dde-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span><span class="sxs-lookup"><span data-stu-id="b8dde-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="b8dde-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span><span class="sxs-lookup"><span data-stu-id="b8dde-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="b8dde-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b8dde-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="b8dde-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="b8dde-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="b8dde-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b8dde-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="b8dde-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b8dde-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="b8dde-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span><span class="sxs-lookup"><span data-stu-id="b8dde-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="b8dde-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span><span class="sxs-lookup"><span data-stu-id="b8dde-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b8dde-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b8dde-117">Prerequisites</span></span>
* <span data-ttu-id="b8dde-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="b8dde-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="b8dde-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span><span class="sxs-lookup"><span data-stu-id="b8dde-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="b8dde-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="b8dde-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="b8dde-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="b8dde-122">Substitute appropriate values for your subscription and service names.</span><span class="sxs-lookup"><span data-stu-id="b8dde-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="b8dde-123">**Additional things to know**</span><span class="sxs-lookup"><span data-stu-id="b8dde-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="b8dde-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b8dde-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="b8dde-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span><span class="sxs-lookup"><span data-stu-id="b8dde-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="b8dde-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span><span class="sxs-lookup"><span data-stu-id="b8dde-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="b8dde-127">Find the SSH connection details for each Linux VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b8dde-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="b8dde-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="b8dde-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="b8dde-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="b8dde-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span><span class="sxs-lookup"><span data-stu-id="b8dde-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="b8dde-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="b8dde-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="b8dde-132">This article is based on Intel MPI version 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="b8dde-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="b8dde-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="b8dde-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="b8dde-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="b8dde-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="b8dde-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="b8dde-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://ensighttransfe.wpengine.com/direct-access-downloads/) visualization and analysis program.</span><span class="sxs-lookup"><span data-stu-id="b8dde-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://ensighttransfe.wpengine.com/direct-access-downloads/) visualization and analysis program.</span></span> <span data-ttu-id="b8dde-137">Licensing and download information are at the EnSight site.</span><span class="sxs-lookup"><span data-stu-id="b8dde-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="b8dde-138">Set up mutual trust between compute nodes</span><span class="sxs-lookup"><span data-stu-id="b8dde-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="b8dde-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span><span class="sxs-lookup"><span data-stu-id="b8dde-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="b8dde-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span><span class="sxs-lookup"><span data-stu-id="b8dde-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="b8dde-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span><span class="sxs-lookup"><span data-stu-id="b8dde-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="b8dde-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span><span class="sxs-lookup"><span data-stu-id="b8dde-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="b8dde-143">Generate an RSA key pair</span><span class="sxs-lookup"><span data-stu-id="b8dde-143">Generate an RSA key pair</span></span>
<span data-ttu-id="b8dde-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span><span class="sxs-lookup"><span data-stu-id="b8dde-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="b8dde-145">Log on to a Linux computer.</span><span class="sxs-lookup"><span data-stu-id="b8dde-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="b8dde-146">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="b8dde-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="b8dde-147">Press **Enter** to use the default settings until the command is completed.</span><span class="sxs-lookup"><span data-stu-id="b8dde-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="b8dde-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generate an RSA key pair][keygen]
3. <span data-ttu-id="b8dde-150">Change directory to the ~/.ssh directory.</span><span class="sxs-lookup"><span data-stu-id="b8dde-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="b8dde-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="b8dde-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Private and public keys][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="b8dde-153">Add the key pair to the HPC Pack cluster</span><span class="sxs-lookup"><span data-stu-id="b8dde-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="b8dde-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span><span class="sxs-lookup"><span data-stu-id="b8dde-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="b8dde-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="b8dde-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="b8dde-156">For example, use the Active Directory User and Computers tool on the head node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="b8dde-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="b8dde-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="b8dde-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span><span class="sxs-lookup"><span data-stu-id="b8dde-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="b8dde-159">A sample cred.xml file is at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="b8dde-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="b8dde-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span><span class="sxs-lookup"><span data-stu-id="b8dde-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="b8dde-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span><span class="sxs-lookup"><span data-stu-id="b8dde-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="b8dde-162">This command completes successfully without output.</span><span class="sxs-lookup"><span data-stu-id="b8dde-162">This command completes successfully without output.</span></span> <span data-ttu-id="b8dde-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span><span class="sxs-lookup"><span data-stu-id="b8dde-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="b8dde-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span><span class="sxs-lookup"><span data-stu-id="b8dde-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="b8dde-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span><span class="sxs-lookup"><span data-stu-id="b8dde-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8dde-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="b8dde-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span><span class="sxs-lookup"><span data-stu-id="b8dde-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="b8dde-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="b8dde-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span><span class="sxs-lookup"><span data-stu-id="b8dde-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="b8dde-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="b8dde-171">To reduce security threats, HPC Pack removes the keys after job completion.</span><span class="sxs-lookup"><span data-stu-id="b8dde-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="b8dde-172">Set up a file share for Linux nodes</span><span class="sxs-lookup"><span data-stu-id="b8dde-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="b8dde-173">Now set up a standard SMB share on a folder on the head node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="b8dde-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="b8dde-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span><span class="sxs-lookup"><span data-stu-id="b8dde-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="b8dde-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b8dde-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="b8dde-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span><span class="sxs-lookup"><span data-stu-id="b8dde-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="b8dde-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="b8dde-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="b8dde-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="b8dde-180">Open a Windows PowerShell window and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="b8dde-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="b8dde-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span><span class="sxs-lookup"><span data-stu-id="b8dde-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="b8dde-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span><span class="sxs-lookup"><span data-stu-id="b8dde-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="b8dde-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="b8dde-184">The “\`” symbol in the second command is an escape symbol for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8dde-184">The “\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="b8dde-185">“\`,” means the “,” (comma character) is a part of the command.</span><span class="sxs-lookup"><span data-stu-id="b8dde-185">“\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="b8dde-186">Install MPI and OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="b8dde-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="b8dde-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span><span class="sxs-lookup"><span data-stu-id="b8dde-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="b8dde-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="b8dde-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8dde-190">These installation and compiling steps are examples.</span><span class="sxs-lookup"><span data-stu-id="b8dde-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="b8dde-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span><span class="sxs-lookup"><span data-stu-id="b8dde-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="b8dde-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="b8dde-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="b8dde-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span><span class="sxs-lookup"><span data-stu-id="b8dde-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="b8dde-194">Install Intel MPI</span><span class="sxs-lookup"><span data-stu-id="b8dde-194">Install Intel MPI</span></span>
<span data-ttu-id="b8dde-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span><span class="sxs-lookup"><span data-stu-id="b8dde-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="b8dde-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="b8dde-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="b8dde-198">To install Intel MPI Library silently, use a silent.cfg file.</span><span class="sxs-lookup"><span data-stu-id="b8dde-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="b8dde-199">You can find an example in the sample files at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="b8dde-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="b8dde-200">Place this file in the shared folder /openfoam.</span><span class="sxs-lookup"><span data-stu-id="b8dde-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="b8dde-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="b8dde-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b8dde-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span><span class="sxs-lookup"><span data-stu-id="b8dde-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="b8dde-203">This step ensures that it runs properly on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="b8dde-204">Install Intel MPI Library in silent mode.</span><span class="sxs-lookup"><span data-stu-id="b8dde-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="b8dde-205">Configure MPI</span><span class="sxs-lookup"><span data-stu-id="b8dde-205">Configure MPI</span></span>
<span data-ttu-id="b8dde-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span><span class="sxs-lookup"><span data-stu-id="b8dde-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="b8dde-207">Restart the Linux nodes after you update the limits.conf file.</span><span class="sxs-lookup"><span data-stu-id="b8dde-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="b8dde-208">For example, use the following **clusrun** command:</span><span class="sxs-lookup"><span data-stu-id="b8dde-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="b8dde-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span><span class="sxs-lookup"><span data-stu-id="b8dde-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="b8dde-210">Compile and install OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="b8dde-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="b8dde-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span><span class="sxs-lookup"><span data-stu-id="b8dde-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="b8dde-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="b8dde-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span><span class="sxs-lookup"><span data-stu-id="b8dde-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="b8dde-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="b8dde-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="b8dde-215">Use a bash script called settings.sh to set the variables.</span><span class="sxs-lookup"><span data-stu-id="b8dde-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="b8dde-216">You can find an example in the sample files at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="b8dde-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="b8dde-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span><span class="sxs-lookup"><span data-stu-id="b8dde-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="b8dde-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="b8dde-219">Install dependent packages needed to compile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="b8dde-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="b8dde-220">Depending on your Linux distribution, you might first need to add a repository.</span><span class="sxs-lookup"><span data-stu-id="b8dde-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="b8dde-221">Run **clusrun** commands similar to the following:</span><span class="sxs-lookup"><span data-stu-id="b8dde-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="b8dde-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span><span class="sxs-lookup"><span data-stu-id="b8dde-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="b8dde-223">Run the following command to compile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="b8dde-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="b8dde-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span><span class="sxs-lookup"><span data-stu-id="b8dde-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="b8dde-225">The “\`” symbol in the command is an escape symbol for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8dde-225">The “\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="b8dde-226">“\`&” means the “&” is a part of the command.</span><span class="sxs-lookup"><span data-stu-id="b8dde-226">“\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="b8dde-227">Prepare to run an OpenFOAM job</span><span class="sxs-lookup"><span data-stu-id="b8dde-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="b8dde-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="b8dde-229">Set up the runtime environment</span><span class="sxs-lookup"><span data-stu-id="b8dde-229">Set up the runtime environment</span></span>
<span data-ttu-id="b8dde-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="b8dde-231">(This command is valid for SUSE Linux only.)</span><span class="sxs-lookup"><span data-stu-id="b8dde-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="b8dde-232">Prepare sample data</span><span class="sxs-lookup"><span data-stu-id="b8dde-232">Prepare sample data</span></span>
<span data-ttu-id="b8dde-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span><span class="sxs-lookup"><span data-stu-id="b8dde-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="b8dde-234">SSH to one of your Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="b8dde-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span><span class="sxs-lookup"><span data-stu-id="b8dde-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="b8dde-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span><span class="sxs-lookup"><span data-stu-id="b8dde-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="b8dde-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span><span class="sxs-lookup"><span data-stu-id="b8dde-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="b8dde-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span><span class="sxs-lookup"><span data-stu-id="b8dde-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="b8dde-239">This file stores all input data relating to the control of time and reading and writing solution data.</span><span class="sxs-lookup"><span data-stu-id="b8dde-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="b8dde-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span><span class="sxs-lookup"><span data-stu-id="b8dde-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Modify step variables][step_variables]
5. <span data-ttu-id="b8dde-242">Specify desired values for the variables in the system/decomposeParDict file.</span><span class="sxs-lookup"><span data-stu-id="b8dde-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="b8dde-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="b8dde-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="b8dde-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Decompose processes][decompose]
6. <span data-ttu-id="b8dde-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span><span class="sxs-lookup"><span data-stu-id="b8dde-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="b8dde-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="b8dde-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="b8dde-248">(C:\OpenFoam is the shared folder on the head node.)</span><span class="sxs-lookup"><span data-stu-id="b8dde-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Data files on the head node][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="b8dde-250">Host file for mpirun</span><span class="sxs-lookup"><span data-stu-id="b8dde-250">Host file for mpirun</span></span>
<span data-ttu-id="b8dde-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span><span class="sxs-lookup"><span data-stu-id="b8dde-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="b8dde-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="b8dde-253">Write your Linux node names into this file.</span><span class="sxs-lookup"><span data-stu-id="b8dde-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="b8dde-254">In this example, the file contains the following names:</span><span class="sxs-lookup"><span data-stu-id="b8dde-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="b8dde-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span><span class="sxs-lookup"><span data-stu-id="b8dde-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="b8dde-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span><span class="sxs-lookup"><span data-stu-id="b8dde-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="b8dde-257">This ensures that it runs properly on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="b8dde-258">**Bash script wrapper**</span><span class="sxs-lookup"><span data-stu-id="b8dde-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="b8dde-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="b8dde-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span><span class="sxs-lookup"><span data-stu-id="b8dde-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="b8dde-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does the following:</span><span class="sxs-lookup"><span data-stu-id="b8dde-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does the following:</span></span>
   
   1. <span data-ttu-id="b8dde-262">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span><span class="sxs-lookup"><span data-stu-id="b8dde-262">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="b8dde-263">In this case, it sets the following variables:</span><span class="sxs-lookup"><span data-stu-id="b8dde-263">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="b8dde-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="b8dde-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="b8dde-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="b8dde-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="b8dde-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="b8dde-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="b8dde-267">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span><span class="sxs-lookup"><span data-stu-id="b8dde-267">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="b8dde-268">The format of $CCP_NODES_CORES follows this pattern:</span><span class="sxs-lookup"><span data-stu-id="b8dde-268">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="b8dde-269">where</span><span class="sxs-lookup"><span data-stu-id="b8dde-269">where</span></span>
      
      * <span data-ttu-id="b8dde-270">`<Number of nodes>` - the number of nodes allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-270">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="b8dde-271">`<Name of node_n_...>` - the name of each node allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-271">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="b8dde-272">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-272">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="b8dde-273">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span><span class="sxs-lookup"><span data-stu-id="b8dde-273">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="b8dde-274">Calls the **mpirun** command and appends two parameters to the command line.</span><span class="sxs-lookup"><span data-stu-id="b8dde-274">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="b8dde-275">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span><span class="sxs-lookup"><span data-stu-id="b8dde-275">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="b8dde-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="b8dde-277">In this case, it specifies the number of processes for **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-277">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="b8dde-278">Submit an OpenFOAM job</span><span class="sxs-lookup"><span data-stu-id="b8dde-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="b8dde-279">Now you can submit a job in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b8dde-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="b8dde-280">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span><span class="sxs-lookup"><span data-stu-id="b8dde-280">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="b8dde-281">Connect to your cluster head node and start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="b8dde-281">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="b8dde-282">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span><span class="sxs-lookup"><span data-stu-id="b8dde-282">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="b8dde-283">If they are not, select them and click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="b8dde-284">In **Job Management**, click **New Job**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="b8dde-285">Enter a name for job such as *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="b8dde-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Job details][job_details]
5. <span data-ttu-id="b8dde-287">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span><span class="sxs-lookup"><span data-stu-id="b8dde-287">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="b8dde-288">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span><span class="sxs-lookup"><span data-stu-id="b8dde-288">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Job resources][job_resources]
6. <span data-ttu-id="b8dde-290">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-290">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="b8dde-291">Add four tasks to the job with the following command lines and settings.</span><span class="sxs-lookup"><span data-stu-id="b8dde-291">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b8dde-292">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span><span class="sxs-lookup"><span data-stu-id="b8dde-292">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="b8dde-293">**Task 1**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-293">**Task 1**.</span></span> <span data-ttu-id="b8dde-294">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span><span class="sxs-lookup"><span data-stu-id="b8dde-294">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="b8dde-295">Assign one node to the task</span><span class="sxs-lookup"><span data-stu-id="b8dde-295">Assign one node to the task</span></span>
     * <span data-ttu-id="b8dde-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b8dde-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b8dde-297">**Working directory** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b8dde-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="b8dde-298">See the following figure.</span><span class="sxs-lookup"><span data-stu-id="b8dde-298">See the following figure.</span></span> <span data-ttu-id="b8dde-299">You configure the remaining tasks similarly.</span><span class="sxs-lookup"><span data-stu-id="b8dde-299">You configure the remaining tasks similarly.</span></span>
     
     ![Task 1 details][task_details1]
   * <span data-ttu-id="b8dde-301">**Task 2**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-301">**Task 2**.</span></span> <span data-ttu-id="b8dde-302">Run **interDyMFoam** in parallel to compute the sample.</span><span class="sxs-lookup"><span data-stu-id="b8dde-302">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="b8dde-303">Assign two nodes to the task</span><span class="sxs-lookup"><span data-stu-id="b8dde-303">Assign two nodes to the task</span></span>
     * <span data-ttu-id="b8dde-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b8dde-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b8dde-305">**Working directory** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b8dde-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="b8dde-306">**Task 3**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-306">**Task 3**.</span></span> <span data-ttu-id="b8dde-307">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span><span class="sxs-lookup"><span data-stu-id="b8dde-307">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="b8dde-308">Assign one node to the task</span><span class="sxs-lookup"><span data-stu-id="b8dde-308">Assign one node to the task</span></span>
     * <span data-ttu-id="b8dde-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b8dde-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b8dde-310">**Working directory** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b8dde-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="b8dde-311">**Task 4**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-311">**Task 4**.</span></span> <span data-ttu-id="b8dde-312">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span><span class="sxs-lookup"><span data-stu-id="b8dde-312">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="b8dde-313">Assign two nodes to the task</span><span class="sxs-lookup"><span data-stu-id="b8dde-313">Assign two nodes to the task</span></span>
     * <span data-ttu-id="b8dde-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="b8dde-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="b8dde-315">**Working directory** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="b8dde-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="b8dde-316">Add dependencies to these tasks in ascending task order.</span><span class="sxs-lookup"><span data-stu-id="b8dde-316">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Task dependencies][task_dependencies]
8. <span data-ttu-id="b8dde-318">Click **Submit** to run this job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-318">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="b8dde-319">By default, HPC Pack submits the job as your current logged-on user account.</span><span class="sxs-lookup"><span data-stu-id="b8dde-319">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="b8dde-320">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span><span class="sxs-lookup"><span data-stu-id="b8dde-320">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![Job credentials][creds]
   
   <span data-ttu-id="b8dde-322">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span><span class="sxs-lookup"><span data-stu-id="b8dde-322">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="b8dde-323">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-323">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="b8dde-324">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span><span class="sxs-lookup"><span data-stu-id="b8dde-324">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="b8dde-325">In the heat map, you see the job running on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-325">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Heat map][heat_map]
   
   <span data-ttu-id="b8dde-327">On each node, eight processes are started.</span><span class="sxs-lookup"><span data-stu-id="b8dde-327">On each node, eight processes are started.</span></span>
   
   ![Linux processes][linux_processes]
10. <span data-ttu-id="b8dde-329">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="b8dde-329">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="b8dde-330">View results in EnSight</span><span class="sxs-lookup"><span data-stu-id="b8dde-330">View results in EnSight</span></span>
<span data-ttu-id="b8dde-331">Optionally use [EnSight](http://www.ensight.com/) to visualize and analyze the results of the OpenFOAM job.</span><span class="sxs-lookup"><span data-stu-id="b8dde-331">Optionally use [EnSight](http://www.ensight.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="b8dde-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ensight.com/ensight.com/envideo/).</span><span class="sxs-lookup"><span data-stu-id="b8dde-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ensight.com/ensight.com/envideo/).</span></span>

1. <span data-ttu-id="b8dde-333">After you install EnSight on the head node, start it.</span><span class="sxs-lookup"><span data-stu-id="b8dde-333">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="b8dde-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="b8dde-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="b8dde-335">You see a tank in the viewer.</span><span class="sxs-lookup"><span data-stu-id="b8dde-335">You see a tank in the viewer.</span></span>
   
   ![Tank in EnSight][tank]
3. <span data-ttu-id="b8dde-337">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-337">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Create an isosurface][isosurface]
4. <span data-ttu-id="b8dde-339">Set the color for **Isosurface_part** created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b8dde-339">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="b8dde-340">For example, set it to water blue.</span><span class="sxs-lookup"><span data-stu-id="b8dde-340">For example, set it to water blue.</span></span>
   
   ![Edit isosurface color][isosurface_color]
5. <span data-ttu-id="b8dde-342">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="b8dde-342">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="b8dde-343">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span><span class="sxs-lookup"><span data-stu-id="b8dde-343">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="b8dde-344">To create the isovolume, click **Create with selected parts**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-344">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="b8dde-345">Set the color for **Iso_volume_part** created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b8dde-345">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="b8dde-346">For example, set it to deep water blue.</span><span class="sxs-lookup"><span data-stu-id="b8dde-346">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="b8dde-347">Set the color for **walls**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-347">Set the color for **walls**.</span></span> <span data-ttu-id="b8dde-348">For example, set it to transparent white.</span><span class="sxs-lookup"><span data-stu-id="b8dde-348">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="b8dde-349">Now click **Play** to see the results of the simulation.</span><span class="sxs-lookup"><span data-stu-id="b8dde-349">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Tank result][tank_result]

## <a name="sample-files"></a><span data-ttu-id="b8dde-351">Sample files</span><span class="sxs-lookup"><span data-stu-id="b8dde-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="b8dde-352">Sample XML configuration file for cluster deployment by PowerShell script</span><span class="sxs-lookup"><span data-stu-id="b8dde-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="b8dde-353">Sample cred.xml file</span><span class="sxs-lookup"><span data-stu-id="b8dde-353">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="b8dde-354">Sample silent.cfg file to install MPI</span><span class="sxs-lookup"><span data-stu-id="b8dde-354">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="b8dde-355">Sample settings.sh script</span><span class="sxs-lookup"><span data-stu-id="b8dde-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="b8dde-356">Sample hpcimpirun.sh script</span><span class="sxs-lookup"><span data-stu-id="b8dde-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
