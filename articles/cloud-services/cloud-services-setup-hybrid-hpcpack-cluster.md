---
title: Set up a hybrid HPC cluster with Microsoft HPC Pack | Microsoft Docs
description: Learn how to use Microsoft HPC Pack and Azure to set up a small, hybrid high performance computing (HPC) cluster
services: cloud-services
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-service-management,hpc-pack
ms.assetid: b11f3e1b-b9e1-4b0d-8455-6607b88814e9
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: ee776a292a4a99f44b8481127d33150a3a7ad583
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663095"
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="61342-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span><span class="sxs-lookup"><span data-stu-id="61342-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="61342-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="61342-105">The cluster will consist of an on-premises head node (a computer running the Windows Server operating system and HPC Pack) and some compute nodes you deploy on-demand as worker role instances in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="61342-105">The cluster will consist of an on-premises head node (a computer running the Windows Server operating system and HPC Pack) and some compute nodes you deploy on-demand as worker role instances in an Azure cloud service.</span></span> <span data-ttu-id="61342-106">You can then run compute jobs on the hybrid cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Hybrid HPC cluster][Overview] 

<span data-ttu-id="61342-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand compute resources in Azure to run compute-intensive applications.</span><span class="sxs-lookup"><span data-stu-id="61342-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand compute resources in Azure to run compute-intensive applications.</span></span>

<span data-ttu-id="61342-109">This tutorial assumes no prior experience with compute clusters or HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="61342-109">This tutorial assumes no prior experience with compute clusters or HPC Pack 2012 R2.</span></span> <span data-ttu-id="61342-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="61342-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="61342-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="61342-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="61342-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61342-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61342-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61342-113">Prerequisites</span></span>
* <span data-ttu-id="61342-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="61342-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="61342-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - This computer will be the head node of the HPC cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - This computer will be the head node of the HPC cluster.</span></span> <span data-ttu-id="61342-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="61342-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="61342-117">The computer must be joined to an Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="61342-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="61342-118">For a test scenario with a fresh installation of Windows Server, you can add the Active Directory Domain Services server role and promote the head node computer as a domain controller in a new domain forest (see the documentation for Windows Server).</span><span class="sxs-lookup"><span data-stu-id="61342-118">For a test scenario with a fresh installation of Windows Server, you can add the Active Directory Domain Services server role and promote the head node computer as a domain controller in a new domain forest (see the documentation for Windows Server).</span></span>
  * <span data-ttu-id="61342-119">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span><span class="sxs-lookup"><span data-stu-id="61342-119">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="61342-120">Verify that important and critical updates are installed.</span><span class="sxs-lookup"><span data-stu-id="61342-120">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="61342-121">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer or to a network location.</span><span class="sxs-lookup"><span data-stu-id="61342-121">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer or to a network location.</span></span> <span data-ttu-id="61342-122">Choose installation files in the same language as your installation of Windows Server.</span><span class="sxs-lookup"><span data-stu-id="61342-122">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="61342-123">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span><span class="sxs-lookup"><span data-stu-id="61342-123">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="61342-124">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="61342-124">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="61342-125">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="61342-125">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="61342-126">**TCP connectivity on port 443** from the head node to Azure.</span><span class="sxs-lookup"><span data-stu-id="61342-126">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="61342-127">Install HPC Pack on the head node</span><span class="sxs-lookup"><span data-stu-id="61342-127">Install HPC Pack on the head node</span></span>
<span data-ttu-id="61342-128">You first install Microsoft HPC Pack on your on-premises computer running Windows Server that will be the head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-128">You first install Microsoft HPC Pack on your on-premises computer running Windows Server that will be the head node of the cluster.</span></span>

1. <span data-ttu-id="61342-129">Log on to the head node by using a domain account that has local Administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="61342-129">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>
2. <span data-ttu-id="61342-130">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span><span class="sxs-lookup"><span data-stu-id="61342-130">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>
3. <span data-ttu-id="61342-131">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span><span class="sxs-lookup"><span data-stu-id="61342-131">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>
   
    ![HPC Pack 2012 Setup][install_hpc1]
4. <span data-ttu-id="61342-133">On the **Microsoft Software User Agreement page**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-133">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>
5. <span data-ttu-id="61342-134">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-134">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>
   
    ![Select Installation Type][install_hpc2]
