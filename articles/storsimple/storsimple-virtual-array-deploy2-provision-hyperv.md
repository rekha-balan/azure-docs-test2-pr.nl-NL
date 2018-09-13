---
title: Provision StorSimple Virtual Array in Hyper-V | Microsoft Docs
description: This second tutorial in StorSimple Virtual Array deployment involves provisioning a virtual array in Hyper-V.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2094a2f1dd589d5aea382976afc13f4be3e2af47
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553545"
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a><span data-ttu-id="014cf-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="014cf-103">Deploy StorSimple Virtual Array - Provision in Hyper-V</span></span>
![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a><span data-ttu-id="014cf-104">Overview</span><span class="sxs-lookup"><span data-stu-id="014cf-104">Overview</span></span>
<span data-ttu-id="014cf-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="014cf-105">This tutorial describes how to provision a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <span data-ttu-id="014cf-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="014cf-106">This article applies to the deployment of StorSimple Virtual Arrays in Azure portal and Microsoft Azure Government Cloud.</span></span>

<span data-ttu-id="014cf-107">You need administrator privileges to provision and configure a virtual array.</span><span class="sxs-lookup"><span data-stu-id="014cf-107">You need administrator privileges to provision and configure a virtual array.</span></span> <span data-ttu-id="014cf-108">The provisioning and initial setup can take around 10 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="014cf-108">The provisioning and initial setup can take around 10 minutes to complete.</span></span>

## <a name="provisioning-prerequisites"></a><span data-ttu-id="014cf-109">Provisioning prerequisites</span><span class="sxs-lookup"><span data-stu-id="014cf-109">Provisioning prerequisites</span></span>
<span data-ttu-id="014cf-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="014cf-110">Here you will find the prerequisites to provision a virtual array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="014cf-111">For the StorSimple Device Manager service</span><span class="sxs-lookup"><span data-stu-id="014cf-111">For the StorSimple Device Manager service</span></span>
<span data-ttu-id="014cf-112">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="014cf-112">Before you begin, make sure that:</span></span>

* <span data-ttu-id="014cf-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="014cf-113">You have completed all the steps in [Prepare the portal for StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>
* <span data-ttu-id="014cf-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="014cf-114">You have downloaded the virtual array image for Hyper-V from the Azure portal.</span></span> <span data-ttu-id="014cf-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span><span class="sxs-lookup"><span data-stu-id="014cf-115">For more information, see **Step 3: Download the virtual array image** of [Prepare the portal for StorSimple Virtual Array guide](storsimple-virtual-array-deploy1-portal-prep.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="014cf-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="014cf-116">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
  >
  >

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="014cf-117">For the StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="014cf-117">For the StorSimple Virtual Array</span></span>
<span data-ttu-id="014cf-118">Before you deploy a virtual array, make sure that:</span><span class="sxs-lookup"><span data-stu-id="014cf-118">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="014cf-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span><span class="sxs-lookup"><span data-stu-id="014cf-119">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later that can be used to a provision a device.</span></span>
* <span data-ttu-id="014cf-120">The host system is able to dedicate the following resources to provision your virtual array:</span><span class="sxs-lookup"><span data-stu-id="014cf-120">The host system is able to dedicate the following resources to provision your virtual array:</span></span>

  * <span data-ttu-id="014cf-121">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="014cf-121">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="014cf-122">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="014cf-122">At least 8 GB of RAM.</span></span> <span data-ttu-id="014cf-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span><span class="sxs-lookup"><span data-stu-id="014cf-123">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="014cf-124">You need 16 GB RAM to support 2 - 4 million files.</span><span class="sxs-lookup"><span data-stu-id="014cf-124">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="014cf-125">One network interface.</span><span class="sxs-lookup"><span data-stu-id="014cf-125">One network interface.</span></span>
  * <span data-ttu-id="014cf-126">A 500 GB virtual disk for data.</span><span class="sxs-lookup"><span data-stu-id="014cf-126">A 500 GB virtual disk for data.</span></span>

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="014cf-127">For the network in the datacenter</span><span class="sxs-lookup"><span data-stu-id="014cf-127">For the network in the datacenter</span></span>
<span data-ttu-id="014cf-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span><span class="sxs-lookup"><span data-stu-id="014cf-128">Before you begin, review the networking requirements to deploy a StorSimple Virtual Array and configure the datacenter network appropriately.</span></span> <span data-ttu-id="014cf-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span><span class="sxs-lookup"><span data-stu-id="014cf-129">For more information, see [StorSimple Virtual Array networking requirements](storsimple-ova-system-requirements.md#networking-requirements).</span></span>

## <a name="step-by-step-provisioning"></a><span data-ttu-id="014cf-130">Step-by-step provisioning</span><span class="sxs-lookup"><span data-stu-id="014cf-130">Step-by-step provisioning</span></span>
<span data-ttu-id="014cf-131">To provision and connect to a virtual array, you need to perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="014cf-131">To provision and connect to a virtual array, you need to perform the following steps:</span></span>

1. <span data-ttu-id="014cf-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span><span class="sxs-lookup"><span data-stu-id="014cf-132">Ensure that the host system has sufficient resources to meet the minimum virtual array requirements.</span></span>
2. <span data-ttu-id="014cf-133">Provision a virtual array in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="014cf-133">Provision a virtual array in your hypervisor.</span></span>
3. <span data-ttu-id="014cf-134">Start the virtual array and get the IP address.</span><span class="sxs-lookup"><span data-stu-id="014cf-134">Start the virtual array and get the IP address.</span></span>

<span data-ttu-id="014cf-135">Each of these steps is explained in the following sections.</span><span class="sxs-lookup"><span data-stu-id="014cf-135">Each of these steps is explained in the following sections.</span></span>

## <a name="step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements"></a><span data-ttu-id="014cf-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span><span class="sxs-lookup"><span data-stu-id="014cf-136">Step 1: Ensure that the host system meets minimum virtual array requirements</span></span>
<span data-ttu-id="014cf-137">To create a virtual array, you need:</span><span class="sxs-lookup"><span data-stu-id="014cf-137">To create a virtual array, you need:</span></span>

* <span data-ttu-id="014cf-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span><span class="sxs-lookup"><span data-stu-id="014cf-138">The Hyper-V role installed on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2 SP1.</span></span>
* <span data-ttu-id="014cf-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span><span class="sxs-lookup"><span data-stu-id="014cf-139">Microsoft Hyper-V Manager on a Microsoft Windows client connected to the host.</span></span>

<span data-ttu-id="014cf-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span><span class="sxs-lookup"><span data-stu-id="014cf-140">Make sure that the underlying hardware (host system) on which you are creating the virtual array is able to dedicate the following resources to your virtual array:</span></span>

* <span data-ttu-id="014cf-141">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="014cf-141">A minimum of 4 cores.</span></span>
* <span data-ttu-id="014cf-142">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="014cf-142">At least 8 GB of RAM.</span></span> <span data-ttu-id="014cf-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span><span class="sxs-lookup"><span data-stu-id="014cf-143">If you plan to configure the virtual array as file server, 8 GB supports less than 2 million files.</span></span> <span data-ttu-id="014cf-144">You need 16 GB RAM to support 2 - 4 million files.</span><span class="sxs-lookup"><span data-stu-id="014cf-144">You need 16 GB RAM to support 2 - 4 million files.</span></span>
* <span data-ttu-id="014cf-145">One network interface.</span><span class="sxs-lookup"><span data-stu-id="014cf-145">One network interface.</span></span>
* <span data-ttu-id="014cf-146">A 500 GB virtual disk for system data.</span><span class="sxs-lookup"><span data-stu-id="014cf-146">A 500 GB virtual disk for system data.</span></span>

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a><span data-ttu-id="014cf-147">Step 2: Provision a virtual array in hypervisor</span><span class="sxs-lookup"><span data-stu-id="014cf-147">Step 2: Provision a virtual array in hypervisor</span></span>
<span data-ttu-id="014cf-148">Perform the following steps to provision a device in your hypervisor.</span><span class="sxs-lookup"><span data-stu-id="014cf-148">Perform the following steps to provision a device in your hypervisor.</span></span>

#### <a name="to-provision-a-virtual-array"></a><span data-ttu-id="014cf-149">To provision a virtual array</span><span class="sxs-lookup"><span data-stu-id="014cf-149">To provision a virtual array</span></span>
1. <span data-ttu-id="014cf-150">On your Windows Server host, copy the virtual array image to a local drive.</span><span class="sxs-lookup"><span data-stu-id="014cf-150">On your Windows Server host, copy the virtual array image to a local drive.</span></span> <span data-ttu-id="014cf-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="014cf-151">You downloaded this image (VHD or VHDX) through the Azure portal.</span></span> <span data-ttu-id="014cf-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span><span class="sxs-lookup"><span data-stu-id="014cf-152">Make a note of the location where you copied the image as you are using this image later in the procedure.</span></span>
2. <span data-ttu-id="014cf-153">Open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="014cf-153">Open **Server Manager**.</span></span> <span data-ttu-id="014cf-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span><span class="sxs-lookup"><span data-stu-id="014cf-154">In the top right corner, click **Tools** and select **Hyper-V Manager**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   <span data-ttu-id="014cf-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="014cf-155">If you are running Windows Server 2008 R2, open the Hyper-V Manager.</span></span> <span data-ttu-id="014cf-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span><span class="sxs-lookup"><span data-stu-id="014cf-156">In Server Manager, click **Roles > Hyper-V > Hyper-V Manager**.</span></span>
3. <span data-ttu-id="014cf-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="014cf-157">In **Hyper-V Manager**, in the scope pane, right-click your system node to open the context menu, and then click **New** > **Virtual Machine**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. <span data-ttu-id="014cf-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-158">On the **Before you begin** page of the New Virtual Machine Wizard, click **Next**.</span></span>
5. <span data-ttu-id="014cf-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span><span class="sxs-lookup"><span data-stu-id="014cf-159">On the **Specify name and location** page, provide a **Name** for your virtual array.</span></span> <span data-ttu-id="014cf-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-160">Click **Next**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. <span data-ttu-id="014cf-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-161">On the **Specify generation** page, choose the device image type, and then click **Next**.</span></span> <span data-ttu-id="014cf-162">This page doesn't appear if you're using Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="014cf-162">This page doesn't appear if you're using Windows Server 2008 R2.</span></span>

   * <span data-ttu-id="014cf-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span><span class="sxs-lookup"><span data-stu-id="014cf-163">Choose **Generation 2** if you downloaded a .vhdx image for Windows Server 2012 or later.</span></span>
   * <span data-ttu-id="014cf-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="014cf-164">Choose **Generation 1** if you downloaded a .vhd image for Windows Server 2008 R2 or later.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. <span data-ttu-id="014cf-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-165">On the **Assign memory** page, specify a **Startup memory** of at least **8192 MB**, don't enable dynamic memory, and then click **Next**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. <span data-ttu-id="014cf-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-166">On the **Configure networking** page, specify the virtual switch that is connected to the Internet and then click **Next**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. <span data-ttu-id="014cf-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-167">On the **Connect virtual hard disk** page, choose **Use an existing virtual hard disk**, specify the location of the virtual array image (.vhdx or .vhd), and then click **Next**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. <span data-ttu-id="014cf-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="014cf-168">Review the **Summary** and then click **Finish** to create the virtual machine.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. <span data-ttu-id="014cf-169">To meet the minimum requirements, you need 4 cores.</span><span class="sxs-lookup"><span data-stu-id="014cf-169">To meet the minimum requirements, you need 4 cores.</span></span> <span data-ttu-id="014cf-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span><span class="sxs-lookup"><span data-stu-id="014cf-170">To add 4 virtual processors, select your host system in the **Hyper-V Manager** window.</span></span> <span data-ttu-id="014cf-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span><span class="sxs-lookup"><span data-stu-id="014cf-171">In the right-pane under the list of **Virtual Machines**, locate the virtual machine you just created.</span></span> <span data-ttu-id="014cf-172">Select and right-click the machine name and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="014cf-172">Select and right-click the machine name and select **Settings**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. <span data-ttu-id="014cf-173">On the **Settings** page, in the left-pane, click **Processor**.</span><span class="sxs-lookup"><span data-stu-id="014cf-173">On the **Settings** page, in the left-pane, click **Processor**.</span></span> <span data-ttu-id="014cf-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span><span class="sxs-lookup"><span data-stu-id="014cf-174">In the right-pane, set **number of virtual processors** to 4 (or more).</span></span> <span data-ttu-id="014cf-175">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="014cf-175">Click **Apply**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. <span data-ttu-id="014cf-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span><span class="sxs-lookup"><span data-stu-id="014cf-176">To meet the minimum requirements, you also need to add a 500 GB virtual data disk.</span></span> <span data-ttu-id="014cf-177">In the **Settings** page:</span><span class="sxs-lookup"><span data-stu-id="014cf-177">In the **Settings** page:</span></span>

    1. <span data-ttu-id="014cf-178">In the left pane, select **SCSI Controller**.</span><span class="sxs-lookup"><span data-stu-id="014cf-178">In the left pane, select **SCSI Controller**.</span></span>
    2. <span data-ttu-id="014cf-179">In the right pane, select **Hard Drive,** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="014cf-179">In the right pane, select **Hard Drive,** and click **Add**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. <span data-ttu-id="014cf-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span><span class="sxs-lookup"><span data-stu-id="014cf-180">On the **Hard drive** page, select the **Virtual hard disk** option and click **New**.</span></span> <span data-ttu-id="014cf-181">The **New Virtual Hard Disk Wizard** starts.</span><span class="sxs-lookup"><span data-stu-id="014cf-181">The **New Virtual Hard Disk Wizard** starts.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. <span data-ttu-id="014cf-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-182">On the **Before you begin** page of the New Virtual Hard Disk Wizard, click **Next**.</span></span>
16. <span data-ttu-id="014cf-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span><span class="sxs-lookup"><span data-stu-id="014cf-183">On the **Choose Disk Format page**, accept the default option of **VHDX** format.</span></span> <span data-ttu-id="014cf-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-184">Click **Next**.</span></span> <span data-ttu-id="014cf-185">This screen is not presented if running Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="014cf-185">This screen is not presented if running Windows Server 2008 R2.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. <span data-ttu-id="014cf-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span><span class="sxs-lookup"><span data-stu-id="014cf-186">On the **Choose Disk Type page**, set virtual hard disk type as **Dynamically expanding** (recommended).</span></span> <span data-ttu-id="014cf-187">**Fixed size** disk would work but you may need to wait a long time.</span><span class="sxs-lookup"><span data-stu-id="014cf-187">**Fixed size** disk would work but you may need to wait a long time.</span></span> <span data-ttu-id="014cf-188">We recommend that you do not use the **Differencing** option.</span><span class="sxs-lookup"><span data-stu-id="014cf-188">We recommend that you do not use the **Differencing** option.</span></span> <span data-ttu-id="014cf-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-189">Click **Next**.</span></span> <span data-ttu-id="014cf-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span><span class="sxs-lookup"><span data-stu-id="014cf-190">In Windows Server 2012 R2 and Windows Server 2012, **Dynamically expanding** is the default option whereas in Windows Server 2008 R2, the default is **Fixed size**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. <span data-ttu-id="014cf-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span><span class="sxs-lookup"><span data-stu-id="014cf-191">On the **Specify Name and Location** page, provide a **name** as well as **location** (you can browse to one) for the data disk.</span></span> <span data-ttu-id="014cf-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-192">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. <span data-ttu-id="014cf-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span><span class="sxs-lookup"><span data-stu-id="014cf-193">On the **Configure Disk** page, select the option **Create a new blank virtual hard disk** and specify the size as **500 GB** (or more).</span></span> <span data-ttu-id="014cf-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span><span class="sxs-lookup"><span data-stu-id="014cf-194">While 500 GB is the minimum requirement, you can always provision a larger disk.</span></span> <span data-ttu-id="014cf-195">Note that you cannot expand or shrink the disk once provisioned.</span><span class="sxs-lookup"><span data-stu-id="014cf-195">Note that you cannot expand or shrink the disk once provisioned.</span></span> <span data-ttu-id="014cf-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="014cf-196">For more information on the size of disk to provision, review the sizing section in the [best practices document](storsimple-ova-best-practices.md).</span></span> <span data-ttu-id="014cf-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="014cf-197">Click **Next**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. <span data-ttu-id="014cf-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span><span class="sxs-lookup"><span data-stu-id="014cf-198">On the **Summary** page, review the details of your virtual data disk and if satisfied, click **Finish** to create the disk.</span></span> <span data-ttu-id="014cf-199">The wizard closes and a virtual hard disk is added to your machine.</span><span class="sxs-lookup"><span data-stu-id="014cf-199">The wizard closes and a virtual hard disk is added to your machine.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. <span data-ttu-id="014cf-200">Return to the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="014cf-200">Return to the **Settings** page.</span></span> <span data-ttu-id="014cf-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span><span class="sxs-lookup"><span data-stu-id="014cf-201">Click **OK** to close the **Settings** page and return to Hyper-V Manager window.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-the-virtual-array-and-get-the-ip"></a><span data-ttu-id="014cf-202">Step 3: Start the virtual array and get the IP</span><span class="sxs-lookup"><span data-stu-id="014cf-202">Step 3: Start the virtual array and get the IP</span></span>
<span data-ttu-id="014cf-203">Perform the following steps to start your virtual array and connect to it.</span><span class="sxs-lookup"><span data-stu-id="014cf-203">Perform the following steps to start your virtual array and connect to it.</span></span>

#### <a name="to-start-the-virtual-array"></a><span data-ttu-id="014cf-204">To start the virtual array</span><span class="sxs-lookup"><span data-stu-id="014cf-204">To start the virtual array</span></span>
1. <span data-ttu-id="014cf-205">Start the virtual array.</span><span class="sxs-lookup"><span data-stu-id="014cf-205">Start the virtual array.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. <span data-ttu-id="014cf-206">After the device is running, select the device, right click, and select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="014cf-206">After the device is running, select the device, right click, and select **Connect**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. <span data-ttu-id="014cf-207">You may have to wait 5-10 minutes for the device to be ready.</span><span class="sxs-lookup"><span data-stu-id="014cf-207">You may have to wait 5-10 minutes for the device to be ready.</span></span> <span data-ttu-id="014cf-208">A status message is displayed on the console to indicate the progress.</span><span class="sxs-lookup"><span data-stu-id="014cf-208">A status message is displayed on the console to indicate the progress.</span></span> <span data-ttu-id="014cf-209">After the device is ready, go to **Action**.</span><span class="sxs-lookup"><span data-stu-id="014cf-209">After the device is ready, go to **Action**.</span></span> <span data-ttu-id="014cf-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span><span class="sxs-lookup"><span data-stu-id="014cf-210">Press `Ctrl + Alt + Delete` to log in to the virtual array.</span></span> <span data-ttu-id="014cf-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="014cf-211">The default user is *StorSimpleAdmin* and the default password is *Password1*.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. <span data-ttu-id="014cf-212">For security reasons, the device administrator password expires at the first logon.</span><span class="sxs-lookup"><span data-stu-id="014cf-212">For security reasons, the device administrator password expires at the first logon.</span></span> <span data-ttu-id="014cf-213">You are prompted to change the password.</span><span class="sxs-lookup"><span data-stu-id="014cf-213">You are prompted to change the password.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   <span data-ttu-id="014cf-214">Enter a password that contains at least 8 characters.</span><span class="sxs-lookup"><span data-stu-id="014cf-214">Enter a password that contains at least 8 characters.</span></span> <span data-ttu-id="014cf-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="014cf-215">The password must satisfy at least 3 out of the following 4 requirements: uppercase, lowercase, numeric, and special characters.</span></span> <span data-ttu-id="014cf-216">Reenter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="014cf-216">Reenter the password to confirm it.</span></span> <span data-ttu-id="014cf-217">You are notified that the password has changed.</span><span class="sxs-lookup"><span data-stu-id="014cf-217">You are notified that the password has changed.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. <span data-ttu-id="014cf-218">After the password is successfully changed, the virtual array may restart.</span><span class="sxs-lookup"><span data-stu-id="014cf-218">After the password is successfully changed, the virtual array may restart.</span></span> <span data-ttu-id="014cf-219">Wait for the device to start.</span><span class="sxs-lookup"><span data-stu-id="014cf-219">Wait for the device to start.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    <span data-ttu-id="014cf-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span><span class="sxs-lookup"><span data-stu-id="014cf-220">The Windows PowerShell console of the device is displayed along with a progress bar.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. <span data-ttu-id="014cf-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span><span class="sxs-lookup"><span data-stu-id="014cf-221">Steps 6-8 only apply when booting up in a non-DHCP environment.</span></span> <span data-ttu-id="014cf-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span><span class="sxs-lookup"><span data-stu-id="014cf-222">If you are in a DHCP environment, then skip these steps and go to step 9.</span></span> <span data-ttu-id="014cf-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span><span class="sxs-lookup"><span data-stu-id="014cf-223">If you booted up your device in non-DHCP environment, you will see the following screen.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    <span data-ttu-id="014cf-224">Next, configure the network.</span><span class="sxs-lookup"><span data-stu-id="014cf-224">Next, configure the network.</span></span>
7. <span data-ttu-id="014cf-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span><span class="sxs-lookup"><span data-stu-id="014cf-225">Use the `Get-HcsIpAddress` command to list the network interfaces enabled on your virtual array.</span></span> <span data-ttu-id="014cf-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span><span class="sxs-lookup"><span data-stu-id="014cf-226">If your device has a single network interface enabled, the default name assigned to this interface is `Ethernet`.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. <span data-ttu-id="014cf-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span><span class="sxs-lookup"><span data-stu-id="014cf-227">Use the `Set-HcsIpAddress` cmdlet to configure the network.</span></span> <span data-ttu-id="014cf-228">See the following example:</span><span class="sxs-lookup"><span data-stu-id="014cf-228">See the following example:</span></span>

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. <span data-ttu-id="014cf-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span><span class="sxs-lookup"><span data-stu-id="014cf-229">After the initial setup is complete and the device has booted up, you will see the device banner text.</span></span> <span data-ttu-id="014cf-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span><span class="sxs-lookup"><span data-stu-id="014cf-230">Make a note of the IP address and the URL displayed in the banner text to manage the device.</span></span> <span data-ttu-id="014cf-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span><span class="sxs-lookup"><span data-stu-id="014cf-231">Use this IP address to connect to the web UI of your virtual array and complete the local setup and registration.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. <span data-ttu-id="014cf-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="014cf-232">(Optional) Perform this step only if you are deploying your device in the Government Cloud.</span></span> <span data-ttu-id="014cf-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span><span class="sxs-lookup"><span data-stu-id="014cf-233">You will now enable the United States Federal Information Processing Standard (FIPS) mode on your device.</span></span> <span data-ttu-id="014cf-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span><span class="sxs-lookup"><span data-stu-id="014cf-234">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span>

    1. <span data-ttu-id="014cf-235">To enable the FIPS mode, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="014cf-235">To enable the FIPS mode, run the following cmdlet:</span></span>

        `Enable-HcsFIPSMode`
    2. <span data-ttu-id="014cf-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span><span class="sxs-lookup"><span data-stu-id="014cf-236">Reboot your device after you have enabled the FIPS mode so that the cryptographic validations take effect.</span></span>

       > [!NOTE]
       > <span data-ttu-id="014cf-237">You can either enable or disable FIPS mode on your device.</span><span class="sxs-lookup"><span data-stu-id="014cf-237">You can either enable or disable FIPS mode on your device.</span></span> <span data-ttu-id="014cf-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span><span class="sxs-lookup"><span data-stu-id="014cf-238">Alternating the device between FIPS and non-FIPS mode is not supported.</span></span>
       >
       >

<span data-ttu-id="014cf-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span><span class="sxs-lookup"><span data-stu-id="014cf-239">If your device does not meet the minimum configuration requirements, you see the following error in the banner text (shown below).</span></span> <span data-ttu-id="014cf-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span><span class="sxs-lookup"><span data-stu-id="014cf-240">Modify the device configuration so that the machine has adequate resources to meet the minimum requirements.</span></span> <span data-ttu-id="014cf-241">You can then restart and connect to the device.</span><span class="sxs-lookup"><span data-stu-id="014cf-241">You can then restart and connect to the device.</span></span> <span data-ttu-id="014cf-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span><span class="sxs-lookup"><span data-stu-id="014cf-242">Refer to the minimum configuration requirements in [Step 1: Ensure that the host system meets minimum virtual array requirements](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

<span data-ttu-id="014cf-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span><span class="sxs-lookup"><span data-stu-id="014cf-243">If you face any other error during the initial configuration using the local web UI, refer to the following workflows:</span></span>

* <span data-ttu-id="014cf-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span><span class="sxs-lookup"><span data-stu-id="014cf-244">Run diagnostic tests to [troubleshoot web UI setup](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).</span></span>
* <span data-ttu-id="014cf-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="014cf-245">[Generate log package and view log files](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="next-steps"></a><span data-ttu-id="014cf-246">Next steps</span><span class="sxs-lookup"><span data-stu-id="014cf-246">Next steps</span></span>
* [<span data-ttu-id="014cf-247">Set up your StorSimple Virtual Array as a file server</span><span class="sxs-lookup"><span data-stu-id="014cf-247">Set up your StorSimple Virtual Array as a file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)
* [<span data-ttu-id="014cf-248">Set up your StorSimple Virtual Array as an iSCSI server</span><span class="sxs-lookup"><span data-stu-id="014cf-248">Set up your StorSimple Virtual Array as an iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md)































