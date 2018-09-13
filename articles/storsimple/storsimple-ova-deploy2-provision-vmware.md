---
title: Deploy StorSimple Virtual Array - Provision in VMware
description: This second tutorial in StorSimple Virtual Array deployment series involves provisioning a virtual device in VMware.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: cdd897af-9c27-4a1b-9e3c-dd1f80de4a0b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/12/2016
ms.author: alkohli
ms.openlocfilehash: 8e7f69383f6fe8a9af0dfa19028b266b23b2b324
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552784"
---
# <a name="deploy-storsimple-virtual-array---provision-a-virtual-array-in-vmware"></a><span data-ttu-id="fbe41-103">Deploy StorSimple Virtual Array - Provision a Virtual Array in VMware</span><span class="sxs-lookup"><span data-stu-id="fbe41-103">Deploy StorSimple Virtual Array - Provision a Virtual Array in VMware</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a><span data-ttu-id="fbe41-104">Overview</span><span class="sxs-lookup"><span data-stu-id="fbe41-104">Overview</span></span>
<span data-ttu-id="fbe41-105">This provisioning tutorial applies to StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices or StorSimple virtual devices) running March 2016 general availability (GA) release.</span><span class="sxs-lookup"><span data-stu-id="fbe41-105">This provisioning tutorial applies to StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices or StorSimple virtual devices) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="fbe41-106">This tutorial describes how to provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span><span class="sxs-lookup"><span data-stu-id="fbe41-106">This tutorial describes how to provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span> <span data-ttu-id="fbe41-107">This article applies to the deployment of StorSimple Virtual Arrays in Azure classic portal as well as Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbe41-107">This article applies to the deployment of StorSimple Virtual Arrays in Azure classic portal as well as Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="fbe41-108">You will need administrator privileges to provision and connect to a virtual device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-108">You will need administrator privileges to provision and connect to a virtual device.</span></span> <span data-ttu-id="fbe41-109">The provisioning and initial setup can take around 10 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="fbe41-109">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="fbe41-110">Provisioning prerequisites</span><span class="sxs-lookup"><span data-stu-id="fbe41-110">Provisioning prerequisites</span></span>
<span data-ttu-id="fbe41-111">Here you will find the prerequisites to provision a virtual device on a host system running VMware ESXi 5.5 and above.</span><span class="sxs-lookup"><span data-stu-id="fbe41-111">Here you will find the prerequisites to provision a virtual device on a host system running VMware ESXi 5.5 and above.</span></span>

### <a name="for-the-storsimple-manager-service"></a><span data-ttu-id="fbe41-112">For the StorSimple Manager service</span><span class="sxs-lookup"><span data-stu-id="fbe41-112">For the StorSimple Manager service</span></span>
<span data-ttu-id="fbe41-113">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="fbe41-113">Before you begin, make sure that:</span></span>

* <span data-ttu-id="fbe41-114">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-ova-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="fbe41-114">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-ova-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="fbe41-115">You have downloaded the virtual device image for VMware from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fbe41-115">You have downloaded the virtual device image for VMware from the Azure portal.</span></span> <span data-ttu-id="fbe41-116">For more information, see [Step 3: Download the virtual device image](storsimple-ova-deploy1-portal-prep.md#step-3-download-the-virtual-device-image).</span><span class="sxs-lookup"><span data-stu-id="fbe41-116">For more information, see [Step 3: Download the virtual device image](storsimple-ova-deploy1-portal-prep.md#step-3-download-the-virtual-device-image).</span></span>

