---
title: How to generate and transfer HSM-protected keys for Azure Key Vault | Microsoft Docs
description: Use this article to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault. Also known as BYOK or bring your own key.
services: key-vault
documentationcenter: ''
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/27/2018
ms.author: barclayn
ms.openlocfilehash: 31998c3b9cc151e96d0b2e0b85895603698f493b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791224"
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="4f587-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4f587-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>

<span data-ttu-id="4f587-105">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span><span class="sxs-lookup"><span data-stu-id="4f587-105">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="4f587-106">This scenario is often referred to as *bring your own key*, or BYOK.</span><span class="sxs-lookup"><span data-stu-id="4f587-106">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="4f587-107">The HSMs are FIPS 140-2 Level 2 validated.</span><span class="sxs-lookup"><span data-stu-id="4f587-107">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="4f587-108">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span><span class="sxs-lookup"><span data-stu-id="4f587-108">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="4f587-109">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-109">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="4f587-110">This functionality is not available for Azure China.</span><span class="sxs-lookup"><span data-stu-id="4f587-110">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="4f587-111">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="4f587-111">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
> <span data-ttu-id="4f587-112">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f587-112">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

<span data-ttu-id="4f587-113">More information about generating and transferring an HSM-protected key over the Internet:</span><span class="sxs-lookup"><span data-stu-id="4f587-113">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="4f587-114">You generate the key from an offline workstation, which reduces the attack surface.</span><span class="sxs-lookup"><span data-stu-id="4f587-114">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="4f587-115">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span><span class="sxs-lookup"><span data-stu-id="4f587-115">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="4f587-116">Only the encrypted version of your key leaves the original workstation.</span><span class="sxs-lookup"><span data-stu-id="4f587-116">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="4f587-117">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span><span class="sxs-lookup"><span data-stu-id="4f587-117">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="4f587-118">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span><span class="sxs-lookup"><span data-stu-id="4f587-118">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="4f587-119">Your key cannot be exported.</span><span class="sxs-lookup"><span data-stu-id="4f587-119">Your key cannot be exported.</span></span> <span data-ttu-id="4f587-120">This binding is enforced by the Thales HSMs.</span><span class="sxs-lookup"><span data-stu-id="4f587-120">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="4f587-121">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span><span class="sxs-lookup"><span data-stu-id="4f587-121">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="4f587-122">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span><span class="sxs-lookup"><span data-stu-id="4f587-122">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="4f587-123">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span><span class="sxs-lookup"><span data-stu-id="4f587-123">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="4f587-124">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span><span class="sxs-lookup"><span data-stu-id="4f587-124">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="4f587-125">This attestation proves to you that Microsoft is using genuine hardware.</span><span class="sxs-lookup"><span data-stu-id="4f587-125">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="4f587-126">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span><span class="sxs-lookup"><span data-stu-id="4f587-126">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="4f587-127">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span><span class="sxs-lookup"><span data-stu-id="4f587-127">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="4f587-128">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span><span class="sxs-lookup"><span data-stu-id="4f587-128">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="4f587-129">More information about Thales HSMs and Microsoft services</span><span class="sxs-lookup"><span data-stu-id="4f587-129">More information about Thales HSMs and Microsoft services</span></span>

<span data-ttu-id="4f587-130">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span><span class="sxs-lookup"><span data-stu-id="4f587-130">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="4f587-131">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span><span class="sxs-lookup"><span data-stu-id="4f587-131">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="4f587-132">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span><span class="sxs-lookup"><span data-stu-id="4f587-132">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="4f587-133">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span><span class="sxs-lookup"><span data-stu-id="4f587-133">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="4f587-134">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span><span class="sxs-lookup"><span data-stu-id="4f587-134">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="4f587-135">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span><span class="sxs-lookup"><span data-stu-id="4f587-135">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="4f587-136">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span><span class="sxs-lookup"><span data-stu-id="4f587-136">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="4f587-137">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span><span class="sxs-lookup"><span data-stu-id="4f587-137">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="4f587-138">Implementing bring your own key (BYOK) for Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4f587-138">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>

<span data-ttu-id="4f587-139">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span><span class="sxs-lookup"><span data-stu-id="4f587-139">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="4f587-140">Prerequisites for BYOK</span><span class="sxs-lookup"><span data-stu-id="4f587-140">Prerequisites for BYOK</span></span>

