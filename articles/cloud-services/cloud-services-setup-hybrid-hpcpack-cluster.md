---
title: Set up a hybrid HPC Pack cluster in Azure | Microsoft Docs
description: Learn how to use Microsoft HPC Pack and Azure to set up a small, hybrid high performance computing (HPC) cluster
services: cloud-services
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: hpc-pack
ms.assetid: ''
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: ad5c13723eef352148a40e3e7f4f2ff616867296
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781071"
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="4d634-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span><span class="sxs-lookup"><span data-stu-id="4d634-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="4d634-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="4d634-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="4d634-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="4d634-106">You can then run compute jobs on the hybrid cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Hybrid HPC cluster][Overview] 

<span data-ttu-id="4d634-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span><span class="sxs-lookup"><span data-stu-id="4d634-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="4d634-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4d634-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="4d634-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="4d634-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="4d634-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4d634-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="4d634-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d634-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d634-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4d634-113">Prerequisites</span></span>
* <span data-ttu-id="4d634-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="4d634-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="4d634-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="4d634-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="4d634-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="4d634-117">The computer must be joined to an Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="4d634-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="4d634-118">For test purposes, you can configure the head node computer as a domain controller.</span><span class="sxs-lookup"><span data-stu-id="4d634-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="4d634-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4d634-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="4d634-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span><span class="sxs-lookup"><span data-stu-id="4d634-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="4d634-121">Verify that important and critical updates are installed.</span><span class="sxs-lookup"><span data-stu-id="4d634-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="4d634-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span><span class="sxs-lookup"><span data-stu-id="4d634-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="4d634-123">Choose installation files in the same language as your installation of Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4d634-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="4d634-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span><span class="sxs-lookup"><span data-stu-id="4d634-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="4d634-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4d634-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="4d634-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4d634-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="4d634-127">**TCP connectivity on port 443** from the head node to Azure.</span><span class="sxs-lookup"><span data-stu-id="4d634-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="4d634-128">Install HPC Pack on the head node</span><span class="sxs-lookup"><span data-stu-id="4d634-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="4d634-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4d634-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="4d634-130">This computer becomes the head node of the cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="4d634-131">Log on to the head node by using a domain account that has local Administrator permissions.</span><span class="sxs-lookup"><span data-stu-id="4d634-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="4d634-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span><span class="sxs-lookup"><span data-stu-id="4d634-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="4d634-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span><span class="sxs-lookup"><span data-stu-id="4d634-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![HPC Pack 2012 Setup][install_hpc1]

4. <span data-ttu-id="4d634-135">On the **Microsoft Software User Agreement page**, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="4d634-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="4d634-137">The wizard runs several pre-installation tests.</span><span class="sxs-lookup"><span data-stu-id="4d634-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="4d634-138">Click **Next** on the **Installation Rules** page if all tests pass.</span><span class="sxs-lookup"><span data-stu-id="4d634-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="4d634-139">Otherwise, review the information provided and make any necessary changes in your environment.</span><span class="sxs-lookup"><span data-stu-id="4d634-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="4d634-140">Then run the tests again or if necessary start the Installation Wizard again.</span><span class="sxs-lookup"><span data-stu-id="4d634-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="4d634-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB Configuration][install_hpc4]

8. <span data-ttu-id="4d634-143">Accept default selections on the remaining pages of the wizard.</span><span class="sxs-lookup"><span data-stu-id="4d634-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="4d634-144">On the **Install Required Components** page, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="4d634-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Install][install_hpc6]