### <a name="for-the-storsimple-virtual-device"></a><span data-ttu-id="fbe41-117">For the StorSimple virtual device</span><span class="sxs-lookup"><span data-stu-id="fbe41-117">For the StorSimple virtual device</span></span>
<span data-ttu-id="fbe41-118">Before you deploy a virtual device, make sure that:</span><span class="sxs-lookup"><span data-stu-id="fbe41-118">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="fbe41-119">You have access to a host system running Hyper-V (2008 R2 or later) that can be used to a provision a device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-119">You have access to a host system running Hyper-V (2008 R2 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="fbe41-120">The host system is able to dedicate the following resources to provision your virtual device:</span><span class="sxs-lookup"><span data-stu-id="fbe41-120">The host system is able to dedicate the following resources to provision your virtual device:</span></span>
  
  * <span data-ttu-id="fbe41-121">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="fbe41-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="fbe41-122">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="fbe41-122">At least 8 GB of RAM.</span></span>
  * <span data-ttu-id="fbe41-123">One network interface.</span><span class="sxs-lookup"><span data-stu-id="fbe41-123">One network interface.</span></span>
  * <span data-ttu-id="fbe41-124">A 500 GB virtual disk for system data.</span><span class="sxs-lookup"><span data-stu-id="fbe41-124">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-network-in-datacenter"></a><span data-ttu-id="fbe41-125">For the network in datacenter</span><span class="sxs-lookup"><span data-stu-id="fbe41-125">For the network in datacenter</span></span>
<span data-ttu-id="fbe41-126">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="fbe41-126">Before you begin, make sure that:</span></span>

