---
title: 'Azure AD Connect sync:  Changing the AD DS account password | Microsoft Docs'
description: This topic document describes how to update Azure AD Connect after the password of the AD DS account is changed.
services: active-directory
keywords: AD DS account, Active Directory account, password
documentationcenter: ''
author: cychua
manager: femila
editor: ''
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: billmath
ms.openlocfilehash: 513f11142e19ee8f674c7907b144d7088f39950a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670255"
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="aeb81-104">Changing the AD DS account password</span><span class="sxs-lookup"><span data-stu-id="aeb81-104">Changing the AD DS account password</span></span>
<span data-ttu-id="aeb81-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aeb81-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="aeb81-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span><span class="sxs-lookup"><span data-stu-id="aeb81-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="aeb81-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span><span class="sxs-lookup"><span data-stu-id="aeb81-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="aeb81-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span><span class="sxs-lookup"><span data-stu-id="aeb81-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="aeb81-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span><span class="sxs-lookup"><span data-stu-id="aeb81-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="aeb81-110">How to update the Synchronization Service with new password for AD DS account</span><span class="sxs-lookup"><span data-stu-id="aeb81-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="aeb81-111">To update the Synchronization Service with the new password:</span><span class="sxs-lookup"><span data-stu-id="aeb81-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="aeb81-112">Start the Synchronization Service Manager (START → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="aeb81-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="aeb81-113">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="aeb81-113">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="aeb81-114">Go to the **Connectors** tab.</span><span class="sxs-lookup"><span data-stu-id="aeb81-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="aeb81-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span><span class="sxs-lookup"><span data-stu-id="aeb81-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="aeb81-116">Under **Actions**, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="aeb81-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="aeb81-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span><span class="sxs-lookup"><span data-stu-id="aeb81-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="aeb81-118">Enter the new password of the AD DS account in the **Password** textbox.</span><span class="sxs-lookup"><span data-stu-id="aeb81-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="aeb81-119">Click **OK** to save the new password and close the pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="aeb81-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="aeb81-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span><span class="sxs-lookup"><span data-stu-id="aeb81-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="aeb81-121">This is to ensure that any reference to the old password is removed from the memory cache.</span><span class="sxs-lookup"><span data-stu-id="aeb81-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb81-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="aeb81-122">Next steps</span></span>
<span data-ttu-id="aeb81-123">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="aeb81-123">**Overview topics**</span></span>

* [<span data-ttu-id="aeb81-124">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="aeb81-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="aeb81-125">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aeb81-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