6. <span data-ttu-id="61342-136">The wizard runs several pre-installation tests.</span><span class="sxs-lookup"><span data-stu-id="61342-136">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="61342-137">Click **Next** on the **Installation Rules** page if all tests pass.</span><span class="sxs-lookup"><span data-stu-id="61342-137">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="61342-138">Otherwise, review the information provided and make any necessary changes in your environment.</span><span class="sxs-lookup"><span data-stu-id="61342-138">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="61342-139">Then run the tests again or if necessary start the Installation Wizard again.</span><span class="sxs-lookup"><span data-stu-id="61342-139">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
   
    ![Installation Rules][install_hpc3]
7. <span data-ttu-id="61342-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span>
   
    ![DB Configuration][install_hpc4]
8. <span data-ttu-id="61342-143">Accept default selections on the remaining pages of the wizard.</span><span class="sxs-lookup"><span data-stu-id="61342-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="61342-144">On the **Install Required Components** page, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="61342-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Install][install_hpc6]
9. <span data-ttu-id="61342-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="61342-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="61342-147">(You will start HPC Cluster Manager in a later step.)</span><span class="sxs-lookup"><span data-stu-id="61342-147">(You will start HPC Cluster Manager in a later step.)</span></span>
   
    ![Finish][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="61342-149">Prepare the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="61342-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="61342-150">Use the [Azure classic portal](https://manage.windowsazure.com) to perform the following steps with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="61342-150">Use the [Azure classic portal](https://manage.windowsazure.com) to perform the following steps with your Azure subscription.</span></span> <span data-ttu-id="61342-151">These are needed so you can later deploy Azure nodes from the on-premises head node.</span><span class="sxs-lookup"><span data-stu-id="61342-151">These are needed so you can later deploy Azure nodes from the on-premises head node.</span></span> <span data-ttu-id="61342-152">Detailed procedures are in the next sections.</span><span class="sxs-lookup"><span data-stu-id="61342-152">Detailed procedures are in the next sections.</span></span>

* <span data-ttu-id="61342-153">Upload a management certificate (needed for secure connections between the head node and the Azure services)</span><span class="sxs-lookup"><span data-stu-id="61342-153">Upload a management certificate (needed for secure connections between the head node and the Azure services)</span></span>
* <span data-ttu-id="61342-154">Create an Azure cloud service in which Azure nodes (worker role instances) will run</span><span class="sxs-lookup"><span data-stu-id="61342-154">Create an Azure cloud service in which Azure nodes (worker role instances) will run</span></span>
* <span data-ttu-id="61342-155">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="61342-155">Create an Azure storage account</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="61342-156">Also make a note of your Azure subscription ID, which you will need later.</span><span class="sxs-lookup"><span data-stu-id="61342-156">Also make a note of your Azure subscription ID, which you will need later.</span></span> <span data-ttu-id="61342-157">Find this in the classic portal by clicking **Settings** > **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="61342-157">Find this in the classic portal by clicking **Settings** > **Subscriptions**.</span></span>
  > 
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="61342-158">Upload the default management certificate</span><span class="sxs-lookup"><span data-stu-id="61342-158">Upload the default management certificate</span></span>
<span data-ttu-id="61342-159">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span><span class="sxs-lookup"><span data-stu-id="61342-159">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="61342-160">This certificate is provided for testing purposes and proof-of-concept deployments.</span><span class="sxs-lookup"><span data-stu-id="61342-160">This certificate is provided for testing purposes and proof-of-concept deployments.</span></span>

1. <span data-ttu-id="61342-161">From the head node computer, sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="61342-161">From the head node computer, sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="61342-162">Click **Settings** > **Management Certificates**.</span><span class="sxs-lookup"><span data-stu-id="61342-162">Click **Settings** > **Management Certificates**.</span></span>
3. <span data-ttu-id="61342-163">On the command bar, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="61342-163">On the command bar, click **Upload**.</span></span>
   
    ![Certificate Settings][upload_cert1]
4. <span data-ttu-id="61342-165">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="61342-165">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="61342-166">Then, click the **Check** button.</span><span class="sxs-lookup"><span data-stu-id="61342-166">Then, click the **Check** button.</span></span>
   
    ![Upload Certificate][install_hpc10]

<span data-ttu-id="61342-168">You will see **Default HPC Azure Management** in the list of management certificates.</span><span class="sxs-lookup"><span data-stu-id="61342-168">You will see **Default HPC Azure Management** in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="61342-169">Create an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="61342-169">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="61342-170">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span><span class="sxs-lookup"><span data-stu-id="61342-170">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="61342-171">In the classic portal, on the command bar, click **New**.</span><span class="sxs-lookup"><span data-stu-id="61342-171">In the classic portal, on the command bar, click **New**.</span></span>
2. <span data-ttu-id="61342-172">Click **Compute** > **Cloud Service** > **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="61342-172">Click **Compute** > **Cloud Service** > **Quick Create**.</span></span>
3. <span data-ttu-id="61342-173">Type a URL for the cloud service, and then click **Create Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="61342-173">Type a URL for the cloud service, and then click **Create Cloud Service**.</span></span>
   
    ![Create Service][createservice1]

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="61342-175">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="61342-175">Create an Azure storage account</span></span>
1. <span data-ttu-id="61342-176">In the classic portal, on the command bar, click **New**.</span><span class="sxs-lookup"><span data-stu-id="61342-176">In the classic portal, on the command bar, click **New**.</span></span>
2. <span data-ttu-id="61342-177">Click **Data Services** > **Storage** > **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="61342-177">Click **Data Services** > **Storage** > **Quick Create**.</span></span>
3. <span data-ttu-id="61342-178">Type a URL for the account, and then click **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="61342-178">Type a URL for the account, and then click **Create Storage Account**.</span></span>
   
    ![Create Storage][createstorage1]

## <a name="configure-the-head-node"></a><span data-ttu-id="61342-180">Configure the head node</span><span class="sxs-lookup"><span data-stu-id="61342-180">Configure the head node</span></span>
<span data-ttu-id="61342-181">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span><span class="sxs-lookup"><span data-stu-id="61342-181">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="61342-182">On the head node, start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="61342-182">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="61342-183">If the **Select Head Node** dialog box appears, click **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="61342-183">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="61342-184">The **Deployment To-do List** appears.</span><span class="sxs-lookup"><span data-stu-id="61342-184">The **Deployment To-do List** appears.</span></span>
2. <span data-ttu-id="61342-185">Under **Required deployment tasks**, click **Configure your network**.</span><span class="sxs-lookup"><span data-stu-id="61342-185">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configure Network][config_hpc2]
3. <span data-ttu-id="61342-187">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span><span class="sxs-lookup"><span data-stu-id="61342-187">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span>
   
    ![Topology 5][config_hpc3]
   
   > [!NOTE]
   > <span data-ttu-id="61342-189">This is the simplest configuration for demonstration purposes, because the head node only needs a single network adapter to connect to Active Directory and the Internet.</span><span class="sxs-lookup"><span data-stu-id="61342-189">This is the simplest configuration for demonstration purposes, because the head node only needs a single network adapter to connect to Active Directory and the Internet.</span></span> <span data-ttu-id="61342-190">This tutorial does not cover cluster scenarios that require additional networks.</span><span class="sxs-lookup"><span data-stu-id="61342-190">This tutorial does not cover cluster scenarios that require additional networks.</span></span>
   > 
   > 
