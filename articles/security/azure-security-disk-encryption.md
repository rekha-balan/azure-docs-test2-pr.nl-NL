---
title: Azure Disk Encryption for Windows and Linux IaaS VMs | Microsoft Docs
description: This article provides an overview of Microsoft Azure Disk Encryption for Windows and Linux IaaS VMs.
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: 3996451ccd2651f8dae2beaf7695cb151a68c647
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556740"
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="b4b16-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="b4b16-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span><span class="sxs-lookup"><span data-stu-id="b4b16-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="b4b16-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="b4b16-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span><span class="sxs-lookup"><span data-stu-id="b4b16-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="b4b16-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span><span class="sxs-lookup"><span data-stu-id="b4b16-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="b4b16-109">Overview</span><span class="sxs-lookup"><span data-stu-id="b4b16-109">Overview</span></span>
<span data-ttu-id="b4b16-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span><span class="sxs-lookup"><span data-stu-id="b4b16-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="b4b16-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span><span class="sxs-lookup"><span data-stu-id="b4b16-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="b4b16-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span><span class="sxs-lookup"><span data-stu-id="b4b16-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="b4b16-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span><span class="sxs-lookup"><span data-stu-id="b4b16-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="b4b16-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span><span class="sxs-lookup"><span data-stu-id="b4b16-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="b4b16-115">Encryption scenarios</span><span class="sxs-lookup"><span data-stu-id="b4b16-115">Encryption scenarios</span></span>
<span data-ttu-id="b4b16-116">The Azure Disk Encryption solution supports the following customer scenarios:</span><span class="sxs-lookup"><span data-stu-id="b4b16-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="b4b16-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span><span class="sxs-lookup"><span data-stu-id="b4b16-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="b4b16-118">Enable encryption on new IaaS VMs created from the Azure Gallery images</span><span class="sxs-lookup"><span data-stu-id="b4b16-118">Enable encryption on new IaaS VMs created from the Azure Gallery images</span></span>
* <span data-ttu-id="b4b16-119">Enable encryption on existing IaaS VMs running in Azure</span><span class="sxs-lookup"><span data-stu-id="b4b16-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="b4b16-120">Disable encryption on Windows IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="b4b16-121">Disable encryption on data drives for Linux IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="b4b16-122">Enable encryption of managed disk VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="b4b16-123">Update encryption settings of an existing encrypted non-premium storage VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="b4b16-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span><span class="sxs-lookup"><span data-stu-id="b4b16-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="b4b16-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="b4b16-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="b4b16-126">Integration with Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b4b16-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="b4b16-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="b4b16-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="b4b16-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="b4b16-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="b4b16-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="b4b16-131">Enable encryption on IaaS VMs running Windows Client OS</span><span class="sxs-lookup"><span data-stu-id="b4b16-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="b4b16-132">Enable encryption on volumes with mount paths</span><span class="sxs-lookup"><span data-stu-id="b4b16-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="b4b16-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span><span class="sxs-lookup"><span data-stu-id="b4b16-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="b4b16-134">Enable encryption on Linux VMs using LVM for data disks</span><span class="sxs-lookup"><span data-stu-id="b4b16-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="b4b16-135">Enable encryption on Windows VMs configured with Storage Spaces</span><span class="sxs-lookup"><span data-stu-id="b4b16-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="b4b16-136">Update encryption settings of an existing encrypted non-premium storage VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="b4b16-137">All Azure Public and AzureGov regions are supported</span><span class="sxs-lookup"><span data-stu-id="b4b16-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="b4b16-138">The solution does not support the following scenarios, features, and technology:</span><span class="sxs-lookup"><span data-stu-id="b4b16-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="b4b16-139">Basic tier IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="b4b16-140">Disabling encryption on an OS drive for Linux IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="b4b16-141">IaaS VMs that are created by using the classic VM creation method</span><span class="sxs-lookup"><span data-stu-id="b4b16-141">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="b4b16-142">Integration with your on-premises Key Management Service</span><span class="sxs-lookup"><span data-stu-id="b4b16-142">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="b4b16-143">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span><span class="sxs-lookup"><span data-stu-id="b4b16-143">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="b4b16-144">Backup and restore of encrypted VMs, encrypted without key encryption key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-144">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="b4b16-145">Update encryption settings of an existing encrypted premium storage VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-145">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-146">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-146">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="b4b16-147">It is not supported on VMs that are encrypted without KEK.</span><span class="sxs-lookup"><span data-stu-id="b4b16-147">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="b4b16-148">KEK is an optional parameter that enables VM encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-148">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="b4b16-149">This support is coming soon.</span><span class="sxs-lookup"><span data-stu-id="b4b16-149">This support is coming soon.</span></span>
> <span data-ttu-id="b4b16-150">Update encryption settings of an existing encrypted premium storage VM are not supported.</span><span class="sxs-lookup"><span data-stu-id="b4b16-150">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="b4b16-151">This support is coming soon.</span><span class="sxs-lookup"><span data-stu-id="b4b16-151">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="b4b16-152">Encryption features</span><span class="sxs-lookup"><span data-stu-id="b4b16-152">Encryption features</span></span>
<span data-ttu-id="b4b16-153">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span><span class="sxs-lookup"><span data-stu-id="b4b16-153">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="b4b16-154">Encryption of the OS volume to protect the boot volume at rest in your storage</span><span class="sxs-lookup"><span data-stu-id="b4b16-154">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="b4b16-155">Encryption of data volumes to protect the data volumes at rest in your storage</span><span class="sxs-lookup"><span data-stu-id="b4b16-155">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="b4b16-156">Disabling encryption on the OS and data drives for Windows IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-156">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="b4b16-157">Disabling encryption on the data drives for Linux IaaS VMs</span><span class="sxs-lookup"><span data-stu-id="b4b16-157">Disabling encryption on the data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="b4b16-158">Safeguarding the encryption keys and secrets in your key vault subscription</span><span class="sxs-lookup"><span data-stu-id="b4b16-158">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="b4b16-159">Reporting the encryption status of the encrypted IaaS VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-159">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="b4b16-160">Removal of disk-encryption configuration settings from the IaaS virtual machine</span><span class="sxs-lookup"><span data-stu-id="b4b16-160">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="b4b16-161">Backup and restore of encrypted VMs by using the Azure Backup service</span><span class="sxs-lookup"><span data-stu-id="b4b16-161">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-162">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-162">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="b4b16-163">It is not supported on VMs that are encrypted without KEK.</span><span class="sxs-lookup"><span data-stu-id="b4b16-163">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="b4b16-164">KEK is an optional parameter that enables VM encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-164">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="b4b16-165">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span><span class="sxs-lookup"><span data-stu-id="b4b16-165">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="b4b16-166">The disk-encryption extension for Windows.</span><span class="sxs-lookup"><span data-stu-id="b4b16-166">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="b4b16-167">The disk-encryption extension for Linux.</span><span class="sxs-lookup"><span data-stu-id="b4b16-167">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="b4b16-168">The disk-encryption PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b4b16-168">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="b4b16-169">The disk-encryption Azure command-line interface (CLI) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b4b16-169">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="b4b16-170">The disk-encryption Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="b4b16-170">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="b4b16-171">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span><span class="sxs-lookup"><span data-stu-id="b4b16-171">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="b4b16-172">For more information about the supported operating systems, see the "Prerequisites" section.</span><span class="sxs-lookup"><span data-stu-id="b4b16-172">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-173">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-173">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="b4b16-174">Value proposition</span><span class="sxs-lookup"><span data-stu-id="b4b16-174">Value proposition</span></span>
<span data-ttu-id="b4b16-175">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span><span class="sxs-lookup"><span data-stu-id="b4b16-175">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="b4b16-176">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span><span class="sxs-lookup"><span data-stu-id="b4b16-176">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="b4b16-177">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-177">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="b4b16-178">Encryption workflow</span><span class="sxs-lookup"><span data-stu-id="b4b16-178">Encryption workflow</span></span>
<span data-ttu-id="b4b16-179">To enable disk encryption for Windows and Linux VMs, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-179">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="b4b16-180">Choose an encryption scenario from among the preceding encryption scenarios.</span><span class="sxs-lookup"><span data-stu-id="b4b16-180">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="b4b16-181">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-181">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="b4b16-182">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-182">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="b4b16-183">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-183">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="b4b16-184">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-184">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="b4b16-185">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-185">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="b4b16-186">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-186">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="b4b16-187">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span><span class="sxs-lookup"><span data-stu-id="b4b16-187">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="b4b16-188">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-188">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="b4b16-190">Decryption workflow</span><span class="sxs-lookup"><span data-stu-id="b4b16-190">Decryption workflow</span></span>
<span data-ttu-id="b4b16-191">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span><span class="sxs-lookup"><span data-stu-id="b4b16-191">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="b4b16-192">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-192">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="b4b16-193">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-193">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="b4b16-194">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span><span class="sxs-lookup"><span data-stu-id="b4b16-194">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="b4b16-195">The decryption step is allowed only for data drives on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-195">The decryption step is allowed only for data drives on Linux VMs.</span></span>
2. <span data-ttu-id="b4b16-196">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span><span class="sxs-lookup"><span data-stu-id="b4b16-196">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="b4b16-197">The contents of the VM are no longer encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="b4b16-197">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-198">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span><span class="sxs-lookup"><span data-stu-id="b4b16-198">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="b4b16-199">Disabling OS disk encryption for Linux is not supported.</span><span class="sxs-lookup"><span data-stu-id="b4b16-199">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="b4b16-200">The decryption step is allowed only for data drives on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-200">The decryption step is allowed only for data drives on Linux VMs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4b16-201">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4b16-201">Prerequisites</span></span>
<span data-ttu-id="b4b16-202">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="b4b16-202">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="b4b16-203">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span><span class="sxs-lookup"><span data-stu-id="b4b16-203">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="b4b16-204">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b4b16-204">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="b4b16-205">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span><span class="sxs-lookup"><span data-stu-id="b4b16-205">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-206">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-206">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="b4b16-207">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="b4b16-207">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="b4b16-208">Azure Disk Encryption is supported on the following Linux server distributions and versions:</span><span class="sxs-lookup"><span data-stu-id="b4b16-208">Azure Disk Encryption is supported on the following Linux server distributions and versions:</span></span>

