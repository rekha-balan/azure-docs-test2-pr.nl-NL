---
title: How to generate and transfer HSM-protected keys for Azure Key Vault | Microsoft Docs
description: Use this article to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.
services: key-vault
documentationcenter: ''
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/30/2016
ms.author: ambapat
ms.openlocfilehash: b189106be19b95366ba0e6d248c69b34b219b8a1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550824"
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="6c0fa-103">How to generate and transfer HSM-protected keys for Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6c0fa-103">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="6c0fa-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="6c0fa-104">Introduction</span></span>
<span data-ttu-id="6c0fa-105">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-105">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="6c0fa-106">This scenario is often referred to as *bring your own key*, or BYOK.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-106">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="6c0fa-107">The HSMs are FIPS 140-2 Level 2 validated.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-107">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="6c0fa-108">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-108">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="6c0fa-109">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-109">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="6c0fa-110">This functionality is not available for Azure China.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-110">This functionality is not available for Azure China.</span></span> 

> [!NOTE]
> <span data-ttu-id="6c0fa-111">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6c0fa-111">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
> 
> <span data-ttu-id="6c0fa-112">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-112">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="6c0fa-113">More information about generating and transferring an HSM-protected key over the Internet:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-113">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="6c0fa-114">You generate the key from an offline workstation, which reduces the attack surface.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-114">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="6c0fa-115">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-115">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="6c0fa-116">Only the encrypted version of your key leaves the original workstation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-116">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="6c0fa-117">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-117">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="6c0fa-118">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-118">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="6c0fa-119">Your key cannot be exported.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-119">Your key cannot be exported.</span></span> <span data-ttu-id="6c0fa-120">This binding is enforced by the Thales HSMs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-120">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="6c0fa-121">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-121">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="6c0fa-122">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-122">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="6c0fa-123">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-123">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="6c0fa-124">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-124">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="6c0fa-125">This attestation proves to you that Microsoft is using genuine hardware.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-125">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="6c0fa-126">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-126">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="6c0fa-127">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-127">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="6c0fa-128">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-128">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="6c0fa-129">More information about Thales HSMs and Microsoft services</span><span class="sxs-lookup"><span data-stu-id="6c0fa-129">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="6c0fa-130">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-130">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="6c0fa-131">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-131">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="6c0fa-132">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-132">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="6c0fa-133">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-133">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="6c0fa-134">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-134">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="6c0fa-135">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-135">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="6c0fa-136">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-136">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="6c0fa-137">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-137">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="6c0fa-138">Implementing bring your own key (BYOK) for Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6c0fa-138">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="6c0fa-139">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-139">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="6c0fa-140">Prerequisites for BYOK</span><span class="sxs-lookup"><span data-stu-id="6c0fa-140">Prerequisites for BYOK</span></span>
<span data-ttu-id="6c0fa-141">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-141">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="6c0fa-142">Requirement</span><span class="sxs-lookup"><span data-stu-id="6c0fa-142">Requirement</span></span> | <span data-ttu-id="6c0fa-143">More information</span><span class="sxs-lookup"><span data-stu-id="6c0fa-143">More information</span></span> |
| --- | --- |
| <span data-ttu-id="6c0fa-144">A subscription to Azure</span><span class="sxs-lookup"><span data-stu-id="6c0fa-144">A subscription to Azure</span></span> |<span data-ttu-id="6c0fa-145">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="6c0fa-145">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="6c0fa-146">The Azure Key Vault Premium service tier to support HSM-protected keys</span><span class="sxs-lookup"><span data-stu-id="6c0fa-146">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="6c0fa-147">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-147">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="6c0fa-148">Thales HSM, smartcards, and support software</span><span class="sxs-lookup"><span data-stu-id="6c0fa-148">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="6c0fa-149">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-149">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="6c0fa-150">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-150">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="6c0fa-151">The following hardware and software:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-151">The following hardware and software:</span></span><ol><li><span data-ttu-id="6c0fa-152">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-152">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="6c0fa-153">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-153">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="6c0fa-154">A workstation that is connected to the Internet and has a minimum Windows operation system of Windows 7.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-154">A workstation that is connected to the Internet and has a minimum Windows operation system of Windows 7.</span></span></li><li><span data-ttu-id="6c0fa-155">A USB drive or other portable storage device that has at least 16 MB free space.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-155">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="6c0fa-156">For security reasons, we recommend that the first workstation is not connected to a network.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-156">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="6c0fa-157">However, this recommendation is not programmatically enforced.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-157">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="6c0fa-158">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-158">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="6c0fa-159">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-159">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="6c0fa-160">But for testing purposes, you can use the same workstation as the first one.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-160">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="6c0fa-161">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-161">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="6c0fa-162">Generate and transfer your key to Azure Key Vault HSM</span><span class="sxs-lookup"><span data-stu-id="6c0fa-162">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="6c0fa-163">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-163">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="6c0fa-164">Step 1: Prepare your Internet-connected workstation</span><span class="sxs-lookup"><span data-stu-id="6c0fa-164">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="6c0fa-165">Step 2: Prepare your disconnected workstation</span><span class="sxs-lookup"><span data-stu-id="6c0fa-165">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="6c0fa-166">Step 3: Generate your key</span><span class="sxs-lookup"><span data-stu-id="6c0fa-166">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="6c0fa-167">Step 4: Prepare your key for transfer</span><span class="sxs-lookup"><span data-stu-id="6c0fa-167">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="6c0fa-168">Step 5: Transfer your key to Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6c0fa-168">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="6c0fa-169">Step 1: Prepare your Internet-connected workstation</span><span class="sxs-lookup"><span data-stu-id="6c0fa-169">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="6c0fa-170">For this first step, do the following procedures on your workstation that is connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-170">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="6c0fa-171">Step 1.1: Install Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c0fa-171">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="6c0fa-172">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-172">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="6c0fa-173">This requires a minimum version of 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-173">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="6c0fa-174">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-174">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="6c0fa-175">Step 1.2: Get your Azure subscription ID</span><span class="sxs-lookup"><span data-stu-id="6c0fa-175">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="6c0fa-176">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-176">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="6c0fa-177">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-177">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="6c0fa-178">Then, use the [Get-AzureSubscription](https://msdn.microsoft.com/library/azure/dn790366.aspx) command:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-178">Then, use the [Get-AzureSubscription](https://msdn.microsoft.com/library/azure/dn790366.aspx) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="6c0fa-179">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-179">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="6c0fa-180">You will need this subscription ID later.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-180">You will need this subscription ID later.</span></span>

<span data-ttu-id="6c0fa-181">Do not close the Azure PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-181">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="6c0fa-182">Step 1.3: Download the BYOK toolset for Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6c0fa-182">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="6c0fa-183">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-183">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="6c0fa-184">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-184">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="6c0fa-185">**United States:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-185">**United States:**</span></span>

<span data-ttu-id="6c0fa-186">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-186">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="6c0fa-187">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="6c0fa-187">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="6c0fa-188">**Europe:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-188">**Europe:**</span></span>

<span data-ttu-id="6c0fa-189">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-189">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="6c0fa-190">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="6c0fa-190">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="6c0fa-191">**Asia:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-191">**Asia:**</span></span>

<span data-ttu-id="6c0fa-192">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-192">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="6c0fa-193">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="6c0fa-193">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="6c0fa-194">**Latin America:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-194">**Latin America:**</span></span>

<span data-ttu-id="6c0fa-195">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-195">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="6c0fa-196">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="6c0fa-196">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="6c0fa-197">**Japan:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-197">**Japan:**</span></span>

<span data-ttu-id="6c0fa-198">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-198">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="6c0fa-199">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="6c0fa-199">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="6c0fa-200">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-200">**Australia:**</span></span>

<span data-ttu-id="6c0fa-201">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-201">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="6c0fa-202">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="6c0fa-202">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="6c0fa-203">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-203">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="6c0fa-204">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-204">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="6c0fa-205">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="6c0fa-205">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="6c0fa-206">**Canada:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-206">**Canada:**</span></span>

<span data-ttu-id="6c0fa-207">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-207">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="6c0fa-208">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="6c0fa-208">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="6c0fa-209">**Germany:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-209">**Germany:**</span></span>

<span data-ttu-id="6c0fa-210">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-210">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="6c0fa-211">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="6c0fa-211">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="6c0fa-212">**India:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-212">**India:**</span></span>

<span data-ttu-id="6c0fa-213">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-213">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="6c0fa-214">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="6c0fa-214">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="6c0fa-215">**United Kingdom:**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-215">**United Kingdom:**</span></span>

<span data-ttu-id="6c0fa-216">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="6c0fa-216">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="6c0fa-217">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="6c0fa-217">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="6c0fa-218">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-218">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="6c0fa-219">The toolset includes the following:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-219">The toolset includes the following:</span></span>

* <span data-ttu-id="6c0fa-220">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-220">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="6c0fa-221">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-221">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="6c0fa-222">A python script named v**erifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-222">A python script named v**erifykeypackage.py.**</span></span>
* <span data-ttu-id="6c0fa-223">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-223">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="6c0fa-224">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-224">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="6c0fa-225">Copy the package to a USB drive or other portable storage.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-225">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="6c0fa-226">Step 2: Prepare your disconnected workstation</span><span class="sxs-lookup"><span data-stu-id="6c0fa-226">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="6c0fa-227">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-227">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="6c0fa-228">Step 2.1: Prepare the disconnected workstation with Thales HSM</span><span class="sxs-lookup"><span data-stu-id="6c0fa-228">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="6c0fa-229">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-229">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="6c0fa-230">Ensure that the Thales tools are in your path (**%nfast_home%\bin** and **%nfast_home%\python\bin**).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-230">Ensure that the Thales tools are in your path (**%nfast_home%\bin** and **%nfast_home%\python\bin**).</span></span> <span data-ttu-id="6c0fa-231">For example, type the following:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-231">For example, type the following:</span></span>

        set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”

<span data-ttu-id="6c0fa-232">For more information, see the user guide included with the Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-232">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="6c0fa-233">Step 2.2: Install the BYOK toolset on the disconnected workstation</span><span class="sxs-lookup"><span data-stu-id="6c0fa-233">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="6c0fa-234">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-234">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="6c0fa-235">Extract the files from the downloaded package into any folder.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-235">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="6c0fa-236">From that folder, run vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-236">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="6c0fa-237">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-237">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="6c0fa-238">Step 3: Generate your key</span><span class="sxs-lookup"><span data-stu-id="6c0fa-238">Step 3: Generate your key</span></span>
<span data-ttu-id="6c0fa-239">For this third step, do the following procedures on the disconnected workstation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-239">For this third step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-31-create-a-security-world"></a><span data-ttu-id="6c0fa-240">Step 3.1: Create a security world</span><span class="sxs-lookup"><span data-stu-id="6c0fa-240">Step 3.1: Create a security world</span></span>
<span data-ttu-id="6c0fa-241">Start a command prompt and run the Thales new-world program.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-241">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="6c0fa-242">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-242">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="6c0fa-243">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-243">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="6c0fa-244">Then, any two cards give full access to the security world.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-244">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="6c0fa-245">These cards become the **Administrator Card Set** for the new security world.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-245">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="6c0fa-246">Then do the following:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-246">Then do the following:</span></span>

* <span data-ttu-id="6c0fa-247">Back up the world file.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-247">Back up the world file.</span></span> <span data-ttu-id="6c0fa-248">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-248">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-32-validate-the-downloaded-package"></a><span data-ttu-id="6c0fa-249">Step 3.2: Validate the downloaded package</span><span class="sxs-lookup"><span data-stu-id="6c0fa-249">Step 3.2: Validate the downloaded package</span></span>
<span data-ttu-id="6c0fa-250">This step is optional but recommended so that you can validate the following:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-250">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="6c0fa-251">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-251">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="6c0fa-252">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-252">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="6c0fa-253">The Key Exchange Key is non-exportable.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-253">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="6c0fa-254">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-254">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
> 
> 

<span data-ttu-id="6c0fa-255">To validate the downloaded package:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-255">To validate the downloaded package:</span></span>

1. <span data-ttu-id="6c0fa-256">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-256">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>
   
   * <span data-ttu-id="6c0fa-257">For North America:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-257">For North America:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="6c0fa-258">For Europe:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-258">For Europe:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="6c0fa-259">For Asia:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-259">For Asia:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="6c0fa-260">For Latin America:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-260">For Latin America:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="6c0fa-261">For Japan:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-261">For Japan:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="6c0fa-262">For Australia:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-262">For Australia:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="6c0fa-263">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-263">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="6c0fa-264">For Canada:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-264">For Canada:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="6c0fa-265">For Germany:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-265">For Germany:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="6c0fa-266">For India:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-266">For India:</span></span>
     
         python verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="6c0fa-267">The Thales software includes python at %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="6c0fa-267">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     > 
     > 
2. <span data-ttu-id="6c0fa-268">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="6c0fa-268">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="6c0fa-269">This script validates the signer chain up to the Thales root key.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-269">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="6c0fa-270">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-270">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="6c0fa-271">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="6c0fa-271">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="6c0fa-272">You’re now ready to create a new key.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-272">You’re now ready to create a new key.</span></span>

### <a name="step-33-create-a-new-key"></a><span data-ttu-id="6c0fa-273">Step 3.3: Create a new key</span><span class="sxs-lookup"><span data-stu-id="6c0fa-273">Step 3.3: Create a new key</span></span>
<span data-ttu-id="6c0fa-274">Generate a key by using the Thales **generatekey** program.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-274">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="6c0fa-275">Run the following command to generate the key:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-275">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="6c0fa-276">When you run this command, use these instructions:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-276">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="6c0fa-277">The parameter *protect* must be set to the value **module**, as shown.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-277">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="6c0fa-278">This creates a module-protected key.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-278">This creates a module-protected key.</span></span> <span data-ttu-id="6c0fa-279">The BYOK toolset does not support OCS-protected keys.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-279">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="6c0fa-280">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-280">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="6c0fa-281">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-281">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="6c0fa-282">The **ident** value must contain only numbers, dashes, and lower case letters.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-282">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="6c0fa-283">The pubexp is left blank (default) in this example, but you can specify specific values.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-283">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="6c0fa-284">For more information, see the Thales documentation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-284">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="6c0fa-285">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-285">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="6c0fa-286">For example: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-286">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="6c0fa-287">This file contains an encrypted key.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-287">This file contains an encrypted key.</span></span>

<span data-ttu-id="6c0fa-288">Back up this Tokenized Key File in a safe location.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-288">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c0fa-289">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-289">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="6c0fa-290">Contact Thales for guidance and best practices for backing up your key.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-290">Contact Thales for guidance and best practices for backing up your key.</span></span>
> 
> 

<span data-ttu-id="6c0fa-291">You are now ready to transfer your key to Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-291">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="6c0fa-292">Step 4: Prepare your key for transfer</span><span class="sxs-lookup"><span data-stu-id="6c0fa-292">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="6c0fa-293">For this fourth step, do the following procedures on the disconnected workstation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-293">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="6c0fa-294">Step 4.1: Create a copy of your key with reduced permissions</span><span class="sxs-lookup"><span data-stu-id="6c0fa-294">Step 4.1: Create a copy of your key with reduced permissions</span></span>
<span data-ttu-id="6c0fa-295">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-295">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="6c0fa-296">For North America:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-296">For North America:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="6c0fa-297">For Europe:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-297">For Europe:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="6c0fa-298">For Asia:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-298">For Asia:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="6c0fa-299">For Latin America:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-299">For Latin America:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="6c0fa-300">For Japan:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-300">For Japan:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="6c0fa-301">For Australia:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-301">For Australia:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="6c0fa-302">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-302">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="6c0fa-303">For Canada:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-303">For Canada:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="6c0fa-304">For Germany:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-304">For Germany:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="6c0fa-305">For India:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-305">For India:</span></span>
  
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="6c0fa-306">When you run this command, replace *contosokey* with the same value you specified in **Step 3.3: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-306">When you run this command, replace *contosokey* with the same value you specified in **Step 3.3: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="6c0fa-307">You are asked to plug in your security world admin cards.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-307">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="6c0fa-308">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-308">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

### <a name="step-42-inspect-the-new-copy-of-the-key"></a><span data-ttu-id="6c0fa-309">Step 4.2: Inspect the new copy of the key</span><span class="sxs-lookup"><span data-stu-id="6c0fa-309">Step 4.2: Inspect the new copy of the key</span></span>
<span data-ttu-id="6c0fa-310">Optionally, run the Thales utilities to confirm the minimal permissions on the new key:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-310">Optionally, run the Thales utilities to confirm the minimal permissions on the new key:</span></span>

* <span data-ttu-id="6c0fa-311">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-311">aclprint.py:</span></span>
  
        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="6c0fa-312">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-312">kmfile-dump.exe:</span></span>
  
        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="6c0fa-313">When you run these commands, replace contosokey with the same value you specified in **Step 3.3: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-313">When you run these commands, replace contosokey with the same value you specified in **Step 3.3: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-43-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="6c0fa-314">Step 4.3: Encrypt your key by using Microsoft’s Key Exchange Key</span><span class="sxs-lookup"><span data-stu-id="6c0fa-314">Step 4.3: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="6c0fa-315">Run one of the following commands, depending on your geographic region or instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-315">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="6c0fa-316">For North America:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-316">For North America:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-317">For Europe:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-317">For Europe:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-318">For Asia:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-318">For Asia:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-319">For Latin America:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-319">For Latin America:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-320">For Japan:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-320">For Japan:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-321">For Australia:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-321">For Australia:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-322">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-322">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-323">For Canada:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-323">For Canada:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-324">For Germany:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-324">For Germany:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="6c0fa-325">For India:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-325">For India:</span></span>
  
        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="6c0fa-326">When you run this command, use these instructions:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-326">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="6c0fa-327">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.3: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-327">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.3: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="6c0fa-328">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-328">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="6c0fa-329">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-329">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="6c0fa-330">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-330">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="6c0fa-331">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: TransferPackage-*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="6c0fa-331">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: TransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-44-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="6c0fa-332">Step 4.4: Copy your key transfer package to the Internet-connected workstation</span><span class="sxs-lookup"><span data-stu-id="6c0fa-332">Step 4.4: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="6c0fa-333">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-333">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="6c0fa-334">Step 5: Transfer your key to Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6c0fa-334">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="6c0fa-335">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](https://msdn.microsoft.com/library/azure/dn868048\(v=azure.300\).aspx) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span><span class="sxs-lookup"><span data-stu-id="6c0fa-335">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](https://msdn.microsoft.com/library/azure/dn868048\(v=azure.300\).aspx) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\TransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="6c0fa-336">If the upload is successful, you see displayed the properties of the key that you just added.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-336">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c0fa-337">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c0fa-337">Next steps</span></span>
<span data-ttu-id="6c0fa-338">You can now use this HSM-protected key in your key vault.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-338">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="6c0fa-339">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="6c0fa-339">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>