* <span data-ttu-id="fbe41-127">You have reviewed the networking requirements to deploy a StorSimple virtual device and configured the datacenter network as per the requirements.</span><span class="sxs-lookup"><span data-stu-id="fbe41-127">You have reviewed the networking requirements to deploy a StorSimple virtual device and configured the datacenter network as per the requirements.</span></span> <span data-ttu-id="fbe41-128">For more information, see [StorSimple Virtual Array system requirements](storsimple-ova-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="fbe41-128">For more information, see [StorSimple Virtual Array system requirements](storsimple-ova-system-requirements.md).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="fbe41-129">Step-by-step provisioning</span><span class="sxs-lookup"><span data-stu-id="fbe41-129">Step-by-step provisioning</span></span>
<span data-ttu-id="fbe41-130">To provision and connect to a virtual device, you will need to perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fbe41-130">To provision and connect to a virtual device, you will need to perform the following steps:</span></span>

1. <span data-ttu-id="fbe41-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span><span class="sxs-lookup"><span data-stu-id="fbe41-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span></span>
2. <span data-ttu-id="fbe41-132">Provision a virtual device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="fbe41-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="fbe41-133">Start the virtual device and get the IP address.</span><span class="sxs-lookup"><span data-stu-id="fbe41-133">Start the virtual device and get the IP address.</span></span>

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="fbe41-134">Step 1: Ensure host system meets minimum virtual device requirements</span><span class="sxs-lookup"><span data-stu-id="fbe41-134">Step 1: Ensure host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="fbe41-135">To create a virtual device, you will need:</span><span class="sxs-lookup"><span data-stu-id="fbe41-135">To create a virtual device, you will need:</span></span>

* <span data-ttu-id="fbe41-136">Access to a host system running VMware ESXi Server 5.5 and above.</span><span class="sxs-lookup"><span data-stu-id="fbe41-136">Access to a host system running VMware ESXi Server 5.5 and above.</span></span>
* <span data-ttu-id="fbe41-137">VMware vSphere client on your system to manage the ESXi host.</span><span class="sxs-lookup"><span data-stu-id="fbe41-137">VMware vSphere client on your system to manage the ESXi host.</span></span>
  
  * <span data-ttu-id="fbe41-138">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="fbe41-138">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="fbe41-139">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="fbe41-139">At least 8 GB of RAM.</span></span>
  * <span data-ttu-id="fbe41-140">One network interface connected to the network capable of routing traffic to Internet.</span><span class="sxs-lookup"><span data-stu-id="fbe41-140">One network interface connected to the network capable of routing traffic to Internet.</span></span> <span data-ttu-id="fbe41-141">The minimum Internet bandwidth should be 5 Mbps to allow for optimal working of the device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-141">The minimum Internet bandwidth should be 5 Mbps to allow for optimal working of the device.</span></span>
  * <span data-ttu-id="fbe41-142">A 500 GB virtual disk for data.</span><span class="sxs-lookup"><span data-stu-id="fbe41-142">A 500 GB virtual disk for data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="fbe41-143">Step 2: Provision a virtual device in hypervisor</span><span class="sxs-lookup"><span data-stu-id="fbe41-143">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="fbe41-144">Perform the following steps to provision a virtual device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="fbe41-144">Perform the following steps to provision a virtual device in your hypervisor.</span></span>

1. <span data-ttu-id="fbe41-145">Copy the virtual device image on your system.</span><span class="sxs-lookup"><span data-stu-id="fbe41-145">Copy the virtual device image on your system.</span></span> <span data-ttu-id="fbe41-146">This is the image that you have downloaded through the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="fbe41-146">This is the image that you have downloaded through the Azure classic portal.</span></span> 
   
   1. <span data-ttu-id="fbe41-147">Ensure that this is the latest image file that you have downloaded.</span><span class="sxs-lookup"><span data-stu-id="fbe41-147">Ensure that this is the latest image file that you have downloaded.</span></span> <span data-ttu-id="fbe41-148">If you downloaded the image earlier, download it again to ensure you have the latest image.</span><span class="sxs-lookup"><span data-stu-id="fbe41-148">If you downloaded the image earlier, download it again to ensure you have the latest image.</span></span> <span data-ttu-id="fbe41-149">The latest image has two files (instead of one).</span><span class="sxs-lookup"><span data-stu-id="fbe41-149">The latest image has two files (instead of one).</span></span>
   2. <span data-ttu-id="fbe41-150">Make a note of the location where you copied the image as you will be using this later in the procedure.</span><span class="sxs-lookup"><span data-stu-id="fbe41-150">Make a note of the location where you copied the image as you will be using this later in the procedure.</span></span>
2. <span data-ttu-id="fbe41-151">Log into the ESXi server using the vSphere client.</span><span class="sxs-lookup"><span data-stu-id="fbe41-151">Log into the ESXi server using the vSphere client.</span></span> <span data-ttu-id="fbe41-152">You will need to have administrator privileges to create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbe41-152">You will need to have administrator privileges to create a virtual machine.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image1.png)
3. <span data-ttu-id="fbe41-153">In the vSphere client, in the inventory section in the left pane, select the ESXi Server.</span><span class="sxs-lookup"><span data-stu-id="fbe41-153">In the vSphere client, in the inventory section in the left pane, select the ESXi Server.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image2.png)
4. <span data-ttu-id="fbe41-154">You will first upload the VMDK to the ESXi server.</span><span class="sxs-lookup"><span data-stu-id="fbe41-154">You will first upload the VMDK to the ESXi server.</span></span> <span data-ttu-id="fbe41-155">Navigate to the **Configuration** tab in the right pane.</span><span class="sxs-lookup"><span data-stu-id="fbe41-155">Navigate to the **Configuration** tab in the right pane.</span></span> <span data-ttu-id="fbe41-156">Under **Hardware**, select **Storage**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-156">Under **Hardware**, select **Storage**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image3.png)
5. <span data-ttu-id="fbe41-157">In the right pane, under **Datastores**, select the datastore where you want to upload the VMDK.</span><span class="sxs-lookup"><span data-stu-id="fbe41-157">In the right pane, under **Datastores**, select the datastore where you want to upload the VMDK.</span></span> <span data-ttu-id="fbe41-158">The datastore must have enough free space for the OS and data disks.</span><span class="sxs-lookup"><span data-stu-id="fbe41-158">The datastore must have enough free space for the OS and data disks.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image4.png)
6. <span data-ttu-id="fbe41-159">Right click and select **Browse Datastore**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-159">Right click and select **Browse Datastore**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image5.png)
7. <span data-ttu-id="fbe41-160">A **Datastore Browser** window will appear.</span><span class="sxs-lookup"><span data-stu-id="fbe41-160">A **Datastore Browser** window will appear.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image6.png)
8. <span data-ttu-id="fbe41-161">In the tool bar, click ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image7.png) icon to create a new folder.</span><span class="sxs-lookup"><span data-stu-id="fbe41-161">In the tool bar, click ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image7.png) icon to create a new folder.</span></span> <span data-ttu-id="fbe41-162">Specify the folder name and make a note of it.</span><span class="sxs-lookup"><span data-stu-id="fbe41-162">Specify the folder name and make a note of it.</span></span> <span data-ttu-id="fbe41-163">You will use this folder name later when creating a virtual machine (recommended best practice).</span><span class="sxs-lookup"><span data-stu-id="fbe41-163">You will use this folder name later when creating a virtual machine (recommended best practice).</span></span> <span data-ttu-id="fbe41-164">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-164">Click **OK**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image8.png)
9. <span data-ttu-id="fbe41-165">The new folder will appear in the left pane of the **Datastore Browser**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-165">The new folder will appear in the left pane of the **Datastore Browser**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image9.png)
10. <span data-ttu-id="fbe41-166">Click the Upload icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image10.png) and select **Upload File**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-166">Click the Upload icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image10.png) and select **Upload File**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image11.png)
11. <span data-ttu-id="fbe41-167">You should now browse and point to the VMDK files that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="fbe41-167">You should now browse and point to the VMDK files that you downloaded.</span></span> <span data-ttu-id="fbe41-168">There will be two files.</span><span class="sxs-lookup"><span data-stu-id="fbe41-168">There will be two files.</span></span> <span data-ttu-id="fbe41-169">Select a file to upload.</span><span class="sxs-lookup"><span data-stu-id="fbe41-169">Select a file to upload.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image12m.png)
12. <span data-ttu-id="fbe41-170">Click **Open**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-170">Click **Open**.</span></span> <span data-ttu-id="fbe41-171">This will now start the upload of the VMDK file to the specified datastore.</span><span class="sxs-lookup"><span data-stu-id="fbe41-171">This will now start the upload of the VMDK file to the specified datastore.</span></span> <span data-ttu-id="fbe41-172">It may take several minutes for the file to upload.</span><span class="sxs-lookup"><span data-stu-id="fbe41-172">It may take several minutes for the file to upload.</span></span>
13. <span data-ttu-id="fbe41-173">After the upload is complete, you will see the file in the datastore in the folder you created.</span><span class="sxs-lookup"><span data-stu-id="fbe41-173">After the upload is complete, you will see the file in the datastore in the folder you created.</span></span> 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image14.png)
    
    <span data-ttu-id="fbe41-174">You will now need to upload the second VMDK file to the same datastore.</span><span class="sxs-lookup"><span data-stu-id="fbe41-174">You will now need to upload the second VMDK file to the same datastore.</span></span>