<span data-ttu-id="4f587-141">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-141">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="4f587-142">Requirement</span><span class="sxs-lookup"><span data-stu-id="4f587-142">Requirement</span></span> | <span data-ttu-id="4f587-143">More information</span><span class="sxs-lookup"><span data-stu-id="4f587-143">More information</span></span> |
| --- | --- |
| <span data-ttu-id="4f587-144">A subscription to Azure</span><span class="sxs-lookup"><span data-stu-id="4f587-144">A subscription to Azure</span></span> |<span data-ttu-id="4f587-145">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="4f587-145">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="4f587-146">The Azure Key Vault Premium service tier to support HSM-protected keys</span><span class="sxs-lookup"><span data-stu-id="4f587-146">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="4f587-147">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span><span class="sxs-lookup"><span data-stu-id="4f587-147">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="4f587-148">Thales HSM, smartcards, and support software</span><span class="sxs-lookup"><span data-stu-id="4f587-148">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="4f587-149">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span><span class="sxs-lookup"><span data-stu-id="4f587-149">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="4f587-150">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span><span class="sxs-lookup"><span data-stu-id="4f587-150">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="4f587-151">The following hardware and software:</span><span class="sxs-lookup"><span data-stu-id="4f587-151">The following hardware and software:</span></span><ol><li><span data-ttu-id="4f587-152">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span><span class="sxs-lookup"><span data-stu-id="4f587-152">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="4f587-153">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="4f587-153">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="4f587-154">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-6.7.0) **minimum version 1.1.0** installed.</span><span class="sxs-lookup"><span data-stu-id="4f587-154">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-6.7.0) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="4f587-155">A USB drive or other portable storage device that has at least 16 MB free space.</span><span class="sxs-lookup"><span data-stu-id="4f587-155">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="4f587-156">For security reasons, we recommend that the first workstation is not connected to a network.</span><span class="sxs-lookup"><span data-stu-id="4f587-156">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="4f587-157">However, this recommendation is not programmatically enforced.</span><span class="sxs-lookup"><span data-stu-id="4f587-157">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="4f587-158">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span><span class="sxs-lookup"><span data-stu-id="4f587-158">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="4f587-159">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span><span class="sxs-lookup"><span data-stu-id="4f587-159">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="4f587-160">But for testing purposes, you can use the same workstation as the first one.</span><span class="sxs-lookup"><span data-stu-id="4f587-160">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="4f587-161">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span><span class="sxs-lookup"><span data-stu-id="4f587-161">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="4f587-162">Generate and transfer your key to Azure Key Vault HSM</span><span class="sxs-lookup"><span data-stu-id="4f587-162">Generate and transfer your key to Azure Key Vault HSM</span></span>

<span data-ttu-id="4f587-163">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="4f587-163">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="4f587-164">Step 1: Prepare your Internet-connected workstation</span><span class="sxs-lookup"><span data-stu-id="4f587-164">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="4f587-165">Step 2: Prepare your disconnected workstation</span><span class="sxs-lookup"><span data-stu-id="4f587-165">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="4f587-166">Step 3: Generate your key</span><span class="sxs-lookup"><span data-stu-id="4f587-166">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="4f587-167">Step 4: Prepare your key for transfer</span><span class="sxs-lookup"><span data-stu-id="4f587-167">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="4f587-168">Step 5: Transfer your key to Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4f587-168">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="4f587-169">Step 1: Prepare your Internet-connected workstation</span><span class="sxs-lookup"><span data-stu-id="4f587-169">Step 1: Prepare your Internet-connected workstation</span></span>

<span data-ttu-id="4f587-170">For this first step, do the following procedures on your workstation that is connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="4f587-170">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="4f587-171">Step 1.1: Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f587-171">Step 1.1: Install Azure PowerShell</span></span>

<span data-ttu-id="4f587-172">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-172">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="4f587-173">This requires a minimum version of 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="4f587-173">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="4f587-174">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4f587-174">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="4f587-175">Step 1.2: Get your Azure subscription ID</span><span class="sxs-lookup"><span data-stu-id="4f587-175">Step 1.2: Get your Azure subscription ID</span></span>

<span data-ttu-id="4f587-176">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4f587-176">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