4. <span data-ttu-id="61342-191">Click **Next** to accept default values on the remaining pages of the wizard.</span><span class="sxs-lookup"><span data-stu-id="61342-191">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="61342-192">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span><span class="sxs-lookup"><span data-stu-id="61342-192">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>
5. <span data-ttu-id="61342-193">In the **Deployment To-do List**, click **Provide installation credentials**.</span><span class="sxs-lookup"><span data-stu-id="61342-193">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>
6. <span data-ttu-id="61342-194">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="61342-194">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="61342-195">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="61342-195">Then click **OK**.</span></span>
   
    ![Installation Credentials][config_hpc6]
   
   > [!NOTE]
   > <span data-ttu-id="61342-197">HPC Pack services only use installation credentials to deploy domain-joined compute nodes.</span><span class="sxs-lookup"><span data-stu-id="61342-197">HPC Pack services only use installation credentials to deploy domain-joined compute nodes.</span></span> <span data-ttu-id="61342-198">The Azure nodes you add in this tutorial are not domain-joined.</span><span class="sxs-lookup"><span data-stu-id="61342-198">The Azure nodes you add in this tutorial are not domain-joined.</span></span>
   > 
   > 
7. <span data-ttu-id="61342-199">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span><span class="sxs-lookup"><span data-stu-id="61342-199">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>
8. <span data-ttu-id="61342-200">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="61342-200">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span>
   
    ![Node Naming][config_hpc8]
   
   > [!NOTE]
   > <span data-ttu-id="61342-202">The naming series only generates names for domain-joined compute nodes.</span><span class="sxs-lookup"><span data-stu-id="61342-202">The naming series only generates names for domain-joined compute nodes.</span></span> <span data-ttu-id="61342-203">Azure worker nodes are named automatically.</span><span class="sxs-lookup"><span data-stu-id="61342-203">Azure worker nodes are named automatically.</span></span>
   > 
   > 
