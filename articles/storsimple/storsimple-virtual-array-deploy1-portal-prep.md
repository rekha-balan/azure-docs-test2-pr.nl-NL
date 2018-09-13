---
title: Portal prep for StorSimple Virtual Array | Microsoft Docs
description: First tutorial to deploy StorSimple virtual array involves preparing the Azure portal
services: storsimple
documentationcenter: NA
author: alkohli
manager: jeconnoc
editor: ''
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2126ff7ffd503e1d7b30997f3f32f30429cffefb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774728"
---
# <a name="deploy-storsimple-virtual-array---prepare-the-azure-portal"></a><span data-ttu-id="33a5c-103">Deploy StorSimple Virtual Array - Prepare the Azure portal</span><span class="sxs-lookup"><span data-stu-id="33a5c-103">Deploy StorSimple Virtual Array - Prepare the Azure portal</span></span>

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a><span data-ttu-id="33a5c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="33a5c-104">Overview</span></span>

<span data-ttu-id="33a5c-105">This is the first article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server using the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="33a5c-105">This is the first article in the series of deployment tutorials required to completely deploy your virtual array as a file server or an iSCSI server using the Resource Manager model.</span></span> <span data-ttu-id="33a5c-106">This article describes the preparation required to create and configure your StorSimple Device Manager service prior to provisioning a virtual array.</span><span class="sxs-lookup"><span data-stu-id="33a5c-106">This article describes the preparation required to create and configure your StorSimple Device Manager service prior to provisioning a virtual array.</span></span> <span data-ttu-id="33a5c-107">This article also links out to a deployment configuration checklist and configuration prerequisites.</span><span class="sxs-lookup"><span data-stu-id="33a5c-107">This article also links out to a deployment configuration checklist and configuration prerequisites.</span></span>

<span data-ttu-id="33a5c-108">You need administrator privileges to complete the setup and configuration process.</span><span class="sxs-lookup"><span data-stu-id="33a5c-108">You need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="33a5c-109">We recommend that you review the deployment configuration checklist before you begin.</span><span class="sxs-lookup"><span data-stu-id="33a5c-109">We recommend that you review the deployment configuration checklist before you begin.</span></span> <span data-ttu-id="33a5c-110">The portal preparation takes less than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="33a5c-110">The portal preparation takes less than 10 minutes.</span></span>

<span data-ttu-id="33a5c-111">The information published in this article applies to the deployment of StorSimple Virtual Arrays in the Azure portal and Microsoft Azure Government Cloud.</span><span class="sxs-lookup"><span data-stu-id="33a5c-111">The information published in this article applies to the deployment of StorSimple Virtual Arrays in the Azure portal and Microsoft Azure Government Cloud.</span></span>

### <a name="get-started"></a><span data-ttu-id="33a5c-112">Get started</span><span class="sxs-lookup"><span data-stu-id="33a5c-112">Get started</span></span>
<span data-ttu-id="33a5c-113">The deployment workflow consists of preparing the portal, provisioning a virtual array in your virtualized environment, and completing the setup.</span><span class="sxs-lookup"><span data-stu-id="33a5c-113">The deployment workflow consists of preparing the portal, provisioning a virtual array in your virtualized environment, and completing the setup.</span></span> <span data-ttu-id="33a5c-114">To get started with the StorSimple Virtual Array deployment as a file server or an iSCSI server, you need to refer to the following tabulated resources.</span><span class="sxs-lookup"><span data-stu-id="33a5c-114">To get started with the StorSimple Virtual Array deployment as a file server or an iSCSI server, you need to refer to the following tabulated resources.</span></span>

#### <a name="deployment-articles"></a><span data-ttu-id="33a5c-115">Deployment articles</span><span class="sxs-lookup"><span data-stu-id="33a5c-115">Deployment articles</span></span>

<span data-ttu-id="33a5c-116">To deploy your StorSimple Virtual Array, refer to the following articles in the prescribed sequence.</span><span class="sxs-lookup"><span data-stu-id="33a5c-116">To deploy your StorSimple Virtual Array, refer to the following articles in the prescribed sequence.</span></span>

