---
title: Troubleshoot password hash synchronization with Azure AD Connect sync | Microsoft Docs
description: This article provides information about how to troubleshoot password hash synchronization problems.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 7cc86f56f7f68c70d66407bd44e6368f31f202d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867230"
---
# <a name="troubleshoot-password-hash-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="07224-103">Troubleshoot password hash synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="07224-103">Troubleshoot password hash synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="07224-104">This topic provides steps for how to troubleshoot issues with password hash synchronization.</span><span class="sxs-lookup"><span data-stu-id="07224-104">This topic provides steps for how to troubleshoot issues with password hash synchronization.</span></span> <span data-ttu-id="07224-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span><span class="sxs-lookup"><span data-stu-id="07224-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span>

<span data-ttu-id="07224-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.614.0 or after, use the troubleshooting task in the wizard to troubleshoot password hash synchronization issues:</span><span class="sxs-lookup"><span data-stu-id="07224-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.614.0 or after, use the troubleshooting task in the wizard to troubleshoot password hash synchronization issues:</span></span>

* <span data-ttu-id="07224-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the troubleshooting task](#no-passwords-are-synchronized-troubleshoot-by-using-the-troubleshooting-task) section.</span><span class="sxs-lookup"><span data-stu-id="07224-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the troubleshooting task](#no-passwords-are-synchronized-troubleshoot-by-using-the-troubleshooting-task) section.</span></span>

* <span data-ttu-id="07224-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the troubleshooting task](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-troubleshooting-task) section.</span><span class="sxs-lookup"><span data-stu-id="07224-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the troubleshooting task](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-troubleshooting-task) section.</span></span>

<span data-ttu-id="07224-109">For deployment with version 1.1.524.0 or later, there is a diagnostic cmdlet that you can use to troubleshoot password hash synchronization issues:</span><span class="sxs-lookup"><span data-stu-id="07224-109">For deployment with version 1.1.524.0 or later, there is a diagnostic cmdlet that you can use to troubleshoot password hash synchronization issues:</span></span>

* <span data-ttu-id="07224-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span><span class="sxs-lookup"><span data-stu-id="07224-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="07224-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span><span class="sxs-lookup"><span data-stu-id="07224-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="07224-112">For older versions of Azure AD Connect deployment:</span><span class="sxs-lookup"><span data-stu-id="07224-112">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="07224-113">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span><span class="sxs-lookup"><span data-stu-id="07224-113">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="07224-114">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span><span class="sxs-lookup"><span data-stu-id="07224-114">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>



## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-troubleshooting-task"></a><span data-ttu-id="07224-115">No passwords are synchronized: troubleshoot by using the troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="07224-115">No passwords are synchronized: troubleshoot by using the troubleshooting task</span></span>
<span data-ttu-id="07224-116">You can use the troubleshooting task to figure out why no passwords are synchronized.</span><span class="sxs-lookup"><span data-stu-id="07224-116">You can use the troubleshooting task to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="07224-117">The troubleshooting task is available only for Azure AD Connect version 1.1.614.0 or later.</span><span class="sxs-lookup"><span data-stu-id="07224-117">The troubleshooting task is available only for Azure AD Connect version 1.1.614.0 or later.</span></span>

### <a name="run-the-troubleshooting-task"></a><span data-ttu-id="07224-118">Run the troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="07224-118">Run the troubleshooting task</span></span>
<span data-ttu-id="07224-119">To troubleshoot issues where no passwords are synchronized:</span><span class="sxs-lookup"><span data-stu-id="07224-119">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="07224-120">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span><span class="sxs-lookup"><span data-stu-id="07224-120">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="07224-121">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="07224-121">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="07224-122">Start the Azure AD Connect wizard.</span><span class="sxs-lookup"><span data-stu-id="07224-122">Start the Azure AD Connect wizard.</span></span>

4. <span data-ttu-id="07224-123">Navigate to the **Additional Tasks** page, select **Troubleshoot**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="07224-123">Navigate to the **Additional Tasks** page, select **Troubleshoot**, and click **Next**.</span></span>

