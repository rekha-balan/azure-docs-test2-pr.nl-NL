---
title: Deploy StorSimple Virtual Array - Provision in Hyper-V
description: This second tutorial in StorSimple Virtual Array deployment involves provisioning a virtual device in Hyper-V.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 38c440e7-81e9-4689-9ec3-c231a499c43e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 06ed7d5f0cbe73701b024774648e2d8f1c50c23c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549527"
---
# <a name="deploy-storsimple-virtual-array---provision-a-virtual-array-in-hyper-v"></a><span data-ttu-id="02db6-103">Deploy StorSimple Virtual Array - Provision a Virtual Array in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="02db6-103">Deploy StorSimple Virtual Array - Provision a Virtual Array in Hyper-V</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="02db6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="02db6-104">Overview</span></span>
<span data-ttu-id="02db6-105">This provisioning tutorial applies to Microsoft Azure StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices or StorSimple virtual devices) running March 2016 general availability (GA) release.</span><span class="sxs-lookup"><span data-stu-id="02db6-105">This provisioning tutorial applies to Microsoft Azure StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices or StorSimple virtual devices) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="02db6-106">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012 or Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="02db6-106">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012 or Windows Server 2008 R2.</span></span> <span data-ttu-id="02db6-107">This article applies to the deployment of StorSimple Virtual Arrays in Azure classic portal as well as Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="02db6-107">This article applies to the deployment of StorSimple Virtual Arrays in Azure classic portal as well as Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="02db6-108">You will need administrator privileges to provision and configure a virtual device.</span><span class="sxs-lookup"><span data-stu-id="02db6-108">You will need administrator privileges to provision and configure a virtual device.</span></span> <span data-ttu-id="02db6-109">The provisioning and initial setup can take around 10 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="02db6-109">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="02db6-110">Provisioning prerequisites</span><span class="sxs-lookup"><span data-stu-id="02db6-110">Provisioning prerequisites</span></span>
<span data-ttu-id="02db6-111">Here you will find the prerequisites to provision a virtual device on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="02db6-111">Here you will find the prerequisites to provision a virtual device on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-manager-service"></a><span data-ttu-id="02db6-112">For the StorSimple Manager service</span><span class="sxs-lookup"><span data-stu-id="02db6-112">For the StorSimple Manager service</span></span>
<span data-ttu-id="02db6-113">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="02db6-113">Before you begin, make sure that:</span></span>

* <span data-ttu-id="02db6-114">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-ova-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="02db6-114">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-ova-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="02db6-115">You have downloaded the virtual device image for Hyper-V from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02db6-115">You have downloaded the virtual device image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="02db6-116">For more information, see [Step 3: Download the virtual device image](storsimple-ova-deploy1-portal-prep.md#step-3-download-the-virtual-device-image).</span><span class="sxs-lookup"><span data-stu-id="02db6-116">For more information, see [Step 3: Download the virtual device image](storsimple-ova-deploy1-portal-prep.md#step-3-download-the-virtual-device-image).</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="02db6-117">The software running on the StorSimple Virtual Array may only be used in conjunction with the Storsimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="02db6-117">The software running on the StorSimple Virtual Array may only be used in conjunction with the Storsimple Manager service.</span></span>
  > 
  > 

### <a name="for-the-storsimple-virtual-device"></a><span data-ttu-id="02db6-118">For the StorSimple virtual device</span><span class="sxs-lookup"><span data-stu-id="02db6-118">For the StorSimple virtual device</span></span>
<span data-ttu-id="02db6-119">Before you deploy a virtual device, make sure that:</span><span class="sxs-lookup"><span data-stu-id="02db6-119">Before you deploy a virtual device, make sure that:</span></span>

* <span data-ttu-id="02db6-120">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span><span class="sxs-lookup"><span data-stu-id="02db6-120">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="02db6-121">The host system is able to dedicate the following resources to provision your virtual device:</span><span class="sxs-lookup"><span data-stu-id="02db6-121">The host system is able to dedicate the following resources to provision your virtual device:</span></span>
  
  * <span data-ttu-id="02db6-122">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="02db6-122">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="02db6-123">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="02db6-123">At least 8 GB of RAM.</span></span>
  * <span data-ttu-id="02db6-124">One network interface.</span><span class="sxs-lookup"><span data-stu-id="02db6-124">One network interface.</span></span>
  * <span data-ttu-id="02db6-125">A 500 GB virtual disk for system data.</span><span class="sxs-lookup"><span data-stu-id="02db6-125">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="02db6-126">For the network in the datacenter</span><span class="sxs-lookup"><span data-stu-id="02db6-126">For the network in the datacenter</span></span>
