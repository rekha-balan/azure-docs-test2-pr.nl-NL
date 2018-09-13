---
title: Apply disk encryption in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Apply disk encryption**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 20b55f993e8a570c737d5849af957b4c40089f61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825474"
---
# <a name="apply-disk-encryption-in-azure-security-center"></a><span data-ttu-id="a298c-103">Apply disk encryption in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a298c-103">Apply disk encryption in Azure Security Center</span></span>
<span data-ttu-id="a298c-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="a298c-104">Azure Security Center recommends that you apply disk encryption if you have Windows or Linux VM disks that are not encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="a298c-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span><span class="sxs-lookup"><span data-stu-id="a298c-105">Disk Encryption lets you encrypt your Windows and Linux IaaS VM disks.</span></span>  <span data-ttu-id="a298c-106">Encryption is recommended for both the OS and data volumes on your VM.</span><span class="sxs-lookup"><span data-stu-id="a298c-106">Encryption is recommended for both the OS and data volumes on your VM.</span></span>

<span data-ttu-id="a298c-107">Disk Encryption uses the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span><span class="sxs-lookup"><span data-stu-id="a298c-107">Disk Encryption uses the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux.</span></span> <span data-ttu-id="a298c-108">These features provide OS and data encryption to help protect and safeguard your data and meet your organizational security and compliance commitments.</span><span class="sxs-lookup"><span data-stu-id="a298c-108">These features provide OS and data encryption to help protect and safeguard your data and meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="a298c-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in the VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="a298c-109">Disk Encryption is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk encryption keys and secrets in your Key Vault subscription, while ensuring that all data in the VM disks are encrypted at rest in your [Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span></span>

> [!NOTE]
> <span data-ttu-id="a298c-110">Azure Disk Encryption is supported on the following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a298c-110">Azure Disk Encryption is supported on the following Windows server operating systems - Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span> <span data-ttu-id="a298c-111">Disk encryption is supported on the following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span><span class="sxs-lookup"><span data-stu-id="a298c-111">Disk encryption is supported on the following Linux server operating systems - Ubuntu, CentOS, SUSE, and SUSE Linux Enterprise Server (SLES).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="a298c-112">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="a298c-112">Implement the recommendation</span></span>
1. <span data-ttu-id="a298c-113">In the **Recommendations** blade, select **Apply disk encryption**.</span><span class="sxs-lookup"><span data-stu-id="a298c-113">In the **Recommendations** blade, select **Apply disk encryption**.</span></span>
2. <span data-ttu-id="a298c-114">In the **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span><span class="sxs-lookup"><span data-stu-id="a298c-114">In the **Apply disk encryption** blade, you see a list of VMs for which Disk Encryption is recommended.</span></span>
3. <span data-ttu-id="a298c-115">Follow the instructions to apply encryption to these VMs.</span><span class="sxs-lookup"><span data-stu-id="a298c-115">Follow the instructions to apply encryption to these VMs.</span></span>

![][1]

<span data-ttu-id="a298c-116">To encrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend the following steps:</span><span class="sxs-lookup"><span data-stu-id="a298c-116">To encrypt Azure Virtual Machines that have been identified by Security Center as needing encryption, we recommend the following steps:</span></span>

* <span data-ttu-id="a298c-117">Install and configure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a298c-117">Install and configure Azure PowerShell.</span></span> <span data-ttu-id="a298c-118">This enables you to run the PowerShell commands required to set up the prerequisites required to encrypt Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="a298c-118">This enables you to run the PowerShell commands required to set up the prerequisites required to encrypt Azure Virtual Machines.</span></span>
* <span data-ttu-id="a298c-119">Obtain and run the Azure Disk Encryption Prerequisites Azure PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="a298c-119">Obtain and run the Azure Disk Encryption Prerequisites Azure PowerShell script.</span></span>
* <span data-ttu-id="a298c-120">Encrypt your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a298c-120">Encrypt your virtual machines.</span></span>

<span data-ttu-id="a298c-121">[Encrypt a Windows IaaS VM with Azure PowerShell](../security/quick-encrypt-vm-powershell.md) walks you through these steps.</span><span class="sxs-lookup"><span data-stu-id="a298c-121">[Encrypt a Windows IaaS VM with Azure PowerShell](../security/quick-encrypt-vm-powershell.md) walks you through these steps.</span></span> <span data-ttu-id="a298c-122">This topic assumes you are using a Windows client machine from which you configure disk encryption.</span><span class="sxs-lookup"><span data-stu-id="a298c-122">This topic assumes you are using a Windows client machine from which you configure disk encryption.</span></span>

<span data-ttu-id="a298c-123">There are many approaches that can be used for Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="a298c-123">There are many approaches that can be used for Azure Virtual Machines.</span></span> <span data-ttu-id="a298c-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer to use alternate approaches.</span><span class="sxs-lookup"><span data-stu-id="a298c-124">If you are already well-versed in Azure PowerShell or Azure CLI, then you may prefer to use alternate approaches.</span></span> <span data-ttu-id="a298c-125">To learn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a298c-125">To learn about these other approaches, see [Azure disk encryption](../security/azure-security-disk-encryption.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a298c-126">See also</span><span class="sxs-lookup"><span data-stu-id="a298c-126">See also</span></span>
<span data-ttu-id="a298c-127">This document showed you how to implement the Security Center recommendation "Apply disk encryption."</span><span class="sxs-lookup"><span data-stu-id="a298c-127">This document showed you how to implement the Security Center recommendation "Apply disk encryption."</span></span> <span data-ttu-id="a298c-128">To learn more about disk encryption, see the following:</span><span class="sxs-lookup"><span data-stu-id="a298c-128">To learn more about disk encryption, see the following:</span></span>

* <span data-ttu-id="a298c-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how to use disk encryption management for IaaS VMs and Azure Key Vault to help protect and safeguard your data.</span><span class="sxs-lookup"><span data-stu-id="a298c-129">[Encryption and key management with Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video, 36 min 39 sec) -- Learn how to use disk encryption management for IaaS VMs and Azure Key Vault to help protect and safeguard your data.</span></span>
* <span data-ttu-id="a298c-130">[Azure disk encryption](../security/azure-security-disk-encryption-overview.md) (document) -- Learn how to enable disk encryption for Windows and Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="a298c-130">[Azure disk encryption](../security/azure-security-disk-encryption-overview.md) (document) -- Learn how to enable disk encryption for Windows and Linux VMs.</span></span>

<span data-ttu-id="a298c-131">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="a298c-131">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="a298c-132">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span><span class="sxs-lookup"><span data-stu-id="a298c-132">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="a298c-133">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a298c-133">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a298c-134">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="a298c-134">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a298c-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a298c-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a298c-136">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="a298c-136">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a298c-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="a298c-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