5. <span data-ttu-id="07224-124">On the Troubleshooting page, click **Launch** to start the troubleshooting menu in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07224-124">On the Troubleshooting page, click **Launch** to start the troubleshooting menu in PowerShell.</span></span>

6. <span data-ttu-id="07224-125">In the main menu, select **Troubleshoot password hash synchronization**.</span><span class="sxs-lookup"><span data-stu-id="07224-125">In the main menu, select **Troubleshoot password hash synchronization**.</span></span>

7. <span data-ttu-id="07224-126">In the sub menu, select **Password hash synchronization does not work at all**.</span><span class="sxs-lookup"><span data-stu-id="07224-126">In the sub menu, select **Password hash synchronization does not work at all**.</span></span>

### <a name="understand-the-results-of-the-troubleshooting-task"></a><span data-ttu-id="07224-127">Understand the results of the troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="07224-127">Understand the results of the troubleshooting task</span></span>
<span data-ttu-id="07224-128">The troubleshooting task performs the following checks:</span><span class="sxs-lookup"><span data-stu-id="07224-128">The troubleshooting task performs the following checks:</span></span>

* <span data-ttu-id="07224-129">Validates that the password hash synchronization feature is enabled for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="07224-129">Validates that the password hash synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="07224-130">Validates that the Azure AD Connect server is not in staging mode.</span><span class="sxs-lookup"><span data-stu-id="07224-130">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="07224-131">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span><span class="sxs-lookup"><span data-stu-id="07224-131">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="07224-132">Validates that the password hash synchronization feature is enabled.</span><span class="sxs-lookup"><span data-stu-id="07224-132">Validates that the password hash synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="07224-133">Searches for password hash synchronization heartbeat events in the Windows Application Event logs.</span><span class="sxs-lookup"><span data-stu-id="07224-133">Searches for password hash synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="07224-134">For each Active Directory domain under the on-premises Active Directory connector:</span><span class="sxs-lookup"><span data-stu-id="07224-134">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="07224-135">Validates that the domain is reachable from the Azure AD Connect server.</span><span class="sxs-lookup"><span data-stu-id="07224-135">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="07224-136">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password hash synchronization.</span><span class="sxs-lookup"><span data-stu-id="07224-136">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password hash synchronization.</span></span>

<span data-ttu-id="07224-137">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span><span class="sxs-lookup"><span data-stu-id="07224-137">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Diagnostic output for password hash synchronization](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phsglobalgeneral.png)

<span data-ttu-id="07224-139">The rest of this section describes specific results that are returned by the task and corresponding issues.</span><span class="sxs-lookup"><span data-stu-id="07224-139">The rest of this section describes specific results that are returned by the task and corresponding issues.</span></span>

