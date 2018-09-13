---
title: Get started Azure MFA in the cloud | Microsoft Docs
description: This is the Microsoft Azure Multi-Factor authentication page that describes how to get started with Azure MFA in the cloud.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: kgremban
ms.openlocfilehash: f9ebf2ed1e9b822695d62b4d47cfeeb70d3c2677
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552746"
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a><span data-ttu-id="c2eec-103">Getting started with Azure Multi-Factor Authentication in the cloud</span><span class="sxs-lookup"><span data-stu-id="c2eec-103">Getting started with Azure Multi-Factor Authentication in the cloud</span></span>
<span data-ttu-id="c2eec-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c2eec-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="c2eec-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span><span class="sxs-lookup"><span data-stu-id="c2eec-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span></span> <span data-ttu-id="c2eec-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="c2eec-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA in the Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="c2eec-108">Prerequisite</span><span class="sxs-lookup"><span data-stu-id="c2eec-108">Prerequisite</span></span>
<span data-ttu-id="c2eec-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span><span class="sxs-lookup"><span data-stu-id="c2eec-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span></span> <span data-ttu-id="c2eec-110">If you are just starting out and using Azure MFA you can use a trial subscription</span><span class="sxs-lookup"><span data-stu-id="c2eec-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="c2eec-111">Enable Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c2eec-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="c2eec-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="c2eec-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="c2eec-113">You can start requiring two-step verification on an individual user basis.</span><span class="sxs-lookup"><span data-stu-id="c2eec-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="c2eec-114">The licenses that enable Azure MFA are:</span><span class="sxs-lookup"><span data-stu-id="c2eec-114">The licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="c2eec-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="c2eec-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="c2eec-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="c2eec-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="c2eec-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="c2eec-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="c2eec-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span><span class="sxs-lookup"><span data-stu-id="c2eec-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span></span> <span data-ttu-id="c2eec-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span><span class="sxs-lookup"><span data-stu-id="c2eec-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="c2eec-120">Turn on two-step verification for users</span><span class="sxs-lookup"><span data-stu-id="c2eec-120">Turn on two-step verification for users</span></span>
<span data-ttu-id="c2eec-121">To start requiring two-start verification on for a user, change the user's state from disabled to enabled.</span><span class="sxs-lookup"><span data-stu-id="c2eec-121">To start requiring two-start verification on for a user, change the user's state from disabled to enabled.</span></span>  <span data-ttu-id="c2eec-122">For more information on user states, see [User States in Azure Multi-Factor Authentication](multi-factor-authentication-get-started-user-states.md)</span><span class="sxs-lookup"><span data-stu-id="c2eec-122">For more information on user states, see [User States in Azure Multi-Factor Authentication](multi-factor-authentication-get-started-user-states.md)</span></span>

<span data-ttu-id="c2eec-123">Use the following procedure to enable MFA for your users.</span><span class="sxs-lookup"><span data-stu-id="c2eec-123">Use the following procedure to enable MFA for your users.</span></span>

### <a name="to-turn-on-multi-factor-authentication"></a><span data-ttu-id="c2eec-124">To turn on multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="c2eec-124">To turn on multi-factor authentication</span></span>
1. <span data-ttu-id="c2eec-125">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c2eec-125">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="c2eec-126">On the left, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2eec-126">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="c2eec-127">Under Directory, select the directory for the user you wish to enable.</span><span class="sxs-lookup"><span data-stu-id="c2eec-127">Under Directory, select the directory for the user you wish to enable.</span></span>
   <span data-ttu-id="c2eec-128">![Click Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/directory1.png)</span><span class="sxs-lookup"><span data-stu-id="c2eec-128">![Click Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/directory1.png)</span></span>
