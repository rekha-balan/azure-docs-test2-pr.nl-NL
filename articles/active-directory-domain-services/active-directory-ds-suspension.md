---
title: 'Azure Active Directory Domain Services: Suspended domains | Microsoft Docs'
description: Managed domain suspension and deletion
services: active-directory-ds
documentationcenter: ''
author: eringreenlee
manager: mtillman
editor: curtand
ms.assetid: 95e1d8da-60c7-4fc1-987d-f48fde56a8cb
ms.service: active-directory
ms.component: domains
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/18/2018
ms.author: ergreenl
ms.openlocfilehash: 72e22fbe61b4e30191bbac553709241e1b13f1f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870764"
---
# <a name="suspended-domains"></a><span data-ttu-id="f1628-103">Suspended domains</span><span class="sxs-lookup"><span data-stu-id="f1628-103">Suspended domains</span></span>
<span data-ttu-id="f1628-104">When Azure Active Directory Domain Services (Azure AD DS) is unable to service a managed domain for a long period of time, it puts the managed domain into a suspended state.</span><span class="sxs-lookup"><span data-stu-id="f1628-104">When Azure Active Directory Domain Services (Azure AD DS) is unable to service a managed domain for a long period of time, it puts the managed domain into a suspended state.</span></span> <span data-ttu-id="f1628-105">This article explains why managed domains are suspended, and how to remediate a suspended domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-105">This article explains why managed domains are suspended, and how to remediate a suspended domain.</span></span>


## <a name="states-your-managed-domain-can-be-in"></a><span data-ttu-id="f1628-106">States your managed domain can be in</span><span class="sxs-lookup"><span data-stu-id="f1628-106">States your managed domain can be in</span></span>

![Suspended domain timeline](media\active-directory-domain-services-suspension\suspension-timeline.PNG)

<span data-ttu-id="f1628-108">The preceding graphic outlines the possible states an Azure AD DS managed domain can be in.</span><span class="sxs-lookup"><span data-stu-id="f1628-108">The preceding graphic outlines the possible states an Azure AD DS managed domain can be in.</span></span>

### <a name="running-state"></a><span data-ttu-id="f1628-109">"Running" state</span><span class="sxs-lookup"><span data-stu-id="f1628-109">"Running" state</span></span>
<span data-ttu-id="f1628-110">A managed domain that is configured correctly and operating regularly is in the **Running** state.</span><span class="sxs-lookup"><span data-stu-id="f1628-110">A managed domain that is configured correctly and operating regularly is in the **Running** state.</span></span>

<span data-ttu-id="f1628-111">**What to expect**</span><span class="sxs-lookup"><span data-stu-id="f1628-111">**What to expect**</span></span>
* <span data-ttu-id="f1628-112">Microsoft can regularly monitor the health of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-112">Microsoft can regularly monitor the health of your managed domain.</span></span>
* <span data-ttu-id="f1628-113">Domain controllers for your managed domain are patched and updated regularly.</span><span class="sxs-lookup"><span data-stu-id="f1628-113">Domain controllers for your managed domain are patched and updated regularly.</span></span>
* <span data-ttu-id="f1628-114">Changes from Azure Active Directory are regularly synchronized to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-114">Changes from Azure Active Directory are regularly synchronized to your managed domain.</span></span>
* <span data-ttu-id="f1628-115">Regular backups are taken for your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-115">Regular backups are taken for your managed domain.</span></span>


### <a name="needs-attention-state"></a><span data-ttu-id="f1628-116">"Needs Attention" state</span><span class="sxs-lookup"><span data-stu-id="f1628-116">"Needs Attention" state</span></span>
<span data-ttu-id="f1628-117">A managed domain is in the **Needs Attention** state if one or more issues require an administrator to take action.</span><span class="sxs-lookup"><span data-stu-id="f1628-117">A managed domain is in the **Needs Attention** state if one or more issues require an administrator to take action.</span></span> <span data-ttu-id="f1628-118">The health page of your managed domain lists one or more alerts in this state.</span><span class="sxs-lookup"><span data-stu-id="f1628-118">The health page of your managed domain lists one or more alerts in this state.</span></span> 

<span data-ttu-id="f1628-119">For example, if you've configured a restrictive NSG for your virtual network, Microsoft might not be able to update and monitor your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-119">For example, if you've configured a restrictive NSG for your virtual network, Microsoft might not be able to update and monitor your managed domain.</span></span> <span data-ttu-id="f1628-120">This invalid configuration triggers an alert that puts your managed domain into the "Needs Attention" state.</span><span class="sxs-lookup"><span data-stu-id="f1628-120">This invalid configuration triggers an alert that puts your managed domain into the "Needs Attention" state.</span></span>

