---
title: Add a new Azure Stack tenant account in Azure Active Directory | Microsoft Docs
description: After deploying Microsoft Azure Stack POC, you’ll need to create at least one tenant user account so you can explore the tenant portal.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: bd0ae4ab62e77eeedf8d9e279b8914838749ddca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549584"
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="848d7-103">Add a new Azure Stack tenant account in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="848d7-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="848d7-104">After [deploying the Azure Stack POC](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore the tenant portal and test your offers and plans.</span><span class="sxs-lookup"><span data-stu-id="848d7-104">After [deploying the Azure Stack POC](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore the tenant portal and test your offers and plans.</span></span> <span data-ttu-id="848d7-105">You can create a tenant account by [using the Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="848d7-105">You can create a tenant account by [using the Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-the-azure-portal"></a><span data-ttu-id="848d7-106">Create an Azure Stack tenant account using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="848d7-106">Create an Azure Stack tenant account using the Azure portal</span></span>
<span data-ttu-id="848d7-107">You must have an Azure subscription to use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="848d7-107">You must have an Azure subscription to use the Azure portal.</span></span>

1. <span data-ttu-id="848d7-108">Log in to [Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="848d7-108">Log in to [Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="848d7-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="848d7-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="848d7-110">In the directory list, click the directory that you want to use for Azure Stack, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="848d7-110">In the directory list, click the directory that you want to use for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="848d7-111">On this directory page, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="848d7-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="848d7-112">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="848d7-112">Click **Add user**.</span></span>
6. <span data-ttu-id="848d7-113">In the **Add user** wizard, in the **Type of user** list, choose **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="848d7-113">In the **Add user** wizard, in the **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="848d7-114">In the **User name** box, type a name for the user.</span><span class="sxs-lookup"><span data-stu-id="848d7-114">In the **User name** box, type a name for the user.</span></span>
8. <span data-ttu-id="848d7-115">In the **@** box, choose the appropriate entry.</span><span class="sxs-lookup"><span data-stu-id="848d7-115">In the **@** box, choose the appropriate entry.</span></span>
9. <span data-ttu-id="848d7-116">Click the next arrow.</span><span class="sxs-lookup"><span data-stu-id="848d7-116">Click the next arrow.</span></span>
10. <span data-ttu-id="848d7-117">In the **User profile** page of the wizard, type a **First name**, **Last name**, and **Display name**.</span><span class="sxs-lookup"><span data-stu-id="848d7-117">In the **User profile** page of the wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="848d7-118">In the **Role** list, choose **User**.</span><span class="sxs-lookup"><span data-stu-id="848d7-118">In the **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="848d7-119">Click the next arrow.</span><span class="sxs-lookup"><span data-stu-id="848d7-119">Click the next arrow.</span></span>
13. <span data-ttu-id="848d7-120">On the **Get temporary password** page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="848d7-120">On the **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="848d7-121">Copy the **New password**.</span><span class="sxs-lookup"><span data-stu-id="848d7-121">Copy the **New password**.</span></span>
15. <span data-ttu-id="848d7-122">Log in to Microsoft Azure with the new account.</span><span class="sxs-lookup"><span data-stu-id="848d7-122">Log in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="848d7-123">Change the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="848d7-123">Change the password when prompted.</span></span>
16. <span data-ttu-id="848d7-124">Log in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span><span class="sxs-lookup"><span data-stu-id="848d7-124">Log in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="848d7-125">Create an Azure Stack tenant account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="848d7-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="848d7-126">If you don't have an Azure subscription, you can't use the Azure portal to add a tenant user account.</span><span class="sxs-lookup"><span data-stu-id="848d7-126">If you don't have an Azure subscription, you can't use the Azure portal to add a tenant user account.</span></span> <span data-ttu-id="848d7-127">In this case, you can use the Azure Active Directory Module for Windows PowerShell instead.</span><span class="sxs-lookup"><span data-stu-id="848d7-127">In this case, you can use the Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="848d7-128">If you are using Microsoft Account (Live ID) to deploy Azure Stack PoC, you can't use AAD PowerShell to create tenant account.</span><span class="sxs-lookup"><span data-stu-id="848d7-128">If you are using Microsoft Account (Live ID) to deploy Azure Stack PoC, you can't use AAD PowerShell to create tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="848d7-129">Install the [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span><span class="sxs-lookup"><span data-stu-id="848d7-129">Install the [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="848d7-130">Install the [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span><span class="sxs-lookup"><span data-stu-id="848d7-130">Install the [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="848d7-131">Run the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="848d7-131">Run the following cmdlets:</span></span>

    ```powershell
    # Provide the AAD credential you use to deploy Azure Stack PoC

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with the initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="848d7-132">Sign in to Microsoft Azure with the new account.</span><span class="sxs-lookup"><span data-stu-id="848d7-132">Sign in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="848d7-133">Change the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="848d7-133">Change the password when prompted.</span></span>
2. <span data-ttu-id="848d7-134">Sign in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span><span class="sxs-lookup"><span data-stu-id="848d7-134">Sign in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