| **#** | <span data-ttu-id="33a5c-117">**In this step**</span><span class="sxs-lookup"><span data-stu-id="33a5c-117">**In this step**</span></span> | <span data-ttu-id="33a5c-118">**You do this …**</span><span class="sxs-lookup"><span data-stu-id="33a5c-118">**You do this …**</span></span> | <span data-ttu-id="33a5c-119">**And use these documents.**</span><span class="sxs-lookup"><span data-stu-id="33a5c-119">**And use these documents.**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="33a5c-120">1.</span><span class="sxs-lookup"><span data-stu-id="33a5c-120">1.</span></span> |<span data-ttu-id="33a5c-121">**Set up the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="33a5c-121">**Set up the Azure portal**</span></span> |<span data-ttu-id="33a5c-122">Create and configure your StorSimple Device Manager service prior to provisioning a StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="33a5c-122">Create and configure your StorSimple Device Manager service prior to provisioning a StorSimple Virtual Array.</span></span> |[<span data-ttu-id="33a5c-123">Prepare the portal</span><span class="sxs-lookup"><span data-stu-id="33a5c-123">Prepare the portal</span></span>](storsimple-virtual-array-deploy1-portal-prep.md) |
| <span data-ttu-id="33a5c-124">2.</span><span class="sxs-lookup"><span data-stu-id="33a5c-124">2.</span></span> |<span data-ttu-id="33a5c-125">**Provision the Virtual Array**</span><span class="sxs-lookup"><span data-stu-id="33a5c-125">**Provision the Virtual Array**</span></span> |<span data-ttu-id="33a5c-126">For Hyper-V, provision and connect to a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="33a5c-126">For Hyper-V, provision and connect to a StorSimple Virtual Array on a host system running Hyper-V on Windows Server 2012 R2, Windows Server 2012, or Windows Server 2008 R2.</span></span> <br></br> <br></br> <span data-ttu-id="33a5c-127">For VMware, provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.0, 5.5, or 6.0.</span><span class="sxs-lookup"><span data-stu-id="33a5c-127">For VMware, provision and connect to a StorSimple Virtual Array on a host system running VMware ESXi 5.0, 5.5, or 6.0.</span></span><br></br> |[<span data-ttu-id="33a5c-128">Provision a virtual array in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="33a5c-128">Provision a virtual array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [<span data-ttu-id="33a5c-129">Provision a virtual array in VMware</span><span class="sxs-lookup"><span data-stu-id="33a5c-129">Provision a virtual array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md) |
| <span data-ttu-id="33a5c-130">3.</span><span class="sxs-lookup"><span data-stu-id="33a5c-130">3.</span></span> |<span data-ttu-id="33a5c-131">**Set up the Virtual Array**</span><span class="sxs-lookup"><span data-stu-id="33a5c-131">**Set up the Virtual Array**</span></span> |<span data-ttu-id="33a5c-132">For your file server, perform initial setup, register your StorSimple file server, and complete the device setup.</span><span class="sxs-lookup"><span data-stu-id="33a5c-132">For your file server, perform initial setup, register your StorSimple file server, and complete the device setup.</span></span> <span data-ttu-id="33a5c-133">You can then provision SMB shares.</span><span class="sxs-lookup"><span data-stu-id="33a5c-133">You can then provision SMB shares.</span></span> <br></br> <br></br> <span data-ttu-id="33a5c-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete the device setup.</span><span class="sxs-lookup"><span data-stu-id="33a5c-134">For your iSCSI server, perform initial setup, register your StorSimple iSCSI server, and complete the device setup.</span></span> <span data-ttu-id="33a5c-135">You can then provision iSCSI volumes.</span><span class="sxs-lookup"><span data-stu-id="33a5c-135">You can then provision iSCSI volumes.</span></span> |[<span data-ttu-id="33a5c-136">Set up virtual array as file server</span><span class="sxs-lookup"><span data-stu-id="33a5c-136">Set up virtual array as file server</span></span>](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[<span data-ttu-id="33a5c-137">Set up virtual array as iSCSI server</span><span class="sxs-lookup"><span data-stu-id="33a5c-137">Set up virtual array as iSCSI server</span></span>](storsimple-virtual-array-deploy3-iscsi-setup.md) |

<span data-ttu-id="33a5c-138">You can now begin to set up the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33a5c-138">You can now begin to set up the Azure portal.</span></span>

## <a name="configuration-checklist"></a><span data-ttu-id="33a5c-139">Configuration checklist</span><span class="sxs-lookup"><span data-stu-id="33a5c-139">Configuration checklist</span></span>

<span data-ttu-id="33a5c-140">The configuration checklist describes the information that you need to collect before you configure the software on your StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="33a5c-140">The configuration checklist describes the information that you need to collect before you configure the software on your StorSimple Virtual Array.</span></span> <span data-ttu-id="33a5c-141">Preparing this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span><span class="sxs-lookup"><span data-stu-id="33a5c-141">Preparing this information ahead of time helps streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="33a5c-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of the following checklists.</span><span class="sxs-lookup"><span data-stu-id="33a5c-142">Depending upon whether your StorSimple Virtual Array is deployed as a file server or an iSCSI server, you need one of the following checklists.</span></span>

* <span data-ttu-id="33a5c-143">Download the [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="33a5c-143">Download the [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).</span></span>
* <span data-ttu-id="33a5c-144">Download the [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span><span class="sxs-lookup"><span data-stu-id="33a5c-144">Download the [StorSimple Virtual Array iSCSI Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33a5c-145">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33a5c-145">Prerequisites</span></span>

<span data-ttu-id="33a5c-146">Here you find the configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and the datacenter network.</span><span class="sxs-lookup"><span data-stu-id="33a5c-146">Here you find the configuration prerequisites for your StorSimple Device Manager service, your StorSimple Virtual Array, and the datacenter network.</span></span>

### <a name="for-the-storsimple-device-manager-service"></a><span data-ttu-id="33a5c-147">For the StorSimple Device Manager service</span><span class="sxs-lookup"><span data-stu-id="33a5c-147">For the StorSimple Device Manager service</span></span>

<span data-ttu-id="33a5c-148">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="33a5c-148">Before you begin, make sure that:</span></span>

* <span data-ttu-id="33a5c-149">You have your Microsoft account with access credentials.</span><span class="sxs-lookup"><span data-stu-id="33a5c-149">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="33a5c-150">You have your Microsoft Azure storage account with access credentials.</span><span class="sxs-lookup"><span data-stu-id="33a5c-150">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="33a5c-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-151">Your Microsoft Azure subscription should be enabled for StorSimple Device Manager service.</span></span>

### <a name="for-the-storsimple-virtual-array"></a><span data-ttu-id="33a5c-152">For the StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="33a5c-152">For the StorSimple Virtual Array</span></span>

<span data-ttu-id="33a5c-153">Before you deploy a virtual array, make sure that:</span><span class="sxs-lookup"><span data-stu-id="33a5c-153">Before you deploy a virtual array, make sure that:</span></span>

* <span data-ttu-id="33a5c-154">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.0, 5.5 or 6.0) that can be used to a provision a device.</span><span class="sxs-lookup"><span data-stu-id="33a5c-154">You have access to a host system running Hyper-V on Windows Server 2008 R2 or later or VMware (ESXi 5.0, 5.5 or 6.0) that can be used to a provision a device.</span></span>
* <span data-ttu-id="33a5c-155">The host system is able to dedicate the following resources to provision your virtual array:</span><span class="sxs-lookup"><span data-stu-id="33a5c-155">The host system is able to dedicate the following resources to provision your virtual array:</span></span>
  
  * <span data-ttu-id="33a5c-156">A minimum of 4 cores.</span><span class="sxs-lookup"><span data-stu-id="33a5c-156">A minimum of 4 cores.</span></span>
  * <span data-ttu-id="33a5c-157">At least 8 GB of RAM.</span><span class="sxs-lookup"><span data-stu-id="33a5c-157">At least 8 GB of RAM.</span></span> <span data-ttu-id="33a5c-158">If you plan to configure the virtual array as file server, 8 GB supports 2 million files.</span><span class="sxs-lookup"><span data-stu-id="33a5c-158">If you plan to configure the virtual array as file server, 8 GB supports 2 million files.</span></span> <span data-ttu-id="33a5c-159">You need 16 GB RAM to support 2 - 4 million files.</span><span class="sxs-lookup"><span data-stu-id="33a5c-159">You need 16 GB RAM to support 2 - 4 million files.</span></span>
  * <span data-ttu-id="33a5c-160">One network interface.</span><span class="sxs-lookup"><span data-stu-id="33a5c-160">One network interface.</span></span>
  * <span data-ttu-id="33a5c-161">A 500 GB virtual disk for system data.</span><span class="sxs-lookup"><span data-stu-id="33a5c-161">A 500 GB virtual disk for system data.</span></span>

### <a name="for-the-datacenter-network"></a><span data-ttu-id="33a5c-162">For the datacenter network</span><span class="sxs-lookup"><span data-stu-id="33a5c-162">For the datacenter network</span></span>

<span data-ttu-id="33a5c-163">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="33a5c-163">Before you begin, make sure that:</span></span>

* <span data-ttu-id="33a5c-164">The network in your datacenter is configured as per the networking requirements for your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="33a5c-164">The network in your datacenter is configured as per the networking requirements for your StorSimple device.</span></span> <span data-ttu-id="33a5c-165">For more information, see the [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="33a5c-165">For more information, see the [StorSimple Virtual Array System Requirements](storsimple-ova-system-requirements.md).</span></span>
* <span data-ttu-id="33a5c-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span><span class="sxs-lookup"><span data-stu-id="33a5c-166">Your StorSimple Virtual Array has a dedicated 5 Mbps Internet bandwidth (or more) available at all times.</span></span> <span data-ttu-id="33a5c-167">This bandwidth should not be shared with any other applications.</span><span class="sxs-lookup"><span data-stu-id="33a5c-167">This bandwidth should not be shared with any other applications.</span></span>

## <a name="step-by-step-preparation"></a><span data-ttu-id="33a5c-168">Step-by-step preparation</span><span class="sxs-lookup"><span data-stu-id="33a5c-168">Step-by-step preparation</span></span>

<span data-ttu-id="33a5c-169">Use the following step-by-step instructions to prepare your portal for the StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-169">Use the following step-by-step instructions to prepare your portal for the StorSimple Device Manager service.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="33a5c-170">Step 1: Create a new service</span><span class="sxs-lookup"><span data-stu-id="33a5c-170">Step 1: Create a new service</span></span>

<span data-ttu-id="33a5c-171">A single instance of the StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span><span class="sxs-lookup"><span data-stu-id="33a5c-171">A single instance of the StorSimple Device Manager service can manage multiple StorSimple Virtual Arrays.</span></span> <span data-ttu-id="33a5c-172">Perform the following steps to create an instance of the StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-172">Perform the following steps to create an instance of the StorSimple Device Manager service.</span></span> <span data-ttu-id="33a5c-173">If you have an existing StorSimple Device Manager service to manage your virtual arrays, skip this step and go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="33a5c-173">If you have an existing StorSimple Device Manager service to manage your virtual arrays, skip this step and go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> <span data-ttu-id="33a5c-174">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-174">If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service.</span></span>
> 
> * <span data-ttu-id="33a5c-175">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span><span class="sxs-lookup"><span data-stu-id="33a5c-175">If you did not create a storage account automatically, go to [Configure a new storage account for the service](#optional-step-configure-a-new-storage-account-for-the-service) for detailed instructions.</span></span>
> * <span data-ttu-id="33a5c-176">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="33a5c-176">If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span>
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="33a5c-177">Step 2: Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="33a5c-177">Step 2: Get the service registration key</span></span>

<span data-ttu-id="33a5c-178">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span><span class="sxs-lookup"><span data-stu-id="33a5c-178">After the StorSimple Device Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="33a5c-179">This key is used to register and connect your StorSimple device with the service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-179">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="33a5c-180">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33a5c-180">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> <span data-ttu-id="33a5c-181">The service registration key is used to register all the StorSimple Device Manager devices that need to register with your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-181">The service registration key is used to register all the StorSimple Device Manager devices that need to register with your StorSimple Device Manager service.</span></span>
> 
> 

## <a name="step-3-download-the-virtual-array-image"></a><span data-ttu-id="33a5c-182">Step 3: Download the virtual array image</span><span class="sxs-lookup"><span data-stu-id="33a5c-182">Step 3: Download the virtual array image</span></span>

<span data-ttu-id="33a5c-183">After you have the service registration key, you will need to download the appropriate virtual array image to provision a virtual array on your host system.</span><span class="sxs-lookup"><span data-stu-id="33a5c-183">After you have the service registration key, you will need to download the appropriate virtual array image to provision a virtual array on your host system.</span></span> <span data-ttu-id="33a5c-184">The virtual array images are operating system specific and can be downloaded from the Quick Start page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33a5c-184">The virtual array images are operating system specific and can be downloaded from the Quick Start page in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33a5c-185">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-185">The software running on the StorSimple Virtual Array may only be used with the StorSimple Device Manager service.</span></span>
> 
> 

<span data-ttu-id="33a5c-186">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33a5c-186">Perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-get-the-virtual-array-image"></a><span data-ttu-id="33a5c-187">To get the virtual array image</span><span class="sxs-lookup"><span data-stu-id="33a5c-187">To get the virtual array image</span></span>

1. <span data-ttu-id="33a5c-188">Sign into the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33a5c-188">Sign into the [Azure portal](https://portal.azure.com/).</span></span> 
2. <span data-ttu-id="33a5c-189">In the Azure portal, click **Browse > StorSimple Device Managers**.</span><span class="sxs-lookup"><span data-stu-id="33a5c-189">In the Azure portal, click **Browse > StorSimple Device Managers**.</span></span>
3. <span data-ttu-id="33a5c-190">Select an existing StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-190">Select an existing StorSimple Device Manager service.</span></span> <span data-ttu-id="33a5c-191">In the **StorSimple Device Manager** blade, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="33a5c-191">In the **StorSimple Device Manager** blade, click **Quick Start**.</span></span> 
4. <span data-ttu-id="33a5c-192">Click the link corresponding to the image that you want to download from the Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="33a5c-192">Click the link corresponding to the image that you want to download from the Microsoft Download Center.</span></span> <span data-ttu-id="33a5c-193">The image files are approximately 4.8 GB.</span><span class="sxs-lookup"><span data-stu-id="33a5c-193">The image files are approximately 4.8 GB.</span></span>
   
   * <span data-ttu-id="33a5c-194">VHDX for Hyper-V on Windows Server 2012 and later</span><span class="sxs-lookup"><span data-stu-id="33a5c-194">VHDX for Hyper-V on Windows Server 2012 and later</span></span>
   * <span data-ttu-id="33a5c-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span><span class="sxs-lookup"><span data-stu-id="33a5c-195">VHD for Hyper-V on Windows Server 2008 R2 and later</span></span>
   * <span data-ttu-id="33a5c-196">VMDK for VMWare ESXi 5.0, 5.5 or 6.0</span><span class="sxs-lookup"><span data-stu-id="33a5c-196">VMDK for VMWare ESXi 5.0, 5.5 or 6.0</span></span>
5. <span data-ttu-id="33a5c-197">Download and unzip the file to a local drive, making a note of where the unzipped file is located.</span><span class="sxs-lookup"><span data-stu-id="33a5c-197">Download and unzip the file to a local drive, making a note of where the unzipped file is located.</span></span>

## <a name="optional-step-configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="33a5c-198">Optional step: Configure a new storage account for the service</span><span class="sxs-lookup"><span data-stu-id="33a5c-198">Optional step: Configure a new storage account for the service</span></span>

<span data-ttu-id="33a5c-199">This step is optional and should be performed only if you did not enable the automatic creation of a storage account with your service.</span><span class="sxs-lookup"><span data-stu-id="33a5c-199">This step is optional and should be performed only if you did not enable the automatic creation of a storage account with your service.</span></span>

<span data-ttu-id="33a5c-200">If you need to create an Azure storage account in a different region, see [How to create a storage account](../storage/common/storage-quickstart-create-account.md) for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="33a5c-200">If you need to create an Azure storage account in a different region, see [How to create a storage account](../storage/common/storage-quickstart-create-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="33a5c-201">Perform the following steps in the [Azure portal](https://ms.portal.azure.com/) on the StorSimple Device Manager service page to add an existing Microsoft Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="33a5c-201">Perform the following steps in the [Azure portal](https://ms.portal.azure.com/) on the StorSimple Device Manager service page to add an existing Microsoft Azure storage account.</span></span>

#### <a name="to-add-a-storage-account-credential-that-has-the-same-azure-subscription-as-the-device-manager-service"></a><span data-ttu-id="33a5c-202">To add a storage account credential that has the same Azure subscription as the Device Manager service</span><span class="sxs-lookup"><span data-stu-id="33a5c-202">To add a storage account credential that has the same Azure subscription as the Device Manager service</span></span>

1. <span data-ttu-id="33a5c-203">Navigate to your Device Manager service, select and double-click it.</span><span class="sxs-lookup"><span data-stu-id="33a5c-203">Navigate to your Device Manager service, select and double-click it.</span></span> <span data-ttu-id="33a5c-204">This opens the **Overview** blade.</span><span class="sxs-lookup"><span data-stu-id="33a5c-204">This opens the **Overview** blade.</span></span>
2. <span data-ttu-id="33a5c-205">Select **Storage account credentials** within the **Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="33a5c-205">Select **Storage account credentials** within the **Configuration** section.</span></span>
3. <span data-ttu-id="33a5c-206">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="33a5c-206">Click **Add**.</span></span>
4. <span data-ttu-id="33a5c-207">In the **Add a storage account** blade, do the following:</span><span class="sxs-lookup"><span data-stu-id="33a5c-207">In the **Add a storage account** blade, do the following:</span></span>
   
    1. <span data-ttu-id="33a5c-208">For **Subscription**, select **Current**.</span><span class="sxs-lookup"><span data-stu-id="33a5c-208">For **Subscription**, select **Current**.</span></span>
   
    2. <span data-ttu-id="33a5c-209">Provide the name of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="33a5c-209">Provide the name of your Azure storage account.</span></span>
   
    3. <span data-ttu-id="33a5c-210">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span><span class="sxs-lookup"><span data-stu-id="33a5c-210">Select **Enable** to create a secure channel for network communication between your StorSimple device and the cloud.</span></span> <span data-ttu-id="33a5c-211">Select **Disable** only if you are operating within a private cloud.</span><span class="sxs-lookup"><span data-stu-id="33a5c-211">Select **Disable** only if you are operating within a private cloud.</span></span>
   
    4. <span data-ttu-id="33a5c-212">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="33a5c-212">Click **Add**.</span></span> <span data-ttu-id="33a5c-213">You are notified after the storage account is successfully created.</span><span class="sxs-lookup"><span data-stu-id="33a5c-213">You are notified after the storage account is successfully created.</span></span><br></br>
   
     ![Add an existing storage account credential](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a><span data-ttu-id="33a5c-215">Next step</span><span class="sxs-lookup"><span data-stu-id="33a5c-215">Next step</span></span>

<span data-ttu-id="33a5c-216">The next step is to provision a virtual machine for your StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="33a5c-216">The next step is to provision a virtual machine for your StorSimple Virtual Array.</span></span> <span data-ttu-id="33a5c-217">Depending on your host operating system, see the detailed instructions in:</span><span class="sxs-lookup"><span data-stu-id="33a5c-217">Depending on your host operating system, see the detailed instructions in:</span></span>

* [<span data-ttu-id="33a5c-218">Provision a StorSimple Virtual Array in Hyper-V</span><span class="sxs-lookup"><span data-stu-id="33a5c-218">Provision a StorSimple Virtual Array in Hyper-V</span></span>](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [<span data-ttu-id="33a5c-219">Provision a StorSimple Virtual Array in VMware</span><span class="sxs-lookup"><span data-stu-id="33a5c-219">Provision a StorSimple Virtual Array in VMware</span></span>](storsimple-virtual-array-deploy2-provision-vmware.md)

