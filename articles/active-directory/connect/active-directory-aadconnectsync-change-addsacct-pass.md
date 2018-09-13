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
# <a name="changing-the-ad-ds-account-password"></a>Changing the AD DS account password
The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory. If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password. Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:

* In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.

* Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a>How to update the Synchronization Service with new password for AD DS account
To update the Synchronization Service with the new password:

1. Start the Synchronization Service Manager (START → Synchronization Service).
</br>![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Go to the **Connectors** tab.

3. Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.

4. Under **Actions**, select **Properties**.

5. In the pop-up dialog, select **Connect to Active Directory Forest**:

6. Enter the new password of the AD DS account in the **Password** textbox.

7. Click **OK** to save the new password and close the pop-up dialog.

8. Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager. This is to ensure that any reference to the old password is removed from the memory cache.

## <a name="next-steps"></a>Next steps
**Overview topics**

* [Azure AD Connect sync: Understand and customize synchronization](active-directory-aadconnectsync-whatis.md)

* [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md)

