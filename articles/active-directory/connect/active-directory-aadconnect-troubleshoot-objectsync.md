---
title: 'Azure AD Connect: Troubleshoot object synchronization | Microsoft Docs'
description: This topic provides steps for how to troubleshoot issues with object synchronization using the troubleshooting task.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: curtand
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: f65e84bff63bbdb781991ff6648b0fb98ca5208f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864352"
---
# <a name="troubleshoot-object-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="97709-103">Troubleshoot object synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="97709-103">Troubleshoot object synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="97709-104">This article provides steps for troubleshooting issues with object synchronization by using the troubleshooting task.</span><span class="sxs-lookup"><span data-stu-id="97709-104">This article provides steps for troubleshooting issues with object synchronization by using the troubleshooting task.</span></span> <span data-ttu-id="97709-105">To see how troubleshooting works in Azure Active Directory (Azure AD) Connect, watch [this short video](https://aka.ms/AADCTSVideo).</span><span class="sxs-lookup"><span data-stu-id="97709-105">To see how troubleshooting works in Azure Active Directory (Azure AD) Connect, watch [this short video](https://aka.ms/AADCTSVideo).</span></span>

## <a name="troubleshooting-task"></a><span data-ttu-id="97709-106">Troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="97709-106">Troubleshooting task</span></span>
<span data-ttu-id="97709-107">For Azure AD Connect deployment with version 1.1.749.0 or higher, use the troubleshooting task in the wizard to troubleshoot object synchronization issues.</span><span class="sxs-lookup"><span data-stu-id="97709-107">For Azure AD Connect deployment with version 1.1.749.0 or higher, use the troubleshooting task in the wizard to troubleshoot object synchronization issues.</span></span> <span data-ttu-id="97709-108">For earlier versions, please troubleshoot manually as described [here](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).</span><span class="sxs-lookup"><span data-stu-id="97709-108">For earlier versions, please troubleshoot manually as described [here](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).</span></span>

### <a name="run-the-troubleshooting-task-in-the-wizard"></a><span data-ttu-id="97709-109">Run the troubleshooting task in the wizard</span><span class="sxs-lookup"><span data-stu-id="97709-109">Run the troubleshooting task in the wizard</span></span>
<span data-ttu-id="97709-110">To run the troubleshooting task in the wizard, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="97709-110">To run the troubleshooting task in the wizard, perform the following steps:</span></span>

1.  <span data-ttu-id="97709-111">Open a new Windows PowerShell session on your Azure AD Connect server with the Run as Administrator option.</span><span class="sxs-lookup"><span data-stu-id="97709-111">Open a new Windows PowerShell session on your Azure AD Connect server with the Run as Administrator option.</span></span>
2.  <span data-ttu-id="97709-112">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="97709-112">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>
3.  <span data-ttu-id="97709-113">Start the Azure AD Connect wizard.</span><span class="sxs-lookup"><span data-stu-id="97709-113">Start the Azure AD Connect wizard.</span></span>
4.  <span data-ttu-id="97709-114">Navigate to the Additional Tasks page, select Troubleshoot, and click Next.</span><span class="sxs-lookup"><span data-stu-id="97709-114">Navigate to the Additional Tasks page, select Troubleshoot, and click Next.</span></span>
5.  <span data-ttu-id="97709-115">On the Troubleshooting page, click Launch to start the troubleshooting menu in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97709-115">On the Troubleshooting page, click Launch to start the troubleshooting menu in PowerShell.</span></span>
6.  <span data-ttu-id="97709-116">In the main menu, select Troubleshoot Object Synchronization.</span><span class="sxs-lookup"><span data-stu-id="97709-116">In the main menu, select Troubleshoot Object Synchronization.</span></span>
![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch11.png)