| <span data-ttu-id="b4b16-209">Linux Distribution</span><span class="sxs-lookup"><span data-stu-id="b4b16-209">Linux Distribution</span></span> | <span data-ttu-id="b4b16-210">Version</span><span class="sxs-lookup"><span data-stu-id="b4b16-210">Version</span></span> | <span data-ttu-id="b4b16-211">Volume Type Supported for Encryption</span><span class="sxs-lookup"><span data-stu-id="b4b16-211">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="b4b16-212">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b4b16-212">Ubuntu</span></span> | <span data-ttu-id="b4b16-213">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="b4b16-213">16.04-DAILY-LTS</span></span> | <span data-ttu-id="b4b16-214">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-214">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-215">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b4b16-215">Ubuntu</span></span> | <span data-ttu-id="b4b16-216">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="b4b16-216">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="b4b16-217">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-217">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-218">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b4b16-218">Ubuntu</span></span> | <span data-ttu-id="b4b16-219">12.10</span><span class="sxs-lookup"><span data-stu-id="b4b16-219">12.10</span></span> | <span data-ttu-id="b4b16-220">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-220">Data disk</span></span> |
| <span data-ttu-id="b4b16-221">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b4b16-221">Ubuntu</span></span> | <span data-ttu-id="b4b16-222">12.04</span><span class="sxs-lookup"><span data-stu-id="b4b16-222">12.04</span></span> | <span data-ttu-id="b4b16-223">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-223">Data disk</span></span> |
| <span data-ttu-id="b4b16-224">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4b16-224">RHEL</span></span> | <span data-ttu-id="b4b16-225">7.3</span><span class="sxs-lookup"><span data-stu-id="b4b16-225">7.3</span></span> | <span data-ttu-id="b4b16-226">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-226">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-227">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4b16-227">RHEL</span></span> | <span data-ttu-id="b4b16-228">7.2</span><span class="sxs-lookup"><span data-stu-id="b4b16-228">7.2</span></span> | <span data-ttu-id="b4b16-229">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-229">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-230">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4b16-230">RHEL</span></span> | <span data-ttu-id="b4b16-231">6.8</span><span class="sxs-lookup"><span data-stu-id="b4b16-231">6.8</span></span> | <span data-ttu-id="b4b16-232">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-232">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-233">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4b16-233">RHEL</span></span> | <span data-ttu-id="b4b16-234">6.7</span><span class="sxs-lookup"><span data-stu-id="b4b16-234">6.7</span></span> | <span data-ttu-id="b4b16-235">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-235">Data disk</span></span> |
| <span data-ttu-id="b4b16-236">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-236">CentOS</span></span> | <span data-ttu-id="b4b16-237">7.3</span><span class="sxs-lookup"><span data-stu-id="b4b16-237">7.3</span></span> | <span data-ttu-id="b4b16-238">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-238">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-239">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-239">CentOS</span></span> | <span data-ttu-id="b4b16-240">7.2n</span><span class="sxs-lookup"><span data-stu-id="b4b16-240">7.2n</span></span> | <span data-ttu-id="b4b16-241">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-241">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-242">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-242">CentOS</span></span> | <span data-ttu-id="b4b16-243">6.8</span><span class="sxs-lookup"><span data-stu-id="b4b16-243">6.8</span></span> | <span data-ttu-id="b4b16-244">OS and Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-244">OS and Data disk</span></span> |
| <span data-ttu-id="b4b16-245">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-245">CentOS</span></span> | <span data-ttu-id="b4b16-246">7.1</span><span class="sxs-lookup"><span data-stu-id="b4b16-246">7.1</span></span> | <span data-ttu-id="b4b16-247">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-247">Data disk</span></span> |
| <span data-ttu-id="b4b16-248">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-248">CentOS</span></span> | <span data-ttu-id="b4b16-249">7.0</span><span class="sxs-lookup"><span data-stu-id="b4b16-249">7.0</span></span> | <span data-ttu-id="b4b16-250">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-250">Data disk</span></span> |
| <span data-ttu-id="b4b16-251">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-251">CentOS</span></span> | <span data-ttu-id="b4b16-252">6.7</span><span class="sxs-lookup"><span data-stu-id="b4b16-252">6.7</span></span> | <span data-ttu-id="b4b16-253">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-253">Data disk</span></span> |
| <span data-ttu-id="b4b16-254">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-254">CentOS</span></span> | <span data-ttu-id="b4b16-255">6.6</span><span class="sxs-lookup"><span data-stu-id="b4b16-255">6.6</span></span> | <span data-ttu-id="b4b16-256">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-256">Data disk</span></span> |
| <span data-ttu-id="b4b16-257">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4b16-257">CentOS</span></span> | <span data-ttu-id="b4b16-258">6.5</span><span class="sxs-lookup"><span data-stu-id="b4b16-258">6.5</span></span> | <span data-ttu-id="b4b16-259">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-259">Data disk</span></span> |
| <span data-ttu-id="b4b16-260">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b4b16-260">openSUSE</span></span> | <span data-ttu-id="b4b16-261">13.2</span><span class="sxs-lookup"><span data-stu-id="b4b16-261">13.2</span></span> | <span data-ttu-id="b4b16-262">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-262">Data disk</span></span> |
| <span data-ttu-id="b4b16-263">SLES</span><span class="sxs-lookup"><span data-stu-id="b4b16-263">SLES</span></span> | <span data-ttu-id="b4b16-264">12 SP1</span><span class="sxs-lookup"><span data-stu-id="b4b16-264">12 SP1</span></span> | <span data-ttu-id="b4b16-265">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-265">Data disk</span></span> |
| <span data-ttu-id="b4b16-266">SLES</span><span class="sxs-lookup"><span data-stu-id="b4b16-266">SLES</span></span> | <span data-ttu-id="b4b16-267">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="b4b16-267">12-SP1 (Premium)</span></span> | <span data-ttu-id="b4b16-268">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-268">Data disk</span></span> |
| <span data-ttu-id="b4b16-269">SLES</span><span class="sxs-lookup"><span data-stu-id="b4b16-269">SLES</span></span> | <span data-ttu-id="b4b16-270">HPC 12</span><span class="sxs-lookup"><span data-stu-id="b4b16-270">HPC 12</span></span> | <span data-ttu-id="b4b16-271">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-271">Data disk</span></span> |
| <span data-ttu-id="b4b16-272">SLES</span><span class="sxs-lookup"><span data-stu-id="b4b16-272">SLES</span></span> | <span data-ttu-id="b4b16-273">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="b4b16-273">11-SP4 (Premium)</span></span> | <span data-ttu-id="b4b16-274">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-274">Data disk</span></span> |
| <span data-ttu-id="b4b16-275">SLES</span><span class="sxs-lookup"><span data-stu-id="b4b16-275">SLES</span></span> | <span data-ttu-id="b4b16-276">11 SP4</span><span class="sxs-lookup"><span data-stu-id="b4b16-276">11 SP4</span></span> | <span data-ttu-id="b4b16-277">Data disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-277">Data disk</span></span> |

