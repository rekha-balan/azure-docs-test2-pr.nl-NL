---
title: Deploy your StorSimple device (Update 2) | Microsoft Docs
description: Describes the steps and best practices for deploying the StorSimple Update 2 device and service.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 7dff0612-617b-4fc8-a3fe-994c24bc7c51
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: cc2704a6fd66d75bd860823d25cd7b044d9801db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550548"
---
# <a name="deploy-your-on-premises-storsimple-device-update-2"></a><span data-ttu-id="2b1ac-103">Deploy your on-premises StorSimple device (Update 2)</span><span class="sxs-lookup"><span data-stu-id="2b1ac-103">Deploy your on-premises StorSimple device (Update 2)</span></span>
> [!div class="op_single_selector"]
> * [Update 2 & later ](storsimple-deployment-walkthrough-u2.md)
> * [Update 1](storsimple-deployment-walkthrough-u1.md)
> * [GA Release](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2b1ac-107">Overview</span><span class="sxs-lookup"><span data-stu-id="2b1ac-107">Overview</span></span>
<span data-ttu-id="2b1ac-108">Welcome to Microsoft Azure StorSimple device deployment.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-108">Welcome to Microsoft Azure StorSimple device deployment.</span></span> <span data-ttu-id="2b1ac-109">These deployment tutorials apply to StorSimple 8000 Series Update 2.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-109">These deployment tutorials apply to StorSimple 8000 Series Update 2.</span></span> <span data-ttu-id="2b1ac-110">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-110">This series of tutorials includes a configuration checklist, configuration prerequisites, and detailed configuration steps for your StorSimple device.</span></span>

<span data-ttu-id="2b1ac-111">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-111">The information in these tutorials assumes that you have reviewed the safety precautions, and unpacked, racked, and cabled your StorSimple device.</span></span> <span data-ttu-id="2b1ac-112">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="2b1ac-112">If you still need to perform those tasks, start with reviewing the [safety precautions](storsimple-safety.md).</span></span> <span data-ttu-id="2b1ac-113">Follow the device specific instructions to unpack, rack mount, and cable your device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-113">Follow the device specific instructions to unpack, rack mount, and cable your device.</span></span>

* [<span data-ttu-id="2b1ac-114">Unpack, rack mount, and cable your 8100</span><span class="sxs-lookup"><span data-stu-id="2b1ac-114">Unpack, rack mount, and cable your 8100</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="2b1ac-115">Unpack, rack mount, and cable your 8600</span><span class="sxs-lookup"><span data-stu-id="2b1ac-115">Unpack, rack mount, and cable your 8600</span></span>](storsimple-8600-hardware-installation.md)

<span data-ttu-id="2b1ac-116">You will need administrator privileges to complete the setup and configuration process.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-116">You will need administrator privileges to complete the setup and configuration process.</span></span> <span data-ttu-id="2b1ac-117">We recommend that you review the configuration checklist before you begin.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-117">We recommend that you review the configuration checklist before you begin.</span></span> <span data-ttu-id="2b1ac-118">The deployment and configuration process can take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-118">The deployment and configuration process can take some time to complete.</span></span>

> [!NOTE]
> The StorSimple deployment information published on the Microsoft Azure website applies to StorSimple 8000 series devices only. For complete information about the 7000 series devices, go to: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). For 7000 series deployment information, see the [StorSimple System Quick Start Guide](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a><span data-ttu-id="2b1ac-122">Deployment steps</span><span class="sxs-lookup"><span data-stu-id="2b1ac-122">Deployment steps</span></span>
<span data-ttu-id="2b1ac-123">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-123">Perform these required steps to configure your StorSimple device and connect it to your StorSimple Manager service.</span></span> <span data-ttu-id="2b1ac-124">In addition to the required steps, there are optional steps and procedures you may need during the deployment.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-124">In addition to the required steps, there are optional steps and procedures you may need during the deployment.</span></span> <span data-ttu-id="2b1ac-125">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-125">The step-by-step deployment instructions indicate when you should perform each of these optional steps.</span></span>

| <span data-ttu-id="2b1ac-126">Step</span><span class="sxs-lookup"><span data-stu-id="2b1ac-126">Step</span></span> | <span data-ttu-id="2b1ac-127">Description</span><span class="sxs-lookup"><span data-stu-id="2b1ac-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b1ac-128">**PREREQUISITES**</span><span class="sxs-lookup"><span data-stu-id="2b1ac-128">**PREREQUISITES**</span></span> |<span data-ttu-id="2b1ac-129">These need to be completed in preparation for the upcoming deployment.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-129">These need to be completed in preparation for the upcoming deployment.</span></span> |
| [<span data-ttu-id="2b1ac-130">Deployment configuration checklist</span><span class="sxs-lookup"><span data-stu-id="2b1ac-130">Deployment configuration checklist</span></span>](#deployment-configuration-checklist) |<span data-ttu-id="2b1ac-131">Use this checklist to gather and record information prior to and during the deployment.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-131">Use this checklist to gather and record information prior to and during the deployment.</span></span> |
| [<span data-ttu-id="2b1ac-132">Deployment prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b1ac-132">Deployment prerequisites</span></span>](#deployment-prerequisites) |<span data-ttu-id="2b1ac-133">These  validate the environment is ready for deployment.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-133">These  validate the environment is ready for deployment.</span></span> |
|  | |
| <span data-ttu-id="2b1ac-134">**STEP-BY-STEP DEPLOYMENT**</span><span class="sxs-lookup"><span data-stu-id="2b1ac-134">**STEP-BY-STEP DEPLOYMENT**</span></span> |<span data-ttu-id="2b1ac-135">These steps are required to deploy your StorSimple device in production.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-135">These steps are required to deploy your StorSimple device in production.</span></span> |
| [<span data-ttu-id="2b1ac-136">Step 1: Create a new service</span><span class="sxs-lookup"><span data-stu-id="2b1ac-136">Step 1: Create a new service</span></span>](#step-1-create-a-new-service) |<span data-ttu-id="2b1ac-137">Set up cloud management and storage for your   StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-137">Set up cloud management and storage for your   StorSimple device.</span></span> <span data-ttu-id="2b1ac-138">*Skip this step if you have an existing service for other StorSimple devices*.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-138">*Skip this step if you have an existing service for other StorSimple devices*.</span></span> |
| [<span data-ttu-id="2b1ac-139">Step 2: Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="2b1ac-139">Step 2: Get the service registration key</span></span>](#step-2-get-the-service-registration-key) |<span data-ttu-id="2b1ac-140">Use this key to register & connect your StorSimple device with the management service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-140">Use this key to register & connect your StorSimple device with the management service.</span></span> |
| [<span data-ttu-id="2b1ac-141">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="2b1ac-141">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |<span data-ttu-id="2b1ac-142">Connect the device to your network and register it with Azure to complete the setup using the management service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-142">Connect the device to your network and register it with Azure to complete the setup using the management service.</span></span> |
| [<span data-ttu-id="2b1ac-143">Step 4: Complete minimum device setup</span><span class="sxs-lookup"><span data-stu-id="2b1ac-143">Step 4: Complete minimum device setup</span></span>](#step-4-complete-minimum-device-setup)</br>[<span data-ttu-id="2b1ac-144">Optional: Update your StorSimple device</span><span class="sxs-lookup"><span data-stu-id="2b1ac-144">Optional: Update your StorSimple device</span></span>](#scan-for-and-apply-updates) |<span data-ttu-id="2b1ac-145">Use the management service to complete the device setup and enable it to provide storage.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-145">Use the management service to complete the device setup and enable it to provide storage.</span></span> |
| [<span data-ttu-id="2b1ac-146">Step 5: Create a volume container</span><span class="sxs-lookup"><span data-stu-id="2b1ac-146">Step 5: Create a volume container</span></span>](#step-5-create-a-volume-container) |<span data-ttu-id="2b1ac-147">Create a container to provision volumes.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-147">Create a container to provision volumes.</span></span> <span data-ttu-id="2b1ac-148">A volume container has storage   account, bandwidth, and encryption settings for all the volumes contained in it.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-148">A volume container has storage   account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> |
| [<span data-ttu-id="2b1ac-149">Step 6: Create a volume</span><span class="sxs-lookup"><span data-stu-id="2b1ac-149">Step 6: Create a volume</span></span>](#step-6-create-a-volume) |<span data-ttu-id="2b1ac-150">Provision storage volume(s) on the StorSimple device for your servers.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-150">Provision storage volume(s) on the StorSimple device for your servers.</span></span> |
| [<span data-ttu-id="2b1ac-151">Step 7: Mount, initialize, and format a volume</span><span class="sxs-lookup"><span data-stu-id="2b1ac-151">Step 7: Mount, initialize, and format a volume</span></span>](#step-7-mount-initialize-and-format-a-volume)</br>[<span data-ttu-id="2b1ac-152">Optional: Configure MPIO</span><span class="sxs-lookup"><span data-stu-id="2b1ac-152">Optional: Configure MPIO</span></span>](storsimple-configure-mpio-windows-server.md) |<span data-ttu-id="2b1ac-153">Connect your servers to the iSCSI storage provided by the device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-153">Connect your servers to the iSCSI storage provided by the device.</span></span> <span data-ttu-id="2b1ac-154">Optionally configure MPIO to ensure that your servers can tolerate link, network and interface failure.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-154">Optionally configure MPIO to ensure that your servers can tolerate link, network and interface failure.</span></span> |
| [<span data-ttu-id="2b1ac-155">Step 8: Take a backup</span><span class="sxs-lookup"><span data-stu-id="2b1ac-155">Step 8: Take a backup</span></span>](#step-8-take-a-backup) |<span data-ttu-id="2b1ac-156">Set up your backup policy to protect your data</span><span class="sxs-lookup"><span data-stu-id="2b1ac-156">Set up your backup policy to protect your data</span></span> |
|  | |
| <span data-ttu-id="2b1ac-157">**OTHER PROCEDURES**</span><span class="sxs-lookup"><span data-stu-id="2b1ac-157">**OTHER PROCEDURES**</span></span> |<span data-ttu-id="2b1ac-158">You may need to refer to these procedures as you deploy your solution.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-158">You may need to refer to these procedures as you deploy your solution.</span></span> |
| [<span data-ttu-id="2b1ac-159">Configure a new storage account for the service</span><span class="sxs-lookup"><span data-stu-id="2b1ac-159">Configure a new storage account for the service</span></span>](#configure-a-new-storage-account-for-the-service) | |
| [<span data-ttu-id="2b1ac-160">Use PuTTY to connect to the device serial console</span><span class="sxs-lookup"><span data-stu-id="2b1ac-160">Use PuTTY to connect to the device serial console</span></span>](#use-putty-to-connect-to-the-device-serial-console) | |
| [<span data-ttu-id="2b1ac-161">Get the IQN of a Windows Server host</span><span class="sxs-lookup"><span data-stu-id="2b1ac-161">Get the IQN of a Windows Server host</span></span>](#get-the-iqn-of-a-windows-server-host) | |
| [<span data-ttu-id="2b1ac-162">Create a manual backup</span><span class="sxs-lookup"><span data-stu-id="2b1ac-162">Create a manual backup</span></span>](#create-a-manual-backup) | |

## <a name="deployment-configuration-checklist"></a><span data-ttu-id="2b1ac-163">Deployment configuration checklist</span><span class="sxs-lookup"><span data-stu-id="2b1ac-163">Deployment configuration checklist</span></span>
<span data-ttu-id="2b1ac-164">Before you deploy your device, you will need to collect information to configure the software on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-164">Before you deploy your device, you will need to collect information to configure the software on your StorSimple device.</span></span> <span data-ttu-id="2b1ac-165">Preparing some of this information ahead of time will help streamline the process of deploying the StorSimple device in your environment.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-165">Preparing some of this information ahead of time will help streamline the process of deploying the StorSimple device in your environment.</span></span> <span data-ttu-id="2b1ac-166">Download and use this checklist to note down the configuration details as you deploy your device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-166">Download and use this checklist to note down the configuration details as you deploy your device.</span></span>

* [<span data-ttu-id="2b1ac-167">Download StorSimple deployment configuration checklist</span><span class="sxs-lookup"><span data-stu-id="2b1ac-167">Download StorSimple deployment configuration checklist</span></span>](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a><span data-ttu-id="2b1ac-168">Deployment prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b1ac-168">Deployment prerequisites</span></span>
<span data-ttu-id="2b1ac-169">The following sections explain the configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-169">The following sections explain the configuration prerequisites for your StorSimple Manager service and your StorSimple device.</span></span>

### <a name="for-the-storsimple-manager-service"></a><span data-ttu-id="2b1ac-170">For the StorSimple Manager service</span><span class="sxs-lookup"><span data-stu-id="2b1ac-170">For the StorSimple Manager service</span></span>
<span data-ttu-id="2b1ac-171">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="2b1ac-171">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2b1ac-172">You have your Microsoft account with access credentials.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-172">You have your Microsoft account with access credentials.</span></span>
* <span data-ttu-id="2b1ac-173">You have your Microsoft Azure storage account with access credentials.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-173">You have your Microsoft Azure storage account with access credentials.</span></span>
* <span data-ttu-id="2b1ac-174">Your Microsoft Azure subscription is enabled for the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-174">Your Microsoft Azure subscription is enabled for the StorSimple Manager service.</span></span> <span data-ttu-id="2b1ac-175">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span><span class="sxs-lookup"><span data-stu-id="2b1ac-175">Your subscription should be purchased through the [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).</span></span>
* <span data-ttu-id="2b1ac-176">You have access to terminal emulation software such as PuTTY.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-176">You have access to terminal emulation software such as PuTTY.</span></span>

### <a name="for-the-device-in-the-datacenter"></a><span data-ttu-id="2b1ac-177">For the device in the datacenter</span><span class="sxs-lookup"><span data-stu-id="2b1ac-177">For the device in the datacenter</span></span>
<span data-ttu-id="2b1ac-178">Before configuring the device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span><span class="sxs-lookup"><span data-stu-id="2b1ac-178">Before configuring the device, make sure that your device is fully unpacked, mounted on a rack and fully cabled for power, network, and serial access as described in:</span></span>

* [<span data-ttu-id="2b1ac-179">Unpack, rack mount, and cable your 8100 device</span><span class="sxs-lookup"><span data-stu-id="2b1ac-179">Unpack, rack mount, and cable your 8100 device</span></span>](storsimple-8100-hardware-installation.md)
* [<span data-ttu-id="2b1ac-180">Unpack, rack mount, and cable your 8600 device</span><span class="sxs-lookup"><span data-stu-id="2b1ac-180">Unpack, rack mount, and cable your 8600 device</span></span>](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a><span data-ttu-id="2b1ac-181">For the network in the datacenter</span><span class="sxs-lookup"><span data-stu-id="2b1ac-181">For the network in the datacenter</span></span>
<span data-ttu-id="2b1ac-182">Before you begin, make sure that:</span><span class="sxs-lookup"><span data-stu-id="2b1ac-182">Before you begin, make sure that:</span></span>

* <span data-ttu-id="2b1ac-183">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span><span class="sxs-lookup"><span data-stu-id="2b1ac-183">The ports in your datacenter firewall are opened to allow for iSCSI and cloud traffic as described in [Networking requirements for your StorSimple device](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).</span></span>

## <a name="step-by-step-deployment"></a><span data-ttu-id="2b1ac-184">Step-by-step deployment</span><span class="sxs-lookup"><span data-stu-id="2b1ac-184">Step-by-step deployment</span></span>
<span data-ttu-id="2b1ac-185">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-185">Use the following step-by-step instructions to deploy your StorSimple device in the datacenter.</span></span>

## <a name="step-1-create-a-new-service"></a><span data-ttu-id="2b1ac-186">Step 1: Create a new service</span><span class="sxs-lookup"><span data-stu-id="2b1ac-186">Step 1: Create a new service</span></span>
<span data-ttu-id="2b1ac-187">A StorSimple Manager service can manage multiple StorSimple devices.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-187">A StorSimple Manager service can manage multiple StorSimple devices.</span></span> <span data-ttu-id="2b1ac-188">Perform the following steps to create a new instance of the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-188">Perform the following steps to create a new instance of the StorSimple Manager service.</span></span>

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> If you did not enable the automatic creation of a storage account with your service, you will need to create at least one storage account after you have successfully created a service. This storage account will be used when you create a volume container. 
> 
> * If you did not create a storage account automatically, go to [Configure a new storage account for the service](#configure-a-new-storage-account-for-the-service) for detailed instructions. 
> * If you enabled the automatic creation of a storage account, go to [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-the-service-registration-key"></a><span data-ttu-id="2b1ac-193">Step 2: Get the service registration key</span><span class="sxs-lookup"><span data-stu-id="2b1ac-193">Step 2: Get the service registration key</span></span>
<span data-ttu-id="2b1ac-194">After the StorSimple Manager service is up and running, you will need to get the service registration key.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-194">After the StorSimple Manager service is up and running, you will need to get the service registration key.</span></span> <span data-ttu-id="2b1ac-195">This key is used to register and connect your StorSimple device with the service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-195">This key is used to register and connect your StorSimple device with the service.</span></span>

<span data-ttu-id="2b1ac-196">Perform the following steps in the Management Portal.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-196">Perform the following steps in the Management Portal.</span></span>

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a><span data-ttu-id="2b1ac-197">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="2b1ac-197">Step 3: Configure and register the device through Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="2b1ac-198">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-198">Use Windows PowerShell for StorSimple to complete the initial setup of your StorSimple device as explained in the following procedure.</span></span> <span data-ttu-id="2b1ac-199">You will need to use terminal emulation software to complete this step.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-199">You will need to use terminal emulation software to complete this step.</span></span> <span data-ttu-id="2b1ac-200">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="2b1ac-200">For more information, see [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console).</span></span>

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a><span data-ttu-id="2b1ac-201">Step 4: Complete minimum device setup</span><span class="sxs-lookup"><span data-stu-id="2b1ac-201">Step 4: Complete minimum device setup</span></span>
<span data-ttu-id="2b1ac-202">For the minimum device configuration of your StorSimple device, you are required to:</span><span class="sxs-lookup"><span data-stu-id="2b1ac-202">For the minimum device configuration of your StorSimple device, you are required to:</span></span> 

* <span data-ttu-id="2b1ac-203">Set up the secondary DNS server.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-203">Set up the secondary DNS server.</span></span>
* <span data-ttu-id="2b1ac-204">Enable iSCSI on at least one network interface.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-204">Enable iSCSI on at least one network interface.</span></span>
* <span data-ttu-id="2b1ac-205">Assign fixed IP addresses to both the controllers.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-205">Assign fixed IP addresses to both the controllers.</span></span>

<span data-ttu-id="2b1ac-206">Perform the following steps in the Management Portal to complete the minimum device setup.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-206">Perform the following steps in the Management Portal to complete the minimum device setup.</span></span>

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a><span data-ttu-id="2b1ac-207">Step 5: Create a volume container</span><span class="sxs-lookup"><span data-stu-id="2b1ac-207">Step 5: Create a volume container</span></span>
<span data-ttu-id="2b1ac-208">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-208">A volume container has storage account, bandwidth, and encryption settings for all the volumes contained in it.</span></span> <span data-ttu-id="2b1ac-209">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-209">You will need to create a volume container before you can start provisioning volumes on your StorSimple device.</span></span> 

<span data-ttu-id="2b1ac-210">Perform the following steps in the Management Portal to create a volume container.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-210">Perform the following steps in the Management Portal to create a volume container.</span></span>

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a><span data-ttu-id="2b1ac-211">Step 6: Create a volume</span><span class="sxs-lookup"><span data-stu-id="2b1ac-211">Step 6: Create a volume</span></span>
<span data-ttu-id="2b1ac-212">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-212">After you create a volume container, you can provision a storage volume on the StorSimple device for your servers.</span></span> <span data-ttu-id="2b1ac-213">Perform the following steps in the Management Portal to create a volume.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-213">Perform the following steps in the Management Portal to create a volume.</span></span>

> [!IMPORTANT]
> StorSimple Manager can create both thin and fully provisioned volumes. You cannot however create partially provisioned volumes. 
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a><span data-ttu-id="2b1ac-216">Step 7: Mount, initialize, and format a volume</span><span class="sxs-lookup"><span data-stu-id="2b1ac-216">Step 7: Mount, initialize, and format a volume</span></span>
<span data-ttu-id="2b1ac-217">The following steps are performed on your Windows Server host.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-217">The following steps are performed on your Windows Server host.</span></span> 

> [!IMPORTANT]
> * For the high availability of your StorSimple solution, we recommend that you configure MPIO on your host servers (optional) prior to configuring iSCSI. MPIO configuration on host servers will ensure that the servers can tolerate a link, network, or interface failure.
> * For MPIO and iSCSI installation and configuration instructions on Windows Server host, go to [Configure MPIO for your StorSimple device](storsimple-configure-mpio-windows-server.md). These will also include the steps to mount, initialize and format StorSimple volumes.
> * For MPIO and iSCSI installation and configuration instructions on a Linux host, go to [Configure MPIO for your StorSimple Linux host](storsimple-configure-mpio-on-linux.md)
> 
> 

<span data-ttu-id="2b1ac-223">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-223">If you decide not to configure MPIO, perform the following steps to mount, initialize, and format your StorSimple volumes on a Windows Server host.</span></span>

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a><span data-ttu-id="2b1ac-224">Step 8: Take a backup</span><span class="sxs-lookup"><span data-stu-id="2b1ac-224">Step 8: Take a backup</span></span>
<span data-ttu-id="2b1ac-225">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-225">Backups provide point-in-time protection of volumes and improve recoverability while minimizing restore times.</span></span> <span data-ttu-id="2b1ac-226">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-226">You can take two types of backup on your StorSimple device: local snapshots and cloud snapshots.</span></span> <span data-ttu-id="2b1ac-227">Each of these backup types can be **Scheduled** or **Manual**.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-227">Each of these backup types can be **Scheduled** or **Manual**.</span></span> 

<span data-ttu-id="2b1ac-228">Perform the following steps in the Management Portal to create a scheduled backup.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-228">Perform the following steps in the Management Portal to create a scheduled backup.</span></span>

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

<span data-ttu-id="2b1ac-229">You can take a manual backup at any time.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-229">You can take a manual backup at any time.</span></span> <span data-ttu-id="2b1ac-230">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span><span class="sxs-lookup"><span data-stu-id="2b1ac-230">For procedures, go to [Create a manual backup](#create-a-manual-backup).</span></span> 

## <a name="configure-a-new-storage-account-for-the-service"></a><span data-ttu-id="2b1ac-231">Configure a new storage account for the service</span><span class="sxs-lookup"><span data-stu-id="2b1ac-231">Configure a new storage account for the service</span></span>
<span data-ttu-id="2b1ac-232">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-232">This is an optional step that you need to perform only if you did not enable the automatic creation of a storage account with your service.</span></span> <span data-ttu-id="2b1ac-233">A Microsoft Azure storage account is required to create a StorSimple volume container.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-233">A Microsoft Azure storage account is required to create a StorSimple volume container.</span></span>

<span data-ttu-id="2b1ac-234">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/storage-create-storage-account.md) for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-234">If you need to create an Azure storage account in a different region, see [About Azure Storage Accounts](../storage/storage-create-storage-account.md) for step-by-step instructions.</span></span>

<span data-ttu-id="2b1ac-235">Perform the following steps in the Management Portal, on the **StorSimple Manager service** page.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-235">Perform the following steps in the Management Portal, on the **StorSimple Manager service** page.</span></span>

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a><span data-ttu-id="2b1ac-236">Use PuTTY to connect to the device serial console</span><span class="sxs-lookup"><span data-stu-id="2b1ac-236">Use PuTTY to connect to the device serial console</span></span>
<span data-ttu-id="2b1ac-237">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-237">To connect to Windows PowerShell for StorSimple, you need to use terminal emulation software such as PuTTY.</span></span> <span data-ttu-id="2b1ac-238">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-238">You can use PuTTY when you access the device directly through the serial console or by opening a telnet session from a remote computer.</span></span>

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a><span data-ttu-id="2b1ac-239">Scan for and apply updates</span><span class="sxs-lookup"><span data-stu-id="2b1ac-239">Scan for and apply updates</span></span>
<span data-ttu-id="2b1ac-240">Updating your device can take several hours.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-240">Updating your device can take several hours.</span></span> <span data-ttu-id="2b1ac-241">Perform the following steps to scan for and apply updates on your device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-241">Perform the following steps to scan for and apply updates on your device.</span></span>
<!--can take 1-4 hours--> 

<!--If you have a gateway configured on a network interface other than Data 0, you will need to disable Data 2 and Data 3 network interfaces before installing the update. Go to **Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after the device is updated.-->

#### <a name="to-update-your-device"></a><span data-ttu-id="2b1ac-242">To update your device</span><span class="sxs-lookup"><span data-stu-id="2b1ac-242">To update your device</span></span>
1. <span data-ttu-id="2b1ac-243">On the device **Quick Start** page, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-243">On the device **Quick Start** page, click **Devices**.</span></span> <span data-ttu-id="2b1ac-244">Select the physical device, click **Maintenance** and then click **Scan Updates**.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-244">Select the physical device, click **Maintenance** and then click **Scan Updates**.</span></span>  
2. <span data-ttu-id="2b1ac-245">A job to scan for available updates is created.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-245">A job to scan for available updates is created.</span></span> <span data-ttu-id="2b1ac-246">If updates are available, the **Scan Updates** changes to **Install Updates**.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-246">If updates are available, the **Scan Updates** changes to **Install Updates**.</span></span> <span data-ttu-id="2b1ac-247">Click **Install Updates**.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-247">Click **Install Updates**.</span></span> 
3. <span data-ttu-id="2b1ac-248">An update job will be created.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-248">An update job will be created.</span></span> <span data-ttu-id="2b1ac-249">Monitor the status of your update by navigating to **Jobs**.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-249">Monitor the status of your update by navigating to **Jobs**.</span></span>
   
   > [!NOTE]
   > When the update job starts, it immediately displays the status as 50 percent. The status changes to 100 percent only after the update job is complete. There is no real-time status for the update process.
   > 
   > 
4. <span data-ttu-id="2b1ac-253">After the device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-253">After the device is successfully updated, enable Data 2 and Data 3 network interfaces if these were disabled.</span></span>

<!-- In step 2, you may be requested to disable Data 2 and Data 3 prior to installing the updates. You must disable these network interfaces or the updates may fail.-->

## <a name="get-the-iqn-of-a-windows-server-host"></a><span data-ttu-id="2b1ac-254">Get the IQN of a Windows Server host</span><span class="sxs-lookup"><span data-stu-id="2b1ac-254">Get the IQN of a Windows Server host</span></span>
<span data-ttu-id="2b1ac-255">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-255">Perform the following steps to get the iSCSI Qualified Name (IQN) of a Windows host that is running Windows Server® 2012.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a><span data-ttu-id="2b1ac-256">Create a manual backup</span><span class="sxs-lookup"><span data-stu-id="2b1ac-256">Create a manual backup</span></span>
<span data-ttu-id="2b1ac-257">Perform the following steps in the Management Portal to create an on-demand manual backup for a single volume on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-257">Perform the following steps in the Management Portal to create an on-demand manual backup for a single volume on your StorSimple device.</span></span>

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="2b1ac-258">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b1ac-258">Next steps</span></span>
* <span data-ttu-id="2b1ac-259">Configure a [virtual device](storsimple-virtual-device-u2.md).</span><span class="sxs-lookup"><span data-stu-id="2b1ac-259">Configure a [virtual device](storsimple-virtual-device-u2.md).</span></span>
* <span data-ttu-id="2b1ac-260">Use the [StorSimple Manager service](storsimple-manager-service-administration.md) to manage your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="2b1ac-260">Use the [StorSimple Manager service](storsimple-manager-service-administration.md) to manage your StorSimple device.</span></span>

