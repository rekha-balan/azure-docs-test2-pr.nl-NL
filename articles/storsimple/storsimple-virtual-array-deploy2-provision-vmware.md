---
title: Provision StorSimple Virtual Array in VMware | Microsoft Docs
description: This second tutorial in StorSimple Virtual Array deployment series involves provisioning a virtual device in VMware.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90ad73c9d0361af80b297fd202d1f699df9b5dfa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553601"
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a><span data-ttu-id="2f91e-103">Deploy StorSimple Virtual Array - Provision in VMware</span><span class="sxs-lookup"><span data-stu-id="2f91e-103">Deploy StorSimple Virtual Array - Provision in VMware</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a><span data-ttu-id="2f91e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2f91e-104">Overview</span></span>
<span data-ttu-id="2f91e-105">This tutorial describes how to provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span><span class="sxs-lookup"><span data-stu-id="2f91e-105">This tutorial describes how to provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.5 and above.</span></span> <span data-ttu-id="2f91e-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and the Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="2f91e-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and the Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="2f91e-107">You need administrator privileges to provision and connect to a virtual device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-107">You need administrator privileges to provision and connect to a virtual device.</span></span> <span data-ttu-id="2f91e-108">The provisioning and initial setup can take around 10 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="2f91e-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="2f91e-109">Provisioning prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f91e-109">Provisioning prerequisites</span></span>
<span data-ttu-id="2f91e-110">The prerequisites to provision a virtual device on a host system running VMware ESXi 5.5 and above, are as follows.</span><span class="sxs-lookup"><span data-stu-id="2f91e-110">The prerequisites to provision a virtual device on a host system running VMware ESXi 5.5 and above, are as follows.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="2f91e-111">For the StorSimple Device Manager service</span><span class="sxs-lookup"><span data-stu-id="2f91e-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="2f91e-112">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="2f91e-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2f91e-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="2f91e-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="2f91e-114">You have downloaded the virtual device image for VMware from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f91e-114">You have downloaded the virtual device image for VMware from the Azure portal.</span></span> <span data-ttu-id="2f91e-115">For more information, see **Step 3: Download the virtual device image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="2f91e-115">For more information, see **Step 3: Download the virtual device image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

### <a name="for-the-storsimple-virtual-device"></a><span data-ttu-id="2f91e-116">For the StorSimple virtual device</span><span class="sxs-lookup"><span data-stu-id="2f91e-116">For the StorSimple virtual device</span></span>
<span data-ttu-id="2f91e-117">Before you deploy a virtual device, make sure that:</span><span class="sxs-lookup"><span data-stu-id="2f91e-117">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="2f91e-118">You have access to a host system running Hyper-V (2008 R2 or later) that can be used to a provision a device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-118">You have access to a host system running Hyper-V (2008 R2 or later) that can be used to a provision a device.</span></span>
* <span data-ttu-id="2f91e-119">The host system is able to dedicate the following resources to provision your virtual device:</span><span class="sxs-lookup"><span data-stu-id="2f91e-119">The host system is able to dedicate the following resources to provision your virtual device:</span></span>

  * <span data-ttu-id="2f91e-120">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="2f91e-120">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="2f91e-121">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="2f91e-121">At least 8 GB of RAM.</span></span> <span data-ttu-id="2f91e-122">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span><span class="sxs-lookup"><span data-stu-id="2f91e-122">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="2f91e-123">You need 16 GB RAM to support 2 - 4 million files.</span><span class="sxs-lookup"><span data-stu-id="2f91e-123">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="2f91e-124">One network interface.</span><span class="sxs-lookup"><span data-stu-id="2f91e-124">One network interface.</span></span>
  * <span data-ttu-id="2f91e-125">A 500 GB virtual disk for system data.</span><span class="sxs-lookup"><span data-stu-id="2f91e-125">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-network-in-datacenter"></a><span data-ttu-id="2f91e-126">For the network in datacenter</span><span class="sxs-lookup"><span data-stu-id="2f91e-126">For the network in datacenter</span></span>
<span data-ttu-id="2f91e-127">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="2f91e-127">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2f91e-128">You have reviewed the networking requirements to deploy a StorSimple virtual device and configured the datacenter network as per the requirements.</span><span class="sxs-lookup"><span data-stu-id="2f91e-128">You have reviewed the networking requirements to deploy a StorSimple virtual device and configured the datacenter network as per the requirements.</span></span> 

