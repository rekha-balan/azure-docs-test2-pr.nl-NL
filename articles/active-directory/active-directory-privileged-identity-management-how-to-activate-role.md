---
title: How to activate or deactivate a role | Microsoft Docs
description: Learn how to activate roles for privileged identities with the Azure Privileged Identity Management application.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 06480ebb5d322e1b565f137290bb0b6f64f3084e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553717"
---
# <a name="how-to-activate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="5bfa5-103">How to activate or deactivate roles in Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="5bfa5-103">How to activate or deactivate roles in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="5bfa5-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="5bfa5-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform a task that requires that role.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform a task that requires that role.</span></span> <span data-ttu-id="5bfa5-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span></span> <span data-ttu-id="5bfa5-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span></span> <span data-ttu-id="5bfa5-108">You can request to activate that role when you need its privileges, and then you'll have admin control for a predetermined time period.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-108">You can request to activate that role when you need its privileges, and then you'll have admin control for a predetermined time period.</span></span>

<span data-ttu-id="5bfa5-109">This article is for admins who need to activate their role in Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="5bfa5-109">This article is for admins who need to activate their role in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="5bfa5-110">It walks you through the steps to activate a role when you need the permissions, and deactivate the role when you're done.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-110">It walks you through the steps to activate a role when you need the permissions, and deactivate the role when you're done.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="5bfa5-111">Add the Privileged Identity Management application</span><span class="sxs-lookup"><span data-stu-id="5bfa5-111">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="5bfa5-112">Use the Azure AD Privileged Identity Management application in the [Azure portal](https://portal.azure.com/) to request a role activation, even if you're going to operate in another portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-112">Use the Azure AD Privileged Identity Management application in the [Azure portal](https://portal.azure.com/) to request a role activation, even if you're going to operate in another portal or PowerShell.</span></span> <span data-ttu-id="5bfa5-113">If you don't have the Azure AD Privileged Identity Management application on your Azure portal, follow these steps to get started.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-113">If you don't have the Azure AD Privileged Identity Management application on your Azure portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="5bfa5-114">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5bfa5-114">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5bfa5-115">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-115">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="5bfa5-116">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-116">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="5bfa5-117">Check **Pin to dashboard** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-117">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="5bfa5-118">The Privileged Identity Management application opens.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-118">The Privileged Identity Management application opens.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="5bfa5-119">Activate a role</span><span class="sxs-lookup"><span data-stu-id="5bfa5-119">Activate a role</span></span>
<span data-ttu-id="5bfa5-120">When you need to take on a role, you can request activation using the **Activate my roles** button in the Azure AD Privileged Identity Management application.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-120">When you need to take on a role, you can request activation using the **Activate my roles** button in the Azure AD Privileged Identity Management application.</span></span>

1. <span data-ttu-id="5bfa5-121">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-121">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="5bfa5-122">Select **Activate my roles**.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-122">Select **Activate my roles**.</span></span> <span data-ttu-id="5bfa5-123">A list of roles that have been assigned to you appears.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-123">A list of roles that have been assigned to you appears.</span></span>
3. <span data-ttu-id="5bfa5-124">Select the role you want to activate.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-124">Select the role you want to activate.</span></span>
4. <span data-ttu-id="5bfa5-125">Select **Activate**.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-125">Select **Activate**.</span></span> <span data-ttu-id="5bfa5-126">The **Request role activation** blade appears.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-126">The **Request role activation** blade appears.</span></span>
5. <span data-ttu-id="5bfa5-127">Some roles require Multi-Factor Authentication (MFA) before you can activate the role.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-127">Some roles require Multi-Factor Authentication (MFA) before you can activate the role.</span></span> <span data-ttu-id="5bfa5-128">You only have to authenticate once per session.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-128">You only have to authenticate once per session.</span></span>
   
    ![Verify with MFA before role activation - screenshot][2]
6. <span data-ttu-id="5bfa5-130">Enter the reason for the activation request in the text field.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-130">Enter the reason for the activation request in the text field.</span></span>  <span data-ttu-id="5bfa5-131">Some roles require you to supply a trouble ticket number.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-131">Some roles require you to supply a trouble ticket number.</span></span>
7. <span data-ttu-id="5bfa5-132">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-132">Select **OK**.</span></span>  <span data-ttu-id="5bfa5-133">The role is now activated, and the role change is visible in the Microsoft Online Services.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-133">The role is now activated, and the role change is visible in the Microsoft Online Services.</span></span>

## <a name="deactivate-a-role"></a><span data-ttu-id="5bfa5-134">Deactivate a role</span><span class="sxs-lookup"><span data-stu-id="5bfa5-134">Deactivate a role</span></span>
<span data-ttu-id="5bfa5-135">Once a role has been activated, it automatically deactivates when its time limit is reached.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-135">Once a role has been activated, it automatically deactivates when its time limit is reached.</span></span>

<span data-ttu-id="5bfa5-136">If you are done early, you can also deactivate a role manually in the Azure AD Privileged Identity Management application.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-136">If you are done early, you can also deactivate a role manually in the Azure AD Privileged Identity Management application.</span></span>  <span data-ttu-id="5bfa5-137">Select **Activate my roles**, choose the role you're done using, and select **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-137">Select **Activate my roles**, choose the role you're done using, and select **Deactivate**.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="5bfa5-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="5bfa5-138">Next steps</span></span>
<span data-ttu-id="5bfa5-139">If you're interested in learning more about Azure AD Privileged Identity Management, the following links have more information.</span><span class="sxs-lookup"><span data-stu-id="5bfa5-139">If you're interested in learning more about Azure AD Privileged Identity Management, the following links have more information.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png


