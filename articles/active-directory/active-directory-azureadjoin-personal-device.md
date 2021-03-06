---
title: Join a personal device to your organization| Microsoft Docs
description: Explains how users can register their personal Windows 10 devices to their corporate network, and provides deployment steps for a BYOD scenario.
services: active-directory
documentationcenter: ''
author: femila
manager: femila
editor: ''
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 6effe246eeb4e4a48f1a695de47047c78f9e509e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552913"
---
# <a name="join-a-personal-device-to-your-organization"></a>Join a personal device to your organization
## <a name="to-join-a-windows-10-device-to-your-organization"></a>To join a Windows 10 device to your organization
1. From the **Start** menu, select **Settings**.
2. Select **Accounts**, and then click **Your account**.
3. Click **Add Work or School account**, and then type in your organizational account.
4. On the sign-in page for your organization, enter your user name and password, and then click **OK**.
5. You will be prompted for a multi-factor authentication challenge. (This challenge is configurable by an IT administrator.)
6. Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.
7. Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.
8. If you are a managed user, Windows takes you to the desktop through the automatic sign-in.
9. If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.

## <a name="additional-information"></a>Additional information
* [Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Authenticating identities without passwords through Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md)
* [Set up Azure AD Join](active-directory-azureadjoin-setup.md)