9. <span data-ttu-id="4d634-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4d634-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="4d634-147">(You start HPC Cluster Manager in a later step.)</span><span class="sxs-lookup"><span data-stu-id="4d634-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Finish][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="4d634-149">Prepare the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4d634-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="4d634-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="4d634-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="4d634-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span><span class="sxs-lookup"><span data-stu-id="4d634-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="4d634-152">Also make a note of your Azure subscription ID, which you need later.</span><span class="sxs-lookup"><span data-stu-id="4d634-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="4d634-153">Find the ID in **Subscriptions** in the portal.</span><span class="sxs-lookup"><span data-stu-id="4d634-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="4d634-154">Upload the default management certificate</span><span class="sxs-lookup"><span data-stu-id="4d634-154">Upload the default management certificate</span></span>
<span data-ttu-id="4d634-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span><span class="sxs-lookup"><span data-stu-id="4d634-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="4d634-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span><span class="sxs-lookup"><span data-stu-id="4d634-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="4d634-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d634-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4d634-158">Click **Subscriptions** > *your_subscription_name*.</span><span class="sxs-lookup"><span data-stu-id="4d634-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="4d634-159">Click **Management certificates** > **Upload**.</span><span class="sxs-lookup"><span data-stu-id="4d634-159">Click **Management certificates** > **Upload**.</span></span>

4. <span data-ttu-id="4d634-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="4d634-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="4d634-161">Then, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="4d634-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="4d634-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span><span class="sxs-lookup"><span data-stu-id="4d634-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="4d634-163">Create an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="4d634-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="4d634-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span><span class="sxs-lookup"><span data-stu-id="4d634-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="4d634-165">In the portal, click **Cloud services (classic)** > **+Add**.</span><span class="sxs-lookup"><span data-stu-id="4d634-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="4d634-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4d634-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="4d634-167">Create an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="4d634-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="4d634-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span><span class="sxs-lookup"><span data-stu-id="4d634-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="4d634-169">Type a name for the account, and select the **Classic** deployment model.</span><span class="sxs-lookup"><span data-stu-id="4d634-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="4d634-170">Choose a resource group and a location, and leave other settings at default values.</span><span class="sxs-lookup"><span data-stu-id="4d634-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="4d634-171">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4d634-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="4d634-172">Configure the head node</span><span class="sxs-lookup"><span data-stu-id="4d634-172">Configure the head node</span></span>
<span data-ttu-id="4d634-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span><span class="sxs-lookup"><span data-stu-id="4d634-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="4d634-174">On the head node, start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="4d634-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="4d634-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="4d634-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="4d634-176">The **Deployment To-do List** appears.</span><span class="sxs-lookup"><span data-stu-id="4d634-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="4d634-177">Under **Required deployment tasks**, click **Configure your network**.</span><span class="sxs-lookup"><span data-stu-id="4d634-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configure Network][config_hpc2]

3. <span data-ttu-id="4d634-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span><span class="sxs-lookup"><span data-stu-id="4d634-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="4d634-180">This network configuration is the simplest for demonstration purposes.</span><span class="sxs-lookup"><span data-stu-id="4d634-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![Topology 5][config_hpc3]
   
4. <span data-ttu-id="4d634-182">Click **Next** to accept default values on the remaining pages of the wizard.</span><span class="sxs-lookup"><span data-stu-id="4d634-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="4d634-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span><span class="sxs-lookup"><span data-stu-id="4d634-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="4d634-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span><span class="sxs-lookup"><span data-stu-id="4d634-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="4d634-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4d634-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="4d634-186">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d634-186">Then click **OK**.</span></span> 
   
    ![Installation Credentials][config_hpc6]
   
7. <span data-ttu-id="4d634-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span><span class="sxs-lookup"><span data-stu-id="4d634-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="4d634-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d634-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="4d634-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span><span class="sxs-lookup"><span data-stu-id="4d634-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Node Naming][config_hpc8]
   
9. <span data-ttu-id="4d634-192">In the **Deployment To-do List**, click **Create a node template**.</span><span class="sxs-lookup"><span data-stu-id="4d634-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="4d634-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="4d634-194">In the Create Node Template Wizard, do the following:</span><span class="sxs-lookup"><span data-stu-id="4d634-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="4d634-195">a.</span><span class="sxs-lookup"><span data-stu-id="4d634-195">a.</span></span> <span data-ttu-id="4d634-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Node Template][config_hpc10]
    
    <span data-ttu-id="4d634-198">b.</span><span class="sxs-lookup"><span data-stu-id="4d634-198">b.</span></span> <span data-ttu-id="4d634-199">Click **Next** to accept the default template name.</span><span class="sxs-lookup"><span data-stu-id="4d634-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="4d634-200">c.</span><span class="sxs-lookup"><span data-stu-id="4d634-200">c.</span></span> <span data-ttu-id="4d634-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span><span class="sxs-lookup"><span data-stu-id="4d634-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="4d634-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span><span class="sxs-lookup"><span data-stu-id="4d634-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="4d634-203">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-203">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc12]
    
    <span data-ttu-id="4d634-205">d.</span><span class="sxs-lookup"><span data-stu-id="4d634-205">d.</span></span> <span data-ttu-id="4d634-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="4d634-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="4d634-207">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-207">Then click **Next**.</span></span>
    
    ![Node Template][config_hpc13]
    
    <span data-ttu-id="4d634-209">e.</span><span class="sxs-lookup"><span data-stu-id="4d634-209">e.</span></span> <span data-ttu-id="4d634-210">Click **Next** to accept default values on the remaining pages of the wizard.</span><span class="sxs-lookup"><span data-stu-id="4d634-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="4d634-211">Then, on the **Review** tab, click **Create** to create the node template.</span><span class="sxs-lookup"><span data-stu-id="4d634-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4d634-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="4d634-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="4d634-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span><span class="sxs-lookup"><span data-stu-id="4d634-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="4d634-214">Add Azure nodes to the cluster</span><span class="sxs-lookup"><span data-stu-id="4d634-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="4d634-215">Now use the node template to add Azure nodes to the cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="4d634-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4d634-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="4d634-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4d634-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="4d634-218">Follow these steps to add two Small nodes.</span><span class="sxs-lookup"><span data-stu-id="4d634-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="4d634-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span><span class="sxs-lookup"><span data-stu-id="4d634-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Add Node][add_node1]

2. <span data-ttu-id="4d634-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Add Azure Node][add_node1_1]

3. <span data-ttu-id="4d634-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span><span class="sxs-lookup"><span data-stu-id="4d634-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="4d634-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4d634-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Specify Nodes][add_node2]
   