4. <span data-ttu-id="c2eec-129">At the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c2eec-129">At the top, click **Users**.</span></span>
5. <span data-ttu-id="c2eec-130">At the bottom of the page, click **Manage Multi-Factor Auth**. A new browser tab opens.</span><span class="sxs-lookup"><span data-stu-id="c2eec-130">At the bottom of the page, click **Manage Multi-Factor Auth**. A new browser tab opens.</span></span>
   <span data-ttu-id="c2eec-131">![Click Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/manage1.png)</span><span class="sxs-lookup"><span data-stu-id="c2eec-131">![Click Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/manage1.png)</span></span>
6. <span data-ttu-id="c2eec-132">Find the user that you wish to enable for two-step verification.</span><span class="sxs-lookup"><span data-stu-id="c2eec-132">Find the user that you wish to enable for two-step verification.</span></span> <span data-ttu-id="c2eec-133">You may need to change the view at the top.</span><span class="sxs-lookup"><span data-stu-id="c2eec-133">You may need to change the view at the top.</span></span> <span data-ttu-id="c2eec-134">Ensure that the status is **disabled.**
   ![Enable user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable1.png)</span><span class="sxs-lookup"><span data-stu-id="c2eec-134">Ensure that the status is **disabled.**
![Enable user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable1.png)</span></span>
7. <span data-ttu-id="c2eec-135">Place a **check** in the box next to their name.</span><span class="sxs-lookup"><span data-stu-id="c2eec-135">Place a **check** in the box next to their name.</span></span>
8. <span data-ttu-id="c2eec-136">On the right, click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="c2eec-136">On the right, click **Enable**.</span></span>
   <span data-ttu-id="c2eec-137">![Enable user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user1.png)</span><span class="sxs-lookup"><span data-stu-id="c2eec-137">![Enable user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user1.png)</span></span>
9. <span data-ttu-id="c2eec-138">Click **enable multi-factor auth**. ![Enable user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable2.png)</span><span class="sxs-lookup"><span data-stu-id="c2eec-138">Click **enable multi-factor auth**. ![Enable user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/enable2.png)</span></span>
10. <span data-ttu-id="c2eec-139">Notice that the user's state has changed from **disabled** to **enabled**.</span><span class="sxs-lookup"><span data-stu-id="c2eec-139">Notice that the user's state has changed from **disabled** to **enabled**.</span></span>
    <span data-ttu-id="c2eec-140">![Enable Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user.png)</span><span class="sxs-lookup"><span data-stu-id="c2eec-140">![Enable Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-cloud/user.png)</span></span>

<span data-ttu-id="c2eec-141">After you have enabled your users, you should notify them via email.</span><span class="sxs-lookup"><span data-stu-id="c2eec-141">After you have enabled your users, you should notify them via email.</span></span> <span data-ttu-id="c2eec-142">The next time they try to sign in, they'll be asked to enroll their account for two-step verification.</span><span class="sxs-lookup"><span data-stu-id="c2eec-142">The next time they try to sign in, they'll be asked to enroll their account for two-step verification.</span></span> <span data-ttu-id="c2eec-143">Once they start using two-step verification, they'll also need to set up app passwords to avoid being locked out of non-browser apps.</span><span class="sxs-lookup"><span data-stu-id="c2eec-143">Once they start using two-step verification, they'll also need to set up app passwords to avoid being locked out of non-browser apps.</span></span>

## <a name="use-powershell-to-automate-turning-on-two-step-verification"></a><span data-ttu-id="c2eec-144">Use PowerShell to automate turning on two-step verification</span><span class="sxs-lookup"><span data-stu-id="c2eec-144">Use PowerShell to automate turning on two-step verification</span></span>
<span data-ttu-id="c2eec-145">To change the [state](multi-factor-authentication-whats-next.md) using [Azure AD PowerShell](/powershell/azureps-cmdlets-docs), you can use the following.</span><span class="sxs-lookup"><span data-stu-id="c2eec-145">To change the [state](multi-factor-authentication-whats-next.md) using [Azure AD PowerShell](/powershell/azureps-cmdlets-docs), you can use the following.</span></span>  <span data-ttu-id="c2eec-146">You can change `$st.State` to equal one of the following states:</span><span class="sxs-lookup"><span data-stu-id="c2eec-146">You can change `$st.State` to equal one of the following states:</span></span>