9. <span data-ttu-id="61342-204">In the **Deployment To-do List**, click **Create a node template**.</span><span class="sxs-lookup"><span data-stu-id="61342-204">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="61342-205">You will use the node template to add Azure nodes to the cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-205">You will use the node template to add Azure nodes to the cluster.</span></span>
10. <span data-ttu-id="61342-206">In the Create Node Template Wizard, do the following:</span><span class="sxs-lookup"><span data-stu-id="61342-206">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="61342-207">a.</span><span class="sxs-lookup"><span data-stu-id="61342-207">a.</span></span> <span data-ttu-id="61342-208">On the **Choose Node Template Type** page, click **Azure node template**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-208">On the **Choose Node Template Type** page, click **Azure node template**, and then click **Next**.</span></span>
    
    ![Node Template][config_hpc10]
    
    <span data-ttu-id="61342-210">b.</span><span class="sxs-lookup"><span data-stu-id="61342-210">b.</span></span> <span data-ttu-id="61342-211">Click **Next** to accept the default template name.</span><span class="sxs-lookup"><span data-stu-id="61342-211">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="61342-212">c.</span><span class="sxs-lookup"><span data-stu-id="61342-212">c.</span></span> <span data-ttu-id="61342-213">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span><span class="sxs-lookup"><span data-stu-id="61342-213">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="61342-214">Then, in **Management certificate**, click **Browse** and select **Default HPC Azure Management.**</span><span class="sxs-lookup"><span data-stu-id="61342-214">Then, in **Management certificate**, click **Browse** and select **Default HPC Azure Management.**</span></span> <span data-ttu-id="61342-215">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-215">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc12]
    
    <span data-ttu-id="61342-217">d.</span><span class="sxs-lookup"><span data-stu-id="61342-217">d.</span></span> <span data-ttu-id="61342-218">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="61342-218">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="61342-219">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-219">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc13]
    
    <span data-ttu-id="61342-221">e.</span><span class="sxs-lookup"><span data-stu-id="61342-221">e.</span></span> <span data-ttu-id="61342-222">Click **Next** to accept default values on the remaining pages of the wizard.</span><span class="sxs-lookup"><span data-stu-id="61342-222">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="61342-223">Then, on the **Review** tab, click **Create** to create the node template.</span><span class="sxs-lookup"><span data-stu-id="61342-223">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="61342-224">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="61342-224">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="61342-225">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span><span class="sxs-lookup"><span data-stu-id="61342-225">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="61342-226">Add Azure nodes to the cluster</span><span class="sxs-lookup"><span data-stu-id="61342-226">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="61342-227">You now use the node template to add Azure nodes to the cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-227">You now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="61342-228">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time as role instances in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="61342-228">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time as role instances in the cloud service.</span></span> <span data-ttu-id="61342-229">Your subscription only gets charged for Azure nodes after the role instances are running in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="61342-229">Your subscription only gets charged for Azure nodes after the role instances are running in the cloud service.</span></span>

<span data-ttu-id="61342-230">For this tutorial you will add two Small nodes.</span><span class="sxs-lookup"><span data-stu-id="61342-230">For this tutorial you will add two Small nodes.</span></span>

1. <span data-ttu-id="61342-231">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in recent versions of HPC Pack), in the **Actions** pane, click **Add Node**.</span><span class="sxs-lookup"><span data-stu-id="61342-231">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in recent versions of HPC Pack), in the **Actions** pane, click **Add Node**.</span></span>
   
    ![Add Node][add_node1]