4. <span data-ttu-id="4d634-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="4d634-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="4d634-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="4d634-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="4d634-228">Both are in the **Not-Deployed** state.</span><span class="sxs-lookup"><span data-stu-id="4d634-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![Added Nodes][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="4d634-230">Start the Azure nodes</span><span class="sxs-lookup"><span data-stu-id="4d634-230">Start the Azure nodes</span></span>
<span data-ttu-id="4d634-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span><span class="sxs-lookup"><span data-stu-id="4d634-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="4d634-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span><span class="sxs-lookup"><span data-stu-id="4d634-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="4d634-233">Click **Start**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d634-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Start Nodes][add_node4]
   
    <span data-ttu-id="4d634-235">The nodes transition to the **Provisioning** state.</span><span class="sxs-lookup"><span data-stu-id="4d634-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="4d634-236">View the provisioning log to track the provisioning progress.</span><span class="sxs-lookup"><span data-stu-id="4d634-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Provision Nodes][add_node6]

3. <span data-ttu-id="4d634-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span><span class="sxs-lookup"><span data-stu-id="4d634-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="4d634-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span><span class="sxs-lookup"><span data-stu-id="4d634-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="4d634-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="4d634-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="4d634-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span><span class="sxs-lookup"><span data-stu-id="4d634-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="4d634-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span><span class="sxs-lookup"><span data-stu-id="4d634-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![Running Instances][view_instances1]

5. <span data-ttu-id="4d634-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span><span class="sxs-lookup"><span data-stu-id="4d634-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Offline Nodes][add_node7]
   
    <span data-ttu-id="4d634-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span><span class="sxs-lookup"><span data-stu-id="4d634-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="4d634-247">Run a command across the cluster</span><span class="sxs-lookup"><span data-stu-id="4d634-247">Run a command across the cluster</span></span>
<span data-ttu-id="4d634-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="4d634-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="4d634-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span><span class="sxs-lookup"><span data-stu-id="4d634-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="4d634-250">On the head node, open a command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4d634-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="4d634-251">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="4d634-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="4d634-252">If prompted, enter your cluster administrator password.</span><span class="sxs-lookup"><span data-stu-id="4d634-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="4d634-253">You should see command output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="4d634-253">You should see command output similar to the following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="4d634-255">Run a test job</span><span class="sxs-lookup"><span data-stu-id="4d634-255">Run a test job</span></span>
<span data-ttu-id="4d634-256">Now submit a test job that runs on the hybrid cluster.</span><span class="sxs-lookup"><span data-stu-id="4d634-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="4d634-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span><span class="sxs-lookup"><span data-stu-id="4d634-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="4d634-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span><span class="sxs-lookup"><span data-stu-id="4d634-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="4d634-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span><span class="sxs-lookup"><span data-stu-id="4d634-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="4d634-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span><span class="sxs-lookup"><span data-stu-id="4d634-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![New Job][test_job1]

2. <span data-ttu-id="4d634-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span><span class="sxs-lookup"><span data-stu-id="4d634-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="4d634-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span><span class="sxs-lookup"><span data-stu-id="4d634-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Parametric Sweep][param_sweep1]

3. <span data-ttu-id="4d634-265">When the job is finished, double-click the **My Sweep Task** job.</span><span class="sxs-lookup"><span data-stu-id="4d634-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="4d634-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span><span class="sxs-lookup"><span data-stu-id="4d634-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Task Results][view_job361]

5. <span data-ttu-id="4d634-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span><span class="sxs-lookup"><span data-stu-id="4d634-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="4d634-269">(Your cluster might show a different node name.)</span><span class="sxs-lookup"><span data-stu-id="4d634-269">(Your cluster might show a different node name.)</span></span>
   
    ![Task Results][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="4d634-271">Stop the Azure nodes</span><span class="sxs-lookup"><span data-stu-id="4d634-271">Stop the Azure nodes</span></span>
<span data-ttu-id="4d634-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span><span class="sxs-lookup"><span data-stu-id="4d634-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="4d634-273">This step stops the cloud service and removes the Azure role instances.</span><span class="sxs-lookup"><span data-stu-id="4d634-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="4d634-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span><span class="sxs-lookup"><span data-stu-id="4d634-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="4d634-275">Then, click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="4d634-275">Then, click **Stop**.</span></span>
   
    ![Stop Nodes][stop_node1]

2. <span data-ttu-id="4d634-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span><span class="sxs-lookup"><span data-stu-id="4d634-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="4d634-278">The nodes transition to the **Stopping** state.</span><span class="sxs-lookup"><span data-stu-id="4d634-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="4d634-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span><span class="sxs-lookup"><span data-stu-id="4d634-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Not Deployed Nodes][stop_node4]

4. <span data-ttu-id="4d634-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="4d634-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="4d634-282">No instances are deployed in the production environment.</span><span class="sxs-lookup"><span data-stu-id="4d634-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="4d634-283">This completes the tutorial.</span><span class="sxs-lookup"><span data-stu-id="4d634-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d634-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d634-284">Next steps</span></span>
* <span data-ttu-id="4d634-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="4d634-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="4d634-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4d634-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="4d634-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4d634-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