<span data-ttu-id="02db6-127">Before you begin, review the networking requirements to deploy a StorSimple virtual device and configure the datacenter network appropriately.</span><span class="sxs-lookup"><span data-stu-id="02db6-127">Before you begin, review the networking requirements to deploy a StorSimple virtual device and configure the datacenter network appropriately.</span></span> <span data-ttu-id="02db6-128">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span><span class="sxs-lookup"><span data-stu-id="02db6-128">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="02db6-129">Step-by-step provisioning</span><span class="sxs-lookup"><span data-stu-id="02db6-129">Step-by-step provisioning</span></span>
<span data-ttu-id="02db6-130">To provision and connect to a virtual device, you will need to perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="02db6-130">To provision and connect to a virtual device, you will need to perform the following steps:</span></span>

1. <span data-ttu-id="02db6-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span><span class="sxs-lookup"><span data-stu-id="02db6-131">Ensure that the host system has sufficient resources to meet the minimum virtual device requirements.</span></span>
2. <span data-ttu-id="02db6-132">Provision a virtual device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="02db6-132">Provision a virtual device in your hypervisor.</span></span>
3. <span data-ttu-id="02db6-133">Start the virtual device and get the IP address.</span><span class="sxs-lookup"><span data-stu-id="02db6-133">Start the virtual device and get the IP address.</span></span>

<span data-ttu-id="02db6-134">Each of these steps is explained in the following sections.</span><span class="sxs-lookup"><span data-stu-id="02db6-134">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements"></a><span data-ttu-id="02db6-135">Step 1: Ensure that the host system meets minimum virtual device requirements</span><span class="sxs-lookup"><span data-stu-id="02db6-135">Step 1: Ensure that the host system meets minimum virtual device requirements</span></span>
<span data-ttu-id="02db6-136">To create a virtual device, you will need:</span><span class="sxs-lookup"><span data-stu-id="02db6-136">To create a virtual device, you will need:</span></span>

* <span data-ttu-id="02db6-137">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span><span class="sxs-lookup"><span data-stu-id="02db6-137">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="02db6-138">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span><span class="sxs-lookup"><span data-stu-id="02db6-138">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="02db6-139">You must make sure that the underlying hardware (host system) on which you are creating the virtual device is able to dedicate the following resources to your virtual device:</span><span class="sxs-lookup"><span data-stu-id="02db6-139">You must make sure that the underlying hardware (host system) on which you are creating the virtual device is able to dedicate the following resources to your virtual device:</span></span>

* <span data-ttu-id="02db6-140">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="02db6-140">A minimum of 4 cores.</span></span>
* <span data-ttu-id="02db6-141">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="02db6-141">At least 8 GB of RAM.</span></span>
* <span data-ttu-id="02db6-142">One network interface.</span><span class="sxs-lookup"><span data-stu-id="02db6-142">One network interface.</span></span>
* <span data-ttu-id="02db6-143">A 500 GB virtual disk for system data.</span><span class="sxs-lookup"><span data-stu-id="02db6-143">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a><span data-ttu-id="02db6-144">Step 2: Provision a virtual device in hypervisor</span><span class="sxs-lookup"><span data-stu-id="02db6-144">Step 2: Provision a virtual device in hypervisor</span></span>
<span data-ttu-id="02db6-145">Perform the following steps to provision a device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="02db6-145">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-device"></a><span data-ttu-id="02db6-146">To provision a virtual device</span><span class="sxs-lookup"><span data-stu-id="02db6-146">To provision a virtual device</span></span>
1. <span data-ttu-id="02db6-147">On your Windows Server host, copy the virtual device image to a local drive.</span><span class="sxs-lookup"><span data-stu-id="02db6-147">On your Windows Server host, copy the virtual device image to a local drive.</span></span> <span data-ttu-id="02db6-148">This is the image (VHD or VHDX) that you downloaded through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="02db6-148">This is the image (VHD or VHDX) that you downloaded through the Azure portal.</span></span> <span data-ttu-id="02db6-149">Make a note of the location where you copied the image as you will be using this later in the procedure.</span><span class="sxs-lookup"><span data-stu-id="02db6-149">Make a note of the location where you copied the image as you will be using this later in the procedure.</span></span>
2. <span data-ttu-id="02db6-150">Open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="02db6-150">Open **Server Manager**.</span></span> <span data-ttu-id="02db6-151">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span><span class="sxs-lookup"><span data-stu-id="02db6-151">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image1.png)
   
   <span data-ttu-id="02db6-152">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="02db6-152">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="02db6-153">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span><span class="sxs-lookup"><span data-stu-id="02db6-153">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="02db6-154">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="02db6-154">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="02db6-155">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-155">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="02db6-156">On the **Specify name and location** page, provide a **Name** for your virtual device.</span><span class="sxs-lookup"><span data-stu-id="02db6-156">On the **Specify name and location** page, provide a **Name** for your virtual device.</span></span> <span data-ttu-id="02db6-157">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-157">Click **Next**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="02db6-158">On the **Specify generation** page, choose the device image type and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-158">On the **Specify generation** page, choose the device image type and then click **Next**.</span></span> <span data-ttu-id="02db6-159">This page doesn't appear if you're using Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="02db6-159">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>
   
   * <span data-ttu-id="02db6-160">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span><span class="sxs-lookup"><span data-stu-id="02db6-160">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="02db6-161">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="02db6-161">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="02db6-162">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-162">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image6.png)