* <span data-ttu-id="b4b16-278">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span><span class="sxs-lookup"><span data-stu-id="b4b16-278">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-279">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span><span class="sxs-lookup"><span data-stu-id="b4b16-279">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="b4b16-280">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span><span class="sxs-lookup"><span data-stu-id="b4b16-280">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="b4b16-281">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span><span class="sxs-lookup"><span data-stu-id="b4b16-281">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="b4b16-282">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span><span class="sxs-lookup"><span data-stu-id="b4b16-282">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="b4b16-283">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span><span class="sxs-lookup"><span data-stu-id="b4b16-283">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="b4b16-284">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span><span class="sxs-lookup"><span data-stu-id="b4b16-284">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="b4b16-285">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span><span class="sxs-lookup"><span data-stu-id="b4b16-285">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="b4b16-286">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-286">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="b4b16-287">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span><span class="sxs-lookup"><span data-stu-id="b4b16-287">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="b4b16-288">Your key vault secret and KEK URLs must be versioned.</span><span class="sxs-lookup"><span data-stu-id="b4b16-288">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="b4b16-289">Azure enforces this restriction of versioning.</span><span class="sxs-lookup"><span data-stu-id="b4b16-289">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="b4b16-290">For valid secret and KEK URLs, see the following examples:</span><span class="sxs-lookup"><span data-stu-id="b4b16-290">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="b4b16-291">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="b4b16-291">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="b4b16-292">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="b4b16-292">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="b4b16-293">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-293">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="b4b16-294">For examples of non-supported and supported key vault URLs, see the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-294">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="b4b16-295">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="b4b16-295">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="b4b16-296">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="b4b16-296">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="b4b16-297">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span><span class="sxs-lookup"><span data-stu-id="b4b16-297">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="b4b16-298">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[Login.windows.net\].</span><span class="sxs-lookup"><span data-stu-id="b4b16-298">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[Login.windows.net\].</span></span>
  * <span data-ttu-id="b4b16-299">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span><span class="sxs-lookup"><span data-stu-id="b4b16-299">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="b4b16-300">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span><span class="sxs-lookup"><span data-stu-id="b4b16-300">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b4b16-301">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-301">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="b4b16-302">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="b4b16-302">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="b4b16-303">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-303">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="b4b16-304">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="b4b16-304">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="b4b16-305">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="b4b16-305">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="b4b16-306">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-306">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="b4b16-307">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="b4b16-307">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="b4b16-308">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b4b16-308">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="b4b16-309">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="b4b16-309">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="b4b16-310">You must use -skipVmBackup parameter when using Azure disk encryption PS cmdlet Set-AzureRmVMDiskEncryptionExtension or CLI command to enable encryption on Azure Managed Disk VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-310">You must use -skipVmBackup parameter when using Azure disk encryption PS cmdlet Set-AzureRmVMDiskEncryptionExtension or CLI command to enable encryption on Azure Managed Disk VM.</span></span>
> [!NOTE]
 > <span data-ttu-id="b4b16-311">If you do not specify -skipVmBackup parameter, the enable encryption step will fail.</span><span class="sxs-lookup"><span data-stu-id="b4b16-311">If you do not specify -skipVmBackup parameter, the enable encryption step will fail.</span></span>

* <span data-ttu-id="b4b16-312">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-312">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="b4b16-313">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span><span class="sxs-lookup"><span data-stu-id="b4b16-313">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="b4b16-314">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="b4b16-314">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="b4b16-315">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/dev/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="b4b16-315">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/dev/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="b4b16-316">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b4b16-316">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="b4b16-317">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-317">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="b4b16-318">The Backup service supports VMs that are encrypted using KEK configuration only.</span><span class="sxs-lookup"><span data-stu-id="b4b16-318">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="b4b16-319">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="b4b16-319">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-320">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-320">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="b4b16-321">It is not supported on VMs that are encrypted without KEK.</span><span class="sxs-lookup"><span data-stu-id="b4b16-321">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="b4b16-322">KEK is an optional parameter that enables VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-322">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="b4b16-323">Set up the Azure AD application in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4b16-323">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="b4b16-324">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-324">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="b4b16-325">Managing encryption keys in your key vault requires Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="b4b16-325">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="b4b16-326">For this purpose, create an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="b4b16-326">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="b4b16-327">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-327">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="b4b16-328">This post also contains a number of helpful examples for setting up and configuring your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-328">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="b4b16-329">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="b4b16-329">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="b4b16-330">Client secret-based authentication for Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4b16-330">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="b4b16-331">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4b16-331">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="b4b16-332">Create an Azure AD application by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4b16-332">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="b4b16-333">Use the following PowerShell cmdlet to create an Azure AD application:</span><span class="sxs-lookup"><span data-stu-id="b4b16-333">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = “yourSecret”
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="b4b16-334">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-334">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="b4b16-335">Safeguard the Azure AD client secret appropriately.</span><span class="sxs-lookup"><span data-stu-id="b4b16-335">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="b4b16-336">Setting up the Azure AD client ID and secret from the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b4b16-336">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="b4b16-337">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b4b16-337">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="b4b16-338">To perform this task, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-338">To perform this task, do the following:</span></span>

