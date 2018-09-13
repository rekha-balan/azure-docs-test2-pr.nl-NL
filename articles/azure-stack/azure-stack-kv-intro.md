---
title: Azure Stack Key Vault introduction | Microsoft Docs
description: Learn how Azure Stack Key Vault manages keys and secrets
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: 6587e1e1b0af7cb57075ed0ceb51addc81eb9ac4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551453"
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="97371-103">Introduction to Key Vault in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="97371-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="97371-104">Before you start</span><span class="sxs-lookup"><span data-stu-id="97371-104">Before you start</span></span>
<span data-ttu-id="97371-105">This article assumes the following:</span><span class="sxs-lookup"><span data-stu-id="97371-105">This article assumes the following:</span></span>

* <span data-ttu-id="97371-106">Azure Stack administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="97371-106">Azure Stack administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="97371-107">Tenants must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="97371-107">Tenants must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="97371-108">PowerShell is configured for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="97371-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure.md) 
 
> [!NOTE]
> <span data-ttu-id="97371-109">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span><span class="sxs-lookup"><span data-stu-id="97371-109">In Technical Preview 3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span></span> <span data-ttu-id="97371-110">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span><span class="sxs-lookup"><span data-stu-id="97371-110">If you are an administrator, sign in to the user portal to access and perform operations on a key vault.</span></span>
 
## <a name="key-vault-basics"></a><span data-ttu-id="97371-111">Key Vault basics</span><span class="sxs-lookup"><span data-stu-id="97371-111">Key Vault basics</span></span>
<span data-ttu-id="97371-112">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span><span class="sxs-lookup"><span data-stu-id="97371-112">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="97371-113">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span><span class="sxs-lookup"><span data-stu-id="97371-113">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="97371-114">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span><span class="sxs-lookup"><span data-stu-id="97371-114">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="97371-115">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span><span class="sxs-lookup"><span data-stu-id="97371-115">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="97371-116">Security administrators can grant (and revoke) permission to keys, as needed.</span><span class="sxs-lookup"><span data-stu-id="97371-116">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="97371-117">Anybody with an Azure Stack subscription can create and use key vaults.</span><span class="sxs-lookup"><span data-stu-id="97371-117">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="97371-118">Although Key Vault benefits developers and security administrators, it can be implemented and managed by an administrator who manages other Azure Stack services for an organization.</span><span class="sxs-lookup"><span data-stu-id="97371-118">Although Key Vault benefits developers and security administrators, it can be implemented and managed by an administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="97371-119">For example, this administrator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span><span class="sxs-lookup"><span data-stu-id="97371-119">For example, this administrator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="97371-120">Create or import a key or secret</span><span class="sxs-lookup"><span data-stu-id="97371-120">Create or import a key or secret</span></span>
* <span data-ttu-id="97371-121">Revoke or delete a key or secret</span><span class="sxs-lookup"><span data-stu-id="97371-121">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="97371-122">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span><span class="sxs-lookup"><span data-stu-id="97371-122">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="97371-123">Configure key usage (for example, sign or encrypt)</span><span class="sxs-lookup"><span data-stu-id="97371-123">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="97371-124">This administrator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span><span class="sxs-lookup"><span data-stu-id="97371-124">This administrator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="97371-125">Developers can also manage the keys directly, by using APIs.</span><span class="sxs-lookup"><span data-stu-id="97371-125">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="97371-126">For more information, see the Key Vault developer's guide.</span><span class="sxs-lookup"><span data-stu-id="97371-126">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="97371-127">Scenarios</span><span class="sxs-lookup"><span data-stu-id="97371-127">Scenarios</span></span>
<span data-ttu-id="97371-128">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span><span class="sxs-lookup"><span data-stu-id="97371-128">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="97371-129">Developer for an Azure Stack application</span><span class="sxs-lookup"><span data-stu-id="97371-129">Developer for an Azure Stack application</span></span>
<span data-ttu-id="97371-130">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span><span class="sxs-lookup"><span data-stu-id="97371-130">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="97371-131">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span><span class="sxs-lookup"><span data-stu-id="97371-131">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="97371-132">Developer for software as a service (SaaS)</span><span class="sxs-lookup"><span data-stu-id="97371-132">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="97371-133">**Problem:** I don’t want the responsibility or potential liability for my customers’ tenant keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="97371-133">**Problem:** I don’t want the responsibility or potential liability for my customers’ tenant keys and secrets.</span></span>

<span data-ttu-id="97371-134">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span><span class="sxs-lookup"><span data-stu-id="97371-134">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="97371-135">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span><span class="sxs-lookup"><span data-stu-id="97371-135">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="97371-136">Chief Security Officer (CSO)</span><span class="sxs-lookup"><span data-stu-id="97371-136">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="97371-137">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span><span class="sxs-lookup"><span data-stu-id="97371-137">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="97371-138">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span><span class="sxs-lookup"><span data-stu-id="97371-138">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="97371-139">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="97371-139">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="97371-140">The application does not see the customers’ keys.</span><span class="sxs-lookup"><span data-stu-id="97371-140">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="97371-141">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="97371-141">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="97371-142">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span><span class="sxs-lookup"><span data-stu-id="97371-142">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97371-143">Next Steps</span><span class="sxs-lookup"><span data-stu-id="97371-143">Next Steps</span></span>
<span data-ttu-id="97371-144">[Manage Key Vault in Azure Stack using the portal](azure-stack-kv-manage-portal.md)
[Manage Key Vault in Azure Stack using PowerShell](azure-stack-kv-manage-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="97371-144">[Manage Key Vault in Azure Stack using the portal](azure-stack-kv-manage-portal.md)
[Manage Key Vault in Azure Stack using PowerShell](azure-stack-kv-manage-powershell.md)</span></span>