14. <span data-ttu-id="fbe41-175">Return to the vSphere client window.</span><span class="sxs-lookup"><span data-stu-id="fbe41-175">Return to the vSphere client window.</span></span> <span data-ttu-id="fbe41-176">With ESXi server selected, right-click and select **New Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-176">With ESXi server selected, right-click and select **New Virtual Machine**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image15.png)
15. <span data-ttu-id="fbe41-177">A **Create New Virtual Machine** window will appear.</span><span class="sxs-lookup"><span data-stu-id="fbe41-177">A **Create New Virtual Machine** window will appear.</span></span> <span data-ttu-id="fbe41-178">On the **Configuration** page, select the **Custom** option.</span><span class="sxs-lookup"><span data-stu-id="fbe41-178">On the **Configuration** page, select the **Custom** option.</span></span> <span data-ttu-id="fbe41-179">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-179">Click **Next**.</span></span>
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image16.png)
16. <span data-ttu-id="fbe41-180">On the **Name and Location** page, specify the name of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbe41-180">On the **Name and Location** page, specify the name of your virtual machine.</span></span> <span data-ttu-id="fbe41-181">This name should match the folder name (recommended best practice) you specified earlier in Step 8.</span><span class="sxs-lookup"><span data-stu-id="fbe41-181">This name should match the folder name (recommended best practice) you specified earlier in Step 8.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image17.png)
17. <span data-ttu-id="fbe41-182">On the **Storage** page, select a datastore you want to use to provision your VM.</span><span class="sxs-lookup"><span data-stu-id="fbe41-182">On the **Storage** page, select a datastore you want to use to provision your VM.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image18.png)
18. <span data-ttu-id="fbe41-183">On the **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-183">On the **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span></span> <span data-ttu-id="fbe41-184">Note that versions 8 to 11 are all supported.</span><span class="sxs-lookup"><span data-stu-id="fbe41-184">Note that versions 8 to 11 are all supported.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image19.png)
19. <span data-ttu-id="fbe41-185">On the **Guest Operating System** page, select the **Guest Operating System** as **Windows**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-185">On the **Guest Operating System** page, select the **Guest Operating System** as **Windows**.</span></span> <span data-ttu-id="fbe41-186">For **Version**, from the dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-186">For **Version**, from the dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image20.png)
20. <span data-ttu-id="fbe41-187">On the **CPUs** page, adjust the **Number of virtual sockets** and **Number of cores per virtual socket** so that the **Total number of cores** is 4 (or more).</span><span class="sxs-lookup"><span data-stu-id="fbe41-187">On the **CPUs** page, adjust the **Number of virtual sockets** and **Number of cores per virtual socket** so that the **Total number of cores** is 4 (or more).</span></span> <span data-ttu-id="fbe41-188">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-188">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image21.png)
21. <span data-ttu-id="fbe41-189">On the **Memory** page, specify 8 GB (or more) of RAM.</span><span class="sxs-lookup"><span data-stu-id="fbe41-189">On the **Memory** page, specify 8 GB (or more) of RAM.</span></span> <span data-ttu-id="fbe41-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-190">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image22.png)
22. <span data-ttu-id="fbe41-191">On the **Network** page, specify the number of the network interfaces.</span><span class="sxs-lookup"><span data-stu-id="fbe41-191">On the **Network** page, specify the number of the network interfaces.</span></span> <span data-ttu-id="fbe41-192">The minimum requirement is one network interface.</span><span class="sxs-lookup"><span data-stu-id="fbe41-192">The minimum requirement is one network interface.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image23.png)
23. <span data-ttu-id="fbe41-193">On the **SCSI Controller** page, accept the default **LSI Logic SAS controller**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-193">On the **SCSI Controller** page, accept the default **LSI Logic SAS controller**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image24.png)
24. <span data-ttu-id="fbe41-194">On the **Select a Disk** page, choose **Use an existing virtual disk**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-194">On the **Select a Disk** page, choose **Use an existing virtual disk**.</span></span> <span data-ttu-id="fbe41-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-195">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image25.png)
25. <span data-ttu-id="fbe41-196">On the **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-196">On the **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span></span> <span data-ttu-id="fbe41-197">This opens a **Browse Datastores** dialog.</span><span class="sxs-lookup"><span data-stu-id="fbe41-197">This opens a **Browse Datastores** dialog.</span></span> <span data-ttu-id="fbe41-198">Navigate to the location where you uploaded the VMDK.</span><span class="sxs-lookup"><span data-stu-id="fbe41-198">Navigate to the location where you uploaded the VMDK.</span></span> <span data-ttu-id="fbe41-199">You will now see only one file in the datastore as the two files that you initially uploaded have been merged.</span><span class="sxs-lookup"><span data-stu-id="fbe41-199">You will now see only one file in the datastore as the two files that you initially uploaded have been merged.</span></span> <span data-ttu-id="fbe41-200">Select the file and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-200">Select the file and click **OK**.</span></span> <span data-ttu-id="fbe41-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-201">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image26.png)
26. <span data-ttu-id="fbe41-202">On the **Advanced Options** page, accept the default and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-202">On the **Advanced Options** page, accept the default and click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image27.png)
27. <span data-ttu-id="fbe41-203">On the **Ready to Complete** page, review all the settings associated with the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbe41-203">On the **Ready to Complete** page, review all the settings associated with the new virtual machine.</span></span> <span data-ttu-id="fbe41-204">Check **Edit the virtual machine settings before completion**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-204">Check **Edit the virtual machine settings before completion**.</span></span> <span data-ttu-id="fbe41-205">Click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-205">Click **Continue**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image28.png)
28. <span data-ttu-id="fbe41-206">On the **Virtual Machines Properties** page, in the **Hardware** tab, locate the device hardware.</span><span class="sxs-lookup"><span data-stu-id="fbe41-206">On the **Virtual Machines Properties** page, in the **Hardware** tab, locate the device hardware.</span></span> <span data-ttu-id="fbe41-207">Select **New Hard Disk**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-207">Select **New Hard Disk**.</span></span> <span data-ttu-id="fbe41-208">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-208">Click **Add**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image29.png)
29. <span data-ttu-id="fbe41-209">This brings up the **Add Hardware** window.</span><span class="sxs-lookup"><span data-stu-id="fbe41-209">This brings up the **Add Hardware** window.</span></span> <span data-ttu-id="fbe41-210">On the **Device Type** page, under **Choose the type of device you wish to add**, select **Hard Disk** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-210">On the **Device Type** page, under **Choose the type of device you wish to add**, select **Hard Disk** and click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image30.png)
30. <span data-ttu-id="fbe41-211">On the **Select a Disk** page, choose **Create a new virtual disk**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-211">On the **Select a Disk** page, choose **Create a new virtual disk**.</span></span> <span data-ttu-id="fbe41-212">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-212">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image31.png)
31. <span data-ttu-id="fbe41-213">On the **Create a Disk** page, change the **Disk Size** to 500 GB (or more).</span><span class="sxs-lookup"><span data-stu-id="fbe41-213">On the **Create a Disk** page, change the **Disk Size** to 500 GB (or more).</span></span> <span data-ttu-id="fbe41-214">Under **Disk Provisioning**, select **Thin Provision**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-214">Under **Disk Provisioning**, select **Thin Provision**.</span></span> <span data-ttu-id="fbe41-215">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-215">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image32.png)
32. <span data-ttu-id="fbe41-216">On the **Advanced Options** page, accept the default.</span><span class="sxs-lookup"><span data-stu-id="fbe41-216">On the **Advanced Options** page, accept the default.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image33.png)
33. <span data-ttu-id="fbe41-217">On the **Ready to Complete** page, review the disk options.</span><span class="sxs-lookup"><span data-stu-id="fbe41-217">On the **Ready to Complete** page, review the disk options.</span></span> <span data-ttu-id="fbe41-218">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-218">Click **Finish**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image34.png)
34. <span data-ttu-id="fbe41-219">You will now return to the Virtual Machine Properties page.</span><span class="sxs-lookup"><span data-stu-id="fbe41-219">You will now return to the Virtual Machine Properties page.</span></span> <span data-ttu-id="fbe41-220">A new hard disk is added to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbe41-220">A new hard disk is added to your virtual machine.</span></span> <span data-ttu-id="fbe41-221">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-221">Click **Finish**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image35.png)
35. <span data-ttu-id="fbe41-222">With your virtual machine selected in the right pane, navigate to the **Summary** tab. Review the settings for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbe41-222">With your virtual machine selected in the right pane, navigate to the **Summary** tab. Review the settings for your virtual machine.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image36.png)