8. <span data-ttu-id="02db6-163">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-163">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="02db6-164">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual device image (.vhdx or .vhd), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-164">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual device image (.vhdx or .vhd), and then click **Next**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="02db6-165">Review the **Summary** and then click **Finish** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="02db6-165">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span> <span data-ttu-id="02db6-166">But don't jump ahead yet - you still need to add some CPU cores and a second drive.</span><span class="sxs-lookup"><span data-stu-id="02db6-166">But don't jump ahead yet - you still need to add some CPU cores and a second drive.</span></span> 
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="02db6-167">To meet the minimum requirements, you will need 4 cores.</span><span class="sxs-lookup"><span data-stu-id="02db6-167">To meet the minimum requirements, you will need 4 cores.</span></span> <span data-ttu-id="02db6-168">To add virtual processors, with your host system selected in the **Hyper-V Manager** window, in the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span><span class="sxs-lookup"><span data-stu-id="02db6-168">To add virtual processors, with your host system selected in the **Hyper-V Manager** window, in the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="02db6-169">Select and right-click the machine name and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="02db6-169">Select and right-click the machine name and select **Settings**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="02db6-170">On the **Settings** page, in the left-pane, click **Processor**.</span><span class="sxs-lookup"><span data-stu-id="02db6-170">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="02db6-171">In the right-pane, set **number of virtual processors** to 4 (or more).</span><span class="sxs-lookup"><span data-stu-id="02db6-171">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="02db6-172">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="02db6-172">Click **Apply**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="02db6-173">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span><span class="sxs-lookup"><span data-stu-id="02db6-173">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="02db6-174">In the **Settings** page:</span><span class="sxs-lookup"><span data-stu-id="02db6-174">In the **Settings** page:</span></span>
    
    1. <span data-ttu-id="02db6-175">In the left pane, select **SCSI Controller**.</span><span class="sxs-lookup"><span data-stu-id="02db6-175">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="02db6-176">In the right pane, select **Hard Drive,** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="02db6-176">In the right pane, select **Hard Drive,** and click **Add**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="02db6-177">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span><span class="sxs-lookup"><span data-stu-id="02db6-177">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="02db6-178">This will start the **New Virtual Hard Disk Wizard**.</span><span class="sxs-lookup"><span data-stu-id="02db6-178">This will start the **New Virtual Hard Disk Wizard**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="02db6-179">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-179">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="02db6-180">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span><span class="sxs-lookup"><span data-stu-id="02db6-180">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="02db6-181">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-181">Click **Next**.</span></span> <span data-ttu-id="02db6-182">You won't see this screen if you're running Windows Server 2012 R2 or Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="02db6-182">You won't see this screen if you're running Windows Server 2012 R2 or Windows Server 2008 R2.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="02db6-183">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span><span class="sxs-lookup"><span data-stu-id="02db6-183">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="02db6-184">If you choose **Fixed size** disk, it will also work but you may need to wait a long time.</span><span class="sxs-lookup"><span data-stu-id="02db6-184">If you choose **Fixed size** disk, it will also work but you may need to wait a long time.</span></span> <span data-ttu-id="02db6-185">We recommend that you do not use the **Differencing** option.</span><span class="sxs-lookup"><span data-stu-id="02db6-185">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="02db6-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-186">Click **Next**.</span></span> <span data-ttu-id="02db6-187">Note that **Dynamically expanding** is the default in Windows Server 2012 R2 and Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="02db6-187">Note that **Dynamically expanding** is the default in Windows Server 2012 R2 and Windows Server 2012.</span></span> <span data-ttu-id="02db6-188">In Windows Server 2008 R2, the default is **Fixed size**.</span><span class="sxs-lookup"><span data-stu-id="02db6-188">In Windows Server 2008 R2, the default is **Fixed size**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="02db6-189">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span><span class="sxs-lookup"><span data-stu-id="02db6-189">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="02db6-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-190">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="02db6-191">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span><span class="sxs-lookup"><span data-stu-id="02db6-191">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="02db6-192">While 500 GB is the minimum requirement, you can always provision a larger disk.</span><span class="sxs-lookup"><span data-stu-id="02db6-192">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="02db6-193">Note that you cannot expand or shrink the disk once provisioned.</span><span class="sxs-lookup"><span data-stu-id="02db6-193">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="02db6-194">For more information on the size of disk to provision, review the sizing section in the [best practices](storsimple-ova-best-practices.md#configuration-best-practices) document.</span><span class="sxs-lookup"><span data-stu-id="02db6-194">For more information on the size of disk to provision, review the sizing section in the [best practices](storsimple-ova-best-practices.md#configuration-best-practices) document.</span></span> <span data-ttu-id="02db6-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="02db6-195">Click **Next**.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="02db6-196">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span><span class="sxs-lookup"><span data-stu-id="02db6-196">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="02db6-197">The wizard will close and a virtual hard disk will be added to your machine.</span><span class="sxs-lookup"><span data-stu-id="02db6-197">The wizard will close and a virtual hard disk will be added to your machine.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="02db6-198">You will return to the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="02db6-198">You will return to the **Settings** page.</span></span> <span data-ttu-id="02db6-199">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span><span class="sxs-lookup"><span data-stu-id="02db6-199">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>
    
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-device-and-get-the-ip"></a><span data-ttu-id="02db6-200">Step 3: Start the virtual device and get the IP</span><span class="sxs-lookup"><span data-stu-id="02db6-200">Step 3: Start the virtual device and get the IP</span></span>
<span data-ttu-id="02db6-201">Perform the following steps to start your virtual device and connect to it.</span><span class="sxs-lookup"><span data-stu-id="02db6-201">Perform the following steps to start your virtual device and connect to it.</span></span>

#### <a name="to-start-the-virtual-device"></a><span data-ttu-id="02db6-202">To start the virtual device</span><span class="sxs-lookup"><span data-stu-id="02db6-202">To start the virtual device</span></span>
1. <span data-ttu-id="02db6-203">Start the virtual device.</span><span class="sxs-lookup"><span data-stu-id="02db6-203">Start the virtual device.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="02db6-204">After the device is running, select the device, right click, and select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="02db6-204">After the device is running, select the device, right click, and select **Connect**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="02db6-205">You may have to wait 5-10 minutes for the device to be ready.</span><span class="sxs-lookup"><span data-stu-id="02db6-205">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="02db6-206">A status message is displayed on the console to indicate the progress.</span><span class="sxs-lookup"><span data-stu-id="02db6-206">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="02db6-207">After the device is ready, go to **Action**.</span><span class="sxs-lookup"><span data-stu-id="02db6-207">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="02db6-208">Press `Ctrl + Alt + Delete` to log into the virtual device.</span><span class="sxs-lookup"><span data-stu-id="02db6-208">Press `Ctrl + Alt + Delete` to log into the virtual device.</span></span> <span data-ttu-id="02db6-209">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="02db6-209">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="02db6-210">For security reasons, the device administrator password expires at the first log on.</span><span class="sxs-lookup"><span data-stu-id="02db6-210">For security reasons, the device administrator password expires at the first log on.</span></span> <span data-ttu-id="02db6-211">You will be prompted to change the password.</span><span class="sxs-lookup"><span data-stu-id="02db6-211">You will be prompted to change the password.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image24.png)
   
   <span data-ttu-id="02db6-212">Enter a password that contains at least 8 characters.</span><span class="sxs-lookup"><span data-stu-id="02db6-212">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="02db6-213">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="02db6-213">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="02db6-214">Reenter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="02db6-214">Reenter the password to confirm it.</span></span> <span data-ttu-id="02db6-215">You will be notified that the password has changed.</span><span class="sxs-lookup"><span data-stu-id="02db6-215">You will be notified that the password has changed.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="02db6-216">After the password is successfully changed, the virtual device may restart.</span><span class="sxs-lookup"><span data-stu-id="02db6-216">After the password is successfully changed, the virtual device may restart.</span></span> <span data-ttu-id="02db6-217">Wait for the device to start.</span><span class="sxs-lookup"><span data-stu-id="02db6-217">Wait for the device to start.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image26.png)
   
    <span data-ttu-id="02db6-218">The Windows PowerShell console of the device will be displayed along with a progress bar.</span><span class="sxs-lookup"><span data-stu-id="02db6-218">The Windows PowerShell console of the device will be displayed along with a progress bar.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="02db6-219">Steps 6-8 only apply when booting up in a non DHCP environment.</span><span class="sxs-lookup"><span data-stu-id="02db6-219">Steps 6-8 only apply when booting up in a non DHCP environment.</span></span> <span data-ttu-id="02db6-220">If you are in a DHCP environment, then skip these steps and go to step 9.</span><span class="sxs-lookup"><span data-stu-id="02db6-220">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="02db6-221">If you booted up your device in non DHCP environment, you will see the following screen.</span><span class="sxs-lookup"><span data-stu-id="02db6-221">If you booted up your device in non DHCP environment, you will see the following screen.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image28m.png)
   
    <span data-ttu-id="02db6-222">You will now need to configure the network.</span><span class="sxs-lookup"><span data-stu-id="02db6-222">You will now need to configure the network.</span></span>