### <a name="troubleshooting-input-parameters"></a><span data-ttu-id="97709-117">Troubleshooting Input Parameters</span><span class="sxs-lookup"><span data-stu-id="97709-117">Troubleshooting Input Parameters</span></span>
<span data-ttu-id="97709-118">The following input parameters are needed by the troubleshooting task:</span><span class="sxs-lookup"><span data-stu-id="97709-118">The following input parameters are needed by the troubleshooting task:</span></span>
1.  <span data-ttu-id="97709-119">**Object Distinguished Name** – This is the distinguished name of the object that needs troubleshooting</span><span class="sxs-lookup"><span data-stu-id="97709-119">**Object Distinguished Name** – This is the distinguished name of the object that needs troubleshooting</span></span>
2.  <span data-ttu-id="97709-120">**AD Connector Name** – This is the name of the AD forest where the above object resides.</span><span class="sxs-lookup"><span data-stu-id="97709-120">**AD Connector Name** – This is the name of the AD forest where the above object resides.</span></span>
3.  <span data-ttu-id="97709-121">Azure AD tenant global administrator credentials ![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch1.png)</span><span class="sxs-lookup"><span data-stu-id="97709-121">Azure AD tenant global administrator credentials ![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch1.png)</span></span>

### <a name="understand-the-results-of-the-troubleshooting-task"></a><span data-ttu-id="97709-122">Understand the results of the troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="97709-122">Understand the results of the troubleshooting task</span></span>
<span data-ttu-id="97709-123">The troubleshooting task performs the following checks:</span><span class="sxs-lookup"><span data-stu-id="97709-123">The troubleshooting task performs the following checks:</span></span>

1.  <span data-ttu-id="97709-124">Detect UPN mismatch if the object is synced to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97709-124">Detect UPN mismatch if the object is synced to Azure Active Directory</span></span>
2.  <span data-ttu-id="97709-125">Check if object is filtered due to domain filtering</span><span class="sxs-lookup"><span data-stu-id="97709-125">Check if object is filtered due to domain filtering</span></span>
3.  <span data-ttu-id="97709-126">Check if object is filtered due to OU filtering</span><span class="sxs-lookup"><span data-stu-id="97709-126">Check if object is filtered due to OU filtering</span></span>
4.  <span data-ttu-id="97709-127">Check if object synchronization is blocked due to a linked mailbox</span><span class="sxs-lookup"><span data-stu-id="97709-127">Check if object synchronization is blocked due to a linked mailbox</span></span>
5. <span data-ttu-id="97709-128">Check if object is dynamic distribution group which is not supposed to be synchronized</span><span class="sxs-lookup"><span data-stu-id="97709-128">Check if object is dynamic distribution group which is not supposed to be synchronized</span></span>

<span data-ttu-id="97709-129">The rest of this section describes specific results that are returned by the task.</span><span class="sxs-lookup"><span data-stu-id="97709-129">The rest of this section describes specific results that are returned by the task.</span></span> <span data-ttu-id="97709-130">In each case, the task provides an analysis followed by recommended actions to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="97709-130">In each case, the task provides an analysis followed by recommended actions to resolve the issue.</span></span>

## <a name="detect-upn-mismatch-if-object-is-synced-to-azure-active-directory"></a><span data-ttu-id="97709-131">Detect UPN mismatch if object is synced to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97709-131">Detect UPN mismatch if object is synced to Azure Active Directory</span></span>
### <a name="upn-suffix-is-not-verified-with-azure-ad-tenant"></a><span data-ttu-id="97709-132">UPN Suffix is NOT verified with Azure AD Tenant</span><span class="sxs-lookup"><span data-stu-id="97709-132">UPN Suffix is NOT verified with Azure AD Tenant</span></span>
<span data-ttu-id="97709-133">When UserPrincipalName (UPN)/Alternate Login ID suffix is not verified with the Azure AD Tenant, then Azure Active Directory replaces the UPN suffixes with the default domain name "onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="97709-133">When UserPrincipalName (UPN)/Alternate Login ID suffix is not verified with the Azure AD Tenant, then Azure Active Directory replaces the UPN suffixes with the default domain name "onmicrosoft.com".</span></span>