<span data-ttu-id="fbe41-223">Your virtual machine is now provisioned.</span><span class="sxs-lookup"><span data-stu-id="fbe41-223">Your virtual machine is now provisioned.</span></span> <span data-ttu-id="fbe41-224">The next step is to power on this machine and get the IP address.</span><span class="sxs-lookup"><span data-stu-id="fbe41-224">The next step is to power on this machine and get the IP address.</span></span>

## <a name="step-3-start-the-virtual-device-and-get-the-ip"></a><span data-ttu-id="fbe41-225">Step 3: Start the virtual device and get the IP</span><span class="sxs-lookup"><span data-stu-id="fbe41-225">Step 3: Start the virtual device and get the IP</span></span>
<span data-ttu-id="fbe41-226">Perform the following steps to start your virtual device and connect to it.</span><span class="sxs-lookup"><span data-stu-id="fbe41-226">Perform the following steps to start your virtual device and connect to it.</span></span>

#### <a name="to-start-the-virtual-device"></a><span data-ttu-id="fbe41-227">To start the virtual device</span><span class="sxs-lookup"><span data-stu-id="fbe41-227">To start the virtual device</span></span>
1. <span data-ttu-id="fbe41-228">Start the virtual device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-228">Start the virtual device.</span></span> <span data-ttu-id="fbe41-229">In the vSphere Configuration Manager, in the left pane, select your device and right-click to bring up the context menu.</span><span class="sxs-lookup"><span data-stu-id="fbe41-229">In the vSphere Configuration Manager, in the left pane, select your device and right-click to bring up the context menu.</span></span> <span data-ttu-id="fbe41-230">Select **Power** and then select **Power on**.</span><span class="sxs-lookup"><span data-stu-id="fbe41-230">Select **Power** and then select **Power on**.</span></span> <span data-ttu-id="fbe41-231">This should power on your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fbe41-231">This should power on your virtual machine.</span></span> <span data-ttu-id="fbe41-232">You can view the status in the bottom **Recent Tasks** pane of the vSphere client.</span><span class="sxs-lookup"><span data-stu-id="fbe41-232">You can view the status in the bottom **Recent Tasks** pane of the vSphere client.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image37.png)
2. <span data-ttu-id="fbe41-233">The setup tasks will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="fbe41-233">The setup tasks will take a few minutes to complete.</span></span> <span data-ttu-id="fbe41-234">Once the device is running, navigate to the **Console** tab. Send Ctrl+Alt+Delete to log into the device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-234">Once the device is running, navigate to the **Console** tab. Send Ctrl+Alt+Delete to log into the device.</span></span> <span data-ttu-id="fbe41-235">Alternatively, you can point the cursor on the console window and press Ctrl+Alt+Insert.</span><span class="sxs-lookup"><span data-stu-id="fbe41-235">Alternatively, you can point the cursor on the console window and press Ctrl+Alt+Insert.</span></span> <span data-ttu-id="fbe41-236">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="fbe41-236">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image38.png)
3. <span data-ttu-id="fbe41-237">For security reasons, the device administrator password expires at the first log on.</span><span class="sxs-lookup"><span data-stu-id="fbe41-237">For security reasons, the device administrator password expires at the first log on.</span></span> <span data-ttu-id="fbe41-238">You will be prompted to change the password.</span><span class="sxs-lookup"><span data-stu-id="fbe41-238">You will be prompted to change the password.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image39.png)
4. <span data-ttu-id="fbe41-239">Enter a password that contains at least 8 characters.</span><span class="sxs-lookup"><span data-stu-id="fbe41-239">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="fbe41-240">The password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="fbe41-240">The password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="fbe41-241">Reenter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="fbe41-241">Reenter the password to confirm it.</span></span> <span data-ttu-id="fbe41-242">You will be notified that the password has changed.</span><span class="sxs-lookup"><span data-stu-id="fbe41-242">You will be notified that the password has changed.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image40.png)
5. <span data-ttu-id="fbe41-243">After the password is successfully changed, the virtual device may reboot.</span><span class="sxs-lookup"><span data-stu-id="fbe41-243">After the password is successfully changed, the virtual device may reboot.</span></span> <span data-ttu-id="fbe41-244">Wait for the reboot to complete.</span><span class="sxs-lookup"><span data-stu-id="fbe41-244">Wait for the reboot to complete.</span></span> <span data-ttu-id="fbe41-245">The Windows PowerShell console of the device may be displayed along with a progress bar.</span><span class="sxs-lookup"><span data-stu-id="fbe41-245">The Windows PowerShell console of the device may be displayed along with a progress bar.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image41.png)
6. <span data-ttu-id="fbe41-246">Steps 6-8 only apply when booting up in a non DHCP environment.</span><span class="sxs-lookup"><span data-stu-id="fbe41-246">Steps 6-8 only apply when booting up in a non DHCP environment.</span></span> <span data-ttu-id="fbe41-247">If you are in a DHCP environment, then skip these steps and go to step 9.</span><span class="sxs-lookup"><span data-stu-id="fbe41-247">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="fbe41-248">If you booted up your device in non DHCP environment, you will see the following screen.</span><span class="sxs-lookup"><span data-stu-id="fbe41-248">If you booted up your device in non DHCP environment, you will see the following screen.</span></span> 
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image42m.png)
   
   <span data-ttu-id="fbe41-249">You will now need to configure the network.</span><span class="sxs-lookup"><span data-stu-id="fbe41-249">You will now need to configure the network.</span></span>