```Powershell
   Add-AzureRMAccount
```
<span data-ttu-id="4f587-177">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="4f587-177">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="4f587-178">Then, use the [Get-AzureSubscription](/powershell/module/servicemanagement/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span><span class="sxs-lookup"><span data-stu-id="4f587-178">Then, use the [Get-AzureSubscription](/powershell/module/servicemanagement/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

```powershell
   Get-AzureRMSubscription
```
<span data-ttu-id="4f587-179">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-179">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="4f587-180">You will need this subscription ID later.</span><span class="sxs-lookup"><span data-stu-id="4f587-180">You will need this subscription ID later.</span></span>

<span data-ttu-id="4f587-181">Do not close the Azure PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="4f587-181">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="4f587-182">Step 1.3: Download the BYOK toolset for Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4f587-182">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>

<span data-ttu-id="4f587-183">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span><span class="sxs-lookup"><span data-stu-id="4f587-183">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="4f587-184">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span><span class="sxs-lookup"><span data-stu-id="4f587-184">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="4f587-185">**United States:**</span><span class="sxs-lookup"><span data-stu-id="4f587-185">**United States:**</span></span>

<span data-ttu-id="4f587-186">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-186">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="4f587-187">2E8C00320400430106366A4E8C67B79015524E4EC24A2D3A6DC513CA1823B0D4</span><span class="sxs-lookup"><span data-stu-id="4f587-187">2E8C00320400430106366A4E8C67B79015524E4EC24A2D3A6DC513CA1823B0D4</span></span>

- - -
<span data-ttu-id="4f587-188">**Europe:**</span><span class="sxs-lookup"><span data-stu-id="4f587-188">**Europe:**</span></span>

<span data-ttu-id="4f587-189">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-189">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="4f587-190">9AAA63E2E7F20CF9BB62485868754203721D2F88D300910634A32DFA1FB19E4A</span><span class="sxs-lookup"><span data-stu-id="4f587-190">9AAA63E2E7F20CF9BB62485868754203721D2F88D300910634A32DFA1FB19E4A</span></span>

- - -
<span data-ttu-id="4f587-191">**Asia:**</span><span class="sxs-lookup"><span data-stu-id="4f587-191">**Asia:**</span></span>

<span data-ttu-id="4f587-192">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-192">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="4f587-193">4BC14059BF0FEC562CA927AF621DF665328F8A13616F44C977388EC7121EF6B5</span><span class="sxs-lookup"><span data-stu-id="4f587-193">4BC14059BF0FEC562CA927AF621DF665328F8A13616F44C977388EC7121EF6B5</span></span>

- - -
<span data-ttu-id="4f587-194">**Latin America:**</span><span class="sxs-lookup"><span data-stu-id="4f587-194">**Latin America:**</span></span>

<span data-ttu-id="4f587-195">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-195">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="4f587-196">E7DFAFF579AFE1B9732C30D6FD80C4D03756642F25A538922DD1B01A4FACB619</span><span class="sxs-lookup"><span data-stu-id="4f587-196">E7DFAFF579AFE1B9732C30D6FD80C4D03756642F25A538922DD1B01A4FACB619</span></span>

- - -
<span data-ttu-id="4f587-197">**Japan:**</span><span class="sxs-lookup"><span data-stu-id="4f587-197">**Japan:**</span></span>

<span data-ttu-id="4f587-198">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-198">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="4f587-199">3933C13CC6DC06651295ADC482B027AF923A76F1F6BF98B4D4B8E94632DEC7DF</span><span class="sxs-lookup"><span data-stu-id="4f587-199">3933C13CC6DC06651295ADC482B027AF923A76F1F6BF98B4D4B8E94632DEC7DF</span></span>

- - -
<span data-ttu-id="4f587-200">**Korea:**</span><span class="sxs-lookup"><span data-stu-id="4f587-200">**Korea:**</span></span>

<span data-ttu-id="4f587-201">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-201">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="4f587-202">71AB6BCFE06950097C8C18D532A9184BEF52A74BB944B8610DDDA05344ED136F</span><span class="sxs-lookup"><span data-stu-id="4f587-202">71AB6BCFE06950097C8C18D532A9184BEF52A74BB944B8610DDDA05344ED136F</span></span>

- - -
<span data-ttu-id="4f587-203">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="4f587-203">**Australia:**</span></span>

<span data-ttu-id="4f587-204">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-204">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="4f587-205">CD0FB7365053DEF8C35116D7C92D203C64A3D3EE2452A025223EEB166901C40A</span><span class="sxs-lookup"><span data-stu-id="4f587-205">CD0FB7365053DEF8C35116D7C92D203C64A3D3EE2452A025223EEB166901C40A</span></span>

- - -
[<span data-ttu-id="4f587-206">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="4f587-206">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="4f587-207">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-207">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="4f587-208">F8DB2FC914A7360650922391D9AA79FF030FD3048B5795EC83ADC59DB018621A</span><span class="sxs-lookup"><span data-stu-id="4f587-208">F8DB2FC914A7360650922391D9AA79FF030FD3048B5795EC83ADC59DB018621A</span></span>

- - -
<span data-ttu-id="4f587-209">**US Government DOD:**</span><span class="sxs-lookup"><span data-stu-id="4f587-209">**US Government DOD:**</span></span>

<span data-ttu-id="4f587-210">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-210">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="4f587-211">A79DD8C6DFFF1B00B91D1812280207A205442B3DDF861B79B8B991BB55C35263</span><span class="sxs-lookup"><span data-stu-id="4f587-211">A79DD8C6DFFF1B00B91D1812280207A205442B3DDF861B79B8B991BB55C35263</span></span>

- - -
<span data-ttu-id="4f587-212">**Canada:**</span><span class="sxs-lookup"><span data-stu-id="4f587-212">**Canada:**</span></span>

<span data-ttu-id="4f587-213">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-213">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="4f587-214">61BE1A1F80AC79912A42DEBBCC42CF87C88C2CE249E271934630885799717C7B</span><span class="sxs-lookup"><span data-stu-id="4f587-214">61BE1A1F80AC79912A42DEBBCC42CF87C88C2CE249E271934630885799717C7B</span></span>

- - -
<span data-ttu-id="4f587-215">**Germany:**</span><span class="sxs-lookup"><span data-stu-id="4f587-215">**Germany:**</span></span>

<span data-ttu-id="4f587-216">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-216">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="4f587-217">5385E615880AAFC02AFD9841F7BADD025D7EE819894AA29ED3C71C3F844C45D6</span><span class="sxs-lookup"><span data-stu-id="4f587-217">5385E615880AAFC02AFD9841F7BADD025D7EE819894AA29ED3C71C3F844C45D6</span></span>

- - -
<span data-ttu-id="4f587-218">**India:**</span><span class="sxs-lookup"><span data-stu-id="4f587-218">**India:**</span></span>

<span data-ttu-id="4f587-219">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-219">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="4f587-220">49EDCEB3091CF1DF7B156D5B495A4ADE1CFBA77641134F61B0E0940121C436C8</span><span class="sxs-lookup"><span data-stu-id="4f587-220">49EDCEB3091CF1DF7B156D5B495A4ADE1CFBA77641134F61B0E0940121C436C8</span></span>

- - -
<span data-ttu-id="4f587-221">**France:**</span><span class="sxs-lookup"><span data-stu-id="4f587-221">**France:**</span></span>

<span data-ttu-id="4f587-222">KeyVault-BYOK-Tools-France.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-222">KeyVault-BYOK-Tools-France.zip</span></span>

<span data-ttu-id="4f587-223">5C9D1F3E4125B0C09E9F60897C9AE3A8B4CB0E7D13A14F3EDBD280128F8FE7DF</span><span class="sxs-lookup"><span data-stu-id="4f587-223">5C9D1F3E4125B0C09E9F60897C9AE3A8B4CB0E7D13A14F3EDBD280128F8FE7DF</span></span>

- - -
<span data-ttu-id="4f587-224">**United Kingdom:**</span><span class="sxs-lookup"><span data-stu-id="4f587-224">**United Kingdom:**</span></span>

<span data-ttu-id="4f587-225">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="4f587-225">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="4f587-226">432746BD0D3176B708672CCFF19D6144FCAA9E5EB29BB056489D3782B3B80849</span><span class="sxs-lookup"><span data-stu-id="4f587-226">432746BD0D3176B708672CCFF19D6144FCAA9E5EB29BB056489D3782B3B80849</span></span>

- - -

<span data-ttu-id="4f587-227">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4f587-227">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

   ```powershell
   Get-FileHash KeyVault-BYOK-Tools-*.zip
   ```

<span data-ttu-id="4f587-228">The toolset includes the following:</span><span class="sxs-lookup"><span data-stu-id="4f587-228">The toolset includes the following:</span></span>

* <span data-ttu-id="4f587-229">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="4f587-229">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="4f587-230">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="4f587-230">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="4f587-231">A python script named **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="4f587-231">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="4f587-232">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span><span class="sxs-lookup"><span data-stu-id="4f587-232">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="4f587-233">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="4f587-233">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="4f587-234">Copy the package to a USB drive or other portable storage.</span><span class="sxs-lookup"><span data-stu-id="4f587-234">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="4f587-235">Step 2: Prepare your disconnected workstation</span><span class="sxs-lookup"><span data-stu-id="4f587-235">Step 2: Prepare your disconnected workstation</span></span>

<span data-ttu-id="4f587-236">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span><span class="sxs-lookup"><span data-stu-id="4f587-236">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="4f587-237">Step 2.1: Prepare the disconnected workstation with Thales HSM</span><span class="sxs-lookup"><span data-stu-id="4f587-237">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>

<span data-ttu-id="4f587-238">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span><span class="sxs-lookup"><span data-stu-id="4f587-238">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="4f587-239">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="4f587-239">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="4f587-240">For example, type the following:</span><span class="sxs-lookup"><span data-stu-id="4f587-240">For example, type the following:</span></span>

  ```cmd
  set PATH=%PATH%;"%nfast_home%\bin"
  ```

<span data-ttu-id="4f587-241">For more information, see the user guide included with the Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="4f587-241">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="4f587-242">Step 2.2: Install the BYOK toolset on the disconnected workstation</span><span class="sxs-lookup"><span data-stu-id="4f587-242">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>

<span data-ttu-id="4f587-243">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="4f587-243">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="4f587-244">Extract the files from the downloaded package into any folder.</span><span class="sxs-lookup"><span data-stu-id="4f587-244">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="4f587-245">From that folder, run vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="4f587-245">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="4f587-246">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4f587-246">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="4f587-247">Step 3: Generate your key</span><span class="sxs-lookup"><span data-stu-id="4f587-247">Step 3: Generate your key</span></span>

<span data-ttu-id="4f587-248">For this third step, do the following procedures on the disconnected workstation.</span><span class="sxs-lookup"><span data-stu-id="4f587-248">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="4f587-249">To complete this step your HSM must be in initialization mode.</span><span class="sxs-lookup"><span data-stu-id="4f587-249">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="4f587-250">Step 3.1: Change the HSM mode to 'I'</span><span class="sxs-lookup"><span data-stu-id="4f587-250">Step 3.1: Change the HSM mode to 'I'</span></span>

<span data-ttu-id="4f587-251">If you are using Thales nShield Edge, to change the mode: 1.</span><span class="sxs-lookup"><span data-stu-id="4f587-251">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="4f587-252">Use the Mode button to highlight the required mode.</span><span class="sxs-lookup"><span data-stu-id="4f587-252">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="4f587-253">2.</span><span class="sxs-lookup"><span data-stu-id="4f587-253">2.</span></span> <span data-ttu-id="4f587-254">Within a few seconds, press and hold the Clear button for a couple of seconds.</span><span class="sxs-lookup"><span data-stu-id="4f587-254">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="4f587-255">If the mode changes, the new mode’s LED stops flashing and remains lit.</span><span class="sxs-lookup"><span data-stu-id="4f587-255">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="4f587-256">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span><span class="sxs-lookup"><span data-stu-id="4f587-256">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="4f587-257">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span><span class="sxs-lookup"><span data-stu-id="4f587-257">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="4f587-258">Step 3.2: Create a security world</span><span class="sxs-lookup"><span data-stu-id="4f587-258">Step 3.2: Create a security world</span></span>

<span data-ttu-id="4f587-259">Start a command prompt and run the Thales new-world program.</span><span class="sxs-lookup"><span data-stu-id="4f587-259">Start a command prompt and run the Thales new-world program.</span></span>

   ```cmd
    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
   ```

<span data-ttu-id="4f587-260">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span><span class="sxs-lookup"><span data-stu-id="4f587-260">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="4f587-261">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span><span class="sxs-lookup"><span data-stu-id="4f587-261">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="4f587-262">Then, any two cards give full access to the security world.</span><span class="sxs-lookup"><span data-stu-id="4f587-262">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="4f587-263">These cards become the **Administrator Card Set** for the new security world.</span><span class="sxs-lookup"><span data-stu-id="4f587-263">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="4f587-264">Then do the following:</span><span class="sxs-lookup"><span data-stu-id="4f587-264">Then do the following:</span></span>

* <span data-ttu-id="4f587-265">Back up the world file.</span><span class="sxs-lookup"><span data-stu-id="4f587-265">Back up the world file.</span></span> <span data-ttu-id="4f587-266">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span><span class="sxs-lookup"><span data-stu-id="4f587-266">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="4f587-267">Step 3.3: Change the HSM mode to 'O'</span><span class="sxs-lookup"><span data-stu-id="4f587-267">Step 3.3: Change the HSM mode to 'O'</span></span>

<span data-ttu-id="4f587-268">If you are using Thales nShield Edge, to change the mode: 1.</span><span class="sxs-lookup"><span data-stu-id="4f587-268">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="4f587-269">Use the Mode button to highlight the required mode.</span><span class="sxs-lookup"><span data-stu-id="4f587-269">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="4f587-270">2.</span><span class="sxs-lookup"><span data-stu-id="4f587-270">2.</span></span> <span data-ttu-id="4f587-271">Within a few seconds, press and hold the Clear button for a couple of seconds.</span><span class="sxs-lookup"><span data-stu-id="4f587-271">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="4f587-272">If the mode changes, the new mode’s LED stops flashing and remains lit.</span><span class="sxs-lookup"><span data-stu-id="4f587-272">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="4f587-273">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span><span class="sxs-lookup"><span data-stu-id="4f587-273">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="4f587-274">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span><span class="sxs-lookup"><span data-stu-id="4f587-274">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="4f587-275">Step 3.4: Validate the downloaded package</span><span class="sxs-lookup"><span data-stu-id="4f587-275">Step 3.4: Validate the downloaded package</span></span>

<span data-ttu-id="4f587-276">This step is optional but recommended so that you can validate the following:</span><span class="sxs-lookup"><span data-stu-id="4f587-276">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="4f587-277">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="4f587-277">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="4f587-278">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="4f587-278">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="4f587-279">The Key Exchange Key is non-exportable.</span><span class="sxs-lookup"><span data-stu-id="4f587-279">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="4f587-280">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span><span class="sxs-lookup"><span data-stu-id="4f587-280">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>

<span data-ttu-id="4f587-281">To validate the downloaded package:</span><span class="sxs-lookup"><span data-stu-id="4f587-281">To validate the downloaded package:</span></span>

1. <span data-ttu-id="4f587-282">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="4f587-282">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="4f587-283">For North America:</span><span class="sxs-lookup"><span data-stu-id="4f587-283">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="4f587-284">For Europe:</span><span class="sxs-lookup"><span data-stu-id="4f587-284">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="4f587-285">For Asia:</span><span class="sxs-lookup"><span data-stu-id="4f587-285">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="4f587-286">For Latin America:</span><span class="sxs-lookup"><span data-stu-id="4f587-286">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="4f587-287">For Japan:</span><span class="sxs-lookup"><span data-stu-id="4f587-287">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="4f587-288">For Korea:</span><span class="sxs-lookup"><span data-stu-id="4f587-288">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="4f587-289">For Australia:</span><span class="sxs-lookup"><span data-stu-id="4f587-289">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="4f587-290">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="4f587-290">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="4f587-291">For US Government DOD:</span><span class="sxs-lookup"><span data-stu-id="4f587-291">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="4f587-292">For Canada:</span><span class="sxs-lookup"><span data-stu-id="4f587-292">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="4f587-293">For Germany:</span><span class="sxs-lookup"><span data-stu-id="4f587-293">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="4f587-294">For India:</span><span class="sxs-lookup"><span data-stu-id="4f587-294">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
   * <span data-ttu-id="4f587-295">For France:</span><span class="sxs-lookup"><span data-stu-id="4f587-295">For France:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-FRANCE-1 -w BYOK-SecurityWorld-pkg-FRANCE-1
   * <span data-ttu-id="4f587-296">For United Kingdom:</span><span class="sxs-lookup"><span data-stu-id="4f587-296">For United Kingdom:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-UK-1 -w BYOK-SecurityWorld-pkg-UK-1

     > [!TIP]
     > <span data-ttu-id="4f587-297">The Thales software includes python at %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="4f587-297">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="4f587-298">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="4f587-298">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="4f587-299">This script validates the signer chain up to the Thales root key.</span><span class="sxs-lookup"><span data-stu-id="4f587-299">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="4f587-300">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="4f587-300">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="4f587-301">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="4f587-301">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="4f587-302">You’re now ready to create a new key.</span><span class="sxs-lookup"><span data-stu-id="4f587-302">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="4f587-303">Step 3.5: Create a new key</span><span class="sxs-lookup"><span data-stu-id="4f587-303">Step 3.5: Create a new key</span></span>

<span data-ttu-id="4f587-304">Generate a key by using the Thales **generatekey** program.</span><span class="sxs-lookup"><span data-stu-id="4f587-304">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="4f587-305">Run the following command to generate the key:</span><span class="sxs-lookup"><span data-stu-id="4f587-305">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="4f587-306">When you run this command, use these instructions:</span><span class="sxs-lookup"><span data-stu-id="4f587-306">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="4f587-307">The parameter *protect* must be set to the value **module**, as shown.</span><span class="sxs-lookup"><span data-stu-id="4f587-307">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="4f587-308">This creates a module-protected key.</span><span class="sxs-lookup"><span data-stu-id="4f587-308">This creates a module-protected key.</span></span> <span data-ttu-id="4f587-309">The BYOK toolset does not support OCS-protected keys.</span><span class="sxs-lookup"><span data-stu-id="4f587-309">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="4f587-310">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span><span class="sxs-lookup"><span data-stu-id="4f587-310">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="4f587-311">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span><span class="sxs-lookup"><span data-stu-id="4f587-311">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="4f587-312">The **ident** value must contain only numbers, dashes, and lower case letters.</span><span class="sxs-lookup"><span data-stu-id="4f587-312">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="4f587-313">The pubexp is left blank (default) in this example, but you can specify specific values.</span><span class="sxs-lookup"><span data-stu-id="4f587-313">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="4f587-314">For more information, see the Thales documentation.</span><span class="sxs-lookup"><span data-stu-id="4f587-314">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="4f587-315">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span><span class="sxs-lookup"><span data-stu-id="4f587-315">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="4f587-316">For example: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="4f587-316">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="4f587-317">This file contains an encrypted key.</span><span class="sxs-lookup"><span data-stu-id="4f587-317">This file contains an encrypted key.</span></span>

<span data-ttu-id="4f587-318">Back up this Tokenized Key File in a safe location.</span><span class="sxs-lookup"><span data-stu-id="4f587-318">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f587-319">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span><span class="sxs-lookup"><span data-stu-id="4f587-319">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="4f587-320">Contact Thales for guidance and best practices for backing up your key.</span><span class="sxs-lookup"><span data-stu-id="4f587-320">Contact Thales for guidance and best practices for backing up your key.</span></span>
>


<span data-ttu-id="4f587-321">You are now ready to transfer your key to Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-321">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="4f587-322">Step 4: Prepare your key for transfer</span><span class="sxs-lookup"><span data-stu-id="4f587-322">Step 4: Prepare your key for transfer</span></span>

<span data-ttu-id="4f587-323">For this fourth step, do the following procedures on the disconnected workstation.</span><span class="sxs-lookup"><span data-stu-id="4f587-323">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="4f587-324">Step 4.1: Create a copy of your key with reduced permissions</span><span class="sxs-lookup"><span data-stu-id="4f587-324">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="4f587-325">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span><span class="sxs-lookup"><span data-stu-id="4f587-325">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="4f587-326">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="4f587-326">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="4f587-327">For North America:</span><span class="sxs-lookup"><span data-stu-id="4f587-327">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="4f587-328">For Europe:</span><span class="sxs-lookup"><span data-stu-id="4f587-328">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="4f587-329">For Asia:</span><span class="sxs-lookup"><span data-stu-id="4f587-329">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="4f587-330">For Latin America:</span><span class="sxs-lookup"><span data-stu-id="4f587-330">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="4f587-331">For Japan:</span><span class="sxs-lookup"><span data-stu-id="4f587-331">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="4f587-332">For Korea:</span><span class="sxs-lookup"><span data-stu-id="4f587-332">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="4f587-333">For Australia:</span><span class="sxs-lookup"><span data-stu-id="4f587-333">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="4f587-334">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="4f587-334">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="4f587-335">For US Government DOD:</span><span class="sxs-lookup"><span data-stu-id="4f587-335">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="4f587-336">For Canada:</span><span class="sxs-lookup"><span data-stu-id="4f587-336">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="4f587-337">For Germany:</span><span class="sxs-lookup"><span data-stu-id="4f587-337">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="4f587-338">For India:</span><span class="sxs-lookup"><span data-stu-id="4f587-338">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1
* <span data-ttu-id="4f587-339">For France:</span><span class="sxs-lookup"><span data-stu-id="4f587-339">For France:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-FRANCE-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-FRANCE-1
* <span data-ttu-id="4f587-340">For United Kingdom:</span><span class="sxs-lookup"><span data-stu-id="4f587-340">For United Kingdom:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-UK-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-UK-1

<span data-ttu-id="4f587-341">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span><span class="sxs-lookup"><span data-stu-id="4f587-341">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="4f587-342">You are asked to plug in your security world admin cards.</span><span class="sxs-lookup"><span data-stu-id="4f587-342">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="4f587-343">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="4f587-343">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="4f587-344">You may inspects the ACLS using following commands using the Thales utilities:</span><span class="sxs-lookup"><span data-stu-id="4f587-344">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="4f587-345">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="4f587-345">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="4f587-346">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="4f587-346">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="4f587-347">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span><span class="sxs-lookup"><span data-stu-id="4f587-347">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="4f587-348">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span><span class="sxs-lookup"><span data-stu-id="4f587-348">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>

<span data-ttu-id="4f587-349">Run one of the following commands, depending on your geographic region or instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="4f587-349">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="4f587-350">For North America:</span><span class="sxs-lookup"><span data-stu-id="4f587-350">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-351">For Europe:</span><span class="sxs-lookup"><span data-stu-id="4f587-351">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-352">For Asia:</span><span class="sxs-lookup"><span data-stu-id="4f587-352">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-353">For Latin America:</span><span class="sxs-lookup"><span data-stu-id="4f587-353">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-354">For Japan:</span><span class="sxs-lookup"><span data-stu-id="4f587-354">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-355">For Korea:</span><span class="sxs-lookup"><span data-stu-id="4f587-355">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-356">For Australia:</span><span class="sxs-lookup"><span data-stu-id="4f587-356">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-357">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="4f587-357">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-358">For US Government DOD:</span><span class="sxs-lookup"><span data-stu-id="4f587-358">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-359">For Canada:</span><span class="sxs-lookup"><span data-stu-id="4f587-359">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-360">For Germany:</span><span class="sxs-lookup"><span data-stu-id="4f587-360">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-361">For India:</span><span class="sxs-lookup"><span data-stu-id="4f587-361">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-362">For France:</span><span class="sxs-lookup"><span data-stu-id="4f587-362">For France:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-France-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-France-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="4f587-363">For United Kingdom:</span><span class="sxs-lookup"><span data-stu-id="4f587-363">For United Kingdom:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-UK-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-UK-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="4f587-364">When you run this command, use these instructions:</span><span class="sxs-lookup"><span data-stu-id="4f587-364">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="4f587-365">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span><span class="sxs-lookup"><span data-stu-id="4f587-365">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="4f587-366">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-366">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="4f587-367">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span><span class="sxs-lookup"><span data-stu-id="4f587-367">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="4f587-368">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span><span class="sxs-lookup"><span data-stu-id="4f587-368">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="4f587-369">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="4f587-369">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="4f587-370">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span><span class="sxs-lookup"><span data-stu-id="4f587-370">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>

<span data-ttu-id="4f587-371">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span><span class="sxs-lookup"><span data-stu-id="4f587-371">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="4f587-372">Step 5: Transfer your key to Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4f587-372">Step 5: Transfer your key to Azure Key Vault</span></span>

<span data-ttu-id="4f587-373">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-add-azurekeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="4f587-373">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-add-azurekeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

   ```powershell
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'
   ```

<span data-ttu-id="4f587-374">If the upload is successful, you see displayed the properties of the key that you just added.</span><span class="sxs-lookup"><span data-stu-id="4f587-374">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f587-375">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f587-375">Next steps</span></span>

<span data-ttu-id="4f587-376">You can now use this HSM-protected key in your key vault.</span><span class="sxs-lookup"><span data-stu-id="4f587-376">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="4f587-377">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="4f587-377">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
