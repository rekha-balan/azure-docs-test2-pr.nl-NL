---
title: Re-running the Azure AD Connect install wizard | Microsoft Docs
description: Explains how the installation wizard works the second time you run it.
keywords: The Azure AD Connect installation wizard lets you configure maintenance settings the second time you run it
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: billmath
ms.openlocfilehash: b03be52aab7b9bdb96f15af5687fcf799d1c9501
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671652"
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="f5c26-104">Azure AD Connect sync: Running the installation wizard a second time</span><span class="sxs-lookup"><span data-stu-id="f5c26-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="f5c26-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span><span class="sxs-lookup"><span data-stu-id="f5c26-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="f5c26-106">If you run the installation wizard again, it offers options for maintenance.</span><span class="sxs-lookup"><span data-stu-id="f5c26-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="f5c26-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="f5c26-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Start menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="f5c26-109">When you start the installation wizard, you see a page with these options:</span><span class="sxs-lookup"><span data-stu-id="f5c26-109">When you start the installation wizard, you see a page with these options:</span></span>

![Page with a list of additional tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="f5c26-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span><span class="sxs-lookup"><span data-stu-id="f5c26-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="f5c26-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="f5c26-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="f5c26-113">Select one of the tasks and click **Next** to continue.</span><span class="sxs-lookup"><span data-stu-id="f5c26-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5c26-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span><span class="sxs-lookup"><span data-stu-id="f5c26-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="f5c26-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span><span class="sxs-lookup"><span data-stu-id="f5c26-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="f5c26-116">View current configuration</span><span class="sxs-lookup"><span data-stu-id="f5c26-116">View current configuration</span></span>
<span data-ttu-id="f5c26-117">This option gives you a quick view of your currently configured options.</span><span class="sxs-lookup"><span data-stu-id="f5c26-117">This option gives you a quick view of your currently configured options.</span></span>

![Page with a list of all options and their state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="f5c26-119">Click **Previous** to go back.</span><span class="sxs-lookup"><span data-stu-id="f5c26-119">Click **Previous** to go back.</span></span> <span data-ttu-id="f5c26-120">If you select **Exit**, you close the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="f5c26-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="f5c26-121">Customize synchronization options</span><span class="sxs-lookup"><span data-stu-id="f5c26-121">Customize synchronization options</span></span>
<span data-ttu-id="f5c26-122">This option is used to make changes to the sync configuration.</span><span class="sxs-lookup"><span data-stu-id="f5c26-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="f5c26-123">You see a subset of options from the custom configuration installation path.</span><span class="sxs-lookup"><span data-stu-id="f5c26-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="f5c26-124">You see this option even if you used express installation initially.</span><span class="sxs-lookup"><span data-stu-id="f5c26-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="f5c26-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="f5c26-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="f5c26-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="f5c26-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="f5c26-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="f5c26-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="f5c26-128">Remove Group filtering.</span><span class="sxs-lookup"><span data-stu-id="f5c26-128">Remove Group filtering.</span></span>
* <span data-ttu-id="f5c26-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="f5c26-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="f5c26-130">The other options from the initial installation cannot be changed and are not available.</span><span class="sxs-lookup"><span data-stu-id="f5c26-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="f5c26-131">These options are:</span><span class="sxs-lookup"><span data-stu-id="f5c26-131">These options are:</span></span>

* <span data-ttu-id="f5c26-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="f5c26-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="f5c26-133">Change the joining method for objects from different forest.</span><span class="sxs-lookup"><span data-stu-id="f5c26-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="f5c26-134">Enable group-based filtering.</span><span class="sxs-lookup"><span data-stu-id="f5c26-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="f5c26-135">Refresh directory schema</span><span class="sxs-lookup"><span data-stu-id="f5c26-135">Refresh directory schema</span></span>
<span data-ttu-id="f5c26-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span><span class="sxs-lookup"><span data-stu-id="f5c26-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="f5c26-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span><span class="sxs-lookup"><span data-stu-id="f5c26-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="f5c26-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span><span class="sxs-lookup"><span data-stu-id="f5c26-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="f5c26-139">This action also regenerates the Sync Rules.</span><span class="sxs-lookup"><span data-stu-id="f5c26-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="f5c26-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f5c26-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="f5c26-141">When you select this option, all the directories in your configuration are listed.</span><span class="sxs-lookup"><span data-stu-id="f5c26-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="f5c26-142">You can keep the default setting and refresh all forests or unselect some of them.</span><span class="sxs-lookup"><span data-stu-id="f5c26-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Page with a list of all directories in the environment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="f5c26-144">Configure staging mode</span><span class="sxs-lookup"><span data-stu-id="f5c26-144">Configure staging mode</span></span>
<span data-ttu-id="f5c26-145">This option allows you to enable and disable staging mode on the server.</span><span class="sxs-lookup"><span data-stu-id="f5c26-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="f5c26-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="f5c26-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="f5c26-147">The option shows if staging is currently enabled or disabled:</span><span class="sxs-lookup"><span data-stu-id="f5c26-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Option that is also showing the current state of staging mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="f5c26-149">To change the state, select this option and select or unselect the checkbox.</span><span class="sxs-lookup"><span data-stu-id="f5c26-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Option that is also showing the current state of staging mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="f5c26-151">Change user sign-in</span><span class="sxs-lookup"><span data-stu-id="f5c26-151">Change user sign-in</span></span>
<span data-ttu-id="f5c26-152">This option allows you to change from password sync to federation or the other way around.</span><span class="sxs-lookup"><span data-stu-id="f5c26-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="f5c26-153">You cannot change to **do not configure**.</span><span class="sxs-lookup"><span data-stu-id="f5c26-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="f5c26-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="f5c26-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5c26-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5c26-155">Next steps</span></span>
* <span data-ttu-id="f5c26-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="f5c26-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="f5c26-157">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="f5c26-157">**Overview topics**</span></span>

* [<span data-ttu-id="f5c26-158">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="f5c26-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="f5c26-159">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5c26-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)






