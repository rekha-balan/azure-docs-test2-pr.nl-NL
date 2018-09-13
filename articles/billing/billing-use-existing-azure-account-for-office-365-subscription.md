---
title: Sign up for Office 365 with Azure account | Microsoft Docs
description: Learn how to create an Office 365 subscription by using an Azure account
services: ''
documentationcenter: ''
author: JiangChen79
manager: vikdesai
editor: ''
tags: billing,top-support-issue
ms.assetid: ''
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: cjiang
ms.openlocfilehash: e72c36020014dbeae8a0ce1712cc9d6c0c0c73da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562929"
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Sign up for an Office 365 subscription with your Azure account
If you're Azure subscriber, use your Azure account to sign up for an Office 365 subscription. If you're part of an organization that has an Azure subscription, you can create an Office 365 subscription for users in your existing Azure Active Directory (Azure AD). Sign up to Office 365 using an account that's a member of the Global Admin or Billing Admin directory role in your Azure Active Directory tenant. For more information, see [Check my account permissions in Azure AD](#RoleInAzureAD) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

If you already have both an Office 365 account and an Azure subscription, see [Associate an Office 365 tenant to an Azure subscription](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Get an Office 365 subscription by using your Azure account

1. Go to the [Office 365 product page](https://products.office.com/business), and select a plan.
2. Click **Sign in** on the upper-right corner of the page.

    ![screenshot of Office 365 trial page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Sign in with your Azure account credentials. If you're creating a subscription for your organization, use an Azure account that's a member of the Global Admin or Billing Admin directory role in your Azure Active Directory tenant.

    ![Screenshot of Office 365 sign-in](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Click **Try now**.

    ![Screenshot that confirms your order for Office 365.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. On the order receipt page, click **Continue**.

    ![Screenshot of the Office 365 order receipt](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Now you're all set. If you created the Office 365 subscription for your organization, use the following steps to check that your Azure AD users are now in Office 365.

1. Open the Office 365 admin center.
2. Expand **USERS**, and then click **Active Users**.

    ![Screenshot of the Office 365 admin center users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

After you sign up, the Office 365 subscription is added to the same Azure Active Directory instance that your Azure subscription belongs to. For more information, see [More about Azure and Office 365 subscriptions](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) and [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Check my account permissions in Azure AD
1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Click **More services**, and then search for **Active Directory**.

    ![Screenshot of Active Directory in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Click **Users and groups** > **All users**.
4. Select the user name. 

    ![Screenshot that shows the Azure Active Directory users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Click **Directory role**.
  
    ![Screenshot that shows the Azure portal directory role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  The role **Global administrator** or **Limited administrator** > **Billing administrator** is required to create an Office 365 subscription for users in your existing Azure Active Directory.

    ![Screenshot that shows Azure portal directory role Billing Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>Need help? Contact support.
If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly. 