7. <span data-ttu-id="02db6-223">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span><span class="sxs-lookup"><span data-stu-id="02db6-223">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual device.</span></span> <span data-ttu-id="02db6-224">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="02db6-224">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="02db6-225">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span><span class="sxs-lookup"><span data-stu-id="02db6-225">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="02db6-226">An example is shown below:</span><span class="sxs-lookup"><span data-stu-id="02db6-226">An example is shown below:</span></span>
   
    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="02db6-227">After the initial setup is complete and the device has booted up, you will see the device banner text.</span><span class="sxs-lookup"><span data-stu-id="02db6-227">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="02db6-228">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span><span class="sxs-lookup"><span data-stu-id="02db6-228">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="02db6-229">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span><span class="sxs-lookup"><span data-stu-id="02db6-229">You will use this IP address to connect to the web UI of your virtual device and complete the local setup and registration.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="02db6-230">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="02db6-230">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="02db6-231">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span><span class="sxs-lookup"><span data-stu-id="02db6-231">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="02db6-232">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span><span class="sxs-lookup"><span data-stu-id="02db6-232">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>
    
    1. <span data-ttu-id="02db6-233">To enable the FIPS mode, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="02db6-233">To enable the FIPS mode, run the following cmdlet:</span></span>
       
        `Enter-HcsFIPSMode`
    2. <span data-ttu-id="02db6-234">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span><span class="sxs-lookup"><span data-stu-id="02db6-234">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="02db6-235">You can either enable or disable FIPS mode on your device.</span><span class="sxs-lookup"><span data-stu-id="02db6-235">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="02db6-236">Alternating the device between FIPS and non-FIPS mode is not supported.</span><span class="sxs-lookup"><span data-stu-id="02db6-236">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       > 
       > 

