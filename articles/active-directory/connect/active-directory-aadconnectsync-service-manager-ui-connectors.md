---
title: Connectors in the Azure AD Synchronization Service Manager UI | Microsoft Docs'
description: Understand the Connectors tab in the Synchronization Service Manager for Azure AD Connect.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 947fab549fb8834cf2cd5149ebb6b3b23b11053b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551769"
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="656a0-103">Using connectors with the Azure AD Connect Sync Service Manager</span><span class="sxs-lookup"><span data-stu-id="656a0-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="656a0-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span><span class="sxs-lookup"><span data-stu-id="656a0-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="656a0-106">Connector actions</span><span class="sxs-lookup"><span data-stu-id="656a0-106">Connector actions</span></span>
| <span data-ttu-id="656a0-107">Action</span><span class="sxs-lookup"><span data-stu-id="656a0-107">Action</span></span> | <span data-ttu-id="656a0-108">Comment</span><span class="sxs-lookup"><span data-stu-id="656a0-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="656a0-109">Create</span><span class="sxs-lookup"><span data-stu-id="656a0-109">Create</span></span> |<span data-ttu-id="656a0-110">Do not use.</span><span class="sxs-lookup"><span data-stu-id="656a0-110">Do not use.</span></span> <span data-ttu-id="656a0-111">For connecting to additional AD forests, use the installation wizard.</span><span class="sxs-lookup"><span data-stu-id="656a0-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="656a0-112">Properties</span><span class="sxs-lookup"><span data-stu-id="656a0-112">Properties</span></span> |<span data-ttu-id="656a0-113">Used for domain and OU filtering.</span><span class="sxs-lookup"><span data-stu-id="656a0-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="656a0-114">Delete</span><span class="sxs-lookup"><span data-stu-id="656a0-114">Delete</span></span>](#delete) |<span data-ttu-id="656a0-115">Used to either delete the data in the connector space or to delete connection to a forest.</span><span class="sxs-lookup"><span data-stu-id="656a0-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="656a0-116">Configure Run Profiles</span><span class="sxs-lookup"><span data-stu-id="656a0-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="656a0-117">Except for domain filtering, nothing to configure here.</span><span class="sxs-lookup"><span data-stu-id="656a0-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="656a0-118">You can use this action to see already configured run profiles.</span><span class="sxs-lookup"><span data-stu-id="656a0-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="656a0-119">Run</span><span class="sxs-lookup"><span data-stu-id="656a0-119">Run</span></span> |<span data-ttu-id="656a0-120">Used to start a one-off run of a profile.</span><span class="sxs-lookup"><span data-stu-id="656a0-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="656a0-121">Stop</span><span class="sxs-lookup"><span data-stu-id="656a0-121">Stop</span></span> |<span data-ttu-id="656a0-122">Stops a Connector currently running a profile.</span><span class="sxs-lookup"><span data-stu-id="656a0-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="656a0-123">Export Connector</span><span class="sxs-lookup"><span data-stu-id="656a0-123">Export Connector</span></span> |<span data-ttu-id="656a0-124">Do not use.</span><span class="sxs-lookup"><span data-stu-id="656a0-124">Do not use.</span></span> |
| <span data-ttu-id="656a0-125">Import Connector</span><span class="sxs-lookup"><span data-stu-id="656a0-125">Import Connector</span></span> |<span data-ttu-id="656a0-126">Do not use.</span><span class="sxs-lookup"><span data-stu-id="656a0-126">Do not use.</span></span> |
| <span data-ttu-id="656a0-127">Update Connector</span><span class="sxs-lookup"><span data-stu-id="656a0-127">Update Connector</span></span> |<span data-ttu-id="656a0-128">Do not use.</span><span class="sxs-lookup"><span data-stu-id="656a0-128">Do not use.</span></span> |
| <span data-ttu-id="656a0-129">Refresh Schema</span><span class="sxs-lookup"><span data-stu-id="656a0-129">Refresh Schema</span></span> |<span data-ttu-id="656a0-130">Refreshes the cached schema.</span><span class="sxs-lookup"><span data-stu-id="656a0-130">Refreshes the cached schema.</span></span> <span data-ttu-id="656a0-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span><span class="sxs-lookup"><span data-stu-id="656a0-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="656a0-132">Search Connector Space</span><span class="sxs-lookup"><span data-stu-id="656a0-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="656a0-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="656a0-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="656a0-134">Delete</span><span class="sxs-lookup"><span data-stu-id="656a0-134">Delete</span></span>
<span data-ttu-id="656a0-135">The delete action is used for two different things.</span><span class="sxs-lookup"><span data-stu-id="656a0-135">The delete action is used for two different things.</span></span>  
![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="656a0-137">The option **Delete connector space only** removes all data, but keep the configuration.</span><span class="sxs-lookup"><span data-stu-id="656a0-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="656a0-138">The option **Delete Connector and connector space** removes the data and the configuration.</span><span class="sxs-lookup"><span data-stu-id="656a0-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="656a0-139">This option is used when you do not want to connect to a forest anymore.</span><span class="sxs-lookup"><span data-stu-id="656a0-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="656a0-140">Both options sync all objects and update the metaverse objects.</span><span class="sxs-lookup"><span data-stu-id="656a0-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="656a0-141">This action is a long running operation.</span><span class="sxs-lookup"><span data-stu-id="656a0-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="656a0-142">Configure Run Profiles</span><span class="sxs-lookup"><span data-stu-id="656a0-142">Configure Run Profiles</span></span>
<span data-ttu-id="656a0-143">This option allows you to see the run profiles configured for a Connector.</span><span class="sxs-lookup"><span data-stu-id="656a0-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="656a0-145">Search Connector Space</span><span class="sxs-lookup"><span data-stu-id="656a0-145">Search Connector Space</span></span>
<span data-ttu-id="656a0-146">The search connector space action is useful to find objects and troubleshoot data issues.</span><span class="sxs-lookup"><span data-stu-id="656a0-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="656a0-148">Start by selecting a **scope**.</span><span class="sxs-lookup"><span data-stu-id="656a0-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="656a0-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span><span class="sxs-lookup"><span data-stu-id="656a0-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="656a0-150">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="656a0-150">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="656a0-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span><span class="sxs-lookup"><span data-stu-id="656a0-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="656a0-152">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="656a0-152">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="656a0-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span><span class="sxs-lookup"><span data-stu-id="656a0-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="656a0-154">Changing the AD DS account password</span><span class="sxs-lookup"><span data-stu-id="656a0-154">Changing the AD DS account password</span></span>
<span data-ttu-id="656a0-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span><span class="sxs-lookup"><span data-stu-id="656a0-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="656a0-156">You may see the following:</span><span class="sxs-lookup"><span data-stu-id="656a0-156">You may see the following:</span></span>

- <span data-ttu-id="656a0-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span><span class="sxs-lookup"><span data-stu-id="656a0-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="656a0-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span><span class="sxs-lookup"><span data-stu-id="656a0-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="656a0-159">To resolve the issue, update the AD DS user account using the following:</span><span class="sxs-lookup"><span data-stu-id="656a0-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="656a0-160">Start the Synchronization Service Manager (START → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="656a0-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="656a0-161">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="656a0-161">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="656a0-162">Go to the **Connectors** tab.</span><span class="sxs-lookup"><span data-stu-id="656a0-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="656a0-163">Select the AD Connector which is configured to use the AD DS account.</span><span class="sxs-lookup"><span data-stu-id="656a0-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="656a0-164">Under Actions, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="656a0-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="656a0-165">In the pop-up dialog, select Connect to Active Directory Forest:</span><span class="sxs-lookup"><span data-stu-id="656a0-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="656a0-166">The Forest name indicates the corresponding on-prem AD.</span><span class="sxs-lookup"><span data-stu-id="656a0-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="656a0-167">The User name indicates the AD DS account used for synchronization.</span><span class="sxs-lookup"><span data-stu-id="656a0-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="656a0-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key6.PNG)</span><span class="sxs-lookup"><span data-stu-id="656a0-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key6.PNG)</span></span>
9. <span data-ttu-id="656a0-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span><span class="sxs-lookup"><span data-stu-id="656a0-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="656a0-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="656a0-170">Next steps</span></span>
<span data-ttu-id="656a0-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="656a0-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="656a0-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="656a0-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>