![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch2.png)

### <a name="changing-upn-suffix-from-one-federated-domain-to-another-federated-domain"></a><span data-ttu-id="97709-134">Changing UPN Suffix from one federated domain to another federated domain</span><span class="sxs-lookup"><span data-stu-id="97709-134">Changing UPN Suffix from one federated domain to another federated domain</span></span>
<span data-ttu-id="97709-135">Azure Active Directory does not allow the synchronization of UserPrincipalName (UPN)/Alternate Login ID suffix change from one federated domain to another federated domain.</span><span class="sxs-lookup"><span data-stu-id="97709-135">Azure Active Directory does not allow the synchronization of UserPrincipalName (UPN)/Alternate Login ID suffix change from one federated domain to another federated domain.</span></span> <span data-ttu-id="97709-136">This applies to domains, that are verified with the Azure AD Tenant and have the Authentication Type as Federated.</span><span class="sxs-lookup"><span data-stu-id="97709-136">This applies to domains, that are verified with the Azure AD Tenant and have the Authentication Type as Federated.</span></span>

![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch3.png) 

### <a name="azure-ad-tenant-dirsync-feature-synchronizeupnformanagedusers-is-disabled"></a><span data-ttu-id="97709-137">Azure AD Tenant DirSync Feature ‘SynchronizeUpnForManagedUsers’ is disabled</span><span class="sxs-lookup"><span data-stu-id="97709-137">Azure AD Tenant DirSync Feature ‘SynchronizeUpnForManagedUsers’ is disabled</span></span>
<span data-ttu-id="97709-138">When the Azure AD Tenant DirSync Feature ‘SynchronizeUpnForManagedUsers’ is disabled, Azure Active Directory does not allow synchronization updates to UserPrincipalName/Alternate Login ID for licensed user accounts with managed authentication.</span><span class="sxs-lookup"><span data-stu-id="97709-138">When the Azure AD Tenant DirSync Feature ‘SynchronizeUpnForManagedUsers’ is disabled, Azure Active Directory does not allow synchronization updates to UserPrincipalName/Alternate Login ID for licensed user accounts with managed authentication.</span></span>

![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch4.png)

## <a name="object-is-filtered-due-to-domain-filtering"></a><span data-ttu-id="97709-139">Object is filtered due to domain filtering</span><span class="sxs-lookup"><span data-stu-id="97709-139">Object is filtered due to domain filtering</span></span>
### <a name="domain-is-not-configured-to-sync"></a><span data-ttu-id="97709-140">Domain is not configured to sync</span><span class="sxs-lookup"><span data-stu-id="97709-140">Domain is not configured to sync</span></span>
<span data-ttu-id="97709-141">Object is out of scope due to domain not being configured.</span><span class="sxs-lookup"><span data-stu-id="97709-141">Object is out of scope due to domain not being configured.</span></span> <span data-ttu-id="97709-142">In the example below, the object is out of sync scope as the domain that it belongs to is filtered from synchronization.</span><span class="sxs-lookup"><span data-stu-id="97709-142">In the example below, the object is out of sync scope as the domain that it belongs to is filtered from synchronization.</span></span>

![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch5.png)

### <a name="domain-is-configured-to-sync-but-is-missing-run-profilesrun-steps"></a><span data-ttu-id="97709-143">Domain is configured to sync but is missing run profiles/run steps</span><span class="sxs-lookup"><span data-stu-id="97709-143">Domain is configured to sync but is missing run profiles/run steps</span></span>
<span data-ttu-id="97709-144">Object is out of scope as the domain is missing run profiles/run steps.</span><span class="sxs-lookup"><span data-stu-id="97709-144">Object is out of scope as the domain is missing run profiles/run steps.</span></span> <span data-ttu-id="97709-145">In the example below, the object is out of sync scope as the domain that it belongs to is missing run steps for the Full Import run profile.</span><span class="sxs-lookup"><span data-stu-id="97709-145">In the example below, the object is out of sync scope as the domain that it belongs to is missing run steps for the Full Import run profile.</span></span>
![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch6.png)

