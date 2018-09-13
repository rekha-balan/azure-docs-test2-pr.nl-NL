---
title: 'Azure AD Connect sync:  Changing the Azure AD Connect Sync service account | Microsoft Docs'
description: This topic document describes the encryption key and how to abandon it after the password is changed.
services: active-directory
keywords: Azure AD sync service account, password
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
ms.date: 04/03/2017
ms.author: billmath
ms.openlocfilehash: 686e4379091435e8c8afa56ec2d4fac8485b1ff6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663078"
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="078a2-104">Changing the Azure AD Connect sync service account password</span><span class="sxs-lookup"><span data-stu-id="078a2-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="078a2-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span><span class="sxs-lookup"><span data-stu-id="078a2-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="078a2-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span><span class="sxs-lookup"><span data-stu-id="078a2-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="078a2-107">These accounts are encrypted before they are stored in the database.</span><span class="sxs-lookup"><span data-stu-id="078a2-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="078a2-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="078a2-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="078a2-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span><span class="sxs-lookup"><span data-stu-id="078a2-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="078a2-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span><span class="sxs-lookup"><span data-stu-id="078a2-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="078a2-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span><span class="sxs-lookup"><span data-stu-id="078a2-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="078a2-112">Issues that arise from changing the password</span><span class="sxs-lookup"><span data-stu-id="078a2-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="078a2-113">There are two things that need to be done when you change the service account password.</span><span class="sxs-lookup"><span data-stu-id="078a2-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="078a2-114">First, you need to change the password under the Windows Service Control Manager.</span><span class="sxs-lookup"><span data-stu-id="078a2-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="078a2-115">Until this issue is resolved you will see following errors:</span><span class="sxs-lookup"><span data-stu-id="078a2-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="078a2-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span><span class="sxs-lookup"><span data-stu-id="078a2-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="078a2-117">**Error 1069: The service did not start due to a logon failure.**"</span><span class="sxs-lookup"><span data-stu-id="078a2-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="078a2-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span><span class="sxs-lookup"><span data-stu-id="078a2-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="078a2-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span><span class="sxs-lookup"><span data-stu-id="078a2-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="078a2-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="078a2-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="078a2-121">You will see errors such as:</span><span class="sxs-lookup"><span data-stu-id="078a2-121">You will see errors such as:</span></span>

- <span data-ttu-id="078a2-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “\*\*Windows could not start the Microsoft Azure AD Sync on Local Computer.</span><span class="sxs-lookup"><span data-stu-id="078a2-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “\*\*Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="078a2-123">For more information, review the System Event log.</span><span class="sxs-lookup"><span data-stu-id="078a2-123">For more information, review the System Event log.</span></span> <span data-ttu-id="078a2-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code \*\*-21451857952\*\*\*\*.”</span><span class="sxs-lookup"><span data-stu-id="078a2-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code \*\*-21451857952\*\*\*\*.”</span></span>
- <span data-ttu-id="078a2-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span><span class="sxs-lookup"><span data-stu-id="078a2-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="078a2-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span><span class="sxs-lookup"><span data-stu-id="078a2-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="078a2-127">Abandoning the Azure AD Connect Sync encryption key</span><span class="sxs-lookup"><span data-stu-id="078a2-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="078a2-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span><span class="sxs-lookup"><span data-stu-id="078a2-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="078a2-129">Use the following procedures to abandon the encryption key.</span><span class="sxs-lookup"><span data-stu-id="078a2-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="078a2-130">What to do if you need to abandon the encryption key</span><span class="sxs-lookup"><span data-stu-id="078a2-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="078a2-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span><span class="sxs-lookup"><span data-stu-id="078a2-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="078a2-132">Abandon the existing encryption key</span><span class="sxs-lookup"><span data-stu-id="078a2-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="078a2-133">Provide the password of the AD DS account</span><span class="sxs-lookup"><span data-stu-id="078a2-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="078a2-134">Reinitialize the password of the Azure AD sync account</span><span class="sxs-lookup"><span data-stu-id="078a2-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="078a2-135">Start the Synchronization Service</span><span class="sxs-lookup"><span data-stu-id="078a2-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="078a2-136">Abandon the existing encryption key</span><span class="sxs-lookup"><span data-stu-id="078a2-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="078a2-137">Abandon the existing encryption key so that new encryption key can be created:</span><span class="sxs-lookup"><span data-stu-id="078a2-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="078a2-138">Log in to your Azure AD Connect Server as administrator.</span><span class="sxs-lookup"><span data-stu-id="078a2-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="078a2-139">Start a new PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="078a2-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="078a2-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="078a2-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="078a2-141">Run the command: `./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="078a2-141">Run the command: `./miiskmu.exe /a`</span></span>

