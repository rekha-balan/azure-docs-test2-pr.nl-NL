---
title: Troubleshoot password synchronization with Azure AD Connect sync | Microsoft Docs
description: Provides information about how to troubleshoot passowrd synchronziation problems
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: billmath
ms.openlocfilehash: f112a6897e6121f63481f38721636f44e59146a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549843"
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="a2c04-103">Troubleshoot password synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="a2c04-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="a2c04-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span><span class="sxs-lookup"><span data-stu-id="a2c04-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="a2c04-105">If passwords are not synchronizing as expected, it can either be for a subset of users or for all users.</span><span class="sxs-lookup"><span data-stu-id="a2c04-105">If passwords are not synchronizing as expected, it can either be for a subset of users or for all users.</span></span>

* <span data-ttu-id="a2c04-106">If you have an issue where no passwords are synchronized, see [Troubleshoot issues where no passwords are synchronized](#no-passwords-are-synchronized).</span><span class="sxs-lookup"><span data-stu-id="a2c04-106">If you have an issue where no passwords are synchronized, see [Troubleshoot issues where no passwords are synchronized](#no-passwords-are-synchronized).</span></span>
* <span data-ttu-id="a2c04-107">If you have an issue with individual objects, then see [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords).</span><span class="sxs-lookup"><span data-stu-id="a2c04-107">If you have an issue with individual objects, then see [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords).</span></span>

## <a name="no-passwords-are-synchronized"></a><span data-ttu-id="a2c04-108">No passwords are synchronized</span><span class="sxs-lookup"><span data-stu-id="a2c04-108">No passwords are synchronized</span></span>
<span data-ttu-id="a2c04-109">Follow these steps to figure out why no passwords are synchronized:</span><span class="sxs-lookup"><span data-stu-id="a2c04-109">Follow these steps to figure out why no passwords are synchronized:</span></span>

1. <span data-ttu-id="a2c04-110">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="a2c04-110">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="a2c04-111">A server in staging mode does not synchronize any passwords.</span><span class="sxs-lookup"><span data-stu-id="a2c04-111">A server in staging mode does not synchronize any passwords.</span></span>
2. <span data-ttu-id="a2c04-112">Run the script in the section [Get the status of password sync settings](#get-the-status-of-password-sync-settings).</span><span class="sxs-lookup"><span data-stu-id="a2c04-112">Run the script in the section [Get the status of password sync settings](#get-the-status-of-password-sync-settings).</span></span> <span data-ttu-id="a2c04-113">It gives you an overview of the password sync configuration.</span><span class="sxs-lookup"><span data-stu-id="a2c04-113">It gives you an overview of the password sync configuration.</span></span>  
<span data-ttu-id="a2c04-114">![PowerShell script output from password sync settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-114">![PowerShell script output from password sync settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)</span></span>  
3. <span data-ttu-id="a2c04-115">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, then run the Connect installation wizard.</span><span class="sxs-lookup"><span data-stu-id="a2c04-115">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, then run the Connect installation wizard.</span></span> <span data-ttu-id="a2c04-116">Select **Customize synchronization options** and unselect password sync. This change temporarily disables the feature.</span><span class="sxs-lookup"><span data-stu-id="a2c04-116">Select **Customize synchronization options** and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="a2c04-117">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span><span class="sxs-lookup"><span data-stu-id="a2c04-117">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>
4. <span data-ttu-id="a2c04-118">Look in the eventlog for errors.</span><span class="sxs-lookup"><span data-stu-id="a2c04-118">Look in the eventlog for errors.</span></span> <span data-ttu-id="a2c04-119">Look for the following events, which would indicate a problem:</span><span class="sxs-lookup"><span data-stu-id="a2c04-119">Look for the following events, which would indicate a problem:</span></span>
    1. <span data-ttu-id="a2c04-120">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these, you have a connectivity problem.</span><span class="sxs-lookup"><span data-stu-id="a2c04-120">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these, you have a connectivity problem.</span></span> <span data-ttu-id="a2c04-121">The eventlog message contains forest information where you have a problem.</span><span class="sxs-lookup"><span data-stu-id="a2c04-121">The eventlog message contains forest information where you have a problem.</span></span> <span data-ttu-id="a2c04-122">For more information, see [Connectivity problem](#connectivity problem)</span><span class="sxs-lookup"><span data-stu-id="a2c04-122">For more information, see [Connectivity problem](#connectivity problem)</span></span>
5. <span data-ttu-id="a2c04-123">If you see no heartbeat or if nothing else worked, then run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="a2c04-123">If you see no heartbeat or if nothing else worked, then run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="a2c04-124">You should only run this script once.</span><span class="sxs-lookup"><span data-stu-id="a2c04-124">You should only run this script once.</span></span>
6. <span data-ttu-id="a2c04-125">Read the section [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords).</span><span class="sxs-lookup"><span data-stu-id="a2c04-125">Read the section [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords).</span></span>

### <a name="connectivity-problem"></a><span data-ttu-id="a2c04-126">Connectivity problem</span><span class="sxs-lookup"><span data-stu-id="a2c04-126">Connectivity problem</span></span>

1. <span data-ttu-id="a2c04-127">Do you have connectivity with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2c04-127">Do you have connectivity with Azure AD.</span></span>
2. <span data-ttu-id="a2c04-128">Does the account have required permissions to read the password hashes in all domains?</span><span class="sxs-lookup"><span data-stu-id="a2c04-128">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="a2c04-129">If you installed Connect using Express settings, the permissions should already be correct.</span><span class="sxs-lookup"><span data-stu-id="a2c04-129">If you installed Connect using Express settings, the permissions should already be correct.</span></span> <span data-ttu-id="a2c04-130">If you used custom install, you need to set the permissions manually.</span><span class="sxs-lookup"><span data-stu-id="a2c04-130">If you used custom install, you need to set the permissions manually.</span></span>
    1. <span data-ttu-id="a2c04-131">To find the account used by the Active Directory Connector, start **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-131">To find the account used by the Active Directory Connector, start **Synchronization Service Manager**.</span></span> <span data-ttu-id="a2c04-132">Go to **Connectors** and find the on-premises Active Directory forest you are troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a2c04-132">Go to **Connectors** and find the on-premises Active Directory forest you are troubleshooting.</span></span> <span data-ttu-id="a2c04-133">Select the Connector and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-133">Select the Connector and click **Properties**.</span></span> <span data-ttu-id="a2c04-134">Go to **Connect to Active Directory Forest**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-134">Go to **Connect to Active Directory Forest**.</span></span>  
    <span data-ttu-id="a2c04-135">![Account used by AD Connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-135">![Account used by AD Connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)</span></span>  
    <span data-ttu-id="a2c04-136">Take a note of the username and the domain the account is located in.</span><span class="sxs-lookup"><span data-stu-id="a2c04-136">Take a note of the username and the domain the account is located in.</span></span>
    2. <span data-ttu-id="a2c04-137">Start **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-137">Start **Active Directory Users and Computers**.</span></span> <span data-ttu-id="a2c04-138">Verify that the account you found in the previous steps have the follow permissions set at the root of all domains in your forest:</span><span class="sxs-lookup"><span data-stu-id="a2c04-138">Verify that the account you found in the previous steps have the follow permissions set at the root of all domains in your forest:</span></span>
        * <span data-ttu-id="a2c04-139">Replicate Directory Changes</span><span class="sxs-lookup"><span data-stu-id="a2c04-139">Replicate Directory Changes</span></span>
        * <span data-ttu-id="a2c04-140">Replicate Directory Changes All</span><span class="sxs-lookup"><span data-stu-id="a2c04-140">Replicate Directory Changes All</span></span>
3. <span data-ttu-id="a2c04-141">Are the domain controllers reachable by Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="a2c04-141">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="a2c04-142">If the Connect server cannot connect to all domain controllers, then you should configure **Only use preferred domain controller**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-142">If the Connect server cannot connect to all domain controllers, then you should configure **Only use preferred domain controller**.</span></span>  
    <span data-ttu-id="a2c04-143">![Domain controller used by AD Connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-143">![Domain controller used by AD Connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)</span></span>  
    <span data-ttu-id="a2c04-144">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-144">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> <span data-ttu-id="a2c04-145">Select your domain in **Select directory partitions**, select the checkbox **Only use preferred domain controllers**, and click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-145">Select your domain in **Select directory partitions**, select the checkbox **Only use preferred domain controllers**, and click **Configure**.</span></span> <span data-ttu-id="a2c04-146">In the list, enter the domain controllers Connect should use for password sync. The same list is used for import and export as well.</span><span class="sxs-lookup"><span data-stu-id="a2c04-146">In the list, enter the domain controllers Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="a2c04-147">Do these steps for all your domains.</span><span class="sxs-lookup"><span data-stu-id="a2c04-147">Do these steps for all your domains.</span></span>
4. <span data-ttu-id="a2c04-148">If the script shows that there is no heartbeat, then run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="a2c04-148">If the script shows that there is no heartbeat, then run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords"></a><span data-ttu-id="a2c04-149">One object is not synchronizing passwords</span><span class="sxs-lookup"><span data-stu-id="a2c04-149">One object is not synchronizing passwords</span></span>
<span data-ttu-id="a2c04-150">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span><span class="sxs-lookup"><span data-stu-id="a2c04-150">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="a2c04-151">Start in **Active Directory Users and Computers**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-151">Start in **Active Directory Users and Computers**.</span></span> <span data-ttu-id="a2c04-152">Find the user and verify that **User must change password at next logon** is unselected.</span><span class="sxs-lookup"><span data-stu-id="a2c04-152">Find the user and verify that **User must change password at next logon** is unselected.</span></span>  
<span data-ttu-id="a2c04-153">![Active Directory productive passwords](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-153">![Active Directory productive passwords](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)</span></span>  
<span data-ttu-id="a2c04-154">If it is selected, then ask the user to sign in and change the password.</span><span class="sxs-lookup"><span data-stu-id="a2c04-154">If it is selected, then ask the user to sign in and change the password.</span></span> <span data-ttu-id="a2c04-155">Temporary passwords are not synchronized to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2c04-155">Temporary passwords are not synchronized to Azure AD.</span></span>
2. <span data-ttu-id="a2c04-156">If it looks correct in Active Directory, then the next step is to follow the user in the sync engine.</span><span class="sxs-lookup"><span data-stu-id="a2c04-156">If it looks correct in Active Directory, then the next step is to follow the user in the sync engine.</span></span> <span data-ttu-id="a2c04-157">By following the user from on-premises Active Directory to Azure AD, you can see if there is a descriptive error on the object.</span><span class="sxs-lookup"><span data-stu-id="a2c04-157">By following the user from on-premises Active Directory to Azure AD, you can see if there is a descriptive error on the object.</span></span>
    1. <span data-ttu-id="a2c04-158">Start the **[Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-158">Start the **[Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md)**.</span></span>
    2. <span data-ttu-id="a2c04-159">Click **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-159">Click **Connectors**.</span></span>
    3. <span data-ttu-id="a2c04-160">Select the **Active Directory Connector** the user is located in.</span><span class="sxs-lookup"><span data-stu-id="a2c04-160">Select the **Active Directory Connector** the user is located in.</span></span>
    4. <span data-ttu-id="a2c04-161">Select **Search Connector Space**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-161">Select **Search Connector Space**.</span></span>
    5. <span data-ttu-id="a2c04-162">In **Scope**, select **DN or anchor**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-162">In **Scope**, select **DN or anchor**.</span></span> <span data-ttu-id="a2c04-163">Enter the full DN of the user you are troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a2c04-163">Enter the full DN of the user you are troubleshooting.</span></span>
    <span data-ttu-id="a2c04-164">![Search for user in cs with DN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-164">![Search for user in cs with DN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)</span></span>  
    6. <span data-ttu-id="a2c04-165">Locate the user you are looking for and click **Properties** to see all attributes.</span><span class="sxs-lookup"><span data-stu-id="a2c04-165">Locate the user you are looking for and click **Properties** to see all attributes.</span></span> <span data-ttu-id="a2c04-166">If the user is not in the search result, then verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span><span class="sxs-lookup"><span data-stu-id="a2c04-166">If the user is not in the search result, then verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>
    7. <span data-ttu-id="a2c04-167">To see the password sync details of the object for the past week, click **Log...**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-167">To see the password sync details of the object for the past week, click **Log...**.</span></span>  
    <span data-ttu-id="a2c04-168">![Object log details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-168">![Object log details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)</span></span>  
    <span data-ttu-id="a2c04-169">If the object log is empty, then Azure AD Connect has not been able to read the password hash from Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a2c04-169">If the object log is empty, then Azure AD Connect has not been able to read the password hash from Active Directory.</span></span> <span data-ttu-id="a2c04-170">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="a2c04-170">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="a2c04-171">If you see any other value than **success**, then refer to the table in [Password sync log](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="a2c04-171">If you see any other value than **success**, then refer to the table in [Password sync log](#password-sync-log).</span></span>
    8. <span data-ttu-id="a2c04-172">Select the **lineage** tab and make sure that at least one Sync Rule shows **Password Sync** as **True**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-172">Select the **lineage** tab and make sure that at least one Sync Rule shows **Password Sync** as **True**.</span></span> <span data-ttu-id="a2c04-173">In the default configuration, the name of the Sync Rule is **In from AD - User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-173">In the default configuration, the name of the Sync Rule is **In from AD - User AccountEnabled**.</span></span>  
    <span data-ttu-id="a2c04-174">![Lineage information about a user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-174">![Lineage information about a user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)</span></span>  
    9. <span data-ttu-id="a2c04-175">Click **Metaverse Object Properties**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-175">Click **Metaverse Object Properties**.</span></span> <span data-ttu-id="a2c04-176">You see a list of attributes in the user.</span><span class="sxs-lookup"><span data-stu-id="a2c04-176">You see a list of attributes in the user.</span></span>  
    <span data-ttu-id="a2c04-177">![Metaverse information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-177">![Metaverse information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)</span></span>  
    <span data-ttu-id="a2c04-178">Verify that there is no attribute **cloudFiltered** present.</span><span class="sxs-lookup"><span data-stu-id="a2c04-178">Verify that there is no attribute **cloudFiltered** present.</span></span> <span data-ttu-id="a2c04-179">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span><span class="sxs-lookup"><span data-stu-id="a2c04-179">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>
    10. <span data-ttu-id="a2c04-180">Click the tab **Connectors**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-180">Click the tab **Connectors**.</span></span> <span data-ttu-id="a2c04-181">Make sure you see connectors to both your on-premises AD and to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2c04-181">Make sure you see connectors to both your on-premises AD and to Azure AD.</span></span>
    <span data-ttu-id="a2c04-182">![Metaverse information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-182">![Metaverse information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)</span></span>  
    11. <span data-ttu-id="a2c04-183">Select the row representing Azure AD and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-183">Select the row representing Azure AD and click **Properties**.</span></span> <span data-ttu-id="a2c04-184">Click the tab **Lineage**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-184">Click the tab **Lineage**.</span></span> <span data-ttu-id="a2c04-185">The connector space object should have an outbound rule with **Password Sync** set to **True**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-185">The connector space object should have an outbound rule with **Password Sync** set to **True**.</span></span> <span data-ttu-id="a2c04-186">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-186">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  
    <span data-ttu-id="a2c04-187">![Connector space properties of a user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)</span><span class="sxs-lookup"><span data-stu-id="a2c04-187">![Connector space properties of a user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)</span></span>  

### <a name="password-sync-log"></a><span data-ttu-id="a2c04-188">Password sync log</span><span class="sxs-lookup"><span data-stu-id="a2c04-188">Password sync log</span></span>
<span data-ttu-id="a2c04-189">The status column can have the following values:</span><span class="sxs-lookup"><span data-stu-id="a2c04-189">The status column can have the following values:</span></span>

| <span data-ttu-id="a2c04-190">Status</span><span class="sxs-lookup"><span data-stu-id="a2c04-190">Status</span></span> | <span data-ttu-id="a2c04-191">Description</span><span class="sxs-lookup"><span data-stu-id="a2c04-191">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2c04-192">Success</span><span class="sxs-lookup"><span data-stu-id="a2c04-192">Success</span></span> |<span data-ttu-id="a2c04-193">Password has been successfully synchronized.</span><span class="sxs-lookup"><span data-stu-id="a2c04-193">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="a2c04-194">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="a2c04-194">FilteredByTarget</span></span> |<span data-ttu-id="a2c04-195">Password is set to **User must change password at next logon**.</span><span class="sxs-lookup"><span data-stu-id="a2c04-195">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="a2c04-196">Password has not been synchronized.</span><span class="sxs-lookup"><span data-stu-id="a2c04-196">Password has not been synchronized.</span></span> |
| <span data-ttu-id="a2c04-197">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="a2c04-197">NoTargetConnection</span></span> |<span data-ttu-id="a2c04-198">No object in the metaverse or in the Azure AD connector space.</span><span class="sxs-lookup"><span data-stu-id="a2c04-198">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="a2c04-199">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="a2c04-199">SourceConnectorNotPresent</span></span> |<span data-ttu-id="a2c04-200">No object found in the on-premises Active Directory connector space.</span><span class="sxs-lookup"><span data-stu-id="a2c04-200">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="a2c04-201">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="a2c04-201">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="a2c04-202">The object in the Azure AD connector space has not yet been exported.</span><span class="sxs-lookup"><span data-stu-id="a2c04-202">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="a2c04-203">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="a2c04-203">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="a2c04-204">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span><span class="sxs-lookup"><span data-stu-id="a2c04-204">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="a2c04-205">Scripts to help troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a2c04-205">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="a2c04-206">Get the status of password sync settings</span><span class="sxs-lookup"><span data-stu-id="a2c04-206">Get the status of password sync settings</span></span>
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="a2c04-207">Trigger a full sync of all passwords</span><span class="sxs-lookup"><span data-stu-id="a2c04-207">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="a2c04-208">You should only run this script once.</span><span class="sxs-lookup"><span data-stu-id="a2c04-208">You should only run this script once.</span></span> <span data-ttu-id="a2c04-209">If you need to run it more than once, then something else is the problem.</span><span class="sxs-lookup"><span data-stu-id="a2c04-209">If you need to run it more than once, then something else is the problem.</span></span> <span data-ttu-id="a2c04-210">Contact Microsoft support to help troubleshoot the problem.</span><span class="sxs-lookup"><span data-stu-id="a2c04-210">Contact Microsoft support to help troubleshoot the problem.</span></span>

<span data-ttu-id="a2c04-211">You can trigger a full sync of all passwords using the following script:</span><span class="sxs-lookup"><span data-stu-id="a2c04-211">You can trigger a full sync of all passwords using the following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a2c04-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2c04-212">Next steps</span></span>
* [<span data-ttu-id="a2c04-213">Implementing password synchronization with Azure AD Connect sync</span><span class="sxs-lookup"><span data-stu-id="a2c04-213">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="a2c04-214">Azure AD Connect Sync: Customizing Synchronization options</span><span class="sxs-lookup"><span data-stu-id="a2c04-214">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="a2c04-215">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2c04-215">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)










