---
title: Azure Stack Key Vault introduction | Microsoft Docs
description: Learn how Azure Stack Key Vault manages keys and secrets
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/15/2018
ms.author: sethm
ms.openlocfilehash: a6b4e8c3543d4681c92fbbde30eec0a543fcb0fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866910"
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="31563-103">Introduction to Key Vault in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="31563-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31563-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31563-104">Prerequisites</span></span> 

* <span data-ttu-id="31563-105">You must subscribe to an offer that includes the Azure Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="31563-105">You must subscribe to an offer that includes the Azure Key Vault service.</span></span>  
* <span data-ttu-id="31563-106">[PowerShell is configured for use with Azure Stack](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="31563-106">[PowerShell is configured for use with Azure Stack](azure-stack-powershell-configure-user.md).</span></span>
 
## <a name="key-vault-basics"></a><span data-ttu-id="31563-107">Key Vault basics</span><span class="sxs-lookup"><span data-stu-id="31563-107">Key Vault basics</span></span>
<span data-ttu-id="31563-108">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span><span class="sxs-lookup"><span data-stu-id="31563-108">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="31563-109">By using Key Vault, you can encrypt keys and secrets, such as:</span><span class="sxs-lookup"><span data-stu-id="31563-109">By using Key Vault, you can encrypt keys and secrets, such as:</span></span>
   * <span data-ttu-id="31563-110">Authentication keys</span><span class="sxs-lookup"><span data-stu-id="31563-110">Authentication keys</span></span> 
   * <span data-ttu-id="31563-111">Storage account keys</span><span class="sxs-lookup"><span data-stu-id="31563-111">Storage account keys</span></span>
   * <span data-ttu-id="31563-112">Data encryption keys</span><span class="sxs-lookup"><span data-stu-id="31563-112">Data encryption keys</span></span>
   * <span data-ttu-id="31563-113">.pfx files</span><span class="sxs-lookup"><span data-stu-id="31563-113">.pfx files</span></span>
   * <span data-ttu-id="31563-114">Passwords</span><span class="sxs-lookup"><span data-stu-id="31563-114">Passwords</span></span>

<span data-ttu-id="31563-115">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span><span class="sxs-lookup"><span data-stu-id="31563-115">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="31563-116">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span><span class="sxs-lookup"><span data-stu-id="31563-116">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="31563-117">Security administrators can grant (and revoke) permission to keys, as needed.</span><span class="sxs-lookup"><span data-stu-id="31563-117">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="31563-118">Anybody with an Azure Stack subscription can create and use key vaults.</span><span class="sxs-lookup"><span data-stu-id="31563-118">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="31563-119">Although Key Vault benefits developers and security administrators, the operator who manages other Azure Stack services for an organization can implement and manage it.</span><span class="sxs-lookup"><span data-stu-id="31563-119">Although Key Vault benefits developers and security administrators, the operator who manages other Azure Stack services for an organization can implement and manage it.</span></span> <span data-ttu-id="31563-120">For example, the Azure Stack operator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span><span class="sxs-lookup"><span data-stu-id="31563-120">For example, the Azure Stack operator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="31563-121">Create or import a key or secret.</span><span class="sxs-lookup"><span data-stu-id="31563-121">Create or import a key or secret.</span></span>
* <span data-ttu-id="31563-122">Revoke or delete a key or secret.</span><span class="sxs-lookup"><span data-stu-id="31563-122">Revoke or delete a key or secret.</span></span>
* <span data-ttu-id="31563-123">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="31563-123">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets.</span></span>
* <span data-ttu-id="31563-124">Configure key usage (for example, sign or encrypt).</span><span class="sxs-lookup"><span data-stu-id="31563-124">Configure key usage (for example, sign or encrypt).</span></span>

<span data-ttu-id="31563-125">The operator can then provide developers with Uniform Resource Identifiers (URIs) to call from their applications.</span><span class="sxs-lookup"><span data-stu-id="31563-125">The operator can then provide developers with Uniform Resource Identifiers (URIs) to call from their applications.</span></span> <span data-ttu-id="31563-126">Operators can also provide security administrators with key-usage logging information.</span><span class="sxs-lookup"><span data-stu-id="31563-126">Operators can also provide security administrators with key-usage logging information.</span></span>

<span data-ttu-id="31563-127">Developers can also manage the keys directly, by using APIs.</span><span class="sxs-lookup"><span data-stu-id="31563-127">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="31563-128">For more information, see the Key Vault developer's guide.</span><span class="sxs-lookup"><span data-stu-id="31563-128">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="31563-129">Scenarios</span><span class="sxs-lookup"><span data-stu-id="31563-129">Scenarios</span></span>
<span data-ttu-id="31563-130">The following scenarios describe how Key Vault can help meet the needs of developers and security administrators.</span><span class="sxs-lookup"><span data-stu-id="31563-130">The following scenarios describe how Key Vault can help meet the needs of developers and security administrators.</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="31563-131">Developer for an Azure Stack application</span><span class="sxs-lookup"><span data-stu-id="31563-131">Developer for an Azure Stack application</span></span>
<span data-ttu-id="31563-132">**Problem:** I want to write an application for Azure Stack that uses keys for signing and encryption.</span><span class="sxs-lookup"><span data-stu-id="31563-132">**Problem:** I want to write an application for Azure Stack that uses keys for signing and encryption.</span></span> <span data-ttu-id="31563-133">I want these keys to be external from my application, so that the solution is suitable for an application that is geographically distributed.</span><span class="sxs-lookup"><span data-stu-id="31563-133">I want these keys to be external from my application, so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="31563-134">**Statement:** Keys are stored in a vault and invoked by a URI, when needed.</span><span class="sxs-lookup"><span data-stu-id="31563-134">**Statement:** Keys are stored in a vault and invoked by a URI, when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="31563-135">Developer for software as a service (SaaS)</span><span class="sxs-lookup"><span data-stu-id="31563-135">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="31563-136">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="31563-136">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span> <span data-ttu-id="31563-137">I want customers to own and manage their keys, so that I can concentrate on doing what I do best, which is providing the core software features.</span><span class="sxs-lookup"><span data-stu-id="31563-137">I want customers to own and manage their keys, so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

<span data-ttu-id="31563-138">**Statement:** Customers can import their own keys into Azure Stack, and then manage them.</span><span class="sxs-lookup"><span data-stu-id="31563-138">**Statement:** Customers can import their own keys into Azure Stack, and then manage them.</span></span> 

### <a name="chief-security-officer-cso"></a><span data-ttu-id="31563-139">Chief Security Officer (CSO)</span><span class="sxs-lookup"><span data-stu-id="31563-139">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="31563-140">**Problem:** I want to make sure that my organization is in control of the key lifecycle and can monitor key usage.</span><span class="sxs-lookup"><span data-stu-id="31563-140">**Problem:** I want to make sure that my organization is in control of the key lifecycle and can monitor key usage.</span></span>

<span data-ttu-id="31563-141">**Statement:** Key Vault is designed so that Microsoft does not see or extract your keys.</span><span class="sxs-lookup"><span data-stu-id="31563-141">**Statement:** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span> <span data-ttu-id="31563-142">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault uses the keys on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="31563-142">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault uses the keys on behalf of the application.</span></span> <span data-ttu-id="31563-143">The application does not see the customers’ keys.</span><span class="sxs-lookup"><span data-stu-id="31563-143">The application does not see the customers’ keys.</span></span> <span data-ttu-id="31563-144">Although we use multiple Azure Stack services and resources, you can manage the keys from a single location in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="31563-144">Although we use multiple Azure Stack services and resources, you can manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="31563-145">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span><span class="sxs-lookup"><span data-stu-id="31563-145">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31563-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="31563-146">Next steps</span></span>

* [<span data-ttu-id="31563-147">Manage Key Vault in Azure Stack by using the portal</span><span class="sxs-lookup"><span data-stu-id="31563-147">Manage Key Vault in Azure Stack by using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="31563-148">Manage Key Vault in Azure Stack by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="31563-148">Manage Key Vault in Azure Stack by using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)