1. <span data-ttu-id="b4b16-339">Click the **Active Directory** tab.</span><span class="sxs-lookup"><span data-stu-id="b4b16-339">Click the **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="b4b16-341">Click **Add Application**, and then type the application name.</span><span class="sxs-lookup"><span data-stu-id="b4b16-341">Click **Add Application**, and then type the application name.</span></span>

 ![Azure Disk Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="b4b16-343">Click the arrow button, and then configure the application properties.</span><span class="sxs-lookup"><span data-stu-id="b4b16-343">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure Disk Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="b4b16-345">Click the check mark in the lower left corner to finish.</span><span class="sxs-lookup"><span data-stu-id="b4b16-345">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="b4b16-346">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b4b16-346">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure Disk Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="b4b16-348">Save the Azure AD client secret by clicking the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b4b16-348">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="b4b16-349">Note the Azure AD client secret in the keys text box.</span><span class="sxs-lookup"><span data-stu-id="b4b16-349">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="b4b16-350">Safeguard it appropriately.</span><span class="sxs-lookup"><span data-stu-id="b4b16-350">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="b4b16-352">The preceding flow is not supported on the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="b4b16-352">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="b4b16-353">Use an existing application</span><span class="sxs-lookup"><span data-stu-id="b4b16-353">Use an existing application</span></span>
<span data-ttu-id="b4b16-354">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-354">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-355">The following commands must be executed from a new PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="b4b16-355">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="b4b16-356">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span><span class="sxs-lookup"><span data-stu-id="b4b16-356">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="b4b16-357">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4b16-357">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="b4b16-358">Certificate-based authentication for Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4b16-358">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="b4b16-359">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-359">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="b4b16-360">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4b16-360">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="b4b16-361">Create an Azure AD application</span><span class="sxs-lookup"><span data-stu-id="b4b16-361">Create an Azure AD application</span></span>
<span data-ttu-id="b4b16-362">To create an Azure AD application, execute the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="b4b16-362">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-363">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span><span class="sxs-lookup"><span data-stu-id="b4b16-363">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="b4b16-364">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-364">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="b4b16-365">Use an existing Azure AD application</span><span class="sxs-lookup"><span data-stu-id="b4b16-365">Use an existing Azure AD application</span></span>
<span data-ttu-id="b4b16-366">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span><span class="sxs-lookup"><span data-stu-id="b4b16-366">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="b4b16-367">Be sure to execute them from a new PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="b4b16-367">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="b4b16-368">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-368">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="b4b16-369">Upload a PFX file to your key vault</span><span class="sxs-lookup"><span data-stu-id="b4b16-369">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="b4b16-370">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-370">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="b4b16-371">However, the following PowerShell cmdlets are all you need for the task.</span><span class="sxs-lookup"><span data-stu-id="b4b16-371">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="b4b16-372">Be sure to execute them from Azure PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="b4b16-372">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-373">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span><span class="sxs-lookup"><span data-stu-id="b4b16-373">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="b4b16-374">Deploy a certificate in your key vault to an existing VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-374">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="b4b16-375">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-375">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="b4b16-376">Set up the key vault access policy for the Azure AD application</span><span class="sxs-lookup"><span data-stu-id="b4b16-376">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="b4b16-377">Your Azure AD application needs rights to access the keys or secrets in the vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-377">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="b4b16-378">Use the [`Set-AzureKeyVaultAccessPolicy`](https://msdn.microsoft.com/library/azure/dn903607.aspx) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span><span class="sxs-lookup"><span data-stu-id="b4b16-378">Use the [`Set-AzureKeyVaultAccessPolicy`](https://msdn.microsoft.com/library/azure/dn903607.aspx) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="b4b16-379">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-379">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="b4b16-380">Here is an example of how to perform this task via PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b4b16-380">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="b4b16-381">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span><span class="sxs-lookup"><span data-stu-id="b4b16-381">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="b4b16-382">Terminology</span><span class="sxs-lookup"><span data-stu-id="b4b16-382">Terminology</span></span>
<span data-ttu-id="b4b16-383">To understand some of the common terms used by this technology, use the following terminology table:</span><span class="sxs-lookup"><span data-stu-id="b4b16-383">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="b4b16-384">Terminology</span><span class="sxs-lookup"><span data-stu-id="b4b16-384">Terminology</span></span> | <span data-ttu-id="b4b16-385">Definition</span><span class="sxs-lookup"><span data-stu-id="b4b16-385">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="b4b16-386">Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4b16-386">Azure AD</span></span> | <span data-ttu-id="b4b16-387">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="b4b16-387">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="b4b16-388">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-388">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="b4b16-389">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b4b16-389">Azure Key Vault</span></span> | <span data-ttu-id="b4b16-390">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span><span class="sxs-lookup"><span data-stu-id="b4b16-390">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="b4b16-391">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span><span class="sxs-lookup"><span data-stu-id="b4b16-391">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="b4b16-392">ARM</span><span class="sxs-lookup"><span data-stu-id="b4b16-392">ARM</span></span> | <span data-ttu-id="b4b16-393">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b4b16-393">Azure Resource Manager</span></span> |
| <span data-ttu-id="b4b16-394">BitLocker</span><span class="sxs-lookup"><span data-stu-id="b4b16-394">BitLocker</span></span> |<span data-ttu-id="b4b16-395">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-395">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="b4b16-396">BEK</span><span class="sxs-lookup"><span data-stu-id="b4b16-396">BEK</span></span> | <span data-ttu-id="b4b16-397">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span><span class="sxs-lookup"><span data-stu-id="b4b16-397">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="b4b16-398">The BitLocker keys are safeguarded in a key vault as secrets.</span><span class="sxs-lookup"><span data-stu-id="b4b16-398">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="b4b16-399">CLI</span><span class="sxs-lookup"><span data-stu-id="b4b16-399">CLI</span></span> | <span data-ttu-id="b4b16-400">See [Azure command-line interface](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b4b16-400">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="b4b16-401">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="b4b16-401">DM-Crypt</span></span> |<span data-ttu-id="b4b16-402">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-402">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="b4b16-403">KEK</span><span class="sxs-lookup"><span data-stu-id="b4b16-403">KEK</span></span> | <span data-ttu-id="b4b16-404">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span><span class="sxs-lookup"><span data-stu-id="b4b16-404">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="b4b16-405">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-405">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="b4b16-406">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span><span class="sxs-lookup"><span data-stu-id="b4b16-406">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="b4b16-407">PS cmdlets</span><span class="sxs-lookup"><span data-stu-id="b4b16-407">PS cmdlets</span></span> | <span data-ttu-id="b4b16-408">See [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b4b16-408">See [Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="b4b16-409">Set up and configure your key vault for Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="b4b16-409">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="b4b16-410">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-410">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="b4b16-411">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span><span class="sxs-lookup"><span data-stu-id="b4b16-411">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="b4b16-412">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="b4b16-412">Create a key vault</span></span>
<span data-ttu-id="b4b16-413">To create a key vault, use one of the following options:</span><span class="sxs-lookup"><span data-stu-id="b4b16-413">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="b4b16-414">"101-Key-Vault-Create" Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="b4b16-414">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="b4b16-415">Azure PowerShell key vault cmdlets</span><span class="sxs-lookup"><span data-stu-id="b4b16-415">Azure PowerShell key vault cmdlets</span></span>](https://msdn.microsoft.com/library/dn868052.aspx)
* <span data-ttu-id="b4b16-416">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b4b16-416">Azure Resource Manager</span></span>
* <span data-ttu-id="b4b16-417">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="b4b16-417">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-418">If you have already set up a key vault for your subscription, skip to the next section.</span><span class="sxs-lookup"><span data-stu-id="b4b16-418">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![Azure Key Vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="b4b16-420">Set up a key encryption key (optional)</span><span class="sxs-lookup"><span data-stu-id="b4b16-420">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="b4b16-421">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-421">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="b4b16-422">Use the [`Add-AzureKeyVaultKey`](https://msdn.microsoft.com/library/dn868048.aspx) cmdlet to create a key encryption key in the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-422">Use the [`Add-AzureKeyVaultKey`](https://msdn.microsoft.com/library/dn868048.aspx) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="b4b16-423">You can also import a KEK from your on-premises key management HSM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-423">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="b4b16-424">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="b4b16-424">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="b4b16-425">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span><span class="sxs-lookup"><span data-stu-id="b4b16-425">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="b4b16-427">Set key vault permissions</span><span class="sxs-lookup"><span data-stu-id="b4b16-427">Set key vault permissions</span></span>
<span data-ttu-id="b4b16-428">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span><span class="sxs-lookup"><span data-stu-id="b4b16-428">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="b4b16-429">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b4b16-429">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="b4b16-430">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4b16-430">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="b4b16-431">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-431">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="b4b16-432">Otherwise, the deployment will fail.</span><span class="sxs-lookup"><span data-stu-id="b4b16-432">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="b4b16-433">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span><span class="sxs-lookup"><span data-stu-id="b4b16-433">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![Azure Key Vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="b4b16-436">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span><span class="sxs-lookup"><span data-stu-id="b4b16-436">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure key vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="b4b16-438">Disk-encryption deployment scenarios and user experiences</span><span class="sxs-lookup"><span data-stu-id="b4b16-438">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="b4b16-439">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span><span class="sxs-lookup"><span data-stu-id="b4b16-439">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="b4b16-440">The following sections cover the scenarios in greater detail.</span><span class="sxs-lookup"><span data-stu-id="b4b16-440">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="b4b16-441">Enable encryption on new IaaS VMs that are created from the Marketplace</span><span class="sxs-lookup"><span data-stu-id="b4b16-441">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="b4b16-442">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="b4b16-442">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="b4b16-443">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-443">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="b4b16-444">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-444">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-445">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span><span class="sxs-lookup"><span data-stu-id="b4b16-445">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="b4b16-446">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="b4b16-446">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="b4b16-447">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="b4b16-447">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="b4b16-448">When the machine returns a status of _VMRestartPending_, restart the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-448">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="b4b16-449">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span><span class="sxs-lookup"><span data-stu-id="b4b16-449">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="b4b16-450">Parameter</span><span class="sxs-lookup"><span data-stu-id="b4b16-450">Parameter</span></span> | <span data-ttu-id="b4b16-451">Description</span><span class="sxs-lookup"><span data-stu-id="b4b16-451">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4b16-452">adminUserName</span><span class="sxs-lookup"><span data-stu-id="b4b16-452">adminUserName</span></span> | <span data-ttu-id="b4b16-453">Admin user name for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b4b16-453">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="b4b16-454">adminPassword</span><span class="sxs-lookup"><span data-stu-id="b4b16-454">adminPassword</span></span> | <span data-ttu-id="b4b16-455">Admin user password for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b4b16-455">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="b4b16-456">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="b4b16-456">newStorageAccountName</span></span> | <span data-ttu-id="b4b16-457">Name of the storage account to store OS and data VHDs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-457">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="b4b16-458">vmSize</span><span class="sxs-lookup"><span data-stu-id="b4b16-458">vmSize</span></span> | <span data-ttu-id="b4b16-459">Size of the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-459">Size of the VM.</span></span> <span data-ttu-id="b4b16-460">Currently, only Standard A, D, and G series are supported.</span><span class="sxs-lookup"><span data-stu-id="b4b16-460">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="b4b16-461">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="b4b16-461">virtualNetworkName</span></span> | <span data-ttu-id="b4b16-462">Name of the VNet that the VM NIC should belong to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-462">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="b4b16-463">subnetName</span><span class="sxs-lookup"><span data-stu-id="b4b16-463">subnetName</span></span> | <span data-ttu-id="b4b16-464">Name of the subnet in the VNet that the VM NIC should belong to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-464">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="b4b16-465">AADClientID</span><span class="sxs-lookup"><span data-stu-id="b4b16-465">AADClientID</span></span> | <span data-ttu-id="b4b16-466">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-466">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="b4b16-467">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="b4b16-467">AADClientSecret</span></span> | <span data-ttu-id="b4b16-468">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-468">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="b4b16-469">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="b4b16-469">keyVaultURL</span></span> | <span data-ttu-id="b4b16-470">URL of the key vault that the BitLocker key should be uploaded to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-470">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="b4b16-471">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-471">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="b4b16-472">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="b4b16-472">keyEncryptionKeyURL</span></span> | <span data-ttu-id="b4b16-473">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span><span class="sxs-lookup"><span data-stu-id="b4b16-473">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="b4b16-474">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4b16-474">keyVaultResourceGroup</span></span> | <span data-ttu-id="b4b16-475">Resource group of the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-475">Resource group of the key vault.</span></span> |
| <span data-ttu-id="b4b16-476">vmName</span><span class="sxs-lookup"><span data-stu-id="b4b16-476">vmName</span></span> | <span data-ttu-id="b4b16-477">Name of the VM that the encryption operation is to be performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-477">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="b4b16-478">_KeyEncryptionKeyURL_ is an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="b4b16-478">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="b4b16-479">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-479">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="b4b16-480">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span><span class="sxs-lookup"><span data-stu-id="b4b16-480">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="b4b16-481">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span><span class="sxs-lookup"><span data-stu-id="b4b16-481">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="b4b16-482">The following sections explain in greater detail the Resource Manager template and CLI commands.</span><span class="sxs-lookup"><span data-stu-id="b4b16-482">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="b4b16-483">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-483">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="b4b16-484">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-484">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="b4b16-485">Prepare a pre-encrypted Windows VHD</span><span class="sxs-lookup"><span data-stu-id="b4b16-485">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="b4b16-486">Prepare a pre-encrypted Linux VHD</span><span class="sxs-lookup"><span data-stu-id="b4b16-486">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="b4b16-487">Using the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="b4b16-487">Using the Resource Manager template</span></span>
<span data-ttu-id="b4b16-488">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="b4b16-488">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="b4b16-489">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-489">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="b4b16-490">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-490">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="b4b16-491">The following table lists the Resource Manager template parameters for your encrypted VHD:</span><span class="sxs-lookup"><span data-stu-id="b4b16-491">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="b4b16-492">Parameter</span><span class="sxs-lookup"><span data-stu-id="b4b16-492">Parameter</span></span> | <span data-ttu-id="b4b16-493">Description</span><span class="sxs-lookup"><span data-stu-id="b4b16-493">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4b16-494">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="b4b16-494">newStorageAccountName</span></span> | <span data-ttu-id="b4b16-495">Name of the storage account to store the encrypted OS VHD.</span><span class="sxs-lookup"><span data-stu-id="b4b16-495">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="b4b16-496">This storage account should already have been created in the same resource group and same location as the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-496">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="b4b16-497">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="b4b16-497">osVhdUri</span></span> | <span data-ttu-id="b4b16-498">URI of the OS VHD from the storage account.</span><span class="sxs-lookup"><span data-stu-id="b4b16-498">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="b4b16-499">osType</span><span class="sxs-lookup"><span data-stu-id="b4b16-499">osType</span></span> | <span data-ttu-id="b4b16-500">OS product type (Windows/Linux).</span><span class="sxs-lookup"><span data-stu-id="b4b16-500">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="b4b16-501">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="b4b16-501">virtualNetworkName</span></span> | <span data-ttu-id="b4b16-502">Name of the VNet that the VM NIC should belong to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-502">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="b4b16-503">The name should already have been created in the same resource group and same location as the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-503">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="b4b16-504">subnetName</span><span class="sxs-lookup"><span data-stu-id="b4b16-504">subnetName</span></span> | <span data-ttu-id="b4b16-505">Name of the subnet on the VNet that the VM NIC should belong to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-505">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="b4b16-506">vmSize</span><span class="sxs-lookup"><span data-stu-id="b4b16-506">vmSize</span></span> | <span data-ttu-id="b4b16-507">Size of the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-507">Size of the VM.</span></span> <span data-ttu-id="b4b16-508">Currently, only Standard A, D, and G series are supported.</span><span class="sxs-lookup"><span data-stu-id="b4b16-508">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="b4b16-509">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="b4b16-509">keyVaultResourceID</span></span> | <span data-ttu-id="b4b16-510">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b4b16-510">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="b4b16-511">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-511">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="b4b16-512">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="b4b16-512">keyVaultSecretUrl</span></span> | <span data-ttu-id="b4b16-513">URL of the disk-encryption key that's set up in the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-513">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="b4b16-514">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="b4b16-514">keyVaultKekUrl</span></span> | <span data-ttu-id="b4b16-515">URL of the key encryption key for encrypting the generated disk-encryption key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-515">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="b4b16-516">vmName</span><span class="sxs-lookup"><span data-stu-id="b4b16-516">vmName</span></span> | <span data-ttu-id="b4b16-517">Name of the IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-517">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="b4b16-518">Using PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b4b16-518">Using PowerShell cmdlets</span></span>
<span data-ttu-id="b4b16-519">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](https://msdn.microsoft.com/library/azure/mt603746.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-519">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](https://msdn.microsoft.com/library/azure/mt603746.aspx).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="b4b16-520">Using CLI commands</span><span class="sxs-lookup"><span data-stu-id="b4b16-520">Using CLI commands</span></span>
<span data-ttu-id="b4b16-521">To enable disk encryption for this scenario by using CLI commands, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-521">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="b4b16-522">Set access policies in your key vault:</span><span class="sxs-lookup"><span data-stu-id="b4b16-522">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="b4b16-523">Set the **EnabledForDiskEncryption** flag:</span><span class="sxs-lookup"><span data-stu-id="b4b16-523">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="b4b16-524">Set permissions to Azure AD application to write secrets to your key vault:</span><span class="sxs-lookup"><span data-stu-id="b4b16-524">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="b4b16-525">To enable encryption on an existing or running VM, type:</span><span class="sxs-lookup"><span data-stu-id="b4b16-525">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="b4b16-526">Get encryption status:</span><span class="sxs-lookup"><span data-stu-id="b4b16-526">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="b4b16-527">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-527">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="b4b16-528">Enable encryption on existing or running IaaS Windows VM in Azure</span><span class="sxs-lookup"><span data-stu-id="b4b16-528">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="b4b16-529">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span><span class="sxs-lookup"><span data-stu-id="b4b16-529">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="b4b16-530">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span><span class="sxs-lookup"><span data-stu-id="b4b16-530">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="b4b16-531">Using the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="b4b16-531">Using the Resource Manager template</span></span>
<span data-ttu-id="b4b16-532">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="b4b16-532">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="b4b16-533">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-533">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="b4b16-534">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-534">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="b4b16-535">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span><span class="sxs-lookup"><span data-stu-id="b4b16-535">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="b4b16-536">Parameter</span><span class="sxs-lookup"><span data-stu-id="b4b16-536">Parameter</span></span> | <span data-ttu-id="b4b16-537">Description</span><span class="sxs-lookup"><span data-stu-id="b4b16-537">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4b16-538">AADClientID</span><span class="sxs-lookup"><span data-stu-id="b4b16-538">AADClientID</span></span> | <span data-ttu-id="b4b16-539">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-539">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="b4b16-540">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="b4b16-540">AADClientSecret</span></span> | <span data-ttu-id="b4b16-541">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-541">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="b4b16-542">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="b4b16-542">keyVaultName</span></span> | <span data-ttu-id="b4b16-543">Name of the key vault that the BitLocker key should be uploaded to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-543">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="b4b16-544">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-544">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="b4b16-545">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="b4b16-545">keyEncryptionKeyURL</span></span> | <span data-ttu-id="b4b16-546">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-546">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="b4b16-547">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b4b16-547">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="b4b16-548">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span><span class="sxs-lookup"><span data-stu-id="b4b16-548">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="b4b16-549">volumeType</span><span class="sxs-lookup"><span data-stu-id="b4b16-549">volumeType</span></span> | <span data-ttu-id="b4b16-550">Type of volume that the encryption operation is performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-550">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="b4b16-551">Valid values are _OS_, _Data_, and _All_.</span><span class="sxs-lookup"><span data-stu-id="b4b16-551">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="b4b16-552">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="b4b16-552">sequenceVersion</span></span> | <span data-ttu-id="b4b16-553">Sequence version of the BitLocker operation.</span><span class="sxs-lookup"><span data-stu-id="b4b16-553">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="b4b16-554">Increment this version number every time a disk-encryption operation is performed on the same VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-554">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="b4b16-555">vmName</span><span class="sxs-lookup"><span data-stu-id="b4b16-555">vmName</span></span> | <span data-ttu-id="b4b16-556">Name of the VM that the encryption operation is to be performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-556">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="b4b16-557">_KeyEncryptionKeyURL_ is an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="b4b16-557">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="b4b16-558">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-558">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="b4b16-559">Using PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b4b16-559">Using PowerShell cmdlets</span></span>
<span data-ttu-id="b4b16-560">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-560">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="b4b16-561">Using CLI commands</span><span class="sxs-lookup"><span data-stu-id="b4b16-561">Using CLI commands</span></span>
<span data-ttu-id="b4b16-562">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-562">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="b4b16-563">To set access policies in the key vault:</span><span class="sxs-lookup"><span data-stu-id="b4b16-563">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="b4b16-564">Set the **EnabledForDiskEncryption** flag:</span><span class="sxs-lookup"><span data-stu-id="b4b16-564">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="b4b16-565">Set permissions to Azure AD application to write secrets to your key vault:</span><span class="sxs-lookup"><span data-stu-id="b4b16-565">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="b4b16-566">To enable encryption on an existing or running VM:</span><span class="sxs-lookup"><span data-stu-id="b4b16-566">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="b4b16-567">To get encryption status:</span><span class="sxs-lookup"><span data-stu-id="b4b16-567">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="b4b16-568">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-568">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="b4b16-569">Enable encryption on an existing or running IaaS Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="b4b16-569">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="b4b16-570">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="b4b16-570">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="b4b16-571">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-571">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="b4b16-572">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-572">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="b4b16-573">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span><span class="sxs-lookup"><span data-stu-id="b4b16-573">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="b4b16-574">Parameter</span><span class="sxs-lookup"><span data-stu-id="b4b16-574">Parameter</span></span> | <span data-ttu-id="b4b16-575">Description</span><span class="sxs-lookup"><span data-stu-id="b4b16-575">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4b16-576">AADClientID</span><span class="sxs-lookup"><span data-stu-id="b4b16-576">AADClientID</span></span> | <span data-ttu-id="b4b16-577">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-577">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="b4b16-578">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="b4b16-578">AADClientSecret</span></span> | <span data-ttu-id="b4b16-579">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-579">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="b4b16-580">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="b4b16-580">keyVaultName</span></span> | <span data-ttu-id="b4b16-581">Name of the key vault that the BitLocker key should be uploaded to.</span><span class="sxs-lookup"><span data-stu-id="b4b16-581">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="b4b16-582">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-582">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="b4b16-583">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="b4b16-583">keyEncryptionKeyURL</span></span> | <span data-ttu-id="b4b16-584">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-584">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="b4b16-585">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b4b16-585">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="b4b16-586">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span><span class="sxs-lookup"><span data-stu-id="b4b16-586">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="b4b16-587">volumeType</span><span class="sxs-lookup"><span data-stu-id="b4b16-587">volumeType</span></span> | <span data-ttu-id="b4b16-588">Type of volume that the encryption operation is performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-588">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="b4b16-589">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span><span class="sxs-lookup"><span data-stu-id="b4b16-589">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="b4b16-590">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="b4b16-590">sequenceVersion</span></span> | <span data-ttu-id="b4b16-591">Sequence version of the BitLocker operation.</span><span class="sxs-lookup"><span data-stu-id="b4b16-591">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="b4b16-592">Increment this version number every time a disk-encryption operation is performed on the same VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-592">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="b4b16-593">vmName</span><span class="sxs-lookup"><span data-stu-id="b4b16-593">vmName</span></span> | <span data-ttu-id="b4b16-594">Name of the VM that the encryption operation is to be performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-594">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="b4b16-595">passPhrase</span><span class="sxs-lookup"><span data-stu-id="b4b16-595">passPhrase</span></span> | <span data-ttu-id="b4b16-596">Type a strong passphrase as the data encryption key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-596">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="b4b16-597">_KeyEncryptionKeyURL_ is an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="b4b16-597">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="b4b16-598">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-598">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="b4b16-599">CLI commands</span><span class="sxs-lookup"><span data-stu-id="b4b16-599">CLI commands</span></span>
<span data-ttu-id="b4b16-600">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b4b16-600">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="b4b16-601">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-601">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="b4b16-602">Set access policies in the key vault:</span><span class="sxs-lookup"><span data-stu-id="b4b16-602">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="b4b16-603">Set the **EnabledForDiskEncryption** flag:</span><span class="sxs-lookup"><span data-stu-id="b4b16-603">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="b4b16-604">Set permissions to Azure AD application to write secrets to your key vault:</span><span class="sxs-lookup"><span data-stu-id="b4b16-604">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="b4b16-605">To enable encryption on an existing or running VM:</span><span class="sxs-lookup"><span data-stu-id="b4b16-605">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="b4b16-606">Get encryption status:</span><span class="sxs-lookup"><span data-stu-id="b4b16-606">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="b4b16-607">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-607">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="b4b16-608">Get the encryption status of an encrypted IaaS VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-608">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="b4b16-609">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](https://msdn.microsoft.com/library/azure/mt622700.aspx), or CLI commands.</span><span class="sxs-lookup"><span data-stu-id="b4b16-609">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](https://msdn.microsoft.com/library/azure/mt622700.aspx), or CLI commands.</span></span> <span data-ttu-id="b4b16-610">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span><span class="sxs-lookup"><span data-stu-id="b4b16-610">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="b4b16-611">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b4b16-611">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="b4b16-612">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-612">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="b4b16-613">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span><span class="sxs-lookup"><span data-stu-id="b4b16-613">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="b4b16-614">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="b4b16-614">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="b4b16-615">At the top of the **Virtual machines** page, click **Columns**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-615">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="b4b16-616">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-616">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="b4b16-617">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="b4b16-617">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Microsoft Antimalware in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="b4b16-619">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="b4b16-619">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="b4b16-620">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-620">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="b4b16-621">To get the encryption settings for your VM, enter the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-621">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="b4b16-622">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-622">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="b4b16-623">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-623">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="b4b16-624">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-624">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-625">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span><span class="sxs-lookup"><span data-stu-id="b4b16-625">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="b4b16-626">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span><span class="sxs-lookup"><span data-stu-id="b4b16-626">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="b4b16-627">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-627">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="b4b16-628">To get the encryption settings for your VM, enter your Azure CLI session:</span><span class="sxs-lookup"><span data-stu-id="b4b16-628">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="b4b16-629">Disable encryption on running Windows IaaS VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-629">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="b4b16-630">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span><span class="sxs-lookup"><span data-stu-id="b4b16-630">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="b4b16-631">Windows VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-631">Windows VM</span></span>
<span data-ttu-id="b4b16-632">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-632">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="b4b16-633">You cannot disable the OS volume and leave the data volume encrypted.</span><span class="sxs-lookup"><span data-stu-id="b4b16-633">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="b4b16-634">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span><span class="sxs-lookup"><span data-stu-id="b4b16-634">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="b4b16-635">The contents of the VM are no longer encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="b4b16-635">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="b4b16-636">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span><span class="sxs-lookup"><span data-stu-id="b4b16-636">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="b4b16-637">Linux VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-637">Linux VM</span></span>
<span data-ttu-id="b4b16-638">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-638">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-639">Disabling encryption on the OS disk is not allowed on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-639">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="b4b16-640">Disable encryption on an existing or running IaaS VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-640">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="b4b16-641">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="b4b16-641">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="b4b16-642">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-642">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="b4b16-643">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-643">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="b4b16-644">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span><span class="sxs-lookup"><span data-stu-id="b4b16-644">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="b4b16-645">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span><span class="sxs-lookup"><span data-stu-id="b4b16-645">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="b4b16-646">Parameter</span><span class="sxs-lookup"><span data-stu-id="b4b16-646">Parameter</span></span> | <span data-ttu-id="b4b16-647">Description</span><span class="sxs-lookup"><span data-stu-id="b4b16-647">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4b16-648">vmName</span><span class="sxs-lookup"><span data-stu-id="b4b16-648">vmName</span></span> | <span data-ttu-id="b4b16-649">Name of the VM that the encryption operation is to be performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-649">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="b4b16-650">volumeType</span><span class="sxs-lookup"><span data-stu-id="b4b16-650">volumeType</span></span> | <span data-ttu-id="b4b16-651">Type of volume that a decryption operation is performed on.</span><span class="sxs-lookup"><span data-stu-id="b4b16-651">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="b4b16-652">Valid values are _OS_, _Data_, and _All_.</span><span class="sxs-lookup"><span data-stu-id="b4b16-652">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="b4b16-653">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span><span class="sxs-lookup"><span data-stu-id="b4b16-653">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="b4b16-654">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-654">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="b4b16-655">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="b4b16-655">sequenceVersion</span></span> | <span data-ttu-id="b4b16-656">Sequence version of the BitLocker operation.</span><span class="sxs-lookup"><span data-stu-id="b4b16-656">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="b4b16-657">Increment this version number every time a disk decryption operation is performed on the same VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-657">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="b4b16-658">Disable encryption on an existing or running IaaS VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-658">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="b4b16-659">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](https://msdn.microsoft.com/library/azure/mt715776.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-659">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](https://msdn.microsoft.com/library/azure/mt715776.aspx).</span></span> <span data-ttu-id="b4b16-660">This cmdlet supports both Windows and Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-660">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="b4b16-661">To disable encryption, it installs an extension on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b4b16-661">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="b4b16-662">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span><span class="sxs-lookup"><span data-stu-id="b4b16-662">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="b4b16-663">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span><span class="sxs-lookup"><span data-stu-id="b4b16-663">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b16-664">This cmdlet reboots the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b4b16-664">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="b4b16-665">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-665">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="b4b16-666">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span><span class="sxs-lookup"><span data-stu-id="b4b16-666">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="b4b16-667">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="b4b16-667">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="b4b16-668">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-668">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="b4b16-669">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span><span class="sxs-lookup"><span data-stu-id="b4b16-669">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="b4b16-670">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="b4b16-670">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="b4b16-671">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-671">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="b4b16-672">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span><span class="sxs-lookup"><span data-stu-id="b4b16-672">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="b4b16-673">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="b4b16-673">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="b4b16-674">You must use -skipVmBackup parameter when using Azure disk encryption PS cmdlet Set-AzureRmVMDiskEncryptionExtension or CLI command to enable encryption on Azure Managed Disk VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-674">You must use -skipVmBackup parameter when using Azure disk encryption PS cmdlet Set-AzureRmVMDiskEncryptionExtension or CLI command to enable encryption on Azure Managed Disk VM.</span></span>
  >
  ><span data-ttu-id="b4b16-675">It is advisable to backup your running VM instance before you enable encryption using the PS cmdlet Set-AzureRmVMDiskEncryptionExtension on your Linux Managed Disk VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-675">It is advisable to backup your running VM instance before you enable encryption using the PS cmdlet Set-AzureRmVMDiskEncryptionExtension on your Linux Managed Disk VM.</span></span>

### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="b4b16-676">Update encryption settings of an existing encrypted non-premium VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-676">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="b4b16-677">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span><span class="sxs-lookup"><span data-stu-id="b4b16-677">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="b4b16-678">It is NNOT supported for VMs backed by premium storage.</span><span class="sxs-lookup"><span data-stu-id="b4b16-678">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="b4b16-679">Appendix</span><span class="sxs-lookup"><span data-stu-id="b4b16-679">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="b4b16-680">Connect to your subscription</span><span class="sxs-lookup"><span data-stu-id="b4b16-680">Connect to your subscription</span></span>
<span data-ttu-id="b4b16-681">Before you proceed, review the *Prerequisites* section in this article.</span><span class="sxs-lookup"><span data-stu-id="b4b16-681">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="b4b16-682">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-682">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="b4b16-683">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-683">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="b4b16-684">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="b4b16-684">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="b4b16-685">To specify the subscription you want to use, type:</span><span class="sxs-lookup"><span data-stu-id="b4b16-685">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="b4b16-686">To verify that the subscription configured is correct, type:</span><span class="sxs-lookup"><span data-stu-id="b4b16-686">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="b4b16-687">To confirm the Azure Disk Encryption cmdlets are installed, type:</span><span class="sxs-lookup"><span data-stu-id="b4b16-687">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="b4b16-688">The following output confirms the Azure Disk Encryption PowerShell installation:</span><span class="sxs-lookup"><span data-stu-id="b4b16-688">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="b4b16-689">Prepare a pre-encrypted Windows VHD</span><span class="sxs-lookup"><span data-stu-id="b4b16-689">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="b4b16-690">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="b4b16-690">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="b4b16-691">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-691">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="b4b16-692">Update group policy to allow non-TPM for OS protection</span><span class="sxs-lookup"><span data-stu-id="b4b16-692">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="b4b16-693">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span><span class="sxs-lookup"><span data-stu-id="b4b16-693">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="b4b16-694">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span><span class="sxs-lookup"><span data-stu-id="b4b16-694">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Microsoft Antimalware in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="b4b16-696">Install BitLocker feature components</span><span class="sxs-lookup"><span data-stu-id="b4b16-696">Install BitLocker feature components</span></span>
<span data-ttu-id="b4b16-697">For Windows Server 2012 and later, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-697">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="b4b16-698">For Windows Server 2008 R2, use the following command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-698">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="b4b16-699">Prepare the OS volume for BitLocker by using `bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="b4b16-699">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="b4b16-700">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span><span class="sxs-lookup"><span data-stu-id="b4b16-700">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="b4b16-701">Protect the OS volume by using BitLocker</span><span class="sxs-lookup"><span data-stu-id="b4b16-701">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="b4b16-702">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span><span class="sxs-lookup"><span data-stu-id="b4b16-702">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="b4b16-703">Also place the external key (.bek file) on the external drive or volume.</span><span class="sxs-lookup"><span data-stu-id="b4b16-703">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="b4b16-704">Encryption is enabled on the system/boot volume after the next reboot.</span><span class="sxs-lookup"><span data-stu-id="b4b16-704">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="b4b16-705">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span><span class="sxs-lookup"><span data-stu-id="b4b16-705">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="b4b16-706">Encrypting an OS drive on a running Linux VM</span><span class="sxs-lookup"><span data-stu-id="b4b16-706">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="b4b16-707">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span><span class="sxs-lookup"><span data-stu-id="b4b16-707">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="b4b16-708">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="b4b16-708">RHEL 7.2</span></span>
* <span data-ttu-id="b4b16-709">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="b4b16-709">CentOS 7.2</span></span>
* <span data-ttu-id="b4b16-710">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="b4b16-710">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="b4b16-711">Prerequisites for OS disk encryption</span><span class="sxs-lookup"><span data-stu-id="b4b16-711">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="b4b16-712">The VM must be created from the Marketplace image in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b4b16-712">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="b4b16-713">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span><span class="sxs-lookup"><span data-stu-id="b4b16-713">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="b4b16-714">(For RHEL and CentOS) Disable SELinux.</span><span class="sxs-lookup"><span data-stu-id="b4b16-714">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="b4b16-715">To disable SELinux, see "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="b4b16-715">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="b4b16-716">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-716">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="b4b16-717">After you disable SELinux, reboot the VM at least once.</span><span class="sxs-lookup"><span data-stu-id="b4b16-717">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="b4b16-718">Steps</span><span class="sxs-lookup"><span data-stu-id="b4b16-718">Steps</span></span>
1. <span data-ttu-id="b4b16-719">Create a VM by using one of the distributions specified previously.</span><span class="sxs-lookup"><span data-stu-id="b4b16-719">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="b4b16-720">For CentOS 7.2, OS disk encryption is supported via a special image.</span><span class="sxs-lookup"><span data-stu-id="b4b16-720">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="b4b16-721">To use this image, specify "7.2n" as the SKU when you create the VM:</span><span class="sxs-lookup"><span data-stu-id="b4b16-721">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="b4b16-722">Configure the VM according to your needs.</span><span class="sxs-lookup"><span data-stu-id="b4b16-722">Configure the VM according to your needs.</span></span> <span data-ttu-id="b4b16-723">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="b4b16-723">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="b4b16-724">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="b4b16-724">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="b4b16-725">During encryption, the order of drives changes on the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-725">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="b4b16-726">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span><span class="sxs-lookup"><span data-stu-id="b4b16-726">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="b4b16-727">Sign out of the SSH sessions.</span><span class="sxs-lookup"><span data-stu-id="b4b16-727">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="b4b16-728">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="b4b16-728">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="b4b16-729">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-729">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="b4b16-730">Reboot the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-730">Reboot the VM.</span></span> <span data-ttu-id="b4b16-731">When you enable OS disk encryption on a running VM, plan on VM downtime.</span><span class="sxs-lookup"><span data-stu-id="b4b16-731">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="b4b16-732">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="b4b16-732">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="b4b16-733">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span><span class="sxs-lookup"><span data-stu-id="b4b16-733">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="b4b16-734">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-734">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="b4b16-735">Monitoring OS encryption progress</span><span class="sxs-lookup"><span data-stu-id="b4b16-735">Monitoring OS encryption progress</span></span>
<span data-ttu-id="b4b16-736">You can monitor OS encryption progress in three ways:</span><span class="sxs-lookup"><span data-stu-id="b4b16-736">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="b4b16-737">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span><span class="sxs-lookup"><span data-stu-id="b4b16-737">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="b4b16-738">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-738">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="b4b16-739">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span><span class="sxs-lookup"><span data-stu-id="b4b16-739">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="b4b16-740">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span><span class="sxs-lookup"><span data-stu-id="b4b16-740">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="b4b16-741">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="b4b16-741">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="b4b16-742">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span><span class="sxs-lookup"><span data-stu-id="b4b16-742">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="b4b16-743">In the InstanceView, scroll down to see the encryption status of your drives.</span><span class="sxs-lookup"><span data-stu-id="b4b16-743">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![VM Instance View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="b4b16-745">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="b4b16-745">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="b4b16-746">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-746">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="b4b16-747">Sign in to the VM via SSH, and get the extension log from:</span><span class="sxs-lookup"><span data-stu-id="b4b16-747">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="b4b16-748">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="b4b16-748">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="b4b16-749">We recommend that you do not sign in to the VM while OS encryption is in progress.</span><span class="sxs-lookup"><span data-stu-id="b4b16-749">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="b4b16-750">Copy the logs only when the other two methods have failed.</span><span class="sxs-lookup"><span data-stu-id="b4b16-750">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="b4b16-751">Prepare a pre-encrypted Linux VHD</span><span class="sxs-lookup"><span data-stu-id="b4b16-751">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="b4b16-752">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="b4b16-752">Ubuntu 16</span></span>
<span data-ttu-id="b4b16-753">Configure encryption during the distribution installation by doing the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-753">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="b4b16-754">Select **Configure encrypted volumes** when you partition the disks.</span><span class="sxs-lookup"><span data-stu-id="b4b16-754">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Ubuntu 16.04 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="b4b16-756">Create a separate boot drive, which must not be encrypted.</span><span class="sxs-lookup"><span data-stu-id="b4b16-756">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="b4b16-757">Encrypt your root drive.</span><span class="sxs-lookup"><span data-stu-id="b4b16-757">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="b4b16-759">Provide a passphrase.</span><span class="sxs-lookup"><span data-stu-id="b4b16-759">Provide a passphrase.</span></span> <span data-ttu-id="b4b16-760">This is the passphrase that you upload to the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-760">This is the passphrase that you upload to the key vault.</span></span>

 ![Ubuntu 16.04 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="b4b16-762">Finish partitioning.</span><span class="sxs-lookup"><span data-stu-id="b4b16-762">Finish partitioning.</span></span>

 ![Ubuntu 16.04 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="b4b16-764">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span><span class="sxs-lookup"><span data-stu-id="b4b16-764">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="b4b16-766">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="b4b16-766">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="b4b16-767">Do not run the last step (deprovisioning the VM) yet.</span><span class="sxs-lookup"><span data-stu-id="b4b16-767">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="b4b16-768">Configure encryption to work with Azure by doing the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-768">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="b4b16-769">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span><span class="sxs-lookup"><span data-stu-id="b4b16-769">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="b4b16-770">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-770">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="b4b16-771">Change the crypt config in */etc/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="b4b16-771">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="b4b16-772">It should look like this:</span><span class="sxs-lookup"><span data-stu-id="b4b16-772">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="b4b16-773">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-773">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="b4b16-774">Add executable permissions to the script:</span><span class="sxs-lookup"><span data-stu-id="b4b16-774">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="b4b16-775">Edit */etc/initramfs-tools/modules* by appending lines:</span><span class="sxs-lookup"><span data-stu-id="b4b16-775">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="b4b16-776">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span><span class="sxs-lookup"><span data-stu-id="b4b16-776">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="b4b16-777">Now you can deprovision the VM.</span><span class="sxs-lookup"><span data-stu-id="b4b16-777">Now you can deprovision the VM.</span></span>

 ![Ubuntu 16.04 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="b4b16-779">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-779">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="b4b16-780">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="b4b16-780">openSUSE 13.2</span></span>
<span data-ttu-id="b4b16-781">To configure encryption during the distribution installation, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-781">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="b4b16-782">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span><span class="sxs-lookup"><span data-stu-id="b4b16-782">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="b4b16-783">This is the password that you will upload to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-783">This is the password that you will upload to your key vault.</span></span>

 ![openSUSE 13.2 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="b4b16-785">Boot the VM using your password.</span><span class="sxs-lookup"><span data-stu-id="b4b16-785">Boot the VM using your password.</span></span>

 ![openSUSE 13.2 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="b4b16-787">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="b4b16-787">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="b4b16-788">Do not run the last step (deprovisioning the VM) yet.</span><span class="sxs-lookup"><span data-stu-id="b4b16-788">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="b4b16-789">To configure encryption to work with Azure, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-789">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="b4b16-790">Edit the /etc/dracut.conf, and add the following line:</span><span class="sxs-lookup"><span data-stu-id="b4b16-790">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="b4b16-791">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="b4b16-791">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="b4b16-792">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="b4b16-792">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="b4b16-793">And change all occurrences of:</span><span class="sxs-lookup"><span data-stu-id="b4b16-793">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="b4b16-794">to:</span><span class="sxs-lookup"><span data-stu-id="b4b16-794">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="b4b16-795">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span><span class="sxs-lookup"><span data-stu-id="b4b16-795">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="b4b16-796">Run `/usr/sbin/dracut -f -v` to update the initrd.</span><span class="sxs-lookup"><span data-stu-id="b4b16-796">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="b4b16-797">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-797">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="b4b16-798">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="b4b16-798">CentOS 7</span></span>
<span data-ttu-id="b4b16-799">To configure encryption during the distribution installation, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-799">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="b4b16-800">Select **Encrypt my data** when you partition disks.</span><span class="sxs-lookup"><span data-stu-id="b4b16-800">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="b4b16-802">Make sure **Encrypt** is selected for root partition.</span><span class="sxs-lookup"><span data-stu-id="b4b16-802">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="b4b16-804">Provide a passphrase.</span><span class="sxs-lookup"><span data-stu-id="b4b16-804">Provide a passphrase.</span></span> <span data-ttu-id="b4b16-805">This is the passphrase that you will upload to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-805">This is the passphrase that you will upload to your key vault.</span></span>

 ![CentOS 7 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="b4b16-807">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span><span class="sxs-lookup"><span data-stu-id="b4b16-807">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![CentOS 7 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="b4b16-809">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="b4b16-809">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="b4b16-810">Do not run the last step (deprovisioning the VM) yet.</span><span class="sxs-lookup"><span data-stu-id="b4b16-810">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="b4b16-811">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span><span class="sxs-lookup"><span data-stu-id="b4b16-811">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="b4b16-812">To configure encryption to work with Azure, do the following:</span><span class="sxs-lookup"><span data-stu-id="b4b16-812">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="b4b16-813">Edit the /etc/dracut.conf, and add the following line:</span><span class="sxs-lookup"><span data-stu-id="b4b16-813">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="b4b16-814">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="b4b16-814">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="b4b16-815">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="b4b16-815">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="b4b16-816">And change all occurrences of:</span><span class="sxs-lookup"><span data-stu-id="b4b16-816">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="b4b16-817">to</span><span class="sxs-lookup"><span data-stu-id="b4b16-817">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="b4b16-818">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span><span class="sxs-lookup"><span data-stu-id="b4b16-818">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="b4b16-819">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span><span class="sxs-lookup"><span data-stu-id="b4b16-819">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![CentOS 7 Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="b4b16-821">Upload encrypted VHD to an Azure storage account</span><span class="sxs-lookup"><span data-stu-id="b4b16-821">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="b4b16-822">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span><span class="sxs-lookup"><span data-stu-id="b4b16-822">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="b4b16-823">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span><span class="sxs-lookup"><span data-stu-id="b4b16-823">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="b4b16-824">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-824">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="b4b16-825">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span><span class="sxs-lookup"><span data-stu-id="b4b16-825">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="b4b16-826">Disk encryption secret not encrypted with a KEK</span><span class="sxs-lookup"><span data-stu-id="b4b16-826">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="b4b16-827">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](https://msdn.microsoft.com/library/dn868050.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4b16-827">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](https://msdn.microsoft.com/library/dn868050.aspx).</span></span> <span data-ttu-id="b4b16-828">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4b16-828">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="b4b16-829">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-829">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="b4b16-830">In addition, make sure that the following tags are set when you create the secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="b4b16-830">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="b4b16-831">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="b4b16-831">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="b4b16-832">Disk encryption secret encrypted with a KEK</span><span class="sxs-lookup"><span data-stu-id="b4b16-832">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="b4b16-833">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-833">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="b4b16-834">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span><span class="sxs-lookup"><span data-stu-id="b4b16-834">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="b4b16-835">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](https://msdn.microsoft.com/library/dn868050.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4b16-835">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](https://msdn.microsoft.com/library/dn868050.aspx) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="b4b16-836">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="b4b16-836">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="b4b16-837">Specify a secret URL when you attach an OS disk</span><span class="sxs-lookup"><span data-stu-id="b4b16-837">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="b4b16-838">Without using a KEK</span><span class="sxs-lookup"><span data-stu-id="b4b16-838">Without using a KEK</span></span>
<span data-ttu-id="b4b16-839">While you are attaching the OS disk, you need to pass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-839">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="b4b16-840">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span><span class="sxs-lookup"><span data-stu-id="b4b16-840">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="b4b16-841">Using a KEK</span><span class="sxs-lookup"><span data-stu-id="b4b16-841">Using a KEK</span></span>
<span data-ttu-id="b4b16-842">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="b4b16-842">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="b4b16-843">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span><span class="sxs-lookup"><span data-stu-id="b4b16-843">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="b4b16-844">Download this guide</span><span class="sxs-lookup"><span data-stu-id="b4b16-844">Download this guide</span></span>
<span data-ttu-id="b4b16-845">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="b4b16-845">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="b4b16-846">For more information</span><span class="sxs-lookup"><span data-stu-id="b4b16-846">For more information</span></span>
[<span data-ttu-id="b4b16-847">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span><span class="sxs-lookup"><span data-stu-id="b4b16-847">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="b4b16-848">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span><span class="sxs-lookup"><span data-stu-id="b4b16-848">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)



























