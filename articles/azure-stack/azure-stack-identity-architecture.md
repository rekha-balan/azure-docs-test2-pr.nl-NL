---
title: Identity architecture for Azure Stack | Microsoft Docs
description: Learn about the identity architecture you can use with Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/01/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: bf69c71a8b361e4a147263bc60324573c710818f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965797"
---
# <a name="identity-architecture-for-azure-stack"></a><span data-ttu-id="5c889-103">Identity architecture for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5c889-103">Identity architecture for Azure Stack</span></span>
<span data-ttu-id="5c889-104">Before you choose an identity provider to use with Azure Stack, understand the important differences between the options of Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="5c889-104">Before you choose an identity provider to use with Azure Stack, understand the important differences between the options of Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS).</span></span> 

## <a name="capabilities-and-limitations"></a><span data-ttu-id="5c889-105">Capabilities and limitations</span><span class="sxs-lookup"><span data-stu-id="5c889-105">Capabilities and limitations</span></span> 
<span data-ttu-id="5c889-106">The identity provider that you choose can limit your options, including support for multi-tenancy.</span><span class="sxs-lookup"><span data-stu-id="5c889-106">The identity provider that you choose can limit your options, including support for multi-tenancy.</span></span> 

  

|<span data-ttu-id="5c889-107">Capability or scenario</span><span class="sxs-lookup"><span data-stu-id="5c889-107">Capability or scenario</span></span>        |<span data-ttu-id="5c889-108">Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c889-108">Azure AD</span></span>  |<span data-ttu-id="5c889-109">AD FS</span><span class="sxs-lookup"><span data-stu-id="5c889-109">AD FS</span></span>  |
|------------------------------|----------|-------|
|<span data-ttu-id="5c889-110">Connected to the internet</span><span class="sxs-lookup"><span data-stu-id="5c889-110">Connected to the internet</span></span>     |<span data-ttu-id="5c889-111">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-111">Yes</span></span>       |<span data-ttu-id="5c889-112">Optional</span><span class="sxs-lookup"><span data-stu-id="5c889-112">Optional</span></span>|
|<span data-ttu-id="5c889-113">Support for multi-tenancy</span><span class="sxs-lookup"><span data-stu-id="5c889-113">Support for multi-tenancy</span></span>     |<span data-ttu-id="5c889-114">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-114">Yes</span></span>       |<span data-ttu-id="5c889-115">No</span><span class="sxs-lookup"><span data-stu-id="5c889-115">No</span></span>      |
|<span data-ttu-id="5c889-116">Offer items in the Marketplace</span><span class="sxs-lookup"><span data-stu-id="5c889-116">Offer items in the Marketplace</span></span> |<span data-ttu-id="5c889-117">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-117">Yes</span></span>       |<span data-ttu-id="5c889-118">Yes.</span><span class="sxs-lookup"><span data-stu-id="5c889-118">Yes.</span></span> <span data-ttu-id="5c889-119">Requires use of the [offline Marketplace Syndication](azure-stack-download-azure-marketplace-item.md#disconnected-or-a-partially-connected-scenario) tool.</span><span class="sxs-lookup"><span data-stu-id="5c889-119">Requires use of the [offline Marketplace Syndication](azure-stack-download-azure-marketplace-item.md#disconnected-or-a-partially-connected-scenario) tool.</span></span>|
|<span data-ttu-id="5c889-120">Support for Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="5c889-120">Support for Active Directory Authentication Library (ADAL)</span></span> |<span data-ttu-id="5c889-121">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-121">Yes</span></span> |<span data-ttu-id="5c889-122">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-122">Yes</span></span>|
|<span data-ttu-id="5c889-123">Support for tools such as Azure CLI, Visual Studio, and PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c889-123">Support for tools such as Azure CLI, Visual Studio, and PowerShell</span></span>  |<span data-ttu-id="5c889-124">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-124">Yes</span></span> |<span data-ttu-id="5c889-125">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-125">Yes</span></span>|
|<span data-ttu-id="5c889-126">Create service principals through the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5c889-126">Create service principals through the Azure portal</span></span>     |<span data-ttu-id="5c889-127">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-127">Yes</span></span> |<span data-ttu-id="5c889-128">No</span><span class="sxs-lookup"><span data-stu-id="5c889-128">No</span></span>|
|<span data-ttu-id="5c889-129">Create service principals with certificates</span><span class="sxs-lookup"><span data-stu-id="5c889-129">Create service principals with certificates</span></span>      |<span data-ttu-id="5c889-130">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-130">Yes</span></span> |<span data-ttu-id="5c889-131">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-131">Yes</span></span>|
|<span data-ttu-id="5c889-132">Create service principals with secrets (keys)</span><span class="sxs-lookup"><span data-stu-id="5c889-132">Create service principals with secrets (keys)</span></span>    |<span data-ttu-id="5c889-133">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-133">Yes</span></span> |<span data-ttu-id="5c889-134">No</span><span class="sxs-lookup"><span data-stu-id="5c889-134">No</span></span>|
|<span data-ttu-id="5c889-135">Applications can use the Graph service</span><span class="sxs-lookup"><span data-stu-id="5c889-135">Applications can use the Graph service</span></span>           |<span data-ttu-id="5c889-136">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-136">Yes</span></span> |<span data-ttu-id="5c889-137">No</span><span class="sxs-lookup"><span data-stu-id="5c889-137">No</span></span>|
|<span data-ttu-id="5c889-138">Applications can use identity provider for sign-in</span><span class="sxs-lookup"><span data-stu-id="5c889-138">Applications can use identity provider for sign-in</span></span> |<span data-ttu-id="5c889-139">Yes</span><span class="sxs-lookup"><span data-stu-id="5c889-139">Yes</span></span> |<span data-ttu-id="5c889-140">Yes.</span><span class="sxs-lookup"><span data-stu-id="5c889-140">Yes.</span></span> <span data-ttu-id="5c889-141">Requires applications to federate with on-premises AD FS instances.</span><span class="sxs-lookup"><span data-stu-id="5c889-141">Requires applications to federate with on-premises AD FS instances.</span></span> |

