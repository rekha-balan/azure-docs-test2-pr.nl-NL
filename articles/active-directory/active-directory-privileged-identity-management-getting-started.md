---
title: Get started with Azure AD Privileged Identity Management | Microsoft Docs
description: Learn how to manage privileged identities with the Azure Active Directory Privileged Identity Management application in Azure portal.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 99488b3de8310326bd30bb028d61a4612a2027e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563910"
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="fc20d-103">Start using Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="fc20d-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="fc20d-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span><span class="sxs-lookup"><span data-stu-id="fc20d-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="fc20d-105">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="fc20d-105">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="fc20d-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="fc20d-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="fc20d-107">Add the Privileged Identity Management application</span><span class="sxs-lookup"><span data-stu-id="fc20d-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="fc20d-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="fc20d-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="fc20d-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span><span class="sxs-lookup"><span data-stu-id="fc20d-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="fc20d-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fc20d-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="fc20d-111">Select the directory where you will use PIM.</span><span class="sxs-lookup"><span data-stu-id="fc20d-111">Select the directory where you will use PIM.</span></span>
3. <span data-ttu-id="fc20d-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="fc20d-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="fc20d-113">Check **Pin to dashboard** and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fc20d-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="fc20d-114">The Privileged Identity Management application opens.</span><span class="sxs-lookup"><span data-stu-id="fc20d-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="fc20d-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, then the [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through the initial assignment experience.</span><span class="sxs-lookup"><span data-stu-id="fc20d-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, then the [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through the initial assignment experience.</span></span> <span data-ttu-id="fc20d-116">After that, you will automatically become the first **Security administrator** and **Privileged role administrator** of the directory.</span><span class="sxs-lookup"><span data-stu-id="fc20d-116">After that, you will automatically become the first **Security administrator** and **Privileged role administrator** of the directory.</span></span> <span data-ttu-id="fc20d-117">Only a privileged role administrator can access this application to manage the access for other administrators.</span><span class="sxs-lookup"><span data-stu-id="fc20d-117">Only a privileged role administrator can access this application to manage the access for other administrators.</span></span>  

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="fc20d-118">Navigate to your tasks</span><span class="sxs-lookup"><span data-stu-id="fc20d-118">Navigate to your tasks</span></span>
<span data-ttu-id="fc20d-119">Once Azure AD Privileged Identity Management is set up, you'll see the navigation blade whenever you open the application.</span><span class="sxs-lookup"><span data-stu-id="fc20d-119">Once Azure AD Privileged Identity Management is set up, you'll see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="fc20d-120">Use this blade to accomplish your identity management tasks.</span><span class="sxs-lookup"><span data-stu-id="fc20d-120">Use this blade to accomplish your identity management tasks.</span></span>

![Top-level tasks for PIM - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-getting-started/pim_tasks.png)

* <span data-ttu-id="fc20d-122">**Activate my roles** takes you to the list of roles that are assigned to you.</span><span class="sxs-lookup"><span data-stu-id="fc20d-122">**Activate my roles** takes you to the list of roles that are assigned to you.</span></span> <span data-ttu-id="fc20d-123">This is where you will activate any roles that you are eligible for.</span><span class="sxs-lookup"><span data-stu-id="fc20d-123">This is where you will activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="fc20d-124">**Manage privileged roles** is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span><span class="sxs-lookup"><span data-stu-id="fc20d-124">**Manage privileged roles** is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="fc20d-125">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span><span class="sxs-lookup"><span data-stu-id="fc20d-125">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>
* <span data-ttu-id="fc20d-126">**Review privileged access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span><span class="sxs-lookup"><span data-stu-id="fc20d-126">**Review privileged access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc20d-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc20d-127">Next steps</span></span>
<span data-ttu-id="fc20d-128">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span><span class="sxs-lookup"><span data-stu-id="fc20d-128">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png