#### <a name="password-hash-synchronization-feature-isnt-enabled"></a><span data-ttu-id="07224-140">password hash synchronization feature isn't enabled</span><span class="sxs-lookup"><span data-stu-id="07224-140">password hash synchronization feature isn't enabled</span></span>
<span data-ttu-id="07224-141">If you haven't enabled password hash synchronization by using the Azure AD Connect wizard, the following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-141">If you haven't enabled password hash synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![password hash synchronization isn't enabled](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="07224-143">Azure AD Connect server is in staging mode</span><span class="sxs-lookup"><span data-stu-id="07224-143">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="07224-144">If the Azure AD Connect server is in staging mode, password hash synchronization is temporarily disabled, and the following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-144">If the Azure AD Connect server is in staging mode, password hash synchronization is temporarily disabled, and the following error is returned:</span></span>

![Azure AD Connect server is in staging mode](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phsglobalstaging.png)

#### <a name="no-password-hash-synchronization-heartbeat-events"></a><span data-ttu-id="07224-146">No password hash synchronization heartbeat events</span><span class="sxs-lookup"><span data-stu-id="07224-146">No password hash synchronization heartbeat events</span></span>
<span data-ttu-id="07224-147">Each on-premises Active Directory connector has its own password hash synchronization channel.</span><span class="sxs-lookup"><span data-stu-id="07224-147">Each on-premises Active Directory connector has its own password hash synchronization channel.</span></span> <span data-ttu-id="07224-148">When the password hash synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span><span class="sxs-lookup"><span data-stu-id="07224-148">When the password hash synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="07224-149">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span><span class="sxs-lookup"><span data-stu-id="07224-149">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="07224-150">If no heartbeat event is found, the following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-150">If no heartbeat event is found, the following error is returned:</span></span>

![No password hash synchronization heart beat event](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="07224-152">AD DS account does not have correct permissions</span><span class="sxs-lookup"><span data-stu-id="07224-152">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="07224-153">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-153">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Incorrect credential](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="07224-155">Incorrect AD DS account username or password</span><span class="sxs-lookup"><span data-stu-id="07224-155">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="07224-156">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-156">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Incorrect credential](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phsglobalaccountincorrectcredential.png)



## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-troubleshooting-task"></a><span data-ttu-id="07224-158">One object is not synchronizing passwords: troubleshoot by using the troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="07224-158">One object is not synchronizing passwords: troubleshoot by using the troubleshooting task</span></span>

<span data-ttu-id="07224-159">You can use the troubleshooting task to determine why one object is not synchronizing passwords.</span><span class="sxs-lookup"><span data-stu-id="07224-159">You can use the troubleshooting task to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="07224-160">The troubleshooting task is available only for Azure AD Connect version 1.1.614.0 or later.</span><span class="sxs-lookup"><span data-stu-id="07224-160">The troubleshooting task is available only for Azure AD Connect version 1.1.614.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="07224-161">Run the diagnostics cmdlet</span><span class="sxs-lookup"><span data-stu-id="07224-161">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="07224-162">To troubleshoot issues for a specific user object:</span><span class="sxs-lookup"><span data-stu-id="07224-162">To troubleshoot issues for a specific user object:</span></span>

1. <span data-ttu-id="07224-163">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span><span class="sxs-lookup"><span data-stu-id="07224-163">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="07224-164">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="07224-164">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="07224-165">Start the Azure AD Connect wizard.</span><span class="sxs-lookup"><span data-stu-id="07224-165">Start the Azure AD Connect wizard.</span></span>

4. <span data-ttu-id="07224-166">Navigate to the **Additional Tasks** page, select **Troubleshoot**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="07224-166">Navigate to the **Additional Tasks** page, select **Troubleshoot**, and click **Next**.</span></span>

5. <span data-ttu-id="07224-167">On the Troubleshooting page, click **Launch** to start the troubleshooting menu in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07224-167">On the Troubleshooting page, click **Launch** to start the troubleshooting menu in PowerShell.</span></span>

6. <span data-ttu-id="07224-168">In the main menu, select **Troubleshoot password hash synchronization**.</span><span class="sxs-lookup"><span data-stu-id="07224-168">In the main menu, select **Troubleshoot password hash synchronization**.</span></span>

7. <span data-ttu-id="07224-169">In the sub menu, select **Password is not synchronized for a specific user account**.</span><span class="sxs-lookup"><span data-stu-id="07224-169">In the sub menu, select **Password is not synchronized for a specific user account**.</span></span>

### <a name="understand-the-results-of-the-troubleshooting-task"></a><span data-ttu-id="07224-170">Understand the results of the troubleshooting task</span><span class="sxs-lookup"><span data-stu-id="07224-170">Understand the results of the troubleshooting task</span></span>
<span data-ttu-id="07224-171">The troubleshooting task performs the following checks:</span><span class="sxs-lookup"><span data-stu-id="07224-171">The troubleshooting task performs the following checks:</span></span>

* <span data-ttu-id="07224-172">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span><span class="sxs-lookup"><span data-stu-id="07224-172">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="07224-173">Validates that there are synchronization rules with password hash synchronization enabled and applied to the Active Directory object.</span><span class="sxs-lookup"><span data-stu-id="07224-173">Validates that there are synchronization rules with password hash synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="07224-174">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span><span class="sxs-lookup"><span data-stu-id="07224-174">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="07224-175">The following diagram illustrates the results of the cmdlet when troubleshooting password hash synchronization for a single object:</span><span class="sxs-lookup"><span data-stu-id="07224-175">The following diagram illustrates the results of the cmdlet when troubleshooting password hash synchronization for a single object:</span></span>

![Diagnostic output for password hash synchronization - single object](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="07224-177">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span><span class="sxs-lookup"><span data-stu-id="07224-177">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="07224-178">The Active Directory object isn't exported to Azure AD</span><span class="sxs-lookup"><span data-stu-id="07224-178">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="07224-179">password hash synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="07224-179">password hash synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="07224-180">The following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-180">The following error is returned:</span></span>

![Azure AD object is missing](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="07224-182">User has a temporary password</span><span class="sxs-lookup"><span data-stu-id="07224-182">User has a temporary password</span></span>
<span data-ttu-id="07224-183">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07224-183">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="07224-184">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span><span class="sxs-lookup"><span data-stu-id="07224-184">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="07224-185">The following error is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-185">The following error is returned:</span></span>

![Temporary password is not exported](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="07224-187">Results of last attempt to synchronize password aren't available</span><span class="sxs-lookup"><span data-stu-id="07224-187">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="07224-188">By default, Azure AD Connect stores the results of password hash synchronization attempts for seven days.</span><span class="sxs-lookup"><span data-stu-id="07224-188">By default, Azure AD Connect stores the results of password hash synchronization attempts for seven days.</span></span> <span data-ttu-id="07224-189">If there are no results available for the selected Active Directory object, the following warning is returned:</span><span class="sxs-lookup"><span data-stu-id="07224-189">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Diagnostic output for single object - no password sync history](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/phssingleobjectnohistory.png)



## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="07224-191">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span><span class="sxs-lookup"><span data-stu-id="07224-191">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="07224-192">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span><span class="sxs-lookup"><span data-stu-id="07224-192">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="07224-193">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span><span class="sxs-lookup"><span data-stu-id="07224-193">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="07224-194">Run the diagnostics cmdlet</span><span class="sxs-lookup"><span data-stu-id="07224-194">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="07224-195">To troubleshoot issues where no passwords are synchronized:</span><span class="sxs-lookup"><span data-stu-id="07224-195">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="07224-196">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span><span class="sxs-lookup"><span data-stu-id="07224-196">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="07224-197">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="07224-197">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="07224-198">Run `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="07224-198">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="07224-199">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="07224-199">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>



## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="07224-200">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span><span class="sxs-lookup"><span data-stu-id="07224-200">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="07224-201">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span><span class="sxs-lookup"><span data-stu-id="07224-201">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="07224-202">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span><span class="sxs-lookup"><span data-stu-id="07224-202">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="07224-203">Run the diagnostics cmdlet</span><span class="sxs-lookup"><span data-stu-id="07224-203">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="07224-204">To troubleshoot issues where no passwords are synchronized for a user:</span><span class="sxs-lookup"><span data-stu-id="07224-204">To troubleshoot issues where no passwords are synchronized for a user:</span></span>

1. <span data-ttu-id="07224-205">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span><span class="sxs-lookup"><span data-stu-id="07224-205">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="07224-206">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="07224-206">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="07224-207">Run `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="07224-207">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="07224-208">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="07224-208">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="07224-209">For example:</span><span class="sxs-lookup"><span data-stu-id="07224-209">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```



## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="07224-210">No passwords are synchronized: manual troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="07224-210">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="07224-211">Follow these steps to determine why no passwords are synchronized:</span><span class="sxs-lookup"><span data-stu-id="07224-211">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="07224-212">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="07224-212">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="07224-213">A server in staging mode does not synchronize any passwords.</span><span class="sxs-lookup"><span data-stu-id="07224-213">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="07224-214">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span><span class="sxs-lookup"><span data-stu-id="07224-214">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="07224-215">It gives you an overview of the password sync configuration.</span><span class="sxs-lookup"><span data-stu-id="07224-215">It gives you an overview of the password sync configuration.</span></span>  

    ![PowerShell script output from password sync settings](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="07224-217">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span><span class="sxs-lookup"><span data-stu-id="07224-217">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="07224-218">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span><span class="sxs-lookup"><span data-stu-id="07224-218">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="07224-219">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span><span class="sxs-lookup"><span data-stu-id="07224-219">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="07224-220">Look in the event log for errors.</span><span class="sxs-lookup"><span data-stu-id="07224-220">Look in the event log for errors.</span></span> <span data-ttu-id="07224-221">Look for the following events, which would indicate a problem:</span><span class="sxs-lookup"><span data-stu-id="07224-221">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="07224-222">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span><span class="sxs-lookup"><span data-stu-id="07224-222">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="07224-223">The event log message contains forest information where you have a problem.</span><span class="sxs-lookup"><span data-stu-id="07224-223">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="07224-224">For more information, see [Connectivity problem](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="07224-224">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="07224-225">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="07224-225">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="07224-226">Run the script only once.</span><span class="sxs-lookup"><span data-stu-id="07224-226">Run the script only once.</span></span>

6. <span data-ttu-id="07224-227">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span><span class="sxs-lookup"><span data-stu-id="07224-227">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="07224-228">Connectivity problems</span><span class="sxs-lookup"><span data-stu-id="07224-228">Connectivity problems</span></span>

<span data-ttu-id="07224-229">Do you have connectivity with Azure AD?</span><span class="sxs-lookup"><span data-stu-id="07224-229">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="07224-230">Does the account have required permissions to read the password hashes in all domains?</span><span class="sxs-lookup"><span data-stu-id="07224-230">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="07224-231">If you installed Connect by using Express settings, the permissions should already be correct.</span><span class="sxs-lookup"><span data-stu-id="07224-231">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="07224-232">If you used custom installation, set the permissions manually by doing the following:</span><span class="sxs-lookup"><span data-stu-id="07224-232">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="07224-233">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="07224-233">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="07224-234">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="07224-234">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="07224-235">Select the connector, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="07224-235">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="07224-236">Go to **Connect to Active Directory Forest**.</span><span class="sxs-lookup"><span data-stu-id="07224-236">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Account used by Active Directory connector](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/connectoraccount.png)  
    <span data-ttu-id="07224-238">Note the username and the domain where the account is located.</span><span class="sxs-lookup"><span data-stu-id="07224-238">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="07224-239">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span><span class="sxs-lookup"><span data-stu-id="07224-239">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="07224-240">Replicate Directory Changes</span><span class="sxs-lookup"><span data-stu-id="07224-240">Replicate Directory Changes</span></span>
    * <span data-ttu-id="07224-241">Replicate Directory Changes All</span><span class="sxs-lookup"><span data-stu-id="07224-241">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="07224-242">Are the domain controllers reachable by Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="07224-242">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="07224-243">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span><span class="sxs-lookup"><span data-stu-id="07224-243">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Domain controller used by Active Directory connector](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="07224-245">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span><span class="sxs-lookup"><span data-stu-id="07224-245">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="07224-246">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="07224-246">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="07224-247">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span><span class="sxs-lookup"><span data-stu-id="07224-247">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="07224-248">Do these steps for all your domains.</span><span class="sxs-lookup"><span data-stu-id="07224-248">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="07224-249">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="07224-249">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="07224-250">One object is not synchronizing passwords: manual troubleshooting steps</span><span class="sxs-lookup"><span data-stu-id="07224-250">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="07224-251">You can easily troubleshoot password hash synchronization issues by reviewing the status of an object.</span><span class="sxs-lookup"><span data-stu-id="07224-251">You can easily troubleshoot password hash synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="07224-252">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span><span class="sxs-lookup"><span data-stu-id="07224-252">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory productive passwords](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/adprodpassword.png)  

    <span data-ttu-id="07224-254">If the check box is selected, ask the user to sign in and change the password.</span><span class="sxs-lookup"><span data-stu-id="07224-254">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="07224-255">Temporary passwords are not synchronized with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07224-255">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="07224-256">If the password looks correct in Active Directory, follow the user in the sync engine.</span><span class="sxs-lookup"><span data-stu-id="07224-256">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="07224-257">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span><span class="sxs-lookup"><span data-stu-id="07224-257">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="07224-258">a.</span><span class="sxs-lookup"><span data-stu-id="07224-258">a.</span></span> <span data-ttu-id="07224-259">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="07224-259">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="07224-260">b.</span><span class="sxs-lookup"><span data-stu-id="07224-260">b.</span></span> <span data-ttu-id="07224-261">Click **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="07224-261">Click **Connectors**.</span></span>

    <span data-ttu-id="07224-262">c.</span><span class="sxs-lookup"><span data-stu-id="07224-262">c.</span></span> <span data-ttu-id="07224-263">Select the **Active Directory Connector** where the user is located.</span><span class="sxs-lookup"><span data-stu-id="07224-263">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="07224-264">d.</span><span class="sxs-lookup"><span data-stu-id="07224-264">d.</span></span> <span data-ttu-id="07224-265">Select **Search Connector Space**.</span><span class="sxs-lookup"><span data-stu-id="07224-265">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="07224-266">e.</span><span class="sxs-lookup"><span data-stu-id="07224-266">e.</span></span> <span data-ttu-id="07224-267">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="07224-267">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Search for user in connector space with DN](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/searchcs.png)  

    <span data-ttu-id="07224-269">f.</span><span class="sxs-lookup"><span data-stu-id="07224-269">f.</span></span> <span data-ttu-id="07224-270">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span><span class="sxs-lookup"><span data-stu-id="07224-270">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="07224-271">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span><span class="sxs-lookup"><span data-stu-id="07224-271">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="07224-272">g.</span><span class="sxs-lookup"><span data-stu-id="07224-272">g.</span></span> <span data-ttu-id="07224-273">To see the password sync details of the object for the past week, click **Log**.</span><span class="sxs-lookup"><span data-stu-id="07224-273">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Object log details](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/csobjectlog.png)  

    <span data-ttu-id="07224-275">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07224-275">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="07224-276">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="07224-276">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="07224-277">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="07224-277">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="07224-278">h.</span><span class="sxs-lookup"><span data-stu-id="07224-278">h.</span></span> <span data-ttu-id="07224-279">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span><span class="sxs-lookup"><span data-stu-id="07224-279">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="07224-280">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="07224-280">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Lineage information about a user](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/cspasswordsync.png)  

    <span data-ttu-id="07224-282">i.</span><span class="sxs-lookup"><span data-stu-id="07224-282">i.</span></span> <span data-ttu-id="07224-283">Click **Metaverse Object Properties** to display a list of user attributes.</span><span class="sxs-lookup"><span data-stu-id="07224-283">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Metaverse information](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="07224-285">Verify that there is no **cloudFiltered** attribute present.</span><span class="sxs-lookup"><span data-stu-id="07224-285">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="07224-286">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span><span class="sxs-lookup"><span data-stu-id="07224-286">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="07224-287">j.</span><span class="sxs-lookup"><span data-stu-id="07224-287">j.</span></span> <span data-ttu-id="07224-288">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07224-288">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Metaverse information](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/mvconnectors.png)  

    <span data-ttu-id="07224-290">k.</span><span class="sxs-lookup"><span data-stu-id="07224-290">k.</span></span> <span data-ttu-id="07224-291">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span><span class="sxs-lookup"><span data-stu-id="07224-291">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="07224-292">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="07224-292">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Connector Space Object Properties dialog box](./media/active-directory-aadconnectsync-troubleshoot-password-hash-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="07224-294">Password sync log</span><span class="sxs-lookup"><span data-stu-id="07224-294">Password sync log</span></span>
<span data-ttu-id="07224-295">The status column can have the following values:</span><span class="sxs-lookup"><span data-stu-id="07224-295">The status column can have the following values:</span></span>

| <span data-ttu-id="07224-296">Status</span><span class="sxs-lookup"><span data-stu-id="07224-296">Status</span></span> | <span data-ttu-id="07224-297">Description</span><span class="sxs-lookup"><span data-stu-id="07224-297">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07224-298">Success</span><span class="sxs-lookup"><span data-stu-id="07224-298">Success</span></span> |<span data-ttu-id="07224-299">Password has been successfully synchronized.</span><span class="sxs-lookup"><span data-stu-id="07224-299">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="07224-300">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="07224-300">FilteredByTarget</span></span> |<span data-ttu-id="07224-301">Password is set to **User must change password at next logon**.</span><span class="sxs-lookup"><span data-stu-id="07224-301">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="07224-302">Password has not been synchronized.</span><span class="sxs-lookup"><span data-stu-id="07224-302">Password has not been synchronized.</span></span> |
| <span data-ttu-id="07224-303">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="07224-303">NoTargetConnection</span></span> |<span data-ttu-id="07224-304">No object in the metaverse or in the Azure AD connector space.</span><span class="sxs-lookup"><span data-stu-id="07224-304">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="07224-305">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="07224-305">SourceConnectorNotPresent</span></span> |<span data-ttu-id="07224-306">No object found in the on-premises Active Directory connector space.</span><span class="sxs-lookup"><span data-stu-id="07224-306">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="07224-307">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="07224-307">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="07224-308">The object in the Azure AD connector space has not yet been exported.</span><span class="sxs-lookup"><span data-stu-id="07224-308">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="07224-309">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="07224-309">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="07224-310">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span><span class="sxs-lookup"><span data-stu-id="07224-310">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="07224-311">Error</span><span class="sxs-lookup"><span data-stu-id="07224-311">Error</span></span> |<span data-ttu-id="07224-312">Service returned an unknown error.</span><span class="sxs-lookup"><span data-stu-id="07224-312">Service returned an unknown error.</span></span> |
| <span data-ttu-id="07224-313">Unknown</span><span class="sxs-lookup"><span data-stu-id="07224-313">Unknown</span></span> |<span data-ttu-id="07224-314">An error occurred while trying to process a batch of password hashes.</span><span class="sxs-lookup"><span data-stu-id="07224-314">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="07224-315">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="07224-315">MissingAttribute</span></span> |<span data-ttu-id="07224-316">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span><span class="sxs-lookup"><span data-stu-id="07224-316">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="07224-317">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="07224-317">RetryRequestedByTarget</span></span> |<span data-ttu-id="07224-318">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span><span class="sxs-lookup"><span data-stu-id="07224-318">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="07224-319">An attempt to resynchronize the user's password hash is made.</span><span class="sxs-lookup"><span data-stu-id="07224-319">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="07224-320">Scripts to help troubleshooting</span><span class="sxs-lookup"><span data-stu-id="07224-320">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="07224-321">Get the status of password sync settings</span><span class="sxs-lookup"><span data-stu-id="07224-321">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="07224-322">Trigger a full sync of all passwords</span><span class="sxs-lookup"><span data-stu-id="07224-322">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="07224-323">Run this script only once.</span><span class="sxs-lookup"><span data-stu-id="07224-323">Run this script only once.</span></span> <span data-ttu-id="07224-324">If you need to run it more than once, something else is the problem.</span><span class="sxs-lookup"><span data-stu-id="07224-324">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="07224-325">To troubleshoot the problem, contact Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="07224-325">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="07224-326">You can trigger a full sync of all passwords by using the following script:</span><span class="sxs-lookup"><span data-stu-id="07224-326">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="07224-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="07224-327">Next steps</span></span>
* [<span data-ttu-id="07224-328">Implementing password hash synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="07224-328">Implementing password hash synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-hash-synchronization.md)
* [<span data-ttu-id="07224-329">Azure AD Connect Sync: Customizing synchronization options</span><span class="sxs-lookup"><span data-stu-id="07224-329">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="07224-330">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07224-330">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
