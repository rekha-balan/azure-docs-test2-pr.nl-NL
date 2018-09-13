---
title: Azure Active Directory password reset | Microsoft Docs
description: Description of password management capabilities in Azure AD, including password reset, change, password management reporting, and writeback to your local on-premises Active Directory.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
editor: curtand
ms.assetid: be6164fc-bae1-49df-af76-761329ba70a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: joflore
ms.openlocfilehash: 1ab61e90d86be5c2ffa89db8e8cd7fe96d4d12f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553716"
---
# <a name="azure-active-directory-password-reset-for-it-administrators"></a>Azure Active Directory password reset for IT administrators
> [!IMPORTANT]
> **Are you here because you're having problems signing in?** If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).
>
>

Self-service has long been a key goal for IT departments across the world as a cost-reduction and labor-saving measure.  Indeed, the market is flooded with products that let you manage your on-premises groups, passwords, or user profiles from the cloud or on-premises. Azure Active Directory (Azure AD) sets itself apart from other offerings by providing some of the easiest to use and most powerful self-service capabilities available today.

**Azure AD Password Management** is a set of capabilities that allow your users to manage any password from any device, at any time, from any location, while remaining in compliance with the security policies you define.

## <a name="admins-learn-about-how-to-get-started-with-azure-ad-password-reset"></a>ADMINS: Learn about how to get started with Azure AD password reset
If you're an admin who wants to enable Azure AD password reset, or just learn more about it, start with the links below to get to what you're interested in.

