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
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a>Using connectors with the Azure AD Connect Sync Service Manager

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

The Connectors tab is used to manage all systems the sync engine is connected to.

## <a name="connector-actions"></a>Connector actions
| Action | Comment |
| --- | --- |
| Create |Do not use. For connecting to additional AD forests, use the installation wizard. |
| Properties |Used for domain and OU filtering. |
| [Delete](#delete) |Used to either delete the data in the connector space or to delete connection to a forest. |
| [Configure Run Profiles](#configure-run-profiles) |Except for domain filtering, nothing to configure here. You can use this action to see already configured run profiles. |
| Run |Used to start a one-off run of a profile. |
| Stop |Stops a Connector currently running a profile. |
| Export Connector |Do not use. |
| Import Connector |Do not use. |
| Update Connector |Do not use. |
| Refresh Schema |Refreshes the cached schema. It is preferred to use the option in the installation wizard instead, since that also updates sync rules. |
| [Search Connector Space](#search-connector-space) |Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Delete
The delete action is used for two different things.  
![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

The option **Delete connector space only** removes all data, but keep the configuration.

The option **Delete Connector and connector space** removes the data and the configuration. This option is used when you do not want to connect to a forest anymore.

Both options sync all objects and update the metaverse objects. This action is a long running operation.

### <a name="configure-run-profiles"></a>Configure Run Profiles
This option allows you to see the run profiles configured for a Connector.

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Search Connector Space
The search connector space action is useful to find objects and troubleshoot data issues.

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Start by selecting a **scope**. You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).  
![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
If you for example do a Sub-Tree search, you get all objects in one OU.  
![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.

### <a name="changing-the-ad-ds-account-password"></a>Changing the AD DS account password
If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.   You may see the following:

- The import/export step for the AD connector fails with "no-start-credentials" error.
- Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”

To resolve the issue, update the AD DS user account using the following:


1. Start the Synchronization Service Manager (START → Synchronization Service).
</br>![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Go to the **Connectors** tab.
3. Select the AD Connector which is configured to use the AD DS account.
4. Under Actions, select **Properties**.
5. In the pop-up dialog, select Connect to Active Directory Forest:
6. The Forest name indicates the corresponding on-prem AD.
7. The User name indicates the AD DS account used for synchronization.
8. Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-encryption-key/key6.PNG)
9. Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.



## <a name="next-steps"></a>Next steps
Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.

Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).