2. <span data-ttu-id="61342-233">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-233">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Add Azure Node][add_node1_1]
3. <span data-ttu-id="61342-235">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span><span class="sxs-lookup"><span data-stu-id="61342-235">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="61342-236">Then specify **2** nodes of size **Small**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="61342-236">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Specify Nodes][add_node2]
   
    <span data-ttu-id="61342-238">For details about the available sizes, see [Sizes for Cloud Services](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="61342-238">For details about the available sizes, see [Sizes for Cloud Services](cloud-services-sizes-specs.md).</span></span>
4. <span data-ttu-id="61342-239">On the **Completing the Add Node Wizard** page, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="61342-239">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
   
     <span data-ttu-id="61342-240">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="61342-240">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="61342-241">Both are in the **Not-Deployed** state.</span><span class="sxs-lookup"><span data-stu-id="61342-241">Both are in the **Not-Deployed** state.</span></span>
   
    ![Added Nodes][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="61342-243">Start the Azure nodes</span><span class="sxs-lookup"><span data-stu-id="61342-243">Start the Azure nodes</span></span>
<span data-ttu-id="61342-244">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span><span class="sxs-lookup"><span data-stu-id="61342-244">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="61342-245">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in recent versions of HPC Pack), click one or both nodes and then, in the **Actions** pane, click **Start**.</span><span class="sxs-lookup"><span data-stu-id="61342-245">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in recent versions of HPC Pack), click one or both nodes and then, in the **Actions** pane, click **Start**.</span></span>
   
   ![Start Nodes][add_node4]
2. <span data-ttu-id="61342-247">In the **Stop Windows Azure nodes** dialog box, click **Start**.</span><span class="sxs-lookup"><span data-stu-id="61342-247">In the **Stop Windows Azure nodes** dialog box, click **Start**.</span></span>
   
    ![Start Nodes][add_node5]
   
    <span data-ttu-id="61342-249">The nodes transition to the **Provisioning** state.</span><span class="sxs-lookup"><span data-stu-id="61342-249">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="61342-250">View the provisioning log to track the provisioning progress.</span><span class="sxs-lookup"><span data-stu-id="61342-250">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Provision Nodes][add_node6]
3. <span data-ttu-id="61342-252">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span><span class="sxs-lookup"><span data-stu-id="61342-252">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="61342-253">In this state the role instances are running but will not yet accept cluster jobs.</span><span class="sxs-lookup"><span data-stu-id="61342-253">In this state the role instances are running but will not yet accept cluster jobs.</span></span>
4. <span data-ttu-id="61342-254">To confirm that the role instances are running, in the [classic portal](https://manage.windowsazure.com), click **Cloud Services** > *your_cloud_service_name* > **Instances**.</span><span class="sxs-lookup"><span data-stu-id="61342-254">To confirm that the role instances are running, in the [classic portal](https://manage.windowsazure.com), click **Cloud Services** > *your_cloud_service_name* > **Instances**.</span></span>
   
    ![Running Instances][view_instances1]
   
    <span data-ttu-id="61342-256">You will see two worker role instances are running in the service.</span><span class="sxs-lookup"><span data-stu-id="61342-256">You will see two worker role instances are running in the service.</span></span> <span data-ttu-id="61342-257">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span><span class="sxs-lookup"><span data-stu-id="61342-257">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>
5. <span data-ttu-id="61342-258">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="61342-258">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Offline Nodes][add_node7]
   
    <span data-ttu-id="61342-260">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span><span class="sxs-lookup"><span data-stu-id="61342-260">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="61342-261">Run a command across the cluster</span><span class="sxs-lookup"><span data-stu-id="61342-261">Run a command across the cluster</span></span>
