---
title: Add an internal support statement to a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to post an internal support statement to a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: c9900333-6c5e-4d7d-b0f4-889015e9550c
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 2d12ca26fb2aa5abddcf44b2e634b2f08b1fb01b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870780"
---
# <a name="add-an-internal-support-statement-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="eb757-103">Add an internal support statement to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="eb757-103">Add an internal support statement to a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="eb757-104">Azure DevTest Labs lets you customize your lab with an internal support statement that provides users with support information about the lab.</span><span class="sxs-lookup"><span data-stu-id="eb757-104">Azure DevTest Labs lets you customize your lab with an internal support statement that provides users with support information about the lab.</span></span> <span data-ttu-id="eb757-105">For example, you can provide contact information so that a user knows how to reach internal support when they need help with troubleshooting or accessing resources in the lab.</span><span class="sxs-lookup"><span data-stu-id="eb757-105">For example, you can provide contact information so that a user knows how to reach internal support when they need help with troubleshooting or accessing resources in the lab.</span></span> <span data-ttu-id="eb757-106">You can also provide links to internal websites or FAQs that your team can access before contacting support.</span><span class="sxs-lookup"><span data-stu-id="eb757-106">You can also provide links to internal websites or FAQs that your team can access before contacting support.</span></span>

<span data-ttu-id="eb757-107">An internal support statement is intended to let you post lab information that doesn't typically change too often.</span><span class="sxs-lookup"><span data-stu-id="eb757-107">An internal support statement is intended to let you post lab information that doesn't typically change too often.</span></span> <span data-ttu-id="eb757-108">To notify users about lab info that is more temporary in nature – such as recent updates to lab policies – see [Post announcement in a lab](devtest-lab-announcements.md).</span><span class="sxs-lookup"><span data-stu-id="eb757-108">To notify users about lab info that is more temporary in nature – such as recent updates to lab policies – see [Post announcement in a lab](devtest-lab-announcements.md).</span></span>

<span data-ttu-id="eb757-109">You can easily disable or edit a support statement after it is no longer applicable.</span><span class="sxs-lookup"><span data-stu-id="eb757-109">You can easily disable or edit a support statement after it is no longer applicable.</span></span>

## <a name="steps-to-add-a-support-statement-to-an-existing-lab"></a><span data-ttu-id="eb757-110">Steps to add a support statement to an existing lab</span><span class="sxs-lookup"><span data-stu-id="eb757-110">Steps to add a support statement to an existing lab</span></span>

1. <span data-ttu-id="eb757-111">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="eb757-111">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="eb757-112">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="eb757-112">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span></span> <span data-ttu-id="eb757-113">(Your lab might already be shown on the Dashboard under **All Resources**).</span><span class="sxs-lookup"><span data-stu-id="eb757-113">(Your lab might already be shown on the Dashboard under **All Resources**).</span></span>
1. <span data-ttu-id="eb757-114">From the list of labs, select the lab in which you want to add a support statement.</span><span class="sxs-lookup"><span data-stu-id="eb757-114">From the list of labs, select the lab in which you want to add a support statement.</span></span>  
1. <span data-ttu-id="eb757-115">On the lab's **Overview** area, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="eb757-115">On the lab's **Overview** area, select **Configuration and policies**.</span></span>  

    ![Configuration and policies button](./media/devtest-lab-internal-support-message/devtestlab-config-and-policies.png)

1. <span data-ttu-id="eb757-117">On the left under **SETTINGS**, select **Internal support**.</span><span class="sxs-lookup"><span data-stu-id="eb757-117">On the left under **SETTINGS**, select **Internal support**.</span></span>

    ![Internal support button](./media/devtest-lab-internal-support-message/devtestlab-internal-support.png)

1. <span data-ttu-id="eb757-119">To create an internal support message for the users in this lab, set Enabled to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="eb757-119">To create an internal support message for the users in this lab, set Enabled to **Yes**.</span></span>

1. <span data-ttu-id="eb757-120">In the **Support message** field, enter the internal support statement that you want to present to your lab users.</span><span class="sxs-lookup"><span data-stu-id="eb757-120">In the **Support message** field, enter the internal support statement that you want to present to your lab users.</span></span> <span data-ttu-id="eb757-121">The support message accepts Markdown.</span><span class="sxs-lookup"><span data-stu-id="eb757-121">The support message accepts Markdown.</span></span> <span data-ttu-id="eb757-122">As you enter the message text, you can view the **Preview** area at the bottom of the screen to see how the message appears to users.</span><span class="sxs-lookup"><span data-stu-id="eb757-122">As you enter the message text, you can view the **Preview** area at the bottom of the screen to see how the message appears to users.</span></span>

    ![Internal support screen to create the message.](./media/devtest-lab-internal-support-message/devtestlab-add-support-statement.png)


1. <span data-ttu-id="eb757-124">Select **Save** once your support statement is ready to post.</span><span class="sxs-lookup"><span data-stu-id="eb757-124">Select **Save** once your support statement is ready to post.</span></span>

<span data-ttu-id="eb757-125">When you no longer want to show this support message to lab users, return to the **Internal support** page and set **Enabled** to **No**.</span><span class="sxs-lookup"><span data-stu-id="eb757-125">When you no longer want to show this support message to lab users, return to the **Internal support** page and set **Enabled** to **No**.</span></span>

## <a name="steps-for-users-to-view-the-support-message"></a><span data-ttu-id="eb757-126">Steps for users to view the support message</span><span class="sxs-lookup"><span data-stu-id="eb757-126">Steps for users to view the support message</span></span>

1. <span data-ttu-id="eb757-127">From the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), select a lab.</span><span class="sxs-lookup"><span data-stu-id="eb757-127">From the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), select a lab.</span></span>

1. <span data-ttu-id="eb757-128">On the lab's **Overview** area, select **Internal support**.</span><span class="sxs-lookup"><span data-stu-id="eb757-128">On the lab's **Overview** area, select **Internal support**.</span></span>  

    ![Internal support button](./media/devtest-lab-internal-support-message/devtestlab-internal-support.png)


1. <span data-ttu-id="eb757-130">If a support message is posted, the user can view it from the Internal support pane.</span><span class="sxs-lookup"><span data-stu-id="eb757-130">If a support message is posted, the user can view it from the Internal support pane.</span></span>

    ![Internal support pane showing support message posted](./media/devtest-lab-internal-support-message/devtestlab-view-suport-statement.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="eb757-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb757-132">Next steps</span></span>
* <span data-ttu-id="eb757-133">Internal support statements are typically used to provide support information that doesn't change that frequently.</span><span class="sxs-lookup"><span data-stu-id="eb757-133">Internal support statements are typically used to provide support information that doesn't change that frequently.</span></span> <span data-ttu-id="eb757-134">You can also learn how to [post an announcement to a lab](devtest-lab-announcements.md) to inform users of temporary changes or updates to the lab.</span><span class="sxs-lookup"><span data-stu-id="eb757-134">You can also learn how to [post an announcement to a lab](devtest-lab-announcements.md) to inform users of temporary changes or updates to the lab.</span></span>
* <span data-ttu-id="eb757-135">[Set policies and schedules](devtest-lab-set-lab-policy.md) provides information about how you can apply other restrictions and conventions across your subscription by using customized policies.</span><span class="sxs-lookup"><span data-stu-id="eb757-135">[Set policies and schedules](devtest-lab-set-lab-policy.md) provides information about how you can apply other restrictions and conventions across your subscription by using customized policies.</span></span>