<span data-ttu-id="02db6-237">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span><span class="sxs-lookup"><span data-stu-id="02db6-237">If your device does not meet the minimum configuration requirements, you will see an error in the banner text (shown below).</span></span> <span data-ttu-id="02db6-238">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span><span class="sxs-lookup"><span data-stu-id="02db6-238">You will need to modify the device configuration so that it has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="02db6-239">You can then restart and connect to the device.</span><span class="sxs-lookup"><span data-stu-id="02db6-239">You can then restart and connect to the device.</span></span> <span data-ttu-id="02db6-240">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="02db6-240">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual device requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="02db6-241">If you face any other error during the initial configuration using the local web UI, refer to the following workflows in [Manage your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="02db6-241">If you face any other error during the initial configuration using the local web UI, refer to the following workflows in [Manage your StorSimple Virtual Array using the local web UI](storsimple-ova-web-ui-admin.md).</span></span>

* <span data-ttu-id="02db6-242">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="02db6-242">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="02db6-243">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="02db6-243">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

<span data-ttu-id="02db6-244">![video icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/video_icon.png)  **Video available**</span><span class="sxs-lookup"><span data-stu-id="02db6-244">![video icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-ova-deploy2-provision-hyperv/video_icon.png)  **Video available**</span></span>

<span data-ttu-id="02db6-245">Watch the video to see how you can provision a StorSimple Virtual Array in Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="02db6-245">Watch the video to see how you can provision a StorSimple Virtual Array in Hyper-V.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Create-a-StorSimple-Virtual-Array/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="02db6-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="02db6-246">Next steps</span></span>
* [<span data-ttu-id="02db6-247">Set up your StorSimple Virtual Array as a file server</span><span class="sxs-lookup"><span data-stu-id="02db6-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-ova-deploy3-fs-setup.md)
* [<span data-ttu-id="02db6-248">Set up your StorSimple Virtual Array as an iSCSI server</span><span class="sxs-lookup"><span data-stu-id="02db6-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-ova-deploy3-iscsi-setup.md)

































