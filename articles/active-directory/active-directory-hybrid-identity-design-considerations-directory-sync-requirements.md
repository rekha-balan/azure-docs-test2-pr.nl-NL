---
title: Azure Active Directory hybrid identity design considerations - determine directory synchronization requirements | Microsoft Docs
description: Identify what requirements are needed for synchronizing all the users between on=premises and cloud for the enterprise.
documentationcenter: ''
services: active-directory
author: billmath
manager: femila
editor: ''
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: e50a308a897878d0985f2a8f1baa044e5c82335f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550554"
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="0cfb9-103">Determine directory synchronization requirements</span><span class="sxs-lookup"><span data-stu-id="0cfb9-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="0cfb9-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="0cfb9-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="0cfb9-106">This identity will need to be maintained and updated periodically.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="0cfb9-107">The updates can take many forms, from title changes to password changes.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="0cfb9-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="0cfb9-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="0cfb9-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="0cfb9-111">Make sure to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="0cfb9-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="0cfb9-112">Do you have one AD forest, multiple, or none?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="0cfb9-113">How many Azure AD directories will you be synchronizing to?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="0cfb9-114">Are you using filtering?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="0cfb9-115">Do you have multiple Azure AD Connect servers planned?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="0cfb9-116">Do you currently have a synchronization tool on-premises?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="0cfb9-117">If yes, does your users if users have a virtual directory/integration of identities?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="0cfb9-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="0cfb9-119">Are you going to be doing any GALSync?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="0cfb9-120">What is the current state of UPNs in your organization?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="0cfb9-121">Do you have a different directory that users authenticate against?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="0cfb9-122">Does your company use Microsoft Exchange?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="0cfb9-123">Do they plan of having a hybrid exchange deployment?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="0cfb9-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="0cfb9-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="0cfb9-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="0cfb9-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="0cfb9-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="0cfb9-129">Make sure to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="0cfb9-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="0cfb9-130">Will these applications be moved to the cloud and use the directory?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="0cfb9-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="0cfb9-132">Will these applications need to be re-written to take advantage of cloud auth?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="0cfb9-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="0cfb9-134">You also need to determine the security requirements and constraints directory synchronization.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="0cfb9-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="0cfb9-136">Make sure to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="0cfb9-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="0cfb9-137">Where will the synchronization server be located?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="0cfb9-138">Will it be domain joined?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-138">Will it be domain joined?</span></span>
* <span data-ttu-id="0cfb9-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="0cfb9-140">Will you be able to open the required firewall ports to support synchronization?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="0cfb9-141">Do you have a disaster recovery plan for the synchronization server?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="0cfb9-142">Do you have an account with the correct permissions for all forests you want to synch with?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="0cfb9-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="0cfb9-144">If you have mutli-forest sync is the sync server able to get to each forest?</span><span class="sxs-lookup"><span data-stu-id="0cfb9-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="0cfb9-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="0cfb9-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="0cfb9-147">By having answered those questions you will select which option best suits your business needs.</span><span class="sxs-lookup"><span data-stu-id="0cfb9-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0cfb9-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="0cfb9-148">Next steps</span></span>
[<span data-ttu-id="0cfb9-149">Determine multi-factor authentication requirements</span><span class="sxs-lookup"><span data-stu-id="0cfb9-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="0cfb9-150">See also</span><span class="sxs-lookup"><span data-stu-id="0cfb9-150">See also</span></span>
[<span data-ttu-id="0cfb9-151">Design considerations overview</span><span class="sxs-lookup"><span data-stu-id="0cfb9-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

