---
title: Self-service password reset reports - Azure Active Directory
description: Reporting on Azure AD self-service password reset events
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 5931958d17ea119e58c066a78a44169be2b9f451
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965741"
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Reporting options for Azure AD password management

After deployment, many organizations want to know how or if self-service password reset (SSPR) is really being used. The reporting feature that Azure Active Directory (Azure AD) provides helps you answer questions by using prebuilt reports. If you're appropriately licensed, you can also create custom queries.

![Reporting][Reporting]

The following questions can be answered by the reports that exist in the [Azure portal] (https://portal.azure.com/):

> [!NOTE]
> You must be [a global administrator](../users-groups-roles/directory-assign-admin-roles.md), and you must opt-in for this data to be gathered on behalf of your organization. To opt in, you must visit the **Reporting** tab or the audit logs at least once. Until then, data is not collected for your organization.
>

* How many people have registered for password reset?
* Who has registered for password reset?
* What data are people registering?
* How many people reset their passwords in the last seven days?
* What are the most common methods that  users or admins use to reset their passwords?
* What are common problems users or admins face when attempting to use password reset?
* What admins are resetting their own passwords frequently?
* Is there any suspicious activity going on with password reset?

## <a name="power-bi-content-pack"></a>Power BI content pack

If you're a Power BI user, there is a content pack for Azure AD that includes easy-to-use reporting for SSPR. For more information on how to use and deploy the content pack, see [How to use the Azure Active Directory Power BI content pack](../reports-monitoring/howto-power-bi-content-pack.md). With the content pack, you can create your own dashboards and share them with others in your organization.

## <a name="how-to-view-password-management-reports-in-the-azure-portal"></a>How to view password management reports in the Azure portal

In the Azure portal experience, we have improved the way that you can view password reset and password reset registration activity. Use the following the steps to find the password reset and password reset registration events:

1. Browse to the [Azure portal](https://portal.azure.com).
2. Select **All services** in the left pane.
3. Search for **Azure Active Directory** in the list of services and select it.
4. Select **Users and groups**.
5. Select **Audit Logs** from the **Users and groups** menu. This shows you all of the audit events that occurred against all the users in your directory. You can filter this view to see all the password-related events.
6. To filter this view to see only the password-reset-related events, select the **Filter** button at the top of the pane.
7. From the **Filter** menu, select the **Category** drop-down list, and change it to the **Self-service Password Management** category type.
8. Optionally, further filter the list by choosing the specific **Activity** you're interested in.

### <a name="converged-registration-preview"></a>Converged registration (preview)

If you are participating in the public preview of converged registration, information regarding user activity in the audit logs will be found under the category **Authentication Methods**.

## <a name="description-of-the-report-columns-in-the-azure-portal"></a>Description of the report columns in the Azure portal

The following list explains each of the report columns in the Azure portal in detail:

* **User**: The user who attempted a password reset registration operation.
* **Role**: The role of the user in the directory.
* **Date and Time**: The date and time of the attempt.
* **Data Registered**: The authentication data that the user provided during password reset registration.

## <a name="description-of-the-report-values-in-the-azure-portal"></a>Description of the report values in the Azure portal

The following table describes the different values that are you can set for each column in the Azure portal:

| Column | Permitted values and their meanings |
| --- | --- |
| Data registered |**Alternate email**: The user used an alternate email or authentication email to authenticate.<p><p>**Office phone**: The user used an office phone to authenticate.<p>**Mobile phone**: The user used a mobile phone or authentication phone to authenticate.<p>**Security questions**: The user used security questions to authenticate.<p>**Any combination of the previous methods, for example, alternate email + mobile phone**: Occurs when a two-gate policy is specified and shows which two methods the user used to authentication their password reset request. |

## <a name="self-service-password-management-activity-types"></a>Self-Service Password Management activity types

The following activity types appear in the **Self-Service Password Management** audit event category:

* [Blocked from self-service password reset](#activity-type-blocked-from-self-service-password-reset): Indicates that a user tried to reset a password, use a specific gate, or validate a phone number more than five total times in 24 hours.
* [Change password (self-service)](#activity-type-change-password-self-service): Indicates that a user performed a voluntary, or forced (due to expiry) password change.
* [Reset password (by admin)](#activity-type-reset-password-by-admin): Indicates that an administrator performed a password reset on behalf of a user from the Azure portal.
* [Reset password (self-service)](#activity-type-reset-password-self-service): Indicates that a user successfully reset their password from the [Azure AD password reset portal](https://passwordreset.microsoftonline.com).
* [Self-service password reset flow activity progress](#activity-type-self-serve-password-reset-flow-activity-progress): Indicates each specific step a user proceeds through, such as passing a specific password reset authentication gate, as part of the password reset process.
* [Unlock user account (self-service)](#activity-type-unlock-user-account-self-service): Indicates that a user successfully unlocked their Active Directory account without resetting their password from the [Azure AD password reset portal](https://passwordreset.microsoftonline.com) by using the Active Directory feature of account unlock without reset.
* [User registered for self-service password reset](#activity-type-user-registered-for-self-service-password-reset): Indicates that a user has registered all the required information to be able to reset their password in accordance with the currently specified tenant password reset policy.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Activity type: Blocked from self-service password reset

The following list explains this activity in detail:

* **Activity description**: Indicates that a user tried to reset a password, use a specific gate, or validate a phone number more than five total times in 24 hours.
* **Activity actor**: The user who was throttled from performing additional reset operations. The user can be an end user or an administrator.
* **Activity target**: The user who was throttled from performing additional reset operations. The user can be an end user or an administrator.
* **Activity status**:
  * _Success_: Indicates that a user was throttled from performing any additional resets, attempting any additional authentication methods, or validating any additional phone numbers for the next 24 hours.
* **Activity status failure reason**: Not applicable.

### <a name="activity-type-change-password-self-service"></a>Activity type: Change password (self-service)

The following list explains this activity in detail:

* **Activity description**: Indicates that a user performed a voluntary, or forced (due to expiry) password change.
* **Activity actor**: The user who changed their password. The user can be an end user or an administrator.
* **Activity target**: The user who changed their password. The user can be an end user or an administrator.
* **Activity statuses**:
  * _Success_: Indicates that a user successfully changed their password.
  * _Failure_: Indicates that a user failed to change their password. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
* **Activity status failure reason**: 
  * _FuzzyPolicyViolationInvalidPassword_: The user selected a password that was automatically banned because the Microsoft Banned Password Detection capabilities found it to be too common or especially weak.

### <a name="activity-type-reset-password-by-admin"></a>Activity type: Reset password (by admin)

The following list explains this activity in detail:

* **Activity description**: Indicates that an administrator performed a password reset on behalf of a user from the Azure portal.
* **Activity actor**: The administrator who performed the password reset on behalf of another end user or administrator. Must be either a global administrator, password administrator, user administrator, or helpdesk administrator.
* **Activity target**: The user whose password was reset. The user can be an end user or a different administrator.
* **Activity statuses**:
  * _Success_: Indicates that an admin successfully reset a user's password.
  * _Failure_: Indicates that an admin failed to change a user's password. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.

### <a name="activity-type-reset-password-self-service"></a>Activity type: Reset password (self-service)

The following list explains this activity in detail:

* **Activity description**: Indicates that a user successfully reset their password from the [Azure AD password reset portal](https://passwordreset.microsoftonline.com).
* **Activity actor**: The user who reset their password. The user can be an end user or an administrator.
* **Activity target**: The user who reset their password. The user can be an end user or an administrator.
* **Activity statuses**:
  * _Success_: Indicates that a user successfully reset their own password.
  * _Failure_: Indicates that a user failed to reset their own password. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
* **Activity status failure reason**: 
  * _FuzzyPolicyViolationInvalidPassword_: The admin selected a password that was automatically banned because the Microsoft Banned Password Detection capabilities found it to be too common or especially weak.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Activity type: Self serve password reset flow activity progress

The following list explains this activity in detail:

* **Activity description**: Indicates each specific step a user proceeds through (such as passing a specific password reset authentication gate) as part of the password reset process.
* **Activity actor**: The user who performed part of the password reset flow. The user can be an end user or an administrator.
* **Activity target**: The user who performed part of the password reset flow. The user can be an end user or an administrator.
* **Activity statuses**:
  * _Success_: Indicates that a user successfully completed a specific step of the password reset flow.
  * _Failure_: Indicates that a specific step of the password reset flow failed. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.
* **Activity status reasons**:   See the following table for [all the permissible reset activity status reasons](#allowed-values-for-details-column).

### <a name="activity-type-unlock-a-user-account-self-service"></a>Activity type: Unlock a user account (self-service)

The following list explains this activity in detail:

* **Activity description**: Indicates that a user successfully unlocked their Active Directory account without resetting their password from the [Azure AD password reset portal](https://passwordreset.microsoftonline.com) by using the Active Directory feature of account unlock without reset.
* **Activity actor**: The user who unlocked their account without resetting their password. The user can be an end user or an administrator.
* **Activity target**: The user who unlocked their account without resetting their password. The user can be an end user or an administrator.
* **Allowed activity statuses**:
  * _Success_: Indicates that a user successfully unlocked their own account.
  * _Failure_: Indicates that a user failed to unlock their account. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Activity type: User registered for self-service password reset

The following list explains this activity in detail:

* **Activity description**: Indicates that a user has registered all the required information to be able to reset their password in accordance with the currently specified tenant password reset policy. 
* **Activity actor**: The user who registered for password reset. The user can be an end user or an administrator.
* **Activity target**: The user who registered for password reset. The user can be an end user or an administrator.
* **Allowed activity statuses**:
  * _Success_: Indicates that a user successfully registered for password reset in accordance with the current policy. 
  * _Failure_: Indicates that a user failed to register for password reset. You can select the row to see the **Activity status reason** category to learn more about why the failure occurred. 

     >[!NOTE]
     >Failure doesn't mean a user is unable to reset their own password. It means that they didn't finish the registration process. If there is unverified data on their account that's correct, such as a phone number that's not validated, even though they have not verified this phone number, they can still use it to reset their password. For more information, see [What happens when a user registers?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers).
     >

## <a name="next-steps"></a>Next steps

* [How do I complete a successful rollout of SSPR?](howto-sspr-deployment.md)
* [Reset or change your password](../user-help/active-directory-passwords-update-your-own-password.md).
* [Register for self-service password reset](../user-help/active-directory-passwords-reset-register.md).
* [Do you have a licensing question?](concept-sspr-licensing.md)
* [What data is used by SSPR and what data should you populate for your users?](howto-sspr-authenticationdata.md)
* [What authentication methods are available to users?](concept-sspr-howitworks.md#authentication-methods)
* [What are the policy options with SSPR?](concept-sspr-policy.md)
* [What is password writeback and why do I care about it?](howto-sspr-writeback.md)
* [What are all of the options in SSPR and what do they mean?](concept-sspr-howitworks.md)
* [I think something is broken. How do I troubleshoot SSPR?](active-directory-passwords-troubleshoot.md)
* [I have a question that was not covered somewhere else](active-directory-passwords-faq.md)

[Reporting]: ./media/howto-sspr-reporting/sspr-reporting.png "Example of SSPR activity audit logs in Azure AD"
