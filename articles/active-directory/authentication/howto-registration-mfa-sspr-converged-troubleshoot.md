---
title: Disable converged registration for Azure AD SSPR and MFA (Public preview)
description: Disable Azure AD Multi-Factor Authentication and self-service password reset registration (Public preview)
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 08/02/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry, michmcla
ms.openlocfilehash: 3ce08f67f001a7c43602627b9eeda3ad60f867c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857012"
---
# <a name="disable-azure-ad-converged-registration-public-preview"></a><span data-ttu-id="5fe06-103">Disable Azure AD converged registration (Public preview)</span><span class="sxs-lookup"><span data-stu-id="5fe06-103">Disable Azure AD converged registration (Public preview)</span></span>

<span data-ttu-id="5fe06-104">When a user registers their phone number and/or mobile app in the new converged experience, our service stamps a set of flags (StrongAuthenticationMethods) for those methods on that user.</span><span class="sxs-lookup"><span data-stu-id="5fe06-104">When a user registers their phone number and/or mobile app in the new converged experience, our service stamps a set of flags (StrongAuthenticationMethods) for those methods on that user.</span></span> <span data-ttu-id="5fe06-105">This functionality allows the user to perform Azure Multi-Factor Authentication (MFA) with those methods whenever MFA is required.</span><span class="sxs-lookup"><span data-stu-id="5fe06-105">This functionality allows the user to perform Azure Multi-Factor Authentication (MFA) with those methods whenever MFA is required.</span></span>

<span data-ttu-id="5fe06-106">The methods that users register through the new experience have the StrongAuthenticationMethods property set.</span><span class="sxs-lookup"><span data-stu-id="5fe06-106">The methods that users register through the new experience have the StrongAuthenticationMethods property set.</span></span> <span data-ttu-id="5fe06-107">This behavior will also occur once public preview is available.</span><span class="sxs-lookup"><span data-stu-id="5fe06-107">This behavior will also occur once public preview is available.</span></span> <span data-ttu-id="5fe06-108">If an admin enables the preview, users register through the new experience, and then the admin disables the preview, users may unknowingly be registered for MFA also.</span><span class="sxs-lookup"><span data-stu-id="5fe06-108">If an admin enables the preview, users register through the new experience, and then the admin disables the preview, users may unknowingly be registered for MFA also.</span></span>

