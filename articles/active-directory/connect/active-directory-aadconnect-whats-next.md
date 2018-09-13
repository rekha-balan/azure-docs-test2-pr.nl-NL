---
title: 'Azure AD Connect: Next steps and how to manage Azure AD Connect | Microsoft Docs'
description: Learn how to extend the default configuration and operational tasks for Azure AD Connect.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: e53bcecd67cdfd0ae53cfc9f244c06a8d5bae5dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670442"
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="8ddb2-103">Next steps and how to manage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8ddb2-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="8ddb2-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="8ddb2-105">Add additional sync admins</span><span class="sxs-lookup"><span data-stu-id="8ddb2-105">Add additional sync admins</span></span>
<span data-ttu-id="8ddb2-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="8ddb2-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="8ddb2-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span><span class="sxs-lookup"><span data-stu-id="8ddb2-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="8ddb2-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="8ddb2-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span><span class="sxs-lookup"><span data-stu-id="8ddb2-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="8ddb2-111">Sign in to the Azure portal as an admin.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="8ddb2-112">On the left, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="8ddb2-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="8ddb2-114">At the top of the directory page, select **Licenses**.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="8ddb2-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="8ddb2-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="8ddb2-117">Verify the scheduled synchronization task</span><span class="sxs-lookup"><span data-stu-id="8ddb2-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="8ddb2-118">Use the Azure portal to check the status of a synchronization.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="8ddb2-119">To verify the scheduled synchronization task</span><span class="sxs-lookup"><span data-stu-id="8ddb2-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="8ddb2-120">Sign in to the Azure portal as an admin.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="8ddb2-121">On the left, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="8ddb2-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="8ddb2-123">At the top of the directory page, select **Directory Integration**.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="8ddb2-124">Under **integration with local active directory**, note the last sync time.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="8ddb2-125"><center>![Directory sync time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="8ddb2-125"><center>![Directory sync time](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="8ddb2-126">Start a scheduled synchronization task</span><span class="sxs-lookup"><span data-stu-id="8ddb2-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="8ddb2-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="8ddb2-128">You need to provide your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="8ddb2-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="8ddb2-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="8ddb2-131"><center>![Start synchronization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="8ddb2-131"><center>![Start synchronization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="8ddb2-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="8ddb2-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="8ddb2-133">Additional tasks available in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8ddb2-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="8ddb2-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="8ddb2-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="8ddb2-136">The following table provides a summary of these tasks and a brief description of each task.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![List of additional tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="8ddb2-138">Additional task</span><span class="sxs-lookup"><span data-stu-id="8ddb2-138">Additional task</span></span> | <span data-ttu-id="8ddb2-139">Description</span><span class="sxs-lookup"><span data-stu-id="8ddb2-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ddb2-140">**View the selected scenario**</span><span class="sxs-lookup"><span data-stu-id="8ddb2-140">**View the selected scenario**</span></span> |<span data-ttu-id="8ddb2-141">View your current Azure AD Connect solution.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="8ddb2-142">This includes general settings, synchronized directories, and sync settings.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="8ddb2-143">**Customize synchronization options**</span><span class="sxs-lookup"><span data-stu-id="8ddb2-143">**Customize synchronization options**</span></span> |<span data-ttu-id="8ddb2-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="8ddb2-145">**Enable Staging Mode**</span><span class="sxs-lookup"><span data-stu-id="8ddb2-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="8ddb2-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="8ddb2-147">With this feature, you can preview the synchronizations before they occur.</span><span class="sxs-lookup"><span data-stu-id="8ddb2-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ddb2-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ddb2-148">Next steps</span></span>
<span data-ttu-id="8ddb2-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="8ddb2-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>