7. <span data-ttu-id="fbe41-250">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-250">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="fbe41-251">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="fbe41-251">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image43m.png)
8. <span data-ttu-id="fbe41-252">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span><span class="sxs-lookup"><span data-stu-id="fbe41-252">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="fbe41-253">An example is shown below:</span><span class="sxs-lookup"><span data-stu-id="fbe41-253">An example is shown below:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image44.png)

1. <span data-ttu-id="fbe41-254">After the initial setup is complete and the device has booted up, you will see the device banner text.</span><span class="sxs-lookup"><span data-stu-id="fbe41-254">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="fbe41-255">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-255">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="fbe41-256">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span><span class="sxs-lookup"><span data-stu-id="fbe41-256">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image45.png)
2. <span data-ttu-id="fbe41-257">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbe41-257">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="fbe41-258">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-258">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="fbe41-259">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span><span class="sxs-lookup"><span data-stu-id="fbe41-259">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>
   
   1. <span data-ttu-id="fbe41-260">To enable the FIPS mode, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fbe41-260">To enable the FIPS mode, run the following cmdlet:</span></span>
      
       `Enter-HcsFIPSMode`
   2. <span data-ttu-id="fbe41-261">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span><span class="sxs-lookup"><span data-stu-id="fbe41-261">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="fbe41-262">You can either enable or disable FIPS mode on your device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-262">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="fbe41-263">Alternating the device between FIPS and non-FIPS mode is not supported.</span><span class="sxs-lookup"><span data-stu-id="fbe41-263">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
      > 
      > 