<span data-ttu-id="5fe06-109">If a user who has completed converged registration navigates to the current SSPR registration page, at [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup), they will be prompted to perform MFA before they can access that page.</span><span class="sxs-lookup"><span data-stu-id="5fe06-109">If a user who has completed converged registration navigates to the current SSPR registration page, at [https://aka.ms/ssprsetup](https://aka.ms/ssprsetup), they will be prompted to perform MFA before they can access that page.</span></span> <span data-ttu-id="5fe06-110">This step is an expected behavior from a technical standpoint, but for users who were previously registered for SSPR only, this step is a new behavior.</span><span class="sxs-lookup"><span data-stu-id="5fe06-110">This step is an expected behavior from a technical standpoint, but for users who were previously registered for SSPR only, this step is a new behavior.</span></span> <span data-ttu-id="5fe06-111">Although this extra step does improve the user’s security posture by providing an additional level of security, admins may want to roll back their users so that they are no longer capable of performing MFA.</span><span class="sxs-lookup"><span data-stu-id="5fe06-111">Although this extra step does improve the user’s security posture by providing an additional level of security, admins may want to roll back their users so that they are no longer capable of performing MFA.</span></span>  

## <a name="how-to-roll-back-users"></a><span data-ttu-id="5fe06-112">How to roll back users</span><span class="sxs-lookup"><span data-stu-id="5fe06-112">How to roll back users</span></span>

<span data-ttu-id="5fe06-113">If you as an administrator want to reset a user's MFA settings, we have created a PowerShell script that will clear the StrongAuthenticationMethods property for a user’s mobile app and/or phone number.</span><span class="sxs-lookup"><span data-stu-id="5fe06-113">If you as an administrator want to reset a user's MFA settings, we have created a PowerShell script that will clear the StrongAuthenticationMethods property for a user’s mobile app and/or phone number.</span></span> <span data-ttu-id="5fe06-114">Running this script for your users means that they will need to re-register for MFA if needed.</span><span class="sxs-lookup"><span data-stu-id="5fe06-114">Running this script for your users means that they will need to re-register for MFA if needed.</span></span> <span data-ttu-id="5fe06-115">We recommend testing rollback with one or two users before rolling back all the affected users.</span><span class="sxs-lookup"><span data-stu-id="5fe06-115">We recommend testing rollback with one or two users before rolling back all the affected users.</span></span>

<span data-ttu-id="5fe06-116">The steps that follow will help you roll back a user or group of users:</span><span class="sxs-lookup"><span data-stu-id="5fe06-116">The steps that follow will help you roll back a user or group of users:</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="5fe06-117">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="5fe06-117">Pre-requisites</span></span>

1. <span data-ttu-id="5fe06-118">You will need to install the appropriate Azure AD PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="5fe06-118">You will need to install the appropriate Azure AD PowerShell modules.</span></span> <span data-ttu-id="5fe06-119">In a PowerShell window, run these commands to install the modules:</span><span class="sxs-lookup"><span data-stu-id="5fe06-119">In a PowerShell window, run these commands to install the modules:</span></span>

   ```powershell
   Install-Module -Name MSOnline
   Import-Module MSOnline
   ```

1. <span data-ttu-id="5fe06-120">Save the list of affected user object ID/IDs to your machine as a text file with one ID per line.</span><span class="sxs-lookup"><span data-stu-id="5fe06-120">Save the list of affected user object ID/IDs to your machine as a text file with one ID per line.</span></span> <span data-ttu-id="5fe06-121">Make note of the location of the file.</span><span class="sxs-lookup"><span data-stu-id="5fe06-121">Make note of the location of the file.</span></span>
1. <span data-ttu-id="5fe06-122">Save the following script to your machine and make note of the location of the script:</span><span class="sxs-lookup"><span data-stu-id="5fe06-122">Save the following script to your machine and make note of the location of the script:</span></span>

```powershell
<# 
//********************************************************
//*                                                      *
//*   Copyright (C) Microsoft. All rights reserved.      *
//*                                                      *
//********************************************************
#>

param($path)

# Define Remediation Fn
function RemediateUser {

    param  
    (
        $ObjectId
    )

    $user = Get-MsolUser -ObjectId $ObjectId

    Write-Host "Checking if user is eligible for rollback: UPN: "  $user.UserPrincipalName  " ObjectId: "  $user.ObjectId -ForegroundColor Yellow

    $hasMfaRelyingParty = $false
    foreach($p in $user.StrongAuthenticationRequirements)
    {
        if ($p.RelyingParty -eq "*")
        {
            $hasMfaRelyingParty = $true
            Write-Host "User was enabled for per-user MFA." -ForegroundColor Yellow
        }
    }

    if ($user.StrongAuthenticationMethods.Count -gt 0 -and -not $hasMfaRelyingParty)
    {
        Write-Host $user.UserPrincipalName " is eligible for rollback" -ForegroundColor Yellow
        Write-Host "Rolling back user ..." -ForegroundColor Yellow
        Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName $user.UserPrincipalName
        Write-Host "Successfully rolled back user " $user.UserPrincipalName -ForegroundColor Green
    }
    else
    {
        Write-Host $user.UserPrincipalName " is not eligible for rollback. No action required."
    }

    Write-Host ""
    Start-Sleep -Milliseconds 750
}

# Connect
Import-Module MSOnline
Connect-MsolService

foreach($line in Get-Content $path)
{
    RemediateUser -ObjectId $line
}
```

### <a name="rollback"></a><span data-ttu-id="5fe06-123">Rollback</span><span class="sxs-lookup"><span data-stu-id="5fe06-123">Rollback</span></span>

<span data-ttu-id="5fe06-124">In a PowerShell window, run the following command after updating the highlighted locations.</span><span class="sxs-lookup"><span data-stu-id="5fe06-124">In a PowerShell window, run the following command after updating the highlighted locations.</span></span> <span data-ttu-id="5fe06-125">Enter global administrator credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="5fe06-125">Enter global administrator credentials when prompted.</span></span> <span data-ttu-id="5fe06-126">The script will output the outcome of each user update operation.</span><span class="sxs-lookup"><span data-stu-id="5fe06-126">The script will output the outcome of each user update operation.</span></span>

`<script location> -path <user file location>`

## <a name="disable-preview-experience"></a><span data-ttu-id="5fe06-127">Disable preview experience</span><span class="sxs-lookup"><span data-stu-id="5fe06-127">Disable preview experience</span></span>

<span data-ttu-id="5fe06-128">To disable the preview experience for your users, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="5fe06-128">To disable the preview experience for your users, complete the following steps:</span></span>

1. <span data-ttu-id="5fe06-129">Sign in to the Azure portal as a global administrator or user administrator.</span><span class="sxs-lookup"><span data-stu-id="5fe06-129">Sign in to the Azure portal as a global administrator or user administrator.</span></span>
2. <span data-ttu-id="5fe06-130">Browse to **Azure Active Directory**, **User settings**, **Manage settings for access panel preview features**.</span><span class="sxs-lookup"><span data-stu-id="5fe06-130">Browse to **Azure Active Directory**, **User settings**, **Manage settings for access panel preview features**.</span></span>
3. <span data-ttu-id="5fe06-131">Under **Users can use preview features for registering and managing security info**, set the selector to **None** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5fe06-131">Under **Users can use preview features for registering and managing security info**, set the selector to **None** and click **Save**.</span></span>

<span data-ttu-id="5fe06-132">Users will no longer be prompted to register using the preview experience.</span><span class="sxs-lookup"><span data-stu-id="5fe06-132">Users will no longer be prompted to register using the preview experience.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fe06-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="5fe06-133">Next steps</span></span>

[<span data-ttu-id="5fe06-134">Learn more about the public preview of converged registration for self-service password reset and Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="5fe06-134">Learn more about the public preview of converged registration for self-service password reset and Azure Multi-Factor Authentication</span></span>](concept-registration-mfa-sspr-converged.md)