---
title: Set up a Windows 10 device with Azure AD from Settings| Microsoft Docs
description: Explains how users can join to Azure AD through the Settings menu.
services: active-directory
documentationcenter: ''
author: femila
manager: swadhwa
editor: ''
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 57e8b16122d857921d6f3106cd7dd64fa1ebdb02
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552433"
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Set up a Windows 10 device with Azure AD from Settings
If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a>To join to Azure AD from the Settings menu
1. From the **Start** menu, click the **Settings** charm.
2. From **Settings**, select     **System**->**About**->**Join Azure AD**.
   
   <center>
   ![Join Azure AD from the Settings menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center>
3. Click **Continue** in the Azure AD Join message window.
   
   <center>
   ![Join Azure AD message window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. Provide your sign-in credentials. This sign-in experience will include all the steps that are required to complete authentication. If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.
   <center>
   ![Provide sign-in credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.
6. Click **Accept** on the **Allow this device to be managed** screen.
7. You should see the message "Your device is now joined to your organization in Azure AD".

## <a name="additional-information"></a>Additional information
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md)
* [Set up Azure AD Join](active-directory-azureadjoin-setup.md)
* [Authenticating identities without passwords through Microsoft Passport](active-directory-azureadjoin-passport.md)