## <a name="object-is-filtered-due-to-ou-filtering"></a><span data-ttu-id="97709-146">Object is filtered due to OU filtering</span><span class="sxs-lookup"><span data-stu-id="97709-146">Object is filtered due to OU filtering</span></span>
<span data-ttu-id="97709-147">The object is out of sync scope due to OU filtering configuration.</span><span class="sxs-lookup"><span data-stu-id="97709-147">The object is out of sync scope due to OU filtering configuration.</span></span> <span data-ttu-id="97709-148">In the example below, the object belongs to OU=NoSync,DC=bvtadwbackdc,DC=com.</span><span class="sxs-lookup"><span data-stu-id="97709-148">In the example below, the object belongs to OU=NoSync,DC=bvtadwbackdc,DC=com.</span></span>  <span data-ttu-id="97709-149">This OU is not included in sync scope.</span><span class="sxs-lookup"><span data-stu-id="97709-149">This OU is not included in sync scope.</span></span></br>

![OU](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch7.png)

## <a name="linked-mailbox-issue"></a><span data-ttu-id="97709-151">Linked Mailbox issue</span><span class="sxs-lookup"><span data-stu-id="97709-151">Linked Mailbox issue</span></span>
<span data-ttu-id="97709-152">A linked mailbox is supposed to be associated with an external master account located in another trusted account forest.</span><span class="sxs-lookup"><span data-stu-id="97709-152">A linked mailbox is supposed to be associated with an external master account located in another trusted account forest.</span></span> <span data-ttu-id="97709-153">If there is no such external master account, then Azure AD Connect will not synchronize the user account corresponds to the linked mailbox in the Exchange forest to the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="97709-153">If there is no such external master account, then Azure AD Connect will not synchronize the user account corresponds to the linked mailbox in the Exchange forest to the Azure AD tenant.</span></span></br>
<span data-ttu-id="97709-154">![Linked Mailbox](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch12.png)</span><span class="sxs-lookup"><span data-stu-id="97709-154">![Linked Mailbox](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch12.png)</span></span>

## <a name="dynamic-distribution-group-issue"></a><span data-ttu-id="97709-155">Dynamic Distribution Group issue</span><span class="sxs-lookup"><span data-stu-id="97709-155">Dynamic Distribution Group issue</span></span>
<span data-ttu-id="97709-156">Due to various differences between on-premises Active Directory and Azure Active Directory, Azure AD Connect does not synchronize dynamic distribution groups to the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="97709-156">Due to various differences between on-premises Active Directory and Azure Active Directory, Azure AD Connect does not synchronize dynamic distribution groups to the Azure AD tenant.</span></span>

![Dynamic Distribution Group](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch13.png)

## <a name="html-report"></a><span data-ttu-id="97709-158">HTML Report</span><span class="sxs-lookup"><span data-stu-id="97709-158">HTML Report</span></span>
<span data-ttu-id="97709-159">In addition to analyzing the object, the troubleshooting task also generates an HTML report that has everything known about the object.</span><span class="sxs-lookup"><span data-stu-id="97709-159">In addition to analyzing the object, the troubleshooting task also generates an HTML report that has everything known about the object.</span></span> <span data-ttu-id="97709-160">This HTML report can be shared with support team to do further troubleshooting, if needed.</span><span class="sxs-lookup"><span data-stu-id="97709-160">This HTML report can be shared with support team to do further troubleshooting, if needed.</span></span>

![](media\active-directory-aadconnect-troubleshoot-objectsynch\objsynch8.png)

## <a name="next-steps"></a><span data-ttu-id="97709-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="97709-161">Next steps</span></span>
<span data-ttu-id="97709-162">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="97709-162">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