## <a name="step-by-step-provisioning"></a><span data-ttu-id="2f91e-129">Step-by-step provisioning</span><span class="sxs-lookup"><span data-stu-id="2f91e-129">Step-by-step provisioning</span></span>
<span data-ttu-id="2f91e-130">To provision and connect to a virtual device, you need to perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f91e-130">To provision and connect to a virtual device, you need to perform the following steps:</span></span>

1. <span data-ttu-id="2f91e-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span><span class="sxs-lookup"><span data-stu-id="2f91e-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span></span>
2. <span data-ttu-id="2f91e-132">Provision a virtual device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="2f91e-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="2f91e-133">Start the virtual device and get the IP address.</span><span class="sxs-lookup"><span data-stu-id="2f91e-133">Start the virtual device and get the IP address.</span></span>

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="2f91e-134">Step 1: Ensure host system meets minimum virtual device requirements</span><span class="sxs-lookup"><span data-stu-id="2f91e-134">Step 1: Ensure host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="2f91e-135">To create a virtual device, you will need:</span><span class="sxs-lookup"><span data-stu-id="2f91e-135">To create a virtual device, you will need:</span></span>

* <span data-ttu-id="2f91e-136">Access to a host system running VMware ESXi Server 5.5 and above.</span><span class="sxs-lookup"><span data-stu-id="2f91e-136">Access to a host system running VMware ESXi Server 5.5 and above.</span></span>
* <span data-ttu-id="2f91e-137">VMware vSphere client on your system to manage the ESXi host.</span><span class="sxs-lookup"><span data-stu-id="2f91e-137">VMware vSphere client on your system to manage the ESXi host.</span></span>

  * <span data-ttu-id="2f91e-138">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="2f91e-138">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="2f91e-139">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="2f91e-139">At least 8 GB of RAM.</span></span> <span data-ttu-id="2f91e-140">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span><span class="sxs-lookup"><span data-stu-id="2f91e-140">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="2f91e-141">You need 16 GB RAM to support 2 - 4 million files.</span><span class="sxs-lookup"><span data-stu-id="2f91e-141">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="2f91e-142">One network interface connected to the network capable of routing traffic to Internet.</span><span class="sxs-lookup"><span data-stu-id="2f91e-142">One network interface connected to the network capable of routing traffic to Internet.</span></span> <span data-ttu-id="2f91e-143">The minimum Internet bandwidth should be 5 Mbps to allow for optimal working of the device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-143">The minimum Internet bandwidth should be 5 Mbps to allow for optimal working of the device.</span></span>
  * <span data-ttu-id="2f91e-144">A 500 GB virtual disk for data.</span><span class="sxs-lookup"><span data-stu-id="2f91e-144">A 500 GB virtual disk for data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="2f91e-145">Step 2: Provision a virtual device in hypervisor</span><span class="sxs-lookup"><span data-stu-id="2f91e-145">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="2f91e-146">Perform the following steps to provision a virtual device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="2f91e-146">Perform the following steps to provision a virtual device in your hypervisor.</span></span>

1. <span data-ttu-id="2f91e-147">Copy the virtual device image on your system.</span><span class="sxs-lookup"><span data-stu-id="2f91e-147">Copy the virtual device image on your system.</span></span> <span data-ttu-id="2f91e-148">You downloaded this virtual image through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f91e-148">You downloaded this virtual image through the Azure portal.</span></span>

   1. <span data-ttu-id="2f91e-149">Ensure that you have downloaded the latest image file.</span><span class="sxs-lookup"><span data-stu-id="2f91e-149">Ensure that you have downloaded the latest image file.</span></span> <span data-ttu-id="2f91e-150">If you downloaded the image earlier, download it again to ensure you have the latest image.</span><span class="sxs-lookup"><span data-stu-id="2f91e-150">If you downloaded the image earlier, download it again to ensure you have the latest image.</span></span> <span data-ttu-id="2f91e-151">The latest image has two files (instead of one).</span><span class="sxs-lookup"><span data-stu-id="2f91e-151">The latest image has two files (instead of one).</span></span>
   2. <span data-ttu-id="2f91e-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span><span class="sxs-lookup"><span data-stu-id="2f91e-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>