<span data-ttu-id="fbe41-264">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span><span class="sxs-lookup"><span data-stu-id="fbe41-264">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span></span> <span data-ttu-id="fbe41-265">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span><span class="sxs-lookup"><span data-stu-id="fbe41-265">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="fbe41-266">You can then restart and connect to the device.</span><span class="sxs-lookup"><span data-stu-id="fbe41-266">You can then restart and connect to the device.</span></span> <span data-ttu-id="fbe41-267">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="fbe41-267">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-vmware/image46.png)

<span data-ttu-id="fbe41-268">If you face any other error during the initial configuration using the local web UI, refer to the following workflows in [Manage your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="fbe41-268">If you face any other error during the initial configuration using the local web UI, refer to the following workflows in [Manage your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span></span>

* <span data-ttu-id="fbe41-269">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="fbe41-269">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="fbe41-270">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package)..</span><span class="sxs-lookup"><span data-stu-id="fbe41-270">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package)..</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbe41-271">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbe41-271">Next steps</span></span>
* [<span data-ttu-id="fbe41-272">Set up your StorSimple Virtual Array as a file server</span><span class="sxs-lookup"><span data-stu-id="fbe41-272">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-ova-deploy3-fs-setup.md)
* [<span data-ttu-id="fbe41-273">Set up your StorSimple Virtual Array as an iSCSI server</span><span class="sxs-lookup"><span data-stu-id="fbe41-273">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-ova-deploy3-iscsi-setup.md)















