## <a name="topologies"></a><span data-ttu-id="5c889-142">Topologies</span><span class="sxs-lookup"><span data-stu-id="5c889-142">Topologies</span></span>
<span data-ttu-id="5c889-143">The following sections discus the various identity topologies that you can use.</span><span class="sxs-lookup"><span data-stu-id="5c889-143">The following sections discus the various identity topologies that you can use.</span></span>

### <a name="azure-ad-single-tenant-topology"></a><span data-ttu-id="5c889-144">Azure AD: single-tenant topology</span><span class="sxs-lookup"><span data-stu-id="5c889-144">Azure AD: single-tenant topology</span></span> 
<span data-ttu-id="5c889-145">By default, when you install Azure Stack and use Azure AD, Azure Stack uses a single-tenant topology.</span><span class="sxs-lookup"><span data-stu-id="5c889-145">By default, when you install Azure Stack and use Azure AD, Azure Stack uses a single-tenant topology.</span></span> 

<span data-ttu-id="5c889-146">A single-tenant topology is useful when:</span><span class="sxs-lookup"><span data-stu-id="5c889-146">A single-tenant topology is useful when:</span></span>
- <span data-ttu-id="5c889-147">All users are part of the same tenant.</span><span class="sxs-lookup"><span data-stu-id="5c889-147">All users are part of the same tenant.</span></span>
- <span data-ttu-id="5c889-148">A service provider hosts an Azure Stack instance for an organization.</span><span class="sxs-lookup"><span data-stu-id="5c889-148">A service provider hosts an Azure Stack instance for an organization.</span></span> 

![Azure Stack single-tenant topology with Azure AD](media/azure-stack-identity-architecture/single-tenant.png)

