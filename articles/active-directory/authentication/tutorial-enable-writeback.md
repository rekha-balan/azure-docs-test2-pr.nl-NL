---
title: Azure AD enable password writeback
description: In this tutorial, you will enable password writeback to get cloud initiated password changes back to on-premises AD as part of Azure AD Connect.
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 9512c800a35ad4a819c657b07227d781c63c6399
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870321"
---
# <a name="tutorial-enabling-password-writeback"></a>Tutorial: Enabling password writeback

In this tutorial, you will enable password writeback for your hybrid environment. Password writeback is used to synchronize password changes in Azure Active Directory (Azure AD) back to your on-premises Active Directory Domain Services (AD DS) environment. Password writeback is enabled as part of Azure AD Connect to provide a secure mechanism to send password changes back to an existing on-premises directory from Azure AD. You can find more detail about the inner workings of password writeback in the article, [What is password writeback](concept-sspr-writeback.md).

> [!div class="checklist"]
> * Enable password writeback option in Azure AD Connect
> * Enable password writeback option in self-service password reset (SSPR)

## <a name="prerequisites"></a>Prerequisites

* Access to a working Azure AD tenant with at least a trial license assigned.
* An account with Global Administrator privileges in your Azure AD tenant.
* An existing server configured running a current version of [Azure AD Connect](../connect/active-directory-aadconnect-get-started-express.md).
* Previous self-service password reset (SSPR) tutorials have been completed.

## <a name="enable-password-writeback-option-in-azure-ad-connect"></a>Enable password writeback option in Azure AD Connect

To enable password writeback we will first need to enable the feature from the server that you have installed Azure AD Connect on.

1. To configure and enable password writeback, sign in to your Azure AD Connect server and start the **Azure AD Connect** configuration wizard.
2. On the **Welcome** page, select **Configure**.
3. On the **Additional tasks** page, select **Customize synchronization options**, and then select **Next**.
4. On the **Connect to Azure AD** page, enter a global administrator credential, and then select **Next**.
5. On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.
6. On the **Optional features** page, select the box next to **Password writeback** and select **Next**.
7. On the **Ready to configure** page, select **Configure** and wait for the process to finish.
8. When you see the configuration finish, select **Exit**.

## <a name="enable-password-writeback-option-in-sspr"></a>Enable password writeback option in SSPR

Enabling the password writeback feature in Azure AD Connect is only half of the story. Allowing SSPR to use password writeback completes the loop thereby allowing users who change or reset their password to have that password set on-premises as well.

1. Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.
2. Browse to **Azure Active Directory**, click on **Password Reset**, then choose **On-premises integration**.
3. Set the option for **Write back passwords to your on-premises directory**, to **Yes**.
4. Set the option for **Allow users to unlock accounts without resetting their password**, to **Yes**.
5. Click **Save**

## <a name="next-steps"></a>Next steps

In this tutorial, you have enabled password writeback for self-service password reset. Leave the Azure portal window open and continue to the next tutorial to configure additional settings related to self-service password reset before you roll out the solution in a pilot.

> [!div class="nextstepaction"]
> [Enabling SSPR at the Windows logon screen](tutorial-sspr-windows.md)
