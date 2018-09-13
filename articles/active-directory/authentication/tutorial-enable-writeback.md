---
title: Azure AD enable password writeback
description: In this tutorial, you will enable password writeback to get cloud initiated password changes back to on-premises AD as part of Azure AD Connect.
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: tutorial
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 9512c800a35ad4a819c657b07227d781c63c6399
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870321"
---
# <a name="tutorial-enabling-password-writeback"></a><span data-ttu-id="c219a-103">Tutorial: Enabling password writeback</span><span class="sxs-lookup"><span data-stu-id="c219a-103">Tutorial: Enabling password writeback</span></span>

<span data-ttu-id="c219a-104">In this tutorial, you will enable password writeback for your hybrid environment.</span><span class="sxs-lookup"><span data-stu-id="c219a-104">In this tutorial, you will enable password writeback for your hybrid environment.</span></span> <span data-ttu-id="c219a-105">Password writeback is used to synchronize password changes in Azure Active Directory (Azure AD) back to your on-premises Active Directory Domain Services (AD DS) environment.</span><span class="sxs-lookup"><span data-stu-id="c219a-105">Password writeback is used to synchronize password changes in Azure Active Directory (Azure AD) back to your on-premises Active Directory Domain Services (AD DS) environment.</span></span> <span data-ttu-id="c219a-106">Password writeback is enabled as part of Azure AD Connect to provide a secure mechanism to send password changes back to an existing on-premises directory from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c219a-106">Password writeback is enabled as part of Azure AD Connect to provide a secure mechanism to send password changes back to an existing on-premises directory from Azure AD.</span></span> <span data-ttu-id="c219a-107">You can find more detail about the inner workings of password writeback in the article, [What is password writeback](concept-sspr-writeback.md).</span><span class="sxs-lookup"><span data-stu-id="c219a-107">You can find more detail about the inner workings of password writeback in the article, [What is password writeback](concept-sspr-writeback.md).</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c219a-108">Enable password writeback option in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c219a-108">Enable password writeback option in Azure AD Connect</span></span>
> * <span data-ttu-id="c219a-109">Enable password writeback option in self-service password reset (SSPR)</span><span class="sxs-lookup"><span data-stu-id="c219a-109">Enable password writeback option in self-service password reset (SSPR)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c219a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c219a-110">Prerequisites</span></span>

* <span data-ttu-id="c219a-111">Access to a working Azure AD tenant with at least a trial license assigned.</span><span class="sxs-lookup"><span data-stu-id="c219a-111">Access to a working Azure AD tenant with at least a trial license assigned.</span></span>
* <span data-ttu-id="c219a-112">An account with Global Administrator privileges in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c219a-112">An account with Global Administrator privileges in your Azure AD tenant.</span></span>
* <span data-ttu-id="c219a-113">An existing server configured running a current version of [Azure AD Connect](../connect/active-directory-aadconnect-get-started-express.md).</span><span class="sxs-lookup"><span data-stu-id="c219a-113">An existing server configured running a current version of [Azure AD Connect](../connect/active-directory-aadconnect-get-started-express.md).</span></span>
* <span data-ttu-id="c219a-114">Previous self-service password reset (SSPR) tutorials have been completed.</span><span class="sxs-lookup"><span data-stu-id="c219a-114">Previous self-service password reset (SSPR) tutorials have been completed.</span></span>

## <a name="enable-password-writeback-option-in-azure-ad-connect"></a><span data-ttu-id="c219a-115">Enable password writeback option in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c219a-115">Enable password writeback option in Azure AD Connect</span></span>

<span data-ttu-id="c219a-116">To enable password writeback we will first need to enable the feature from the server that you have installed Azure AD Connect on.</span><span class="sxs-lookup"><span data-stu-id="c219a-116">To enable password writeback we will first need to enable the feature from the server that you have installed Azure AD Connect on.</span></span>

