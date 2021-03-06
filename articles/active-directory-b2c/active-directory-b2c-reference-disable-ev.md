---
title: Disable email verification during consumer sign-up in Azure Active Directory B2C | Microsoft Docs
description: A topic demonstrating how to disable email verification during consumer sign-up in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 2/06/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e008fb87b57b92f8f7e914e6b4344b52d42f9ef8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44798140"
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: Disable email verification during consumer sign-up
When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account. Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process. It also prevents a malicious automated process from generating fake accounts for the applications.

Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later. To support this, Azure AD B2C can be configured to disable email verification. Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.

By default, sign-up policies have email verification turned on. Use the following steps to turn it off:

1. [Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.
3. Click your policy (for example, "B2C_1_SiUp") to open it. 
4. Click **Edit** at the top of the blade.
5. Click **Page UI Customization**.
6. Click **Local account sign-up page**.
7. Click **Email Address** in the **Name** column under the **Sign-up attributes** section.
8. Toggle the **Require verification** option to **No**.
9. Click **OK** at the bottom until you reach the **Edit policy** blade.
10. Click **Save** at the top of the blade. You're done!

> [!NOTE]
> Disabling email verification in the sign-up process may lead to spam. If you disable the default one, we recommend adding your own verification system.
> 
> 

We are always open to feedback and suggestions! If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page. For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