<span data-ttu-id="61342-262">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="61342-262">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="61342-263">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span><span class="sxs-lookup"><span data-stu-id="61342-263">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="61342-264">On the head node, open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="61342-264">On the head node, open a command prompt.</span></span>
2. <span data-ttu-id="61342-265">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="61342-265">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`
3. <span data-ttu-id="61342-266">You will see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="61342-266">You will see output similar to the following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="61342-268">Run a test job</span><span class="sxs-lookup"><span data-stu-id="61342-268">Run a test job</span></span>
<span data-ttu-id="61342-269">Now submit a test job that runs on the hybrid cluster.</span><span class="sxs-lookup"><span data-stu-id="61342-269">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="61342-270">This example is a very simple parametric sweep job (a type of intrinsically parallel computation).</span><span class="sxs-lookup"><span data-stu-id="61342-270">This example is a very simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="61342-271">This example runs subtasks that add an integer to itself by using the **set /a** command.</span><span class="sxs-lookup"><span data-stu-id="61342-271">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="61342-272">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span><span class="sxs-lookup"><span data-stu-id="61342-272">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="61342-273">In HPC Cluster Manager, in **Job Management**, in the **Actions** pane, click **New Parametric Sweep Job**.</span><span class="sxs-lookup"><span data-stu-id="61342-273">In HPC Cluster Manager, in **Job Management**, in the **Actions** pane, click **New Parametric Sweep Job**.</span></span>
   
    ![New Job][test_job1]
2. <span data-ttu-id="61342-275">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span><span class="sxs-lookup"><span data-stu-id="61342-275">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="61342-276">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span><span class="sxs-lookup"><span data-stu-id="61342-276">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Parametric Sweep][param_sweep1]
3. <span data-ttu-id="61342-278">When the job is finished, double-click the **My Sweep Task** job.</span><span class="sxs-lookup"><span data-stu-id="61342-278">When the job is finished, double-click the **My Sweep Task** job.</span></span>
4. <span data-ttu-id="61342-279">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span><span class="sxs-lookup"><span data-stu-id="61342-279">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Task Results][view_job361]
5. <span data-ttu-id="61342-281">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span><span class="sxs-lookup"><span data-stu-id="61342-281">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="61342-282">(Your cluster might show a different node name.)</span><span class="sxs-lookup"><span data-stu-id="61342-282">(Your cluster might show a different node name.)</span></span>
   
    ![Task Results][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="61342-284">Stop the Azure nodes</span><span class="sxs-lookup"><span data-stu-id="61342-284">Stop the Azure nodes</span></span>
<span data-ttu-id="61342-285">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span><span class="sxs-lookup"><span data-stu-id="61342-285">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="61342-286">This stops the cloud service and removes the Azure role instances.</span><span class="sxs-lookup"><span data-stu-id="61342-286">This stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="61342-287">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in recent versions of HPC Pack), select both Azure nodes.</span><span class="sxs-lookup"><span data-stu-id="61342-287">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in recent versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="61342-288">Then, in the **Actions** pane, click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="61342-288">Then, in the **Actions** pane, click **Stop**.</span></span>
   
    ![Stop Nodes][stop_node1]
2. <span data-ttu-id="61342-290">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="61342-290">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span>
   
    ![Stop Nodes][stop_node2]
3. <span data-ttu-id="61342-292">The nodes transition to the **Stopping** state.</span><span class="sxs-lookup"><span data-stu-id="61342-292">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="61342-293">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span><span class="sxs-lookup"><span data-stu-id="61342-293">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Not Deployed Nodes][stop_node4]
4. <span data-ttu-id="61342-295">To confirm that the role instances are no longer running in Azure, in the [classic portal](https://manage.windowsazure.com), click **Cloud Services** > *your_cloud_service_name* > **Instances**.</span><span class="sxs-lookup"><span data-stu-id="61342-295">To confirm that the role instances are no longer running in Azure, in the [classic portal](https://manage.windowsazure.com), click **Cloud Services** > *your_cloud_service_name* > **Instances**.</span></span> <span data-ttu-id="61342-296">No instances will be deployed in the production environment.</span><span class="sxs-lookup"><span data-stu-id="61342-296">No instances will be deployed in the production environment.</span></span>
   
    ![No Instances][view_instances2]
   
    <span data-ttu-id="61342-298">This completes the tutorial.</span><span class="sxs-lookup"><span data-stu-id="61342-298">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61342-299">Next steps</span><span class="sxs-lookup"><span data-stu-id="61342-299">Next steps</span></span>
* <span data-ttu-id="61342-300">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="61342-300">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="61342-301">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="61342-301">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="61342-302">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61342-302">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="61342-303">See [Big Compute in Azure: Technical Resources for Batch and High Performance Computing (HPC)](../batch/big-compute-resources.md) for more about the range of Big Compute and HPC cloud solutions in Azure.</span><span class="sxs-lookup"><span data-stu-id="61342-303">See [Big Compute in Azure: Technical Resources for Batch and High Performance Computing (HPC)](../batch/big-compute-resources.md) for more about the range of Big Compute and HPC cloud solutions in Azure.</span></span>

[Overview]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc2.png
[install_hpc3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc3.png
[install_hpc4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[upload_cert1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/upload_cert1.png
[createstorage1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/createstorage1.png
[createservice1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/createservice1.png
[config_hpc2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node5.png
[add_node6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node2.png
[stop_node4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png




