1. <span data-ttu-id="c219a-117">To configure and enable password writeback, sign in to your Azure AD Connect server and start the **Azure AD Connect** configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="c219a-117">To configure and enable password writeback, sign in to your Azure AD Connect server and start the **Azure AD Connect** configuration wizard.</span></span>
2. <span data-ttu-id="c219a-118">On the **Welcome** page, select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="c219a-118">On the **Welcome** page, select **Configure**.</span></span>
3. <span data-ttu-id="c219a-119">On the **Additional tasks** page, select **Customize synchronization options**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="c219a-119">On the **Additional tasks** page, select **Customize synchronization options**, and then select **Next**.</span></span>
4. <span data-ttu-id="c219a-120">On the **Connect to Azure AD** page, enter a global administrator credential, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="c219a-120">On the **Connect to Azure AD** page, enter a global administrator credential, and then select **Next**.</span></span>
5. <span data-ttu-id="c219a-121">On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="c219a-121">On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.</span></span>
6. <span data-ttu-id="c219a-122">On the **Optional features** page, select the box next to **Password writeback** and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="c219a-122">On the **Optional features** page, select the box next to **Password writeback** and select **Next**.</span></span>
7. <span data-ttu-id="c219a-123">On the **Ready to configure** page, select **Configure** and wait for the process to finish.</span><span class="sxs-lookup"><span data-stu-id="c219a-123">On the **Ready to configure** page, select **Configure** and wait for the process to finish.</span></span>
8. <span data-ttu-id="c219a-124">When you see the configuration finish, select **Exit**.</span><span class="sxs-lookup"><span data-stu-id="c219a-124">When you see the configuration finish, select **Exit**.</span></span>

## <a name="enable-password-writeback-option-in-sspr"></a><span data-ttu-id="c219a-125">Enable password writeback option in SSPR</span><span class="sxs-lookup"><span data-stu-id="c219a-125">Enable password writeback option in SSPR</span></span>

<span data-ttu-id="c219a-126">Enabling the password writeback feature in Azure AD Connect is only half of the story.</span><span class="sxs-lookup"><span data-stu-id="c219a-126">Enabling the password writeback feature in Azure AD Connect is only half of the story.</span></span> <span data-ttu-id="c219a-127">Allowing SSPR to use password writeback completes the loop thereby allowing users who change or reset their password to have that password set on-premises as well.</span><span class="sxs-lookup"><span data-stu-id="c219a-127">Allowing SSPR to use password writeback completes the loop thereby allowing users who change or reset their password to have that password set on-premises as well.</span></span>

1. <span data-ttu-id="c219a-128">Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.</span><span class="sxs-lookup"><span data-stu-id="c219a-128">Sign in to the [Azure portal](https://portal.azure.com) using a Global Administrator account.</span></span>
2. <span data-ttu-id="c219a-129">Browse to **Azure Active Directory**, click on **Password Reset**, then choose **On-premises integration**.</span><span class="sxs-lookup"><span data-stu-id="c219a-129">Browse to **Azure Active Directory**, click on **Password Reset**, then choose **On-premises integration**.</span></span>
3. <span data-ttu-id="c219a-130">Set the option for **Write back passwords to your on-premises directory**, to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c219a-130">Set the option for **Write back passwords to your on-premises directory**, to **Yes**.</span></span>
4. <span data-ttu-id="c219a-131">Set the option for **Allow users to unlock accounts without resetting their password**, to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c219a-131">Set the option for **Allow users to unlock accounts without resetting their password**, to **Yes**.</span></span>
5. <span data-ttu-id="c219a-132">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="c219a-132">Click **Save**</span></span>

## <a name="next-steps"></a><span data-ttu-id="c219a-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="c219a-133">Next steps</span></span>

<span data-ttu-id="c219a-134">In this tutorial, you have enabled password writeback for self-service password reset.</span><span class="sxs-lookup"><span data-stu-id="c219a-134">In this tutorial, you have enabled password writeback for self-service password reset.</span></span> <span data-ttu-id="c219a-135">Leave the Azure portal window open and continue to the next tutorial to configure additional settings related to self-service password reset before you roll out the solution in a pilot.</span><span class="sxs-lookup"><span data-stu-id="c219a-135">Leave the Azure portal window open and continue to the next tutorial to configure additional settings related to self-service password reset before you roll out the solution in a pilot.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c219a-136">Enabling SSPR at the Windows logon screen</span><span class="sxs-lookup"><span data-stu-id="c219a-136">Enabling SSPR at the Windows logon screen</span></span>](tutorial-sspr-windows.md)