<span data-ttu-id="f1628-121">Each alert has a set of resolution steps.</span><span class="sxs-lookup"><span data-stu-id="f1628-121">Each alert has a set of resolution steps.</span></span> <span data-ttu-id="f1628-122">Some alerts are transient and get automatically resolved by the service.</span><span class="sxs-lookup"><span data-stu-id="f1628-122">Some alerts are transient and get automatically resolved by the service.</span></span> <span data-ttu-id="f1628-123">You can resolve some other alerts by following the instructions in the corresponding resolution steps for that alert.</span><span class="sxs-lookup"><span data-stu-id="f1628-123">You can resolve some other alerts by following the instructions in the corresponding resolution steps for that alert.</span></span> <span data-ttu-id="f1628-124">For some critical alerts, you need to contact Microsoft support to get a resolution.</span><span class="sxs-lookup"><span data-stu-id="f1628-124">For some critical alerts, you need to contact Microsoft support to get a resolution.</span></span>

<span data-ttu-id="f1628-125">For more information, see [How to troubleshoot alerts on a managed domain](active-directory-ds-troubleshoot-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f1628-125">For more information, see [How to troubleshoot alerts on a managed domain](active-directory-ds-troubleshoot-alerts.md).</span></span>

<span data-ttu-id="f1628-126">**What to expect**</span><span class="sxs-lookup"><span data-stu-id="f1628-126">**What to expect**</span></span>

<span data-ttu-id="f1628-127">In some cases (for example, if you have an invalid network configuration), the domain controllers for your managed domain might be unreachable.</span><span class="sxs-lookup"><span data-stu-id="f1628-127">In some cases (for example, if you have an invalid network configuration), the domain controllers for your managed domain might be unreachable.</span></span> <span data-ttu-id="f1628-128">When your managed domain is in the "Needs Attention" state, Microsoft can't guarantee that it will be monitored, patched, updated, or backed-up on a regular basis.</span><span class="sxs-lookup"><span data-stu-id="f1628-128">When your managed domain is in the "Needs Attention" state, Microsoft can't guarantee that it will be monitored, patched, updated, or backed-up on a regular basis.</span></span>

* <span data-ttu-id="f1628-129">Your managed domain is in an unhealthy state and ongoing health monitoring might stop until the alert is resolved.</span><span class="sxs-lookup"><span data-stu-id="f1628-129">Your managed domain is in an unhealthy state and ongoing health monitoring might stop until the alert is resolved.</span></span>
* <span data-ttu-id="f1628-130">Domain controllers for your managed domain can't be patched or updated.</span><span class="sxs-lookup"><span data-stu-id="f1628-130">Domain controllers for your managed domain can't be patched or updated.</span></span>
* <span data-ttu-id="f1628-131">Changes from Azure Active Directory might not be synchronized to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-131">Changes from Azure Active Directory might not be synchronized to your managed domain.</span></span>
* <span data-ttu-id="f1628-132">Backups for your managed domain might be taken, if possible.</span><span class="sxs-lookup"><span data-stu-id="f1628-132">Backups for your managed domain might be taken, if possible.</span></span>
* <span data-ttu-id="f1628-133">If you resolve alerts that are impacting your managed domain, you might be able to restore it to the "Running" state.</span><span class="sxs-lookup"><span data-stu-id="f1628-133">If you resolve alerts that are impacting your managed domain, you might be able to restore it to the "Running" state.</span></span>
* <span data-ttu-id="f1628-134">Critical alerts are triggered for configuration issues where Microsoft is unable to reach your domain controllers.</span><span class="sxs-lookup"><span data-stu-id="f1628-134">Critical alerts are triggered for configuration issues where Microsoft is unable to reach your domain controllers.</span></span> <span data-ttu-id="f1628-135">If such alerts aren't resolved within 15 days, your managed domain is put in the "Suspended" state.</span><span class="sxs-lookup"><span data-stu-id="f1628-135">If such alerts aren't resolved within 15 days, your managed domain is put in the "Suspended" state.</span></span>


### <a name="the-suspended-state"></a><span data-ttu-id="f1628-136">The "Suspended" state</span><span class="sxs-lookup"><span data-stu-id="f1628-136">The "Suspended" state</span></span>
<span data-ttu-id="f1628-137">A managed domain is put in the **Suspended** state for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="f1628-137">A managed domain is put in the **Suspended** state for the following reasons:</span></span>

* <span data-ttu-id="f1628-138">One or more critical alerts haven't been resolved in 15 days.</span><span class="sxs-lookup"><span data-stu-id="f1628-138">One or more critical alerts haven't been resolved in 15 days.</span></span> <span data-ttu-id="f1628-139">Critical alerts can be caused by a misconfiguration that blocks access to resources that are needed by Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="f1628-139">Critical alerts can be caused by a misconfiguration that blocks access to resources that are needed by Azure AD DS.</span></span>
    * <span data-ttu-id="f1628-140">For example, the alert [AADDS104: Network Error](active-directory-ds-troubleshoot-nsg.md) has been unresolved for more than 15 days in the managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-140">For example, the alert [AADDS104: Network Error](active-directory-ds-troubleshoot-nsg.md) has been unresolved for more than 15 days in the managed domain.</span></span>
* <span data-ttu-id="f1628-141">There's a billing issue with your Azure subscription or your Azure subscription has expired.</span><span class="sxs-lookup"><span data-stu-id="f1628-141">There's a billing issue with your Azure subscription or your Azure subscription has expired.</span></span>

<span data-ttu-id="f1628-142">Managed domains are suspended when Microsoft is unable to manage, monitor, patch, or back up the domain on an ongoing basis.</span><span class="sxs-lookup"><span data-stu-id="f1628-142">Managed domains are suspended when Microsoft is unable to manage, monitor, patch, or back up the domain on an ongoing basis.</span></span>

<span data-ttu-id="f1628-143">**What to expect**</span><span class="sxs-lookup"><span data-stu-id="f1628-143">**What to expect**</span></span>
* <span data-ttu-id="f1628-144">Domain controllers for your managed domain are de-provisioned and aren't reachable within the virtual network.</span><span class="sxs-lookup"><span data-stu-id="f1628-144">Domain controllers for your managed domain are de-provisioned and aren't reachable within the virtual network.</span></span>
* <span data-ttu-id="f1628-145">Secure LDAP access to the managed domain over the internet (if it's enabled) stops working.</span><span class="sxs-lookup"><span data-stu-id="f1628-145">Secure LDAP access to the managed domain over the internet (if it's enabled) stops working.</span></span>
* <span data-ttu-id="f1628-146">You notice failures in authenticating to the managed domain, logging on to domain-joined virtual machines, or connecting over LDAP/LDAPS.</span><span class="sxs-lookup"><span data-stu-id="f1628-146">You notice failures in authenticating to the managed domain, logging on to domain-joined virtual machines, or connecting over LDAP/LDAPS.</span></span>
* <span data-ttu-id="f1628-147">Backups for your managed domain are no longer taken.</span><span class="sxs-lookup"><span data-stu-id="f1628-147">Backups for your managed domain are no longer taken.</span></span>
* <span data-ttu-id="f1628-148">Synchronization with Azure AD stops.</span><span class="sxs-lookup"><span data-stu-id="f1628-148">Synchronization with Azure AD stops.</span></span>

<span data-ttu-id="f1628-149">After you resolve the alert, your managed domain goes into the "Suspended" state.</span><span class="sxs-lookup"><span data-stu-id="f1628-149">After you resolve the alert, your managed domain goes into the "Suspended" state.</span></span> <span data-ttu-id="f1628-150">Then you need to contact support.</span><span class="sxs-lookup"><span data-stu-id="f1628-150">Then you need to contact support.</span></span>
<span data-ttu-id="f1628-151">Support might restore your managed domain, but only if a backup that is less than 30 days old exists.</span><span class="sxs-lookup"><span data-stu-id="f1628-151">Support might restore your managed domain, but only if a backup that is less than 30 days old exists.</span></span>

<span data-ttu-id="f1628-152">The managed domain only stays in a suspended state for 15 days.</span><span class="sxs-lookup"><span data-stu-id="f1628-152">The managed domain only stays in a suspended state for 15 days.</span></span> <span data-ttu-id="f1628-153">To recover your managed domain, Microsoft recommends that you resolve critical alerts immediately.</span><span class="sxs-lookup"><span data-stu-id="f1628-153">To recover your managed domain, Microsoft recommends that you resolve critical alerts immediately.</span></span>


### <a name="deleted-state"></a><span data-ttu-id="f1628-154">"Deleted" state</span><span class="sxs-lookup"><span data-stu-id="f1628-154">"Deleted" state</span></span>
<span data-ttu-id="f1628-155">A managed domain that stays in the "Suspended" state for 15 days is **Deleted**.</span><span class="sxs-lookup"><span data-stu-id="f1628-155">A managed domain that stays in the "Suspended" state for 15 days is **Deleted**.</span></span>

<span data-ttu-id="f1628-156">**What to expect**</span><span class="sxs-lookup"><span data-stu-id="f1628-156">**What to expect**</span></span>
* <span data-ttu-id="f1628-157">All resources and backups for the managed domain are deleted.</span><span class="sxs-lookup"><span data-stu-id="f1628-157">All resources and backups for the managed domain are deleted.</span></span>
* <span data-ttu-id="f1628-158">You can't restore the managed domain, and need to create a new managed domain to use Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="f1628-158">You can't restore the managed domain, and need to create a new managed domain to use Azure AD DS.</span></span>
* <span data-ttu-id="f1628-159">After it's deleted, you aren't billed for the managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-159">After it's deleted, you aren't billed for the managed domain.</span></span>


## <a name="how-do-you-know-if-your-managed-domain-is-suspended"></a><span data-ttu-id="f1628-160">How do you know if your managed domain is suspended?</span><span class="sxs-lookup"><span data-stu-id="f1628-160">How do you know if your managed domain is suspended?</span></span>
<span data-ttu-id="f1628-161">You see an [alert](active-directory-ds-troubleshoot-alerts.md) on the Azure AD DS Health page in the Azure portal that declares that the domain is suspended.</span><span class="sxs-lookup"><span data-stu-id="f1628-161">You see an [alert](active-directory-ds-troubleshoot-alerts.md) on the Azure AD DS Health page in the Azure portal that declares that the domain is suspended.</span></span> <span data-ttu-id="f1628-162">The state of the domain also shows "Suspended".</span><span class="sxs-lookup"><span data-stu-id="f1628-162">The state of the domain also shows "Suspended".</span></span>


## <a name="restore-a-suspended-domain"></a><span data-ttu-id="f1628-163">Restore a suspended domain</span><span class="sxs-lookup"><span data-stu-id="f1628-163">Restore a suspended domain</span></span>
<span data-ttu-id="f1628-164">To restore a domain that's in the "Suspended" state, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1628-164">To restore a domain that's in the "Suspended" state, take the following steps:</span></span>

1. <span data-ttu-id="f1628-165">Go to the [Azure Active Directory Domain Services page](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.AAD%2FdomainServices) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f1628-165">Go to the [Azure Active Directory Domain Services page](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.AAD%2FdomainServices) in the Azure portal.</span></span>
2. <span data-ttu-id="f1628-166">Select the managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-166">Select the managed domain.</span></span>
3. <span data-ttu-id="f1628-167">In the left panel, select **Health**.</span><span class="sxs-lookup"><span data-stu-id="f1628-167">In the left panel, select **Health**.</span></span>
4. <span data-ttu-id="f1628-168">Select the alert.</span><span class="sxs-lookup"><span data-stu-id="f1628-168">Select the alert.</span></span> <span data-ttu-id="f1628-169">The alert ID will be either AADDS503 or AADDS504, depending on the cause of suspension.</span><span class="sxs-lookup"><span data-stu-id="f1628-169">The alert ID will be either AADDS503 or AADDS504, depending on the cause of suspension.</span></span>
5. <span data-ttu-id="f1628-170">Select the resolution link that's provided in the alert.</span><span class="sxs-lookup"><span data-stu-id="f1628-170">Select the resolution link that's provided in the alert.</span></span> <span data-ttu-id="f1628-171">Then follow the steps to resolve the alert.</span><span class="sxs-lookup"><span data-stu-id="f1628-171">Then follow the steps to resolve the alert.</span></span>

<span data-ttu-id="f1628-172">Your managed domain can only be restored to the date of the last backup.</span><span class="sxs-lookup"><span data-stu-id="f1628-172">Your managed domain can only be restored to the date of the last backup.</span></span> <span data-ttu-id="f1628-173">The date of your last backup is displayed on the Health page of your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f1628-173">The date of your last backup is displayed on the Health page of your managed domain.</span></span> <span data-ttu-id="f1628-174">Any changes that occurred after the last backup won't be restored.</span><span class="sxs-lookup"><span data-stu-id="f1628-174">Any changes that occurred after the last backup won't be restored.</span></span> <span data-ttu-id="f1628-175">Backups for a managed domain are stored for up to 30 days.</span><span class="sxs-lookup"><span data-stu-id="f1628-175">Backups for a managed domain are stored for up to 30 days.</span></span> <span data-ttu-id="f1628-176">Backups that are older than 30 days are deleted.</span><span class="sxs-lookup"><span data-stu-id="f1628-176">Backups that are older than 30 days are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f1628-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1628-177">Next steps</span></span>
- [<span data-ttu-id="f1628-178">Resolve alerts for your managed domain</span><span class="sxs-lookup"><span data-stu-id="f1628-178">Resolve alerts for your managed domain</span></span>](active-directory-ds-troubleshoot-alerts.md)
- [<span data-ttu-id="f1628-179">Read more about Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="f1628-179">Read more about Azure Active Directory Domain Services</span></span>](active-directory-ds-overview.md)
- [<span data-ttu-id="f1628-180">Contact the product team</span><span class="sxs-lookup"><span data-stu-id="f1628-180">Contact the product team</span></span>](active-directory-ds-contact-us.md)

## <a name="contact-us"></a><span data-ttu-id="f1628-181">Contact us</span><span class="sxs-lookup"><span data-stu-id="f1628-181">Contact us</span></span>
<span data-ttu-id="f1628-182">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span><span class="sxs-lookup"><span data-stu-id="f1628-182">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span></span>
