---
title: Problems signing in to a Microsoft application | Microsoft Docs
description: Troubleshoot common problems faced when signing in to first-party Microsoft Applications using Azure AD (like Office 365)
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: c4e4316c38cc568bb5a8dbbd2db353ee75f9af4c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662947"
---
## <a name="problems-signing-in-to-a-microsoft-application"></a>Problems signing in to a Microsoft application

Microsoft Applications (like Office 365 Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than 3rd party SaaS applications or other applications you integrate with Azure AD for single sign on.

There are three main ways that a user can get access to a Microsoft-published application.

-   For applications in the Office 365 or other paid suites, users are granted access through **license assignment** either directly to their user account, or through a group using our group-based license assignment capability.

-   For applications that Microsoft or a Third Party publishes freely for anyone to use, users may be granted access through **user consent**. This0 means that they sign in to the application with their Azure AD Work or School account and allow it to have access to some limited set of data on their account.

-   For applications that Microsoft or a 3rd Party publishes freely for anyone to use, users may also be granted access through **administrator consent**. This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.

To troubleshoot your issue, start with the [General Problem Areas with Application Access to consider](#general-problem-areas-with-application-access-to-consider) and then read the [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access) to get into the details.

## <a name="general-problem-areas-with-application-access-to-consider"></a>General Problem Areas with Application Access to consider

Below is a list of the general problem areas that you can drill into if you have an idea of where to start, but we recommend you read the walkthrough to get going quickly: [Walkthrough: Steps to troubleshoot Microsoft Application access](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problems with the user’s account](#problems-with-the-users-account)

-   [Problems with groups](#problems-with-groups)

-   [Problems with conditional access policies](#problems-with-conditional-access-policies)

-   [Problems with application consent](#problems-with-application-consent)

## <a name="steps-to-troubleshoot-microsoft-application-access"></a>Steps to troubleshoot Microsoft Application access

Below are some common issues folks run into when their users cannot sign in to a Microsoft application.

-   General issues to check first

  * Make sure the user is signing in to the **correct URL** and not a local application URL.

  * Make sure the user’s account is **not locked out.**

  * Make sure the **user’s account exists** in Azure Active Directory. [Check if a user account exists in Azure Active Directory](#problems-with-the-users-account)

  * Make sure the user’s account is **enabled** for sign ins. [Check a user’s account status](#problems-with-the-users-account)

  * Make sure the user’s **password is not expired or forgotten.** [Reset a user’s password](#reset-a-users-password) or [Enable self-service password reset](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Make sure **Multi-Factor Authentication** is not blocking user access. [Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)

   * Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access. [Check a specific conditional access policy](#problems-with-conditional-access-policies) or [Check a specific application’s conditional access policy](#check-a-specific-applications-conditional-access-policy) or [Disable a specific conditional access policy](#disable-a-specific-conditional-access-policy)

   * Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced. [Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status) or [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)

-   For **Microsoft** **applications that require a license** (like Office365), here are some specific issues to check once you have ruled out the general issues above:

   * Ensure the user or has a **license assigned.** [Check a user’s assigned licenses](#check-a-users-assigned-licenses) or [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)

   * If the license is **assigned to a** **static group**, ensure that the **user is a member** of that group. [Check a user’s group memberships](#check-a-users-group-memberships)

   * If the license is **assigned to a** **dynamic group**, ensure that the **dynamic group rule is set correctly**. [Check a dynamic group’s membership criteria](#check-a-dynamic-groups-membership-criteria)

   * If the license is **assigned to a** **dynamic group**, ensure that the dynamic group has **finished processing** its membership and that the **user is a member** (this can take some time). [Check a user’s group memberships](#check-a-users-group-memberships)

   *  Once you make sure the license is assigned, make sure the license is **not expired**.

   *  Make sure the license is **for the application** they are accessing.

-   For **Microsoft** **applications that don’t require a license**, here are some other things to check:

   * If the application is requesting **user-level permissions** (for example “Access this user’s mailbox”), make sure that the user has signed in to the application and has performed a **user-level consent operation** to let the application access her data.

   * If the application is requesting **administrator-level permissions** (for example “Access all user’s mailboxes”), make sure that a Global Administrator has performed an **administrator-level consent operation on behalf of all users** in the organization.

## <a name="problems-with-the-users-account"></a>Problems with the user’s account

Application access can be blocked due to a problem with a user that is assigned to the application. Below are some ways you can troubleshoot and solve problems with users and their account settings:

-   [Check if a user account exists in Azure Active Directory](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Check a user’s account status](#check-a-users-account-status)

-   [Reset a user’s password](#reset-a-users-password)

-   [Enable self-service password reset](#enable-self-service-password-reset)

-   [Check a user’s multi-factor authentication status](#check-a-users-multi-factor-authentication-status)

-   [Check a user’s authentication contact info](#check-a-users-authentication-contact-info)

-   [Check a user’s group memberships](#check-a-users-group-memberships)

-   [Check a user’s assigned licenses](#check-a-users-assigned-licenses)

-   [Assign a user a license](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Check if a user account exists in Azure Active Directory

To check if a user’s account is present, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  Check the properties of the user object to be sure that they look as you expect and no data is missing.

### <a name="check-a-users-account-status"></a>Check a user’s account status

To check a user’s account status, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Profile**.

8.  Under **Settings** ensure that **Block sign in** is set to **No**.

### <a name="reset-a-users-password"></a>Reset a user’s password

To reset a user’s password, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click the **Reset password** button at the top of the user blade.

8.  click the **Reset password** button on the **Reset password** blade that appears.

9.  Copy the **temporary password** or **enter a new password** for the user.

10. Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.

### <a name="enable-self-service-password-reset"></a>Enable self-service password reset

To enable self-service password reset, follow the deployment steps below:

-   [Enable users to reset their Azure Active Directory passwords](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Enable users to reset or change their Active Directory on-premises passwords](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Check a user’s multi-factor authentication status

To check a user’s multi-factor authentication status, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  click the **Multi-Factor Authentication** button at the top of the blade.

7.  Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.

8.  Find the user in the list of users by searching, filtering, or sorting.

9.  Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.

  * **Note**: If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account. Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in. Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.

### <a name="check-a-users-authentication-contact-info"></a>Check a user’s authentication contact info

To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Profile**.

8.  Scroll down to **Authentication contact info**.

9.  **Review** the data registered for the user and update as needed.

### <a name="check-a-users-group-memberships"></a>Check a user’s group memberships

To check a user’s group memberships, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Groups** to see which groups the user is a member of.

### <a name="check-a-users-assigned-licenses"></a>Check a user’s assigned licenses

To check a user’s assigned licenses, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Licenses** to see which licenses the user currently has assigned.

### <a name="assign-a-user-a-license"></a>Assign a user a license 

To assign a license to a user, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Licenses** to see which licenses the user currently has assigned.

8.  click the **Assign** button.

9.  Select **one or more products** from the list of available products.

10. **Optional** click the **assignment options** item to granularly assign products. Click **Ok** when this is completed.

11. Click the **Assign** button to assign these licenses to this user.

## <a name="problems-with-groups"></a>Problems with groups

Application access can be blocked due to a problem with a group that is assigned to the application. Below are some ways you can troubleshoot and solve problems with groups and group memberships:

-   [Check a group’s membership](#check-a-groups-membership)

-   [Check a dynamic group’s membership criteria](#check-a-dynamic-groups-membership-criteria)

-   [Check a group’s assigned licenses](#check-a-groups-assigned-licenses)

-   [Reprocess a group’s licenses](#reprocess-a-groups-licenses)

-   [Assign a group a license](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Check a group’s membership

To check a group’s membership, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All groups**.

6.  **Search** for the group you are interested in and **click the row** to select.

7.  click **Members** to review the list of users assigned to this group.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Check a dynamic group’s membership criteria 

To check a dynamic group’s membership criteria, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All groups**.

6.  **Search** for the group you are interested in and **click the row** to select.

7.  click **Dynamic membership rules.**

8.  Review the **simple** or **advanced** rule defined for this group and ensure that the user you want to be a member of this group meets these criteria.

### <a name="check-a-groups-assigned-licenses"></a>Check a group’s assigned licenses

To check a group’s assigned licenses, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All groups**.

6.  **Search** for the group you are interested in and **click the row** to select.

7.  click **Licenses** to see which licenses the group currently has assigned.

### <a name="reprocess-a-groups-licenses"></a>Reprocess a group’s licenses

To reprocess a group’s assigned licenses, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All groups**.

6.  **Search** for the group you are interested in and **click the row** to select.

7.  click **Licenses** to see which licenses the group currently has assigned.

8.  click the **Reprocess** button to ensure that the licenses assigned to this group’s members are up-to-date. This may take a long time, depending on the size and complexity of the group.

   >[!NOTE]
   >To do this faster, consider temporarily assigning a license to the user directly. [Assign a user a license](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>Assign a group a license

To assign a license to a group, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All groups**.

6.  **Search** for the group you are interested in and **click the row** to select.

7.  click **Licenses** to see which licenses the group currently has assigned.

8.  click the **Assign** button.

9.  Select **one or more products** from the list of available products.

10. **Optional** click the **assignment options** item to granularly assign products. Click **Ok** when this is completed.

11. Click the **Assign** button to assign these licenses to this group. This may take a long time, depending on the size and complexity of the group.

   >[!NOTE]
   >To do this faster, consider temporarily assigning a license to the user directly. [Assign a user a license](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problems with conditional access policies

### <a name="check-a-specific-conditional-access-policy"></a>Check a specific conditional access policy

To check or validate a single conditional access policy:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise applications** in the navigation menu.

5.  click the **Conditional access** navigation item.

6.  click the policy you are interested in inspecting.

7.  Review that there are no specific conditions, assignments, or other settings which may be blocking user access.

   >[!NOTE]
   >You may wish to temporarily disable this policy to ensure it is not affecting sign ins. To do this, set the **Enable policy** toggle to **No** and click the **Save** button.
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Check a specific application’s conditional access policy

To check or validate a single application’s currently configured conditional access policy:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise applications** in the navigation menu.

5.  click **All applications**.

6.  Search for the application you are interested in, or the user is attempting to sign in to by application display name or application id.

     >[!NOTE]
     >If you don’t see the application you are looking for, click the **Filter** button and expand the scope of the list to **All applications**. If you want to see more columns, click the **Columns** button to add additional details for your applications.
     >
     >

7.  click the **Conditional access** navigation item.

8.  click the policy you are interested in inspecting.

9.  Review that there are no specific conditions, assignments, or other settings which may be blocking user access.

     >[!NOTE]
     >You may wish to temporarily disable this policy to ensure it is not affecting sign ins. To do this, set the **Enable policy** toggle to **No** and click the **Save** button.
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Disable a specific conditional access policy

To check or validate a single conditional access policy:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise applications** in the navigation menu.

5.  click the **Conditional access** navigation item.

6.  click the policy you are interested in inspecting.

7.  Disable the policy by setting the **Enable policy** toggle to **No** and click the **Save** button.

## <a name="problems-with-application-consent"></a>Problems with application consent

Application access can be blocked because the proper permissions consent operation has not occurred. Below are some ways you can troubleshoot and solve application consent issues:

-   [Perform a user-level consent operation](#perform-a-user-level-consent-operation)

-   [Perform administrator-level consent operation for any application](#perform-administrator-level-consent-operation-for-any-application)

-   [Perform administrator-level consent for a single-tenant application](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Perform administrator-level consent for a multi-tenant application](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Perform a user-level consent operation

-   For any application, navigating to the application’s sign in screen perform a user level consent to the application for the signed-in user.

-   If you wish to do this programmatically, see [Requesting individual user consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>Perform administrator-level consent operation for any application

-   For **only applications developed using the V1 application model**, you can force this administrator level consent to occur by adding “**?prompt=admin\_consent**” to the end of an application’s sign in URL.

-   For **any application developed using the V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Perform administrator-level consent for a single-tenant application

-   For **single-tenant applications** that request permissions (like those you are developing or own in your organization), you can perform an **administrative-level consent** operation on behalf of all users by signing in as a Global Administrator and clicking on the **Grant permissions** button at the top of the **Application Registry -&gt; All Applications -&gt; Select an App -&gt; Required Permissions** blade.

-   For **any application developed using the V1 or V2 application model**, you can enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Perform administrator-level consent for a multi-tenant application

-   For **multi-tenant applications** that request permissions (like an application a third party, or Microsoft, develops), you can perform an **administrative-level consent** operation. Sign in as a Global Administrator and clicking on the **Grant permissions** button under the **Enterprise Applications -&gt; All Applications -&gt; Select an App -&gt; Permissions** blade (available soon).

-   You can also enforce this administrator-level consent to occur by following the instructions under the **Request the permissions from a directory admin** section of [Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Next steps
[Using the admin consent endpoint](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