* <span data-ttu-id="c2eec-147">Enabled</span><span class="sxs-lookup"><span data-stu-id="c2eec-147">Enabled</span></span>
* <span data-ttu-id="c2eec-148">Enforced</span><span class="sxs-lookup"><span data-stu-id="c2eec-148">Enforced</span></span>
* <span data-ttu-id="c2eec-149">Disabled</span><span class="sxs-lookup"><span data-stu-id="c2eec-149">Disabled</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c2eec-150">We discourage against moving users directly from the Disable state to the Enforced state.</span><span class="sxs-lookup"><span data-stu-id="c2eec-150">We discourage against moving users directly from the Disable state to the Enforced state.</span></span> <span data-ttu-id="c2eec-151">Non-browser-based apps will stop working because the user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span><span class="sxs-lookup"><span data-stu-id="c2eec-151">Non-browser-based apps will stop working because the user has not gone through MFA registration and obtained an [app password](multi-factor-authentication-whats-next.md#app-passwords).</span></span> <span data-ttu-id="c2eec-152">If you have non-browser-based apps and require app passwords, we recommend that you go from a Disabled state to Enabled.</span><span class="sxs-lookup"><span data-stu-id="c2eec-152">If you have non-browser-based apps and require app passwords, we recommend that you go from a Disabled state to Enabled.</span></span> <span data-ttu-id="c2eec-153">This allows users to register and obtain their app passwords.</span><span class="sxs-lookup"><span data-stu-id="c2eec-153">This allows users to register and obtain their app passwords.</span></span> <span data-ttu-id="c2eec-154">After that, you can move them to Enforced.</span><span class="sxs-lookup"><span data-stu-id="c2eec-154">After that, you can move them to Enforced.</span></span>

<span data-ttu-id="c2eec-155">Using PowerShell would be an option for bulk enabling users.</span><span class="sxs-lookup"><span data-stu-id="c2eec-155">Using PowerShell would be an option for bulk enabling users.</span></span> <span data-ttu-id="c2eec-156">Currently there is no bulk enable feature in the Azure portal and you need to select each user individually.</span><span class="sxs-lookup"><span data-stu-id="c2eec-156">Currently there is no bulk enable feature in the Azure portal and you need to select each user individually.</span></span> <span data-ttu-id="c2eec-157">This can be quite a task if you have many users.</span><span class="sxs-lookup"><span data-stu-id="c2eec-157">This can be quite a task if you have many users.</span></span> <span data-ttu-id="c2eec-158">By creating a PowerShell script using the following, you can loop through a list of users and enable them.</span><span class="sxs-lookup"><span data-stu-id="c2eec-158">By creating a PowerShell script using the following, you can loop through a list of users and enable them.</span></span>

        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

<span data-ttu-id="c2eec-159">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="c2eec-159">Here is an example:</span></span>

    $users = "bsimon@contoso.com","jsmith@contoso.com","ljacobson@contoso.com"
    foreach ($user in $users)
    {
        $st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
        $st.RelyingParty = "*"
        $st.State = “Enabled”
        $sta = @($st)
        Set-MsolUser -UserPrincipalName $user -StrongAuthenticationRequirements $sta
    }


<span data-ttu-id="c2eec-160">For more information, see [User states in Azure Multi-Factor Authentication](multi-factor-authentication-get-started-user-states.md)</span><span class="sxs-lookup"><span data-stu-id="c2eec-160">For more information, see [User states in Azure Multi-Factor Authentication](multi-factor-authentication-get-started-user-states.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2eec-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c2eec-161">Next Steps</span></span>
<span data-ttu-id="c2eec-162">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span><span class="sxs-lookup"><span data-stu-id="c2eec-162">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="c2eec-163">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="c2eec-163">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>