![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key5.PNG)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="078a2-143">Provide the password of the AD DS account</span><span class="sxs-lookup"><span data-stu-id="078a2-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="078a2-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span><span class="sxs-lookup"><span data-stu-id="078a2-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="078a2-145">The Synchronization Service encrypts the passwords using the new encryption key:</span><span class="sxs-lookup"><span data-stu-id="078a2-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="078a2-146">Start the Synchronization Service Manager (START → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="078a2-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="078a2-147">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="078a2-147">![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="078a2-148">Go to the **Connectors** tab.</span><span class="sxs-lookup"><span data-stu-id="078a2-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="078a2-149">Select the **AD Connector** that corresponds to your on-premises AD.</span><span class="sxs-lookup"><span data-stu-id="078a2-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="078a2-150">If you have more than one AD connector, repeat the following steps for each of them.</span><span class="sxs-lookup"><span data-stu-id="078a2-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="078a2-151">Under **Actions**, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="078a2-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="078a2-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span><span class="sxs-lookup"><span data-stu-id="078a2-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="078a2-153">Enter the password of the AD DS account in the **Password** textbox.</span><span class="sxs-lookup"><span data-stu-id="078a2-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="078a2-154">If you do not know its password, you must set it to a known value before performing this step.</span><span class="sxs-lookup"><span data-stu-id="078a2-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="078a2-155">Click **OK** to save the new password and close the pop-up dialog.</span><span class="sxs-lookup"><span data-stu-id="078a2-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="078a2-156">![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key6.PNG)</span><span class="sxs-lookup"><span data-stu-id="078a2-156">![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key6.PNG)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="078a2-157">Reinitialize the password of the Azure AD sync account</span><span class="sxs-lookup"><span data-stu-id="078a2-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="078a2-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span><span class="sxs-lookup"><span data-stu-id="078a2-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="078a2-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span><span class="sxs-lookup"><span data-stu-id="078a2-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="078a2-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span><span class="sxs-lookup"><span data-stu-id="078a2-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="078a2-161">Start a new PowerShell session on the Azure AD Connect server.</span><span class="sxs-lookup"><span data-stu-id="078a2-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="078a2-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="078a2-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="078a2-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="078a2-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="078a2-164">![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key7.PNG)</span><span class="sxs-lookup"><span data-stu-id="078a2-164">![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key7.PNG)</span></span>
4. <span data-ttu-id="078a2-165">If it is successful, you will see the PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="078a2-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="078a2-166">Start the Synchronization Service</span><span class="sxs-lookup"><span data-stu-id="078a2-166">Start the Synchronization Service</span></span>
<span data-ttu-id="078a2-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span><span class="sxs-lookup"><span data-stu-id="078a2-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="078a2-168">Go to Windows Service Control Manager (START → Services).</span><span class="sxs-lookup"><span data-stu-id="078a2-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="078a2-169">Select **Microsoft Azure AD Sync** and click Restart.</span><span class="sxs-lookup"><span data-stu-id="078a2-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="078a2-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="078a2-170">Next steps</span></span>
<span data-ttu-id="078a2-171">**Overview topics**</span><span class="sxs-lookup"><span data-stu-id="078a2-171">**Overview topics**</span></span>

* [<span data-ttu-id="078a2-172">Azure AD Connect sync: Understand and customize synchronization</span><span class="sxs-lookup"><span data-stu-id="078a2-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="078a2-173">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="078a2-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)



