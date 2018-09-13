---
title: Multi-factor authentication (MFA) and PIM - Azure | Microsoft Docs
description: Learn how Azure AD Privileged Identity Management (PIM) validates multi-factor authentication (MFA).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 08/31/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: cfa092e8aebe92192ecca8aec2721282e603cc5b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866700"
---
# <a name="multi-factor-authentication-mfa-and-pim"></a><span data-ttu-id="eaf1a-103">Multi-factor authentication (MFA) and PIM</span><span class="sxs-lookup"><span data-stu-id="eaf1a-103">Multi-factor authentication (MFA) and PIM</span></span>

<span data-ttu-id="eaf1a-104">We recommend that you require multi-factor authentication (MFA) for all your administrators.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-104">We recommend that you require multi-factor authentication (MFA) for all your administrators.</span></span> <span data-ttu-id="eaf1a-105">This reduces the risk of an attack due to a compromised password.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-105">This reduces the risk of an attack due to a compromised password.</span></span>

<span data-ttu-id="eaf1a-106">You can require that users complete an MFA challenge when they sign in.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-106">You can require that users complete an MFA challenge when they sign in.</span></span> <span data-ttu-id="eaf1a-107">You can also require that users complete an MFA challenge when they activate a role in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="eaf1a-107">You can also require that users complete an MFA challenge when they activate a role in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="eaf1a-108">This way, if the user didn't complete an MFA challenge when they signed in, they will be prompted to do so by PIM.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-108">This way, if the user didn't complete an MFA challenge when they signed in, they will be prompted to do so by PIM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eaf1a-109">Right now, Azure MFA only works with work or school accounts, not Microsoft accounts (usually a personal account that's used to sign in to Microsoft services like Skype, Xbox, Outlook.com, etc.).</span><span class="sxs-lookup"><span data-stu-id="eaf1a-109">Right now, Azure MFA only works with work or school accounts, not Microsoft accounts (usually a personal account that's used to sign in to Microsoft services like Skype, Xbox, Outlook.com, etc.).</span></span> <span data-ttu-id="eaf1a-110">Because of this, anyone using a Microsoft account can't be an eligible administrator because they can't use MFA to activate their roles.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-110">Because of this, anyone using a Microsoft account can't be an eligible administrator because they can't use MFA to activate their roles.</span></span> <span data-ttu-id="eaf1a-111">If these users need to continue managing workloads using a Microsoft account, elevate them to permanent administrators for now.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-111">If these users need to continue managing workloads using a Microsoft account, elevate them to permanent administrators for now.</span></span>

## <a name="how-pim-validates-mfa"></a><span data-ttu-id="eaf1a-112">How PIM validates MFA</span><span class="sxs-lookup"><span data-stu-id="eaf1a-112">How PIM validates MFA</span></span>

<span data-ttu-id="eaf1a-113">There are two options for validating MFA when a user activates a role.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-113">There are two options for validating MFA when a user activates a role.</span></span>

<span data-ttu-id="eaf1a-114">The simplest option is to rely on Azure MFA for users who are activating a privileged role.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-114">The simplest option is to rely on Azure MFA for users who are activating a privileged role.</span></span> <span data-ttu-id="eaf1a-115">To do this, first check that those users are licensed, if necessary, and have registered for Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-115">To do this, first check that those users are licensed, if necessary, and have registered for Azure MFA.</span></span> <span data-ttu-id="eaf1a-116">For more information about how to deploy Azure MFA, see [Deploy cloud-based Azure Multi-Factor Authentication](../authentication/howto-mfa-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="eaf1a-116">For more information about how to deploy Azure MFA, see [Deploy cloud-based Azure Multi-Factor Authentication](../authentication/howto-mfa-getstarted.md).</span></span> <span data-ttu-id="eaf1a-117">It is recommended, but not required, that you configure Azure AD to enforce MFA for these users when they sign in.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-117">It is recommended, but not required, that you configure Azure AD to enforce MFA for these users when they sign in.</span></span> <span data-ttu-id="eaf1a-118">This is because the MFA checks will be made by PIM itself.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-118">This is because the MFA checks will be made by PIM itself.</span></span>

<span data-ttu-id="eaf1a-119">Alternatively, if users authenticate on-premises you can have your identity provider be responsible for MFA.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-119">Alternatively, if users authenticate on-premises you can have your identity provider be responsible for MFA.</span></span> <span data-ttu-id="eaf1a-120">For example, if you have configured AD Federation Services to require smartcard-based authentication before accessing Azure AD, [Securing cloud resources with Azure Multi-Factor Authentication and AD FS](../authentication/howto-mfa-adfs.md) includes instructions for configuring AD FS to send claims to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-120">For example, if you have configured AD Federation Services to require smartcard-based authentication before accessing Azure AD, [Securing cloud resources with Azure Multi-Factor Authentication and AD FS](../authentication/howto-mfa-adfs.md) includes instructions for configuring AD FS to send claims to Azure AD.</span></span> <span data-ttu-id="eaf1a-121">When a user tries to activate a role, PIM will accept that MFA has already been validated for the user once it receives the appropriate claims.</span><span class="sxs-lookup"><span data-stu-id="eaf1a-121">When a user tries to activate a role, PIM will accept that MFA has already been validated for the user once it receives the appropriate claims.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaf1a-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="eaf1a-122">Next steps</span></span>

- [<span data-ttu-id="eaf1a-123">Configure Azure AD directory role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="eaf1a-123">Configure Azure AD directory role settings in PIM</span></span>](pim-how-to-change-default-settings.md)
- [<span data-ttu-id="eaf1a-124">Configure Azure resource role settings in PIM</span><span class="sxs-lookup"><span data-stu-id="eaf1a-124">Configure Azure resource role settings in PIM</span></span>](pim-resource-roles-configure-role-settings.md)
