---
title: Manage access to Azure billing using roles | Microsoft Docs
description: ''
services: ''
documentationcenter: ''
author: vikramdesai01
manager: vikdesai
editor: ''
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 38702fde344bb5fb831f7c26177438456035beae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865777"
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="051a6-102">Manage access to billing information for Azure using role-based access control</span><span class="sxs-lookup"><span data-stu-id="051a6-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="051a6-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span><span class="sxs-lookup"><span data-stu-id="051a6-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="051a6-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span><span class="sxs-lookup"><span data-stu-id="051a6-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="051a6-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../role-based-access-control/built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="051a6-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../role-based-access-control/built-in-roles.md).</span></span>

## <a name="opt-in"></a> <span data-ttu-id="051a6-106">Allowing additional users to access invoices</span><span class="sxs-lookup"><span data-stu-id="051a6-106">Allowing additional users to access invoices</span></span>

<span data-ttu-id="051a6-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span><span class="sxs-lookup"><span data-stu-id="051a6-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="051a6-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="051a6-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="051a6-109">Select **Invoices** and then **Access to invoices**.</span><span class="sxs-lookup"><span data-stu-id="051a6-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![Screenshot shows how to delegate access to invoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="051a6-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span><span class="sxs-lookup"><span data-stu-id="051a6-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![Screenshot shows on-off to delegate access to invoice](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="051a6-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="051a6-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="051a6-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span><span class="sxs-lookup"><span data-stu-id="051a6-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="051a6-115">The Account Administrator can also configure to have invoices sent via email.</span><span class="sxs-lookup"><span data-stu-id="051a6-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="051a6-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="051a6-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="051a6-117">Adding users to the Billing Reader role</span><span class="sxs-lookup"><span data-stu-id="051a6-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="051a6-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="051a6-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="051a6-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span><span class="sxs-lookup"><span data-stu-id="051a6-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="051a6-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="051a6-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="051a6-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="051a6-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="051a6-122">Select **Access control (IAM)** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="051a6-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Screenshot shows IAM in the subscription blade](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="051a6-124">Choose **Billing Reader** in the **Select a role** page.</span><span class="sxs-lookup"><span data-stu-id="051a6-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![Screenshot shows Billing Reader in the popup view](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="051a6-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span><span class="sxs-lookup"><span data-stu-id="051a6-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![Screenshot that shows to enter email to invite someone](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="051a6-128">Follow instructions in the invite email to log in as a Billing Reader.</span><span class="sxs-lookup"><span data-stu-id="051a6-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![Screenshot that shows what the Billing Reader can see in Azure portal](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="051a6-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span><span class="sxs-lookup"><span data-stu-id="051a6-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="051a6-131">Adding users to other roles</span><span class="sxs-lookup"><span data-stu-id="051a6-131">Adding users to other roles</span></span>

<span data-ttu-id="051a6-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span><span class="sxs-lookup"><span data-stu-id="051a6-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="051a6-133">To manage these roles, see [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="051a6-133">To manage these roles, see [Manage access using RBAC and the Azure portal](../role-based-access-control/role-assignments-portal.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="051a6-134">Who can access the [Account Center](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="051a6-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="051a6-135">Only the Account Administrator can log in to the Account center.</span><span class="sxs-lookup"><span data-stu-id="051a6-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="051a6-136">The Account Administrator is the legal owner of the subscription.</span><span class="sxs-lookup"><span data-stu-id="051a6-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="051a6-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span><span class="sxs-lookup"><span data-stu-id="051a6-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="051a6-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span><span class="sxs-lookup"><span data-stu-id="051a6-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="051a6-139">Need help?</span><span class="sxs-lookup"><span data-stu-id="051a6-139">Need help?</span></span> <span data-ttu-id="051a6-140">Contact support.</span><span class="sxs-lookup"><span data-stu-id="051a6-140">Contact support.</span></span>

<span data-ttu-id="051a6-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="051a6-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
