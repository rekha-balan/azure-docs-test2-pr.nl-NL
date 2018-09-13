---
title: Set password expiration policies in Azure Active Directory | Microsoft Docs
description: Learn how to check expiration policies and change user password expiration either singly or in bulk for Azure Active Directory passwords
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 6887250c-15d4-4b59-a161-f0380c0f0acb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: curtand
ms.openlocfilehash: e279ca5f86ec2870955f0fd204e852252a34a42e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550067"
---
# <a name="set-password-expiration-policies-in-azure-active-directory"></a><span data-ttu-id="00ab1-103">Set password expiration policies in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00ab1-103">Set password expiration policies in Azure Active Directory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="00ab1-104">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="00ab1-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="00ab1-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="00ab1-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
>
>

<span data-ttu-id="00ab1-106">As a global administrator for a Microsoft cloud service, you can use the Microsoft Azure Active Directory Module for Windows PowerShell to set up user passwords not to expire.</span><span class="sxs-lookup"><span data-stu-id="00ab1-106">As a global administrator for a Microsoft cloud service, you can use the Microsoft Azure Active Directory Module for Windows PowerShell to set up user passwords not to expire.</span></span> <span data-ttu-id="00ab1-107">You can also use Windows PowerShell cmdlets to remove the never-expires configuration, or to see which user passwords are set up not to expire.</span><span class="sxs-lookup"><span data-stu-id="00ab1-107">You can also use Windows PowerShell cmdlets to remove the never-expires configuration, or to see which user passwords are set up not to expire.</span></span> <span data-ttu-id="00ab1-108">This article provides help for cloud services, such as Microsoft Intune and Office 365, which rely on Microsoft Azure Active Directory for identity and directory services.</span><span class="sxs-lookup"><span data-stu-id="00ab1-108">This article provides help for cloud services, such as Microsoft Intune and Office 365, which rely on Microsoft Azure Active Directory for identity and directory services.</span></span>

> [!NOTE]
> <span data-ttu-id="00ab1-109">Only passwords for user accounts that are not synchronized through directory synchronization can be configured not to expire.</span><span class="sxs-lookup"><span data-stu-id="00ab1-109">Only passwords for user accounts that are not synchronized through directory synchronization can be configured not to expire.</span></span> <span data-ttu-id="00ab1-110">For more information about directory synchronization, see the list of topics in [Directory synchronization roadmap](https://msdn.microsoft.com/library/azure/hh967642.aspx).</span><span class="sxs-lookup"><span data-stu-id="00ab1-110">For more information about directory synchronization, see the list of topics in [Directory synchronization roadmap](https://msdn.microsoft.com/library/azure/hh967642.aspx).</span></span>
>
>

<span data-ttu-id="00ab1-111">To use Windows PowerShell cmdlets, you first must install them.</span><span class="sxs-lookup"><span data-stu-id="00ab1-111">To use Windows PowerShell cmdlets, you first must install them.</span></span>

## <a name="what-do-you-want-to-do"></a><span data-ttu-id="00ab1-112">What do you want to do?</span><span class="sxs-lookup"><span data-stu-id="00ab1-112">What do you want to do?</span></span>
* [<span data-ttu-id="00ab1-113">How to check expiration policy for a password</span><span class="sxs-lookup"><span data-stu-id="00ab1-113">How to check expiration policy for a password</span></span>](#how-to-check-expiration-policy-for-a-password)
* [<span data-ttu-id="00ab1-114">Set a password to expire</span><span class="sxs-lookup"><span data-stu-id="00ab1-114">Set a password to expire</span></span>](#set-a-password-to-expire)
* [<span data-ttu-id="00ab1-115">Set a password so that it will not expire</span><span class="sxs-lookup"><span data-stu-id="00ab1-115">Set a password so that it will not expire</span></span>](#set-a-password-to-never-expire)

## <a name="how-to-check-expiration-policy-for-a-password"></a><span data-ttu-id="00ab1-116">How to check expiration policy for a password</span><span class="sxs-lookup"><span data-stu-id="00ab1-116">How to check expiration policy for a password</span></span>
1. <span data-ttu-id="00ab1-117">Connect to Windows PowerShell using your company administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="00ab1-117">Connect to Windows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="00ab1-118">Do one of the following:</span><span class="sxs-lookup"><span data-stu-id="00ab1-118">Do one of the following:</span></span>

   * <span data-ttu-id="00ab1-119">To see whether a single user’s password is set to never expire, run the following cmdlet by using the user principal name (UPN) (for example, aprilr@contoso.onmicrosoft.com) or the user ID of the user you want to check: `Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`</span><span class="sxs-lookup"><span data-stu-id="00ab1-119">To see whether a single user’s password is set to never expire, run the following cmdlet by using the user principal name (UPN) (for example, aprilr@contoso.onmicrosoft.com) or the user ID of the user you want to check: `Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`</span></span>
   * <span data-ttu-id="00ab1-120">To see the "Password never expires" setting for all users, run the following cmdlet: `Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`</span><span class="sxs-lookup"><span data-stu-id="00ab1-120">To see the "Password never expires" setting for all users, run the following cmdlet: `Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`</span></span>

## <a name="set-a-password-to-expire"></a><span data-ttu-id="00ab1-121">Set a password to expire</span><span class="sxs-lookup"><span data-stu-id="00ab1-121">Set a password to expire</span></span>
1. <span data-ttu-id="00ab1-122">Connect to Windows PowerShell using your company administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="00ab1-122">Connect to Windows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="00ab1-123">Do one of the following:</span><span class="sxs-lookup"><span data-stu-id="00ab1-123">Do one of the following:</span></span>

   * <span data-ttu-id="00ab1-124">To set the password of one user so that the password will expire, run the following cmdlet by using the user principal name (UPN) or the user ID of the user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`</span><span class="sxs-lookup"><span data-stu-id="00ab1-124">To set the password of one user so that the password will expire, run the following cmdlet by using the user principal name (UPN) or the user ID of the user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`</span></span>
   * <span data-ttu-id="00ab1-125">To set the passwords of all users in the organization so that they will expire, use the following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`</span><span class="sxs-lookup"><span data-stu-id="00ab1-125">To set the passwords of all users in the organization so that they will expire, use the following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`</span></span>

## <a name="set-a-password-to-never-expire"></a><span data-ttu-id="00ab1-126">Set a password to never expire</span><span class="sxs-lookup"><span data-stu-id="00ab1-126">Set a password to never expire</span></span>
1. <span data-ttu-id="00ab1-127">Connect to Windows PowerShell using your company administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="00ab1-127">Connect to Windows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="00ab1-128">Do one of the following:</span><span class="sxs-lookup"><span data-stu-id="00ab1-128">Do one of the following:</span></span>

   * <span data-ttu-id="00ab1-129">To set the password of one user to never expire, run the following cmdlet by using the user principal name (UPN) or the user ID of the user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`</span><span class="sxs-lookup"><span data-stu-id="00ab1-129">To set the password of one user to never expire, run the following cmdlet by using the user principal name (UPN) or the user ID of the user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`</span></span>
   * <span data-ttu-id="00ab1-130">To set the passwords of all the users in an organization to never expire, run the following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`</span><span class="sxs-lookup"><span data-stu-id="00ab1-130">To set the passwords of all the users in an organization to never expire, run the following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`</span></span>

## <a name="next-steps"></a><span data-ttu-id="00ab1-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="00ab1-131">Next steps</span></span>
* <span data-ttu-id="00ab1-132">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="00ab1-132">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="00ab1-133">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="00ab1-133">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
