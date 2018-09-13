---
title: Security wizard in PIM - Azure | Microsoft Docs
description: Describes the security wizard that appears the first time you use Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 02/27/2017
ms.author: rolyon
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 178a4c5e978075f2a59b22a1cccf462138527964
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867999"
---
# <a name="security-wizard-in-pim"></a><span data-ttu-id="17401-103">Security wizard in PIM</span><span class="sxs-lookup"><span data-stu-id="17401-103">Security wizard in PIM</span></span>
<span data-ttu-id="17401-104">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span><span class="sxs-lookup"><span data-stu-id="17401-104">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="17401-105">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span><span class="sxs-lookup"><span data-stu-id="17401-105">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="17401-106">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span><span class="sxs-lookup"><span data-stu-id="17401-106">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="17401-107">What to expect</span><span class="sxs-lookup"><span data-stu-id="17401-107">What to expect</span></span>
<span data-ttu-id="17401-108">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span><span class="sxs-lookup"><span data-stu-id="17401-108">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="17401-109">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span><span class="sxs-lookup"><span data-stu-id="17401-109">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="17401-110">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span><span class="sxs-lookup"><span data-stu-id="17401-110">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="17401-111">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span><span class="sxs-lookup"><span data-stu-id="17401-111">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="17401-112">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span><span class="sxs-lookup"><span data-stu-id="17401-112">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="17401-113">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span><span class="sxs-lookup"><span data-stu-id="17401-113">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="17401-114">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="17401-114">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="17401-115">If you plan to require MFA for activation for that role, that user will be locked out.</span><span class="sxs-lookup"><span data-stu-id="17401-115">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="17401-116">After you have made changes, the wizard will no longer show up.</span><span class="sxs-lookup"><span data-stu-id="17401-116">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="17401-117">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span><span class="sxs-lookup"><span data-stu-id="17401-117">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="17401-118">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](pim-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="17401-118">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](pim-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="17401-119">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](pim-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="17401-119">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](pim-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="17401-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="17401-120">Next steps</span></span>

- [<span data-ttu-id="17401-121">Start using PIM</span><span class="sxs-lookup"><span data-stu-id="17401-121">Start using PIM</span></span>](pim-getting-started.md)
- [<span data-ttu-id="17401-122">Assign Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="17401-122">Assign Azure AD directory roles in PIM</span></span>](pim-how-to-add-role-to-user.md)
- [<span data-ttu-id="17401-123">Grant access to other administrators to manage PIM</span><span class="sxs-lookup"><span data-stu-id="17401-123">Grant access to other administrators to manage PIM</span></span>](pim-how-to-give-access-to-pim.md)
