---
title: Azure Active Directory user authentication
description: As an Azure AD Administrator how do I protect user authentication while reducing end-user impact?
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: overview
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry, michmcla
ms.openlocfilehash: 0b232ed8bacfeb896fd5ee6ff9e2a58b71dc1517
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870752"
---
# <a name="what-methods-are-available-for-authentication"></a>What methods are available for authentication?

We hear reports in the news, passwords being stolen, and identities being compromised. Requiring a second factor in addition to a password immediately increases the security of your organization. Microsoft Azure Active Directory (Azure AD) includes features, like Azure Multi-Factor Authentication (Azure MFA) and Azure AD self-service password reset (SSPR), to help administrators protect their organizations and users with additional authentication methods.

When a user needs to access a sensitive application, reset their password, or enable Windows Hello, they may be asked to provide additional verification that they are who they say they are.

Additional verification may come in the form of authentication methods such as:

* A code provided in an email or text message
* A phone call
* A notification or code on their phone
* Answers to security questions

![Example login.microsoftonline.com login page in Chrome](media/overview-authentication/overview-login.png)

Azure MFA and Azure AD self-service password reset give administrators control over configuration, policy, monitoring, and reporting using Azure AD and the Azure portal to protect their organizations.

## <a name="self-service-password-reset"></a>Self-service password reset

Self-service password reset provides your users the ability to reset their password, with no administrator intervention, when and where they need to.

> [!VIDEO https://www.youtube.com/embed/hc97Yx5PJiM]

Self-service password reset includes:

* **Password change:** I know my password but want to change it to something new.
* **Password reset:** I can't sign in and want to reset my password using one or more approved authentication methods.
* **Account unlock:** I can't sign in because my account is locked out and I want to unlock using one or more approved authentication methods.

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication

Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution. Using administrator approved authentication methods, Azure MFA helps safeguard your access to data and applications, while meeting the demand for a simple sign-in process.

## <a name="next-steps"></a>Next steps

The next step is to dive in and configure self-service password reset and Azure Multi-Factor Authentication.

To get started with self-service password reset, see the [enable SSPR quickstart article](quickstart-sspr.md).

Learn more about self-service password reset in the article, [How it works: Azure AD self-service password reset](concept-sspr-howitworks.md)

Learn more about Azure Multi-Factor Authentication in the article, [How it works: Azure Multi-Factor Authentication](concept-mfa-howitworks.md)