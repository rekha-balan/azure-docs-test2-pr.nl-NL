---
title: NAMD with Microsoft HPC Pack on Linux VMs | Microsoft Docs
description: Deploy a Microsoft HPC Pack cluster on Azure and run a NAMD simulation with charmrun on multiple Linux compute nodes
services: virtual-machines-linux
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: c92e10fde73c3734714e53104e0ee166ffd6f91a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554771"
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="ef942-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span><span class="sxs-lookup"><span data-stu-id="ef942-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="ef942-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ef942-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="ef942-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span><span class="sxs-lookup"><span data-stu-id="ef942-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="ef942-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span><span class="sxs-lookup"><span data-stu-id="ef942-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span></span> <span data-ttu-id="ef942-107">Examples of these systems include viruses, cell structures, and large proteins.</span><span class="sxs-lookup"><span data-stu-id="ef942-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="ef942-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span><span class="sxs-lookup"><span data-stu-id="ef942-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span></span>
* <span data-ttu-id="ef942-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ef942-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="ef942-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span><span class="sxs-lookup"><span data-stu-id="ef942-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="ef942-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span><span class="sxs-lookup"><span data-stu-id="ef942-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="ef942-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ef942-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef942-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ef942-113">Prerequisites</span></span>
* <span data-ttu-id="ef942-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="ef942-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="ef942-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span><span class="sxs-lookup"><span data-stu-id="ef942-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="ef942-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="ef942-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="ef942-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span><span class="sxs-lookup"><span data-stu-id="ef942-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="ef942-118">Customize this file as needed for your environment.</span><span class="sxs-lookup"><span data-stu-id="ef942-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="ef942-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span><span class="sxs-lookup"><span data-stu-id="ef942-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="ef942-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span><span class="sxs-lookup"><span data-stu-id="ef942-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="ef942-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="ef942-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="ef942-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span></span> <span data-ttu-id="ef942-123">To extract the files, follow the instructions later in this article.</span><span class="sxs-lookup"><span data-stu-id="ef942-123">To extract the files, follow the instructions later in this article.</span></span> 
* <span data-ttu-id="ef942-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span><span class="sxs-lookup"><span data-stu-id="ef942-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="ef942-125">The current version is 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="ef942-125">The current version is 1.9.2.</span></span> <span data-ttu-id="ef942-126">See the VMD download site to get started.</span><span class="sxs-lookup"><span data-stu-id="ef942-126">See the VMD download site to get started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="ef942-127">Set up mutual trust between compute nodes</span><span class="sxs-lookup"><span data-stu-id="ef942-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="ef942-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span><span class="sxs-lookup"><span data-stu-id="ef942-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="ef942-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span><span class="sxs-lookup"><span data-stu-id="ef942-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="ef942-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span><span class="sxs-lookup"><span data-stu-id="ef942-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span></span> <span data-ttu-id="ef942-131">Then, destroy the relationship after the job is complete.</span><span class="sxs-lookup"><span data-stu-id="ef942-131">Then, destroy the relationship after the job is complete.</span></span> <span data-ttu-id="ef942-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span><span class="sxs-lookup"><span data-stu-id="ef942-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span></span> <span data-ttu-id="ef942-133">Instructions follow.</span><span class="sxs-lookup"><span data-stu-id="ef942-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="ef942-134">Generate an RSA key pair</span><span class="sxs-lookup"><span data-stu-id="ef942-134">Generate an RSA key pair</span></span>
<span data-ttu-id="ef942-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span><span class="sxs-lookup"><span data-stu-id="ef942-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="ef942-136">Log on to a Linux computer.</span><span class="sxs-lookup"><span data-stu-id="ef942-136">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="ef942-137">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="ef942-137">Run the following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="ef942-138">Press **Enter** to use the default settings until the command is completed.</span><span class="sxs-lookup"><span data-stu-id="ef942-138">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="ef942-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ef942-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generate an RSA key pair][keygen]
3. <span data-ttu-id="ef942-141">Change directory to the ~/.ssh directory.</span><span class="sxs-lookup"><span data-stu-id="ef942-141">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="ef942-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="ef942-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Private and public keys][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="ef942-144">Add the key pair to the HPC Pack cluster</span><span class="sxs-lookup"><span data-stu-id="ef942-144">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="ef942-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="ef942-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="ef942-146">You manage the cluster from the head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-146">You manage the cluster from the head node.</span></span>
2. <span data-ttu-id="ef942-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="ef942-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="ef942-148">For example, use the Active Directory User and Computers tool on the head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-148">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="ef942-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="ef942-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="ef942-150">Add the domain user to the HPC Pack cluster as a cluster user.</span><span class="sxs-lookup"><span data-stu-id="ef942-150">Add the domain user to the HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="ef942-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef942-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="ef942-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span><span class="sxs-lookup"><span data-stu-id="ef942-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="ef942-153">You can find an example in the sample files at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="ef942-153">You can find an example in the sample files at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="ef942-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span><span class="sxs-lookup"><span data-stu-id="ef942-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="ef942-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span><span class="sxs-lookup"><span data-stu-id="ef942-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="ef942-156">This command completes successfully without output.</span><span class="sxs-lookup"><span data-stu-id="ef942-156">This command completes successfully without output.</span></span> <span data-ttu-id="ef942-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span><span class="sxs-lookup"><span data-stu-id="ef942-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="ef942-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span><span class="sxs-lookup"><span data-stu-id="ef942-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="ef942-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span><span class="sxs-lookup"><span data-stu-id="ef942-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef942-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="ef942-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="ef942-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span><span class="sxs-lookup"><span data-stu-id="ef942-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="ef942-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span><span class="sxs-lookup"><span data-stu-id="ef942-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span></span> <span data-ttu-id="ef942-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span><span class="sxs-lookup"><span data-stu-id="ef942-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="ef942-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span><span class="sxs-lookup"><span data-stu-id="ef942-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="ef942-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span><span class="sxs-lookup"><span data-stu-id="ef942-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="ef942-166">Set up a file share for Linux nodes</span><span class="sxs-lookup"><span data-stu-id="ef942-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="ef942-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span><span class="sxs-lookup"><span data-stu-id="ef942-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span></span> <span data-ttu-id="ef942-168">Following are steps to mount a shared folder on the head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-168">Following are steps to mount a shared folder on the head node.</span></span> <span data-ttu-id="ef942-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span><span class="sxs-lookup"><span data-stu-id="ef942-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span></span> <span data-ttu-id="ef942-170">If your Linux nodes support an Azure File share, see [How to use Azure File Storage with Linux](../../../storage/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ef942-170">If your Linux nodes support an Azure File share, see [How to use Azure File Storage with Linux](../../../storage/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="ef942-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ef942-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="ef942-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span><span class="sxs-lookup"><span data-stu-id="ef942-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="ef942-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span></span>
2. <span data-ttu-id="ef942-174">Create a subfolder named namd2 in the shared folder.</span><span class="sxs-lookup"><span data-stu-id="ef942-174">Create a subfolder named namd2 in the shared folder.</span></span> <span data-ttu-id="ef942-175">In namd2, create another subfolder named namdsample.</span><span class="sxs-lookup"><span data-stu-id="ef942-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="ef942-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span><span class="sxs-lookup"><span data-stu-id="ef942-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="ef942-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="ef942-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="ef942-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="ef942-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="ef942-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="ef942-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="ef942-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span><span class="sxs-lookup"><span data-stu-id="ef942-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="ef942-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span><span class="sxs-lookup"><span data-stu-id="ef942-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="ef942-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="ef942-183">The “\`” symbol in the second command is an escape symbol for PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef942-183">The “\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ef942-184">“\`,” means the “,” (comma character) is a part of the command.</span><span class="sxs-lookup"><span data-stu-id="ef942-184">“\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="create-a-bash-script-to-run-a-namd-job"></a><span data-ttu-id="ef942-185">Create a Bash script to run a NAMD job</span><span class="sxs-lookup"><span data-stu-id="ef942-185">Create a Bash script to run a NAMD job</span></span>
<span data-ttu-id="ef942-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span><span class="sxs-lookup"><span data-stu-id="ef942-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span></span> <span data-ttu-id="ef942-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span><span class="sxs-lookup"><span data-stu-id="ef942-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="ef942-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span><span class="sxs-lookup"><span data-stu-id="ef942-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="ef942-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="ef942-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="ef942-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span><span class="sxs-lookup"><span data-stu-id="ef942-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="ef942-191">This ensures that it runs properly on the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="ef942-191">This ensures that it runs properly on the Linux nodes.</span></span>
> 
> 

<span data-ttu-id="ef942-192">Following are details about what this bash script does.</span><span class="sxs-lookup"><span data-stu-id="ef942-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="ef942-193">Define some variables.</span><span class="sxs-lookup"><span data-stu-id="ef942-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # The path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="ef942-194">Get node information from the environment variables.</span><span class="sxs-lookup"><span data-stu-id="ef942-194">Get node information from the environment variables.</span></span> <span data-ttu-id="ef942-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="ef942-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="ef942-196">$COUNT is the size of $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="ef942-196">$COUNT is the size of $NODESCORES.</span></span>
   
   ```
   # Get node information from the environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="ef942-197">The format for the $CCP_NODES_CORES variable is as follows:</span><span class="sxs-lookup"><span data-stu-id="ef942-197">The format for the $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="ef942-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span><span class="sxs-lookup"><span data-stu-id="ef942-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span></span> <span data-ttu-id="ef942-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span><span class="sxs-lookup"><span data-stu-id="ef942-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="ef942-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span><span class="sxs-lookup"><span data-stu-id="ef942-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="ef942-201">(This should only occur when you run this script directly on your Linux nodes.)</span><span class="sxs-lookup"><span data-stu-id="ef942-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="ef942-202">Or create a nodelist file for **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="ef942-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create the nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write the head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into the nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="ef942-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span><span class="sxs-lookup"><span data-stu-id="ef942-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span></span>
   
   <span data-ttu-id="ef942-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span><span class="sxs-lookup"><span data-stu-id="ef942-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span></span> <span data-ttu-id="ef942-205">It stores the number of total cores allocated to this job.</span><span class="sxs-lookup"><span data-stu-id="ef942-205">It stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="ef942-206">We use it to specify the number of processes for charmrun.</span><span class="sxs-lookup"><span data-stu-id="ef942-206">We use it to specify the number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="ef942-207">Exit with the **charmrun** return status.</span><span class="sxs-lookup"><span data-stu-id="ef942-207">Exit with the **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="ef942-208">Following is the information in the nodelist file, which the script generates:</span><span class="sxs-lookup"><span data-stu-id="ef942-208">Following is the information in the nodelist file, which the script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="ef942-209">For example:</span><span class="sxs-lookup"><span data-stu-id="ef942-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="ef942-210">Submit a NAMD job</span><span class="sxs-lookup"><span data-stu-id="ef942-210">Submit a NAMD job</span></span>
<span data-ttu-id="ef942-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="ef942-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="ef942-212">Connect to your cluster head node and start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="ef942-212">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="ef942-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span><span class="sxs-lookup"><span data-stu-id="ef942-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="ef942-214">If they are not, select them and click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="ef942-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="ef942-215">In **Job Management**, click **New Job**.</span><span class="sxs-lookup"><span data-stu-id="ef942-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="ef942-216">Enter a name for job such as *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="ef942-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![New HPC job][namd_job]
5. <span data-ttu-id="ef942-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span><span class="sxs-lookup"><span data-stu-id="ef942-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span></span> <span data-ttu-id="ef942-219">, we run the job on three Linux nodes and each node has four cores.</span><span class="sxs-lookup"><span data-stu-id="ef942-219">, we run the job on three Linux nodes and each node has four cores.</span></span>
   
   ![Job resources][job_resources]
6. <span data-ttu-id="ef942-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span><span class="sxs-lookup"><span data-stu-id="ef942-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span>    
7. <span data-ttu-id="ef942-222">On the **Task Details and I/O Redirection** page, set the following values:</span><span class="sxs-lookup"><span data-stu-id="ef942-222">On the **Task Details and I/O Redirection** page, set the following values:</span></span>
   
   * <span data-ttu-id="ef942-223">**Command line** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="ef942-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="ef942-224">The preceding command line is a single command without line breaks.</span><span class="sxs-lookup"><span data-stu-id="ef942-224">The preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="ef942-225">It wraps to appear on several lines under **Command line**.</span><span class="sxs-lookup"><span data-stu-id="ef942-225">It wraps to appear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="ef942-226">**Working directory** - /namd2</span><span class="sxs-lookup"><span data-stu-id="ef942-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="ef942-227">**Minimum** - 3</span><span class="sxs-lookup"><span data-stu-id="ef942-227">**Minimum** - 3</span></span>
     
     ![Task details][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="ef942-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span><span class="sxs-lookup"><span data-stu-id="ef942-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span></span> <span data-ttu-id="ef942-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="ef942-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span></span> <span data-ttu-id="ef942-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span><span class="sxs-lookup"><span data-stu-id="ef942-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="ef942-232">Click **OK** and then click **Submit** to run this job.</span><span class="sxs-lookup"><span data-stu-id="ef942-232">Click **OK** and then click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="ef942-233">By default, HPC Pack submits the job as your current logged-on user account.</span><span class="sxs-lookup"><span data-stu-id="ef942-233">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="ef942-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="ef942-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span></span>
   
   ![Job credentials][creds]
   
   <span data-ttu-id="ef942-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span><span class="sxs-lookup"><span data-stu-id="ef942-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="ef942-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span><span class="sxs-lookup"><span data-stu-id="ef942-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="ef942-238">The job takes several minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="ef942-238">The job takes several minutes to finish.</span></span>
10. <span data-ttu-id="ef942-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="ef942-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="ef942-240">Optionally, start VMD to view your job results.</span><span class="sxs-lookup"><span data-stu-id="ef942-240">Optionally, start VMD to view your job results.</span></span> <span data-ttu-id="ef942-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="ef942-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span></span> <span data-ttu-id="ef942-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span><span class="sxs-lookup"><span data-stu-id="ef942-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Job results][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="ef942-244">Sample files</span><span class="sxs-lookup"><span data-stu-id="ef942-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="ef942-245">Sample XML configuration file for cluster deployment by PowerShell script</span><span class="sxs-lookup"><span data-stu-id="ef942-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="ef942-246">Sample cred.xml file</span><span class="sxs-lookup"><span data-stu-id="ef942-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="ef942-247">Sample hpccharmrun.sh script</span><span class="sxs-lookup"><span data-stu-id="ef942-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run the charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create the nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write the head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into the nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/keygen.png
[keys]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/keys.png
[namd_job]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/namd_job.png
[job_resources]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/job_resources.png
[creds]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/creds.png
[task_details]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/task_details.png
[vmd_view]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/hpcpack-cluster-namd/vmd_view.png