<span data-ttu-id="5c889-150">This topology features the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="5c889-150">This topology features the following characteristics:</span></span>
- <span data-ttu-id="5c889-151">Azure Stack registers all applications and services to the same Azure AD tenant directory.</span><span class="sxs-lookup"><span data-stu-id="5c889-151">Azure Stack registers all applications and services to the same Azure AD tenant directory.</span></span> 
- <span data-ttu-id="5c889-152">Azure Stack authenticates only the users and applications from that directory, including tokens.</span><span class="sxs-lookup"><span data-stu-id="5c889-152">Azure Stack authenticates only the users and applications from that directory, including tokens.</span></span> 
- <span data-ttu-id="5c889-153">Identities for administrators (cloud operators) and tenant users are in the same directory tenant.</span><span class="sxs-lookup"><span data-stu-id="5c889-153">Identities for administrators (cloud operators) and tenant users are in the same directory tenant.</span></span> 
- <span data-ttu-id="5c889-154">To enable a user from another directory to access this Azure Stack environment, you must [invite the user as a guest](azure-stack-identity-overview.md#guest-users) to the tenant directory.</span><span class="sxs-lookup"><span data-stu-id="5c889-154">To enable a user from another directory to access this Azure Stack environment, you must [invite the user as a guest](azure-stack-identity-overview.md#guest-users) to the tenant directory.</span></span> 

### <a name="azure-ad-multi-tenant-topology"></a><span data-ttu-id="5c889-155">Azure AD: multi-tenant topology</span><span class="sxs-lookup"><span data-stu-id="5c889-155">Azure AD: multi-tenant topology</span></span>
<span data-ttu-id="5c889-156">Cloud operators can configure Azure Stack to allow access to applications by tenants from one or more organizations.</span><span class="sxs-lookup"><span data-stu-id="5c889-156">Cloud operators can configure Azure Stack to allow access to applications by tenants from one or more organizations.</span></span> <span data-ttu-id="5c889-157">Users access applications through the user portal.</span><span class="sxs-lookup"><span data-stu-id="5c889-157">Users access applications through the user portal.</span></span> <span data-ttu-id="5c889-158">In this configuration, the Admin portal (used by the cloud operator) is limited to users from a single directory.</span><span class="sxs-lookup"><span data-stu-id="5c889-158">In this configuration, the Admin portal (used by the cloud operator) is limited to users from a single directory.</span></span> 

<span data-ttu-id="5c889-159">A multi-tenant topology is useful when:</span><span class="sxs-lookup"><span data-stu-id="5c889-159">A multi-tenant topology is useful when:</span></span>
- <span data-ttu-id="5c889-160">A service provider wants to allow users from multiple organizations to access Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5c889-160">A service provider wants to allow users from multiple organizations to access Azure Stack.</span></span>

![Azure Stack multi-tenant topology with Azure AD](media/azure-stack-identity-architecture/multi-tenant.png)

<span data-ttu-id="5c889-162">This topology features the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="5c889-162">This topology features the following characteristics:</span></span>
- <span data-ttu-id="5c889-163">Access to resources should be on a per-organization basis.</span><span class="sxs-lookup"><span data-stu-id="5c889-163">Access to resources should be on a per-organization basis.</span></span> 
- <span data-ttu-id="5c889-164">Users from one organization should be unable to grant access to resources to users who are outside their organization.</span><span class="sxs-lookup"><span data-stu-id="5c889-164">Users from one organization should be unable to grant access to resources to users who are outside their organization.</span></span> 
- <span data-ttu-id="5c889-165">Identities for administrators (cloud operators) can be in a separate directory tenant from the identities for users.</span><span class="sxs-lookup"><span data-stu-id="5c889-165">Identities for administrators (cloud operators) can be in a separate directory tenant from the identities for users.</span></span> <span data-ttu-id="5c889-166">This separation provides account isolation at the identity provider level.</span><span class="sxs-lookup"><span data-stu-id="5c889-166">This separation provides account isolation at the identity provider level.</span></span> 
 
### <a name="ad-fs"></a><span data-ttu-id="5c889-167">AD FS</span><span class="sxs-lookup"><span data-stu-id="5c889-167">AD FS</span></span>  
<span data-ttu-id="5c889-168">The AD FS topology is required when either of the following conditions is true:</span><span class="sxs-lookup"><span data-stu-id="5c889-168">The AD FS topology is required when either of the following conditions is true:</span></span>
- <span data-ttu-id="5c889-169">Azure Stack does not connect to the internet.</span><span class="sxs-lookup"><span data-stu-id="5c889-169">Azure Stack does not connect to the internet.</span></span>
- <span data-ttu-id="5c889-170">Azure Stack can connect to the internet, but you choose to use AD FS for your identity provider.</span><span class="sxs-lookup"><span data-stu-id="5c889-170">Azure Stack can connect to the internet, but you choose to use AD FS for your identity provider.</span></span>
  
![Azure Stack topology using AD FS](media/azure-stack-identity-architecture/adfs.png)

<span data-ttu-id="5c889-172">This topology features the following characteristics:</span><span class="sxs-lookup"><span data-stu-id="5c889-172">This topology features the following characteristics:</span></span>
- <span data-ttu-id="5c889-173">To support the use of this topology in production, you must integrate the built-in Azure Stack AD FS instance with an existing AD FS instance that's backed by Active Directory, through a federation trust.</span><span class="sxs-lookup"><span data-stu-id="5c889-173">To support the use of this topology in production, you must integrate the built-in Azure Stack AD FS instance with an existing AD FS instance that's backed by Active Directory, through a federation trust.</span></span> 
- <span data-ttu-id="5c889-174">You can integrate the Graph service in Azure Stack with your existing Active Directory instance.</span><span class="sxs-lookup"><span data-stu-id="5c889-174">You can integrate the Graph service in Azure Stack with your existing Active Directory instance.</span></span> <span data-ttu-id="5c889-175">You can also use the OData-based Graph API service that supports APIs that are consistent with the Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="5c889-175">You can also use the OData-based Graph API service that supports APIs that are consistent with the Azure AD Graph API.</span></span> 

  <span data-ttu-id="5c889-176">To interact with your Active Directory instance, the Graph API requires user credentials from your Active Directory instance that have read-only permissions.</span><span class="sxs-lookup"><span data-stu-id="5c889-176">To interact with your Active Directory instance, the Graph API requires user credentials from your Active Directory instance that have read-only permissions.</span></span> 
  - <span data-ttu-id="5c889-177">The built-in AD FS instance is based on Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="5c889-177">The built-in AD FS instance is based on Windows Server 2016.</span></span> 
  - <span data-ttu-id="5c889-178">Your AD FS and Active Directory instances must be based on Windows Server 2012 or later.</span><span class="sxs-lookup"><span data-stu-id="5c889-178">Your AD FS and Active Directory instances must be based on Windows Server 2012 or later.</span></span> 
  
  <span data-ttu-id="5c889-179">Between your Active Directory instance and the built-in AD FS instance, interactions aren't restricted to OpenID Connect, and they can use any mutually supported protocol.</span><span class="sxs-lookup"><span data-stu-id="5c889-179">Between your Active Directory instance and the built-in AD FS instance, interactions aren't restricted to OpenID Connect, and they can use any mutually supported protocol.</span></span> 
  - <span data-ttu-id="5c889-180">User accounts are created and managed in your on-premises Active Directory instance.</span><span class="sxs-lookup"><span data-stu-id="5c889-180">User accounts are created and managed in your on-premises Active Directory instance.</span></span>
  - <span data-ttu-id="5c889-181">Service principals and registrations for applications are managed in the built-in Active Directory instance.</span><span class="sxs-lookup"><span data-stu-id="5c889-181">Service principals and registrations for applications are managed in the built-in Active Directory instance.</span></span>



## <a name="next-steps"></a><span data-ttu-id="5c889-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c889-182">Next steps</span></span>
- [<span data-ttu-id="5c889-183">Identity overview</span><span class="sxs-lookup"><span data-stu-id="5c889-183">Identity overview</span></span>](azure-stack-identity-overview.md)   
- [<span data-ttu-id="5c889-184">Datacenter integration - identity</span><span class="sxs-lookup"><span data-stu-id="5c889-184">Datacenter integration - identity</span></span>](azure-stack-integrate-identity.md)