2. <span data-ttu-id="2f91e-153">Log in to the ESXi server using the vSphere client.</span><span class="sxs-lookup"><span data-stu-id="2f91e-153">Log in to the ESXi server using the vSphere client.</span></span> <span data-ttu-id="2f91e-154">You need to have administrator privileges to create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f91e-154">You need to have administrator privileges to create a virtual machine.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. <span data-ttu-id="2f91e-155">In the vSphere client, in the inventory section in the left pane, select the ESXi Server.</span><span class="sxs-lookup"><span data-stu-id="2f91e-155">In the vSphere client, in the inventory section in the left pane, select the ESXi Server.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. <span data-ttu-id="2f91e-156">Upload the VMDK to the ESXi server.</span><span class="sxs-lookup"><span data-stu-id="2f91e-156">Upload the VMDK to the ESXi server.</span></span> <span data-ttu-id="2f91e-157">Navigate to the **Configuration** tab in the right pane.</span><span class="sxs-lookup"><span data-stu-id="2f91e-157">Navigate to the **Configuration** tab in the right pane.</span></span> <span data-ttu-id="2f91e-158">Under **Hardware**, select **Storage**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-158">Under **Hardware**, select **Storage**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. <span data-ttu-id="2f91e-159">In the right pane, under **Datastores**, select the datastore where you want to upload the VMDK.</span><span class="sxs-lookup"><span data-stu-id="2f91e-159">In the right pane, under **Datastores**, select the datastore where you want to upload the VMDK.</span></span> <span data-ttu-id="2f91e-160">The datastore must have enough free space for the OS and data disks.</span><span class="sxs-lookup"><span data-stu-id="2f91e-160">The datastore must have enough free space for the OS and data disks.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. <span data-ttu-id="2f91e-161">Right-click and select **Browse Datastore**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-161">Right-click and select **Browse Datastore**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. <span data-ttu-id="2f91e-162">A **Datastore Browser** window appears.</span><span class="sxs-lookup"><span data-stu-id="2f91e-162">A **Datastore Browser** window appears.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. <span data-ttu-id="2f91e-163">In the tool bar, click ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icon to create a new folder.</span><span class="sxs-lookup"><span data-stu-id="2f91e-163">In the tool bar, click ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icon to create a new folder.</span></span> <span data-ttu-id="2f91e-164">Specify the folder name and make a note of it.</span><span class="sxs-lookup"><span data-stu-id="2f91e-164">Specify the folder name and make a note of it.</span></span> <span data-ttu-id="2f91e-165">You will use this folder name later when creating a virtual machine (recommended best practice).</span><span class="sxs-lookup"><span data-stu-id="2f91e-165">You will use this folder name later when creating a virtual machine (recommended best practice).</span></span> <span data-ttu-id="2f91e-166">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-166">Click **OK**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. <span data-ttu-id="2f91e-167">The new folder appears in the left pane of the **Datastore Browser**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-167">The new folder appears in the left pane of the **Datastore Browser**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. <span data-ttu-id="2f91e-168">Click the Upload icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) and select **Upload File**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-168">Click the Upload icon ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) and select **Upload File**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. <span data-ttu-id="2f91e-169">Browse and point to the VMDK files that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="2f91e-169">Browse and point to the VMDK files that you downloaded.</span></span> <span data-ttu-id="2f91e-170">There are two files.</span><span class="sxs-lookup"><span data-stu-id="2f91e-170">There are two files.</span></span> <span data-ttu-id="2f91e-171">Select a file to upload.</span><span class="sxs-lookup"><span data-stu-id="2f91e-171">Select a file to upload.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. <span data-ttu-id="2f91e-172">Click **Open**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-172">Click **Open**.</span></span> <span data-ttu-id="2f91e-173">The upload of the VMDK file to the specified datastore starts.</span><span class="sxs-lookup"><span data-stu-id="2f91e-173">The upload of the VMDK file to the specified datastore starts.</span></span> <span data-ttu-id="2f91e-174">It may take several minutes for the file to upload.</span><span class="sxs-lookup"><span data-stu-id="2f91e-174">It may take several minutes for the file to upload.</span></span>
13. <span data-ttu-id="2f91e-175">After the upload is complete, you see the file in the datastore in the folder you created.</span><span class="sxs-lookup"><span data-stu-id="2f91e-175">After the upload is complete, you see the file in the datastore in the folder you created.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    <span data-ttu-id="2f91e-176">Now upload the second VMDK file to the same datastore.</span><span class="sxs-lookup"><span data-stu-id="2f91e-176">Now upload the second VMDK file to the same datastore.</span></span>
14. <span data-ttu-id="2f91e-177">Return to the vSphere client window.</span><span class="sxs-lookup"><span data-stu-id="2f91e-177">Return to the vSphere client window.</span></span> <span data-ttu-id="2f91e-178">With ESXi server selected, right-click and select **New Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-178">With ESXi server selected, right-click and select **New Virtual Machine**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. <span data-ttu-id="2f91e-179">A **Create New Virtual Machine** window will appear.</span><span class="sxs-lookup"><span data-stu-id="2f91e-179">A **Create New Virtual Machine** window will appear.</span></span> <span data-ttu-id="2f91e-180">On the **Configuration** page, select the **Custom** option.</span><span class="sxs-lookup"><span data-stu-id="2f91e-180">On the **Configuration** page, select the **Custom** option.</span></span> <span data-ttu-id="2f91e-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-181">Click **Next**.</span></span>
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. <span data-ttu-id="2f91e-182">On the **Name and Location** page, specify the name of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f91e-182">On the **Name and Location** page, specify the name of your virtual machine.</span></span> <span data-ttu-id="2f91e-183">This name should match the folder name (recommended best practice) you specified earlier in Step 8.</span><span class="sxs-lookup"><span data-stu-id="2f91e-183">This name should match the folder name (recommended best practice) you specified earlier in Step 8.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. <span data-ttu-id="2f91e-184">On the **Storage** page, select a datastore you want to use to provision your VM.</span><span class="sxs-lookup"><span data-stu-id="2f91e-184">On the **Storage** page, select a datastore you want to use to provision your VM.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. <span data-ttu-id="2f91e-185">On the **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-185">On the **Virtual Machine Version** page, select **Virtual Machine Version: 8**.</span></span> <span data-ttu-id="2f91e-186">Versions 8 to 11 are all supported.</span><span class="sxs-lookup"><span data-stu-id="2f91e-186">Versions 8 to 11 are all supported.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. <span data-ttu-id="2f91e-187">On the **Guest Operating System** page, select the **Guest Operating System** as **Windows**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-187">On the **Guest Operating System** page, select the **Guest Operating System** as **Windows**.</span></span> <span data-ttu-id="2f91e-188">For **Version**, from the dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-188">For **Version**, from the dropdown list, select **Microsoft Windows Server 2012 (64-bit)**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. <span data-ttu-id="2f91e-189">On the **CPUs** page, adjust the **Number of virtual sockets** and **Number of cores per virtual socket** so that the **Total number of cores** is 4 (or more).</span><span class="sxs-lookup"><span data-stu-id="2f91e-189">On the **CPUs** page, adjust the **Number of virtual sockets** and **Number of cores per virtual socket** so that the **Total number of cores** is 4 (or more).</span></span> <span data-ttu-id="2f91e-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-190">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. <span data-ttu-id="2f91e-191">On the **Memory** page, specify 8 GB (or more) of RAM.</span><span class="sxs-lookup"><span data-stu-id="2f91e-191">On the **Memory** page, specify 8 GB (or more) of RAM.</span></span> <span data-ttu-id="2f91e-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-192">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. <span data-ttu-id="2f91e-193">On the **Network** page, specify the number of the network interfaces.</span><span class="sxs-lookup"><span data-stu-id="2f91e-193">On the **Network** page, specify the number of the network interfaces.</span></span> <span data-ttu-id="2f91e-194">The minimum requirement is one network interface.</span><span class="sxs-lookup"><span data-stu-id="2f91e-194">The minimum requirement is one network interface.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. <span data-ttu-id="2f91e-195">On the **SCSI Controller** page, accept the default **LSI Logic SAS controller**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-195">On the **SCSI Controller** page, accept the default **LSI Logic SAS controller**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. <span data-ttu-id="2f91e-196">On the **Select a Disk** page, choose **Use an existing virtual disk**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-196">On the **Select a Disk** page, choose **Use an existing virtual disk**.</span></span> <span data-ttu-id="2f91e-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-197">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. <span data-ttu-id="2f91e-198">On the **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-198">On the **Select Existing Disk** page, under **Disk File Path**, click **Browse**.</span></span> <span data-ttu-id="2f91e-199">This opens a **Browse Datastores** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f91e-199">This opens a **Browse Datastores** dialog.</span></span> <span data-ttu-id="2f91e-200">Navigate to the location where you uploaded the VMDK.</span><span class="sxs-lookup"><span data-stu-id="2f91e-200">Navigate to the location where you uploaded the VMDK.</span></span> <span data-ttu-id="2f91e-201">You now see only one file in the datastore as the two files that you initially uploaded have been merged.</span><span class="sxs-lookup"><span data-stu-id="2f91e-201">You now see only one file in the datastore as the two files that you initially uploaded have been merged.</span></span> <span data-ttu-id="2f91e-202">Select the file and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-202">Select the file and click **OK**.</span></span> <span data-ttu-id="2f91e-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-203">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. <span data-ttu-id="2f91e-204">On the **Advanced Options** page, accept the default and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-204">On the **Advanced Options** page, accept the default and click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. <span data-ttu-id="2f91e-205">On the **Ready to Complete** page, review all the settings associated with the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f91e-205">On the **Ready to Complete** page, review all the settings associated with the new virtual machine.</span></span> <span data-ttu-id="2f91e-206">Check **Edit the virtual machine settings before completion**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-206">Check **Edit the virtual machine settings before completion**.</span></span> <span data-ttu-id="2f91e-207">Click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-207">Click **Continue**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. <span data-ttu-id="2f91e-208">On the **Virtual Machines Properties** page, in the **Hardware** tab, locate the device hardware.</span><span class="sxs-lookup"><span data-stu-id="2f91e-208">On the **Virtual Machines Properties** page, in the **Hardware** tab, locate the device hardware.</span></span> <span data-ttu-id="2f91e-209">Select **New Hard Disk**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-209">Select **New Hard Disk**.</span></span> <span data-ttu-id="2f91e-210">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-210">Click **Add**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. <span data-ttu-id="2f91e-211">You see a **Add Hardware** window.</span><span class="sxs-lookup"><span data-stu-id="2f91e-211">You see a **Add Hardware** window.</span></span> <span data-ttu-id="2f91e-212">On the **Device Type** page, under **Choose the type of device you wish to add**, select **Hard Disk**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-212">On the **Device Type** page, under **Choose the type of device you wish to add**, select **Hard Disk**, and click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. <span data-ttu-id="2f91e-213">On the **Select a Disk** page, choose **Create a new virtual disk**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-213">On the **Select a Disk** page, choose **Create a new virtual disk**.</span></span> <span data-ttu-id="2f91e-214">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-214">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. <span data-ttu-id="2f91e-215">On the **Create a Disk** page, change the **Disk Size** to 500 GB (or more).</span><span class="sxs-lookup"><span data-stu-id="2f91e-215">On the **Create a Disk** page, change the **Disk Size** to 500 GB (or more).</span></span> <span data-ttu-id="2f91e-216">While 500 GB is the minimum requirement, you can always provision a larger disk.</span><span class="sxs-lookup"><span data-stu-id="2f91e-216">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="2f91e-217">Note that you cannot expand or shrink the disk once provisioned.</span><span class="sxs-lookup"><span data-stu-id="2f91e-217">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="2f91e-218">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2f91e-218">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="2f91e-219">Under **Disk Provisioning**, select **Thin Provision**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-219">Under **Disk Provisioning**, select **Thin Provision**.</span></span> <span data-ttu-id="2f91e-220">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-220">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. <span data-ttu-id="2f91e-221">On the **Advanced Options** page, accept the default.</span><span class="sxs-lookup"><span data-stu-id="2f91e-221">On the **Advanced Options** page, accept the default.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. <span data-ttu-id="2f91e-222">On the **Ready to Complete** page, review the disk options.</span><span class="sxs-lookup"><span data-stu-id="2f91e-222">On the **Ready to Complete** page, review the disk options.</span></span> <span data-ttu-id="2f91e-223">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-223">Click **Finish**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. <span data-ttu-id="2f91e-224">Return to the Virtual Machine Properties page.</span><span class="sxs-lookup"><span data-stu-id="2f91e-224">Return to the Virtual Machine Properties page.</span></span> <span data-ttu-id="2f91e-225">A new hard disk is added to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f91e-225">A new hard disk is added to your virtual machine.</span></span> <span data-ttu-id="2f91e-226">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-226">Click **Finish**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. <span data-ttu-id="2f91e-227">With your virtual machine selected in the right pane, navigate to the **Summary** tab. Review the settings for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f91e-227">With your virtual machine selected in the right pane, navigate to the **Summary** tab. Review the settings for your virtual machine.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