| Topic |  |
| --- | --- |
| Supported scenarios |[What is possible with Azure AD password reset?](#what-is-possible-with-azure-ad-password-reset) |
| Why use it? |[Why use Azure AD password reset?](#why-use-azure-ad-password-reset) |
| Pricing and availability |[Pricing and availability](#pricing-and-availability) |
| Enable password reset |[Enable password reset for your users](#enable-password-reset-for-your-users) |
| Customize how it works |[Customize password reset behavior](#customize-password-reset-behavior) |
| Roll it out to my users |[Configure your users to use password reset](#configure-your-users-to-use-password-reset) |
| View reports |[View password reset activity with integrated reports](#view-password-reset-activity-with-integrated-reports) |
| Reset a user's password |[Manage your users' passwords](#manage-your-users-passwords) |
| Set my organization's password policies |[Set password policies](#set-password-policies) |
| Troubleshoot a problem |[Troubleshoot a problem](#troubleshoot-a-problem) |
| FAQ |[Read a FAQ](#read-a-faq) |
| Technical details |[Understand the technical details](#understand-the-technical-details) |
| Newly released features |[Recent service updates](#recent-service-updates) |
| Links to other documentation |[Links to password reset documentation](#links-to-password-reset-documentation) |

### <a name="what-is-possible-with-azure-ad-password-reset"></a>What is possible with Azure AD password reset?
Here are some of the things you can do with Azure AD's password management capabilities.

* **Self-service password change** allows end users or administrators to change their expired or non-expired passwords without calling an administrator or helpdesk for support.
* **Self-service password reset** allows end users or administrators to reset their passwords automatically without calling an administrator or helpdesk for support. Self-service password reset requires Azure AD Premium or Basic. For more information, see Azure Active Directory Editions.
* **Administrator-initiated password reset** allows an administrator to reset an end user’s or another administrator’s password from within the [Azure Management Portal](https://manage.windowsazure.com).
* **Password management activity reports** give administrators insights into password reset and registration activity occurring in their organization.
* **Password Writeback** allows management of on-premises passwords from the cloud so all of the above scenarios can be performed by, or on the behalf of, federated or password synchronized users. Password Writeback requires Azure AD Premium. For more information, see Getting started with Azure AD Premium.

### <a name="why-use-azure-ad-password-reset"></a>Why use Azure AD password reset?
Here are some of the reasons you should use Azure AD's password management capabilities

* **Reduce costs** - support-assisted password reset is typically 20% of organization's IT spend
* **Improve user experiences** - users don't want to call helpdesk and spend an hour on the phone every time they forget their passwords
* **Lower helpdesk volumes** - password management is the single largest helpdesk driver for most organizations
* **Enable mobility** - users can reset their passwords from wherever they are

### <a name="pricing-and-availability"></a>Pricing and availability
Azure AD password reset is available in 3 tiers, depending on which subscription you have:

* **Azure AD Free** - cloud-only administrators can reset their own passwords
* **Azure AD Basic or any Paid O365 Subscription** - cloud-only users and cloud-only administrators can reset their own passwords
* **Azure AD Premium** - any user or administrator, including cloud-only, federated, or password synced users, can reset their own passwords (requires [password writeback to be enabled](active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords))

For more information on Azure AD Premium or Basic pricing, visit the [Active Directory Pricing Details](https://azure.microsoft.com/pricing/details/active-directory/) page.

## <a name="enable-password-reset-for-your-users"></a>Enable password reset for your users
| Topic |  |
| --- | --- |
| How do I enable password reset for cloud users? |[Enable users to reset their cloud Azure Active Directory passwords](active-directory-passwords-getting-started.md#enable-users-to-reset-their-azure-ad-passwords) |
| How do I enable password reset and change for on-premises users? |[Enable users to reset or change their on-premises Active Directory passwords](active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords) |
| How do I scope password reset to a specific set of users? |[Restrict password reset to specific users](active-directory-passwords-customize.md#restrict-access-to-password-reset) |
| How do I test cloud password reset? |[Reset your Azure AD password as a user](active-directory-passwords-getting-started.md#step-3-reset-your-azure-ad-password-as-a-user) |
| How do I test on-premises password reset? |[Reset your on-premises AD password as a user](active-directory-passwords-getting-started.md#step-5-reset-your-ad-password-as-a-user) |
| How do I disable password reset at a later time? |[Setting: users enabled for password reset](active-directory-passwords-customize.md#users-enabled-for-password-reset) |

## <a name="customize-password-reset-behavior"></a>Customize password reset behavior
| Topic |  |
| --- | --- |
| How do I change what authentication methods are supported? |[Setting: authentication methods available to users](active-directory-passwords-customize.md#authentication-methods-available-to-users) |
| How do I change number of authentication methods required? |[Setting: number of authentication methods required](active-directory-passwords-customize.md#number-of-authentication-methods-required) |
| How do I set up custom security questions? |[Setting: custom security questions](active-directory-passwords-customize.md#custom-security-questions) |
| How do I set up pre-canned localized security questions? |[Setting: knowledge-based security questions](active-directory-passwords-customize.md#knowledge-based-security-questions) |
| How can I change how many security questions are required? |[Setting: number of security questions for registration or reset](active-directory-passwords-customize.md#number-of-questions-required-to-register) |
| How can I customize how a user gets in touch with an admin? |[Setting: customize the "contact your administrator" link](active-directory-passwords-customize.md#customize-the-contact-your-administrator-link) |
| How can I allow users to unlock AD accounts without resetting a password? |[Setting: enable users to unlock their AD accounts without resetting a password](active-directory-passwords-customize.md#allow-users-to-unlock-accounts-without-resetting-their-password) |
| How can I enable password reset notifications for users? |[Setting: notify users when their passwords have been reset](active-directory-passwords-customize.md#notify-users-and-admins-when-their-own-password-has-been-reset) |
| How can I enable password reset notifications for admins? |[Setting: notify other admins when an admin reset their own password](active-directory-passwords-customize.md#notify-admins-when-other-admins-reset-their-own-passwords) |
| How can I customize password reset look and feel? |[Setting: company name, branding, and logo ](active-directory-passwords-customize.md#password-management-look-and-feel) |

## <a name="configure-your-users-to-use-password-reset"></a>Configure your users to use password reset
| Topic |  |
| --- | --- |
| How do I know if an account is configured for password reset? |[What makes an account configured for password reset?](active-directory-passwords-best-practices.md#what-makes-an-account-configured) |
| How do I get my users configured for password reset? |[Ways to populate password reset authentication data for your users](active-directory-passwords-best-practices.md#ways-to-populate-authentication-data) |
| How do I manually upload data for my users? |[Uploading password reset data yourself](active-directory-passwords-best-practices.md#uploading-data-yourself) |
| How do I use PowerShell to read or set data for my users? |[How to access password reset data for your users](active-directory-passwords-learn-more.md#how-to-access-password-reset-data-for-your-users) |
| How can I synchronize password reset data from on-premises? |[What data is used by password reset](active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset) |
| How can I use an email campaign to get my users to register for and use password reset? |[Email-based rollout of password reset](active-directory-passwords-best-practices.md#email-based-rollout) |
| How can I force my users to register when signing in? |[Enforced registration-based rollout of password reset](active-directory-passwords-customize.md#require-users-to-register-when-signing-in) |
| How can I force my users to re-confirm their registered periodically? |[Setting: number of days before users must re-confirm their authentication data](active-directory-passwords-customize.md#number-of-days-before-users-must-confirm-their-contact-data) |
| What are best practices around communicating password reset to end users? |[Creating your own password portal for your users to use](active-directory-passwords-best-practices.md#creating-your-own-password-portal) |

## <a name="view-password-reset-activity-with-integrated-reports"></a>View password reset activity with integrated reports
| Topic |  |
| --- | --- |
| Where do I go to see password reset reports? |[Overview of password management reports](active-directory-passwords-get-insights.md#overview-of-password-management-reports) |
| Where can I see how users are using password reset in my organization? |[View password reset activity](active-directory-passwords-get-insights.md#how-to-view-password-management-reports) |
| Where can I see how many users are registering, and what they are registering for? |[View password reset registration activity](active-directory-passwords-get-insights.md#how-to-view-password-management-reports) |
| How can I get password reset reports from an API? |[Creating an azure ad application to access the reporting API](active-directory-reporting-api-getting-started.md) |
| What kind of password reset reporting information is available through an API? |[Password reset and registration events available in the reporting API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview#SsprActivityEvent) |

## <a name="manage-your-users-passwords"></a>Manage your users' passwords
| Topic |  |
| --- | --- |
| How do I reset a user's password from the O365 management portal? |[Reset a user's password in Office 365](https://support.office.com/article/Reset-a-user-s-password-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C) |
| How do I reset a user's password using PowerShell? |[Reset a user's password with Set-MsolUserPassword](https://msdn.microsoft.com/library/azure/dn194140.aspx) |

## <a name="set-password-policies"></a>Set password policies
| Topic |  |
| --- | --- |
| How do I set organization password expiration policy from Office 365? |[Set password expiration policy](https://support.office.com/article/Set-a-user-s-password-expiration-policy-0f54736f-eb22-414c-8273-498a0918678f) |
| How do I set a specific user's passwords to never expire with PowerShell? |[Set individual user's password to never expire using PowerShell](https://support.office.com/article/Set-an-individual-user-s-password-to-never-expire-f493e3af-e1d8-4668-9211-230c245a0466) |
| How do I find out whether a user's password is set to never expire using PowerShell |[Check individual user's password expiration status using PowerShell](https://support.office.com/article/Set-an-individual-user-s-password-to-never-expire-f493e3af-e1d8-4668-9211-230c245a0466#__toc378845827) |

## <a name="troubleshoot-a-problem"></a>Troubleshoot a problem
| Topic |  |
| --- | --- |
| What information should I provide to support if I need help? |[Information to include when you need help](active-directory-passwords-troubleshoot.md#information-to-include-when-you-need-help) |
| How can I fix a problem with password reset |[Troubleshoot the password reset portal](active-directory-passwords-troubleshoot.md#troubleshoot-the-password-reset-portal) |
| How can I fix a problem with password writeback |[Troubleshoot password writeback](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| How can I fix a problem with password writeback connectivity |[Troubleshoot password writeback connectivity](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback-connectivity) |
| How can I fix a problem with password reset configuration |[Troubleshoot password reset configuration in the azure management portal](active-directory-passwords-troubleshoot.md#troubleshoot-password-reset-configuration-in-the-azure-management-portal) |
| How can I fix a problem with password reset reports |[Troubleshoot password management reports in the azure management portal](active-directory-passwords-troubleshoot.md#troubleshoot-password-management-reports-in-the-azure-management-portal) |
| How can I fix a problem with password reset registration |[Troubleshoot the password reset registration portal](active-directory-passwords-troubleshoot.md#troubleshoot-the-password-reset-registration-portal) |
| Password writeback event log error codes |[Password writeback event log error codes](active-directory-passwords-troubleshoot.md#password-writeback-event-log-error-codes) |

## <a name="read-a-faq"></a>Read a FAQ
| Topic |  |
| --- | --- |
| I want to read a FAQ about password reset registration |[Password reset registration FAQ](active-directory-passwords-faq.md#password-reset-registration) |
| I want to read a FAQ about password reset |[Password reset FAQ](active-directory-passwords-faq.md#password-reset) |
| I want to read a FAQ about password reset reports |[Password management reports FAQ](active-directory-passwords-faq.md#password-management-reports) |
| I want to read a FAQ about password writeback |[Password writeback FAQ](active-directory-passwords-faq.md#password-writeback) |

## <a name="understand-the-technical-details"></a>Understand the technical details
| Topic |  |
| --- | --- |
| I want to learn about what password writeback is |[Password writeback overview](active-directory-passwords-learn-more.md#password-writeback-overview) |
| I want to learn about how password writeback works |[How does password writeback work?](active-directory-passwords-learn-more.md#how-password-writeback-works) |
| I want to learn about what scenarios are supported by password writeback |[Scenarios supported for password writeback](active-directory-passwords-learn-more.md#scenarios-supported-for-password-writeback) |
| I want to learn about how password writeback is secured |[Password writeback security model](active-directory-passwords-learn-more.md#password-writeback-security-model) |
| I want to learn about how the password reset portal works |[How does the password reset portal work?](active-directory-passwords-learn-more.md#how-does-the-password-reset-portal-work) |
| I want to learn about what data is used by password reset |[What data is used by password reset?](active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset) |

## <a name="recent-service-updates"></a>Recent service updates
#### <a name="enforce-password-reset-registration-at-sign-in-to-office-365-apps---november-2015"></a>Enforce password reset registration at sign-in to Office 365 apps - November 2015
* Now, after enabling the [enforced registration](active-directory-passwords-customize.md#require-users-to-register-when-signing-in) feature, your users will be required to register from anywhere they sign in with a work or school account.  This dramatically increases the speed at which many organizations can onboard to password reset.  With this new feature we've seen large organizations onboarding in as little as 2 weeks!

#### <a name="support-for-unlocking-on-premises-ad-accounts-without-resetting-a-password---november-2015"></a>Support for unlocking on-premises AD Accounts without resetting a password - November 2015
* Unlock only (without reset) is a huge helpdesk driver these days.  In fact, many organizations spend up to 70% of their password reset budget unlocking accounts!  To meet this demand, now with Azure AD password reset, you can enable a feature to let your users unlock on-premises AD accounts separately from password reset.  Check out how to turn it on here: [Setting: enable users to unlock their on-premises AD accounts without resetting a password](active-directory-passwords-customize.md#allow-users-to-unlock-accounts-without-resetting-their-password).

#### <a name="usability-updates-to-registration-page---october-2015"></a>Usability updates to registration page - October 2015
* Now, when a user has data already registered, he or she can just click "looks good" to update the data without needing to re-send the email or phone call.

#### <a name="improved-reliability-of-password-writeback---september-2015"></a>Improved reliability of password writeback - September 2015
* As of the September release of Azure AD Connect, the password writeback agent will now more aggressively retry connections and additional, more robust, failover capabilities.

#### <a name="api-for-retrieving-password-reset-reporting-data---august-2015"></a>API for retrieving password reset reporting data - August 2015
* Now, the data behind the password reset reports can be retrieved directly from the [Azure AD Reports and Events API](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).

#### <a name="support-for-azure-ad-password-reset-during-cloud-domain-join---august-2015"></a>Support for Azure AD password reset during cloud domain join - August 2015
* Now, any cloud user can reset his or her password right from the Windows 10 sign in screen during the cloud domain join onboarding experience.  Note, this is not yet exposed on the Windows 10 sign in screen.

#### <a name="enforce-password-reset-registration-at-sign-in-to-azure-and-federated-apps---july-2015"></a>Enforce password reset registration at sign-in to Azure and federated apps - July 2015
* In addition to enforcing registration when signing into myapps.microsoft.com, we now support enforcing registration during sign ins to the Azure Management Portal and any of your federated single-sign on applications

#### <a name="security-question-localization-support---may-2015"></a>Security question localization support - May 2015
* Now, you have the option to select pre-defined security questions which are localized in the full O365 language set when configuring Security Questions for password reset.

#### <a name="account-unlock-support-during-password-reset---june-2015"></a>Account unlock support during password reset - June 2015
* If you're using password writeback and you reset your password when your account is locked, we'll automatically unlock your Active Directory account!

#### <a name="branded-self-service-password-reset-sspr-registration---april-2015"></a>Branded self-service password reset (SSPR) registration - April 2015
* The password reset registration page is now branded with your company logo!

#### <a name="security-questions---march-2015"></a>Security questions - March 2015
* We released security questions to GA!

#### <a name="account-unlock---march-2015"></a>Account unlock - March 2015
* Now users can unlock their accounts when password reset occurs

## <a name="coming-soon"></a>Coming soon
Below are some of the cool features we're working on right now!

**Support for Reminding Users to Update their Registered Data During Sign-in** - Work in progress

* Today, we support reminding users to update their registered data when accessing myapps.microsoft.com, but we're working on the ability to do so for all sign ins.

## <a name="next-steps"></a>Next steps
Below are links to all of the Azure AD password reset documentation pages:

* **Are you here because you're having problems signing in?** If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).
* [**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does
* [**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords
* [**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs
* [**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization
* [**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities
* [**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions
* [**Troubleshooting**](active-directory-passwords-troubleshoot.md) - learn how to quickly troubleshoot problems with the service
* [**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works