<span data-ttu-id="2f91e-228">Your virtual machine is now provisioned.</span><span class="sxs-lookup"><span data-stu-id="2f91e-228">Your virtual machine is now provisioned.</span></span> <span data-ttu-id="2f91e-229">The next step is to power on this machine and get the IP address.</span><span class="sxs-lookup"><span data-stu-id="2f91e-229">The next step is to power on this machine and get the IP address.</span></span>

## <a name="step-3-start-the-virtual-device-and-get-the-ip"></a><span data-ttu-id="2f91e-230">Step 3: Start the virtual device and get the IP</span><span class="sxs-lookup"><span data-stu-id="2f91e-230">Step 3: Start the virtual device and get the IP</span></span>
<span data-ttu-id="2f91e-231">Perform the following steps to start your virtual device and connect to it.</span><span class="sxs-lookup"><span data-stu-id="2f91e-231">Perform the following steps to start your virtual device and connect to it.</span></span>

#### <a name="to-start-the-virtual-device"></a><span data-ttu-id="2f91e-232">To start the virtual device</span><span class="sxs-lookup"><span data-stu-id="2f91e-232">To start the virtual device</span></span>
1. <span data-ttu-id="2f91e-233">Start the virtual device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-233">Start the virtual device.</span></span> <span data-ttu-id="2f91e-234">In the vSphere Configuration Manager, in the left pane, select your device and right-click to bring up the context menu.</span><span class="sxs-lookup"><span data-stu-id="2f91e-234">In the vSphere Configuration Manager, in the left pane, select your device and right-click to bring up the context menu.</span></span> <span data-ttu-id="2f91e-235">Select **Power** and then select **Power on**.</span><span class="sxs-lookup"><span data-stu-id="2f91e-235">Select **Power** and then select **Power on**.</span></span> <span data-ttu-id="2f91e-236">This should power on your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2f91e-236">This should power on your virtual machine.</span></span> <span data-ttu-id="2f91e-237">You can view the status in the bottom **Recent Tasks** pane of the vSphere client.</span><span class="sxs-lookup"><span data-stu-id="2f91e-237">You can view the status in the bottom **Recent Tasks** pane of the vSphere client.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. <span data-ttu-id="2f91e-238">The setup tasks will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="2f91e-238">The setup tasks will take a few minutes to complete.</span></span> <span data-ttu-id="2f91e-239">Once the device is running, navigate to the **Console** tab. Send Ctrl+Alt+Delete to log in to the device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-239">Once the device is running, navigate to the **Console** tab. Send Ctrl+Alt+Delete to log in to the device.</span></span> <span data-ttu-id="2f91e-240">Alternatively, you can point the cursor on the console window and press Ctrl+Alt+Insert.</span><span class="sxs-lookup"><span data-stu-id="2f91e-240">Alternatively, you can point the cursor on the console window and press Ctrl+Alt+Insert.</span></span> <span data-ttu-id="2f91e-241">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="2f91e-241">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. <span data-ttu-id="2f91e-242">For security reasons, the device administrator password expires at the first logon.</span><span class="sxs-lookup"><span data-stu-id="2f91e-242">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="2f91e-243">You are prompted to change the password.</span><span class="sxs-lookup"><span data-stu-id="2f91e-243">You are prompted to change the password.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. <span data-ttu-id="2f91e-244">Enter a password that contains at least 8 characters.</span><span class="sxs-lookup"><span data-stu-id="2f91e-244">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="2f91e-245">The password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="2f91e-245">The password must contain 3 out of 4 of these requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="2f91e-246">Reenter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="2f91e-246">Reenter the password to confirm it.</span></span> <span data-ttu-id="2f91e-247">You will be notified that the password has changed.</span><span class="sxs-lookup"><span data-stu-id="2f91e-247">You will be notified that the password has changed.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. <span data-ttu-id="2f91e-248">After the password is successfully changed, the virtual device may reboot.</span><span class="sxs-lookup"><span data-stu-id="2f91e-248">After the password is successfully changed, the virtual device may reboot.</span></span> <span data-ttu-id="2f91e-249">Wait for the reboot to complete.</span><span class="sxs-lookup"><span data-stu-id="2f91e-249">Wait for the reboot to complete.</span></span> <span data-ttu-id="2f91e-250">The Windows PowerShell console of the device may be displayed along with a progress bar.</span><span class="sxs-lookup"><span data-stu-id="2f91e-250">The Windows PowerShell console of the device may be displayed along with a progress bar.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. <span data-ttu-id="2f91e-251">Steps 6-8 only apply when booting up in a non-DHCP environment.</span><span class="sxs-lookup"><span data-stu-id="2f91e-251">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="2f91e-252">If you are in a DHCP environment, then skip these steps and go to step 9.</span><span class="sxs-lookup"><span data-stu-id="2f91e-252">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="2f91e-253">If you booted up your device in non-DHCP environment, you will see the following screen.</span><span class="sxs-lookup"><span data-stu-id="2f91e-253">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   <span data-ttu-id="2f91e-254">Next, configure the network.</span><span class="sxs-lookup"><span data-stu-id="2f91e-254">Next, configure the network.</span></span>
7. <span data-ttu-id="2f91e-255">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-255">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="2f91e-256">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="2f91e-256">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. <span data-ttu-id="2f91e-257">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span><span class="sxs-lookup"><span data-stu-id="2f91e-257">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="2f91e-258">An example is shown below:</span><span class="sxs-lookup"><span data-stu-id="2f91e-258">An example is shown below:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. <span data-ttu-id="2f91e-259">After the initial setup is complete and the device has booted up, you will see the device banner text.</span><span class="sxs-lookup"><span data-stu-id="2f91e-259">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="2f91e-260">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-260">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="2f91e-261">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span><span class="sxs-lookup"><span data-stu-id="2f91e-261">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. <span data-ttu-id="2f91e-262">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="2f91e-262">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="2f91e-263">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-263">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="2f91e-264">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span><span class="sxs-lookup"><span data-stu-id="2f91e-264">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="2f91e-265">To enable the FIPS mode, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2f91e-265">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="2f91e-266">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span><span class="sxs-lookup"><span data-stu-id="2f91e-266">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="2f91e-267">You can either enable or disable FIPS mode on your device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-267">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="2f91e-268">Alternating the device between FIPS and non-FIPS mode is not supported.</span><span class="sxs-lookup"><span data-stu-id="2f91e-268">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="2f91e-269">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span><span class="sxs-lookup"><span data-stu-id="2f91e-269">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span></span> <span data-ttu-id="2f91e-270">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span><span class="sxs-lookup"><span data-stu-id="2f91e-270">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="2f91e-271">You can then restart and connect to the device.</span><span class="sxs-lookup"><span data-stu-id="2f91e-271">You can then restart and connect to the device.</span></span> <span data-ttu-id="2f91e-272">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="2f91e-272">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

<span data-ttu-id="2f91e-273">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span><span class="sxs-lookup"><span data-stu-id="2f91e-273">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="2f91e-274">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="2f91e-274">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="2f91e-275">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="2f91e-275">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f91e-276">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f91e-276">Next steps</span></span>
* [<span data-ttu-id="2f91e-277">Set up your StorSimple Virtual Array as a file server</span><span class="sxs-lookup"><span data-stu-id="2f91e-277">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="2f91e-278">Set up your StorSimple Virtual Array as an iSCSI server</span><span class="sxs-lookup"><span data-stu-id="2f91e-278">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)














































