---
title: Usage scenarios and deployment considerations for Azure AD Join| Microsoft Docs
description: Explains how administrators can set up Azure AD Join for their end users (employees, students, other users). It also discusses the different real-world scenarios for using Azure AD Join.
services: active-directory
documentationcenter: ''
author: femila
manager: femila
editor: ''
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: markvi
ms.openlocfilehash: 4333db6fb459b34829cb7bbe160f54109bb4b26d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550636"
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="2edb9-104">Usage scenarios and deployment considerations for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2edb9-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="2edb9-105">Usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2edb9-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-the-cloud"></a><span data-ttu-id="2edb9-106">Scenario 1: Businesses largely in the cloud</span><span class="sxs-lookup"><span data-stu-id="2edb9-106">Scenario 1: Businesses largely in the cloud</span></span>
<span data-ttu-id="2edb9-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span><span class="sxs-lookup"><span data-stu-id="2edb9-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span></span> <span data-ttu-id="2edb9-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2edb9-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span></span> <span data-ttu-id="2edb9-109">Through [the first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [the settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2edb9-109">Through [the first run experience (FRX) process](active-directory-azureadjoin-user-frx.md), or by joining Azure AD from [the settings menu](active-directory-azureadjoin-user-upgrade.md), your users can join their machines to Azure AD.</span></span>  <span data-ttu-id="2edb9-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span><span class="sxs-lookup"><span data-stu-id="2edb9-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="2edb9-111">Scenario 2: Educational institutions</span><span class="sxs-lookup"><span data-stu-id="2edb9-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="2edb9-112">Educational institutions usually have two user types: faculty and students.</span><span class="sxs-lookup"><span data-stu-id="2edb9-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="2edb9-113">Faculty members are considered longer-term members of the organization.</span><span class="sxs-lookup"><span data-stu-id="2edb9-113">Faculty members are considered longer-term members of the organization.</span></span> <span data-ttu-id="2edb9-114">Creating on-premises accounts for them is desirable.</span><span class="sxs-lookup"><span data-stu-id="2edb9-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="2edb9-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2edb9-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="2edb9-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span><span class="sxs-lookup"><span data-stu-id="2edb9-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span></span> <span data-ttu-id="2edb9-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span><span class="sxs-lookup"><span data-stu-id="2edb9-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="2edb9-118">Scenario 3: Retail businesses</span><span class="sxs-lookup"><span data-stu-id="2edb9-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="2edb9-119">Retail businesses have seasonal workers and long-term employees.</span><span class="sxs-lookup"><span data-stu-id="2edb9-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="2edb9-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span><span class="sxs-lookup"><span data-stu-id="2edb9-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="2edb9-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span><span class="sxs-lookup"><span data-stu-id="2edb9-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="2edb9-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span><span class="sxs-lookup"><span data-stu-id="2edb9-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="2edb9-123">Scenario 4: Additional scenarios</span><span class="sxs-lookup"><span data-stu-id="2edb9-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="2edb9-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="2edb9-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="2edb9-125">Deployment considerations for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2edb9-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-to-join-a-company-owned-device-directly-to-azure-ad"></a><span data-ttu-id="2edb9-126">Enable your users to join a company-owned device directly to Azure AD</span><span class="sxs-lookup"><span data-stu-id="2edb9-126">Enable your users to join a company-owned device directly to Azure AD</span></span>
<span data-ttu-id="2edb9-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span><span class="sxs-lookup"><span data-stu-id="2edb9-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span></span> <span data-ttu-id="2edb9-128">These partners can then easily access company apps and resources with single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2edb9-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="2edb9-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span><span class="sxs-lookup"><span data-stu-id="2edb9-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2edb9-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2edb9-130">Prerequisites</span></span>
<span data-ttu-id="2edb9-131">**At the enterprise level (administrator)**</span><span class="sxs-lookup"><span data-stu-id="2edb9-131">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="2edb9-132">Azure subscription with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2edb9-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="2edb9-133">**At the user level**</span><span class="sxs-lookup"><span data-stu-id="2edb9-133">**At the user level**</span></span>

* <span data-ttu-id="2edb9-134">Windows 10 (Professional and Enterprise editions)</span><span class="sxs-lookup"><span data-stu-id="2edb9-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="2edb9-135">Administrator tasks</span><span class="sxs-lookup"><span data-stu-id="2edb9-135">Administrator tasks</span></span>
* [<span data-ttu-id="2edb9-136">Set up device registration</span><span class="sxs-lookup"><span data-stu-id="2edb9-136">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="2edb9-137">User tasks</span><span class="sxs-lookup"><span data-stu-id="2edb9-137">User tasks</span></span>
* [<span data-ttu-id="2edb9-138">Set up a new Windows 10 device with Azure AD during setup</span><span class="sxs-lookup"><span data-stu-id="2edb9-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md)
* [<span data-ttu-id="2edb9-139">Set up a Windows 10 device with Azure AD from the settings menu</span><span class="sxs-lookup"><span data-stu-id="2edb9-139">Set up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2edb9-140">Join a personal Windows 10 device to your organization</span><span class="sxs-lookup"><span data-stu-id="2edb9-140">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="2edb9-141">Enable BYOD in your organization for Windows 10</span><span class="sxs-lookup"><span data-stu-id="2edb9-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="2edb9-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span><span class="sxs-lookup"><span data-stu-id="2edb9-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span></span> <span data-ttu-id="2edb9-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span><span class="sxs-lookup"><span data-stu-id="2edb9-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2edb9-144">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2edb9-144">Prerequisites</span></span>
<span data-ttu-id="2edb9-145">**At the enterprise level (administrator)**</span><span class="sxs-lookup"><span data-stu-id="2edb9-145">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="2edb9-146">Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2edb9-146">Azure AD subscription</span></span>

<span data-ttu-id="2edb9-147">**At the user level**</span><span class="sxs-lookup"><span data-stu-id="2edb9-147">**At the user level**</span></span>

* <span data-ttu-id="2edb9-148">Windows 10 (Professional and Enterprise editions)</span><span class="sxs-lookup"><span data-stu-id="2edb9-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="2edb9-149">Administrator tasks</span><span class="sxs-lookup"><span data-stu-id="2edb9-149">Administrator tasks</span></span>
* [<span data-ttu-id="2edb9-150">Set up device registration</span><span class="sxs-lookup"><span data-stu-id="2edb9-150">Set up device registration</span></span>](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a><span data-ttu-id="2edb9-151">User tasks</span><span class="sxs-lookup"><span data-stu-id="2edb9-151">User tasks</span></span>
* [<span data-ttu-id="2edb9-152">Join a personal Windows 10 device to your organization</span><span class="sxs-lookup"><span data-stu-id="2edb9-152">Join a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a><span data-ttu-id="2edb9-153">Additional information</span><span class="sxs-lookup"><span data-stu-id="2edb9-153">Additional information</span></span>
* [<span data-ttu-id="2edb9-154">Windows 10 for the enterprise: Ways to use devices for work</span><span class="sxs-lookup"><span data-stu-id="2edb9-154">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="2edb9-155">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="2edb9-155">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="2edb9-156">Authenticating identities without passwords through Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="2edb9-156">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="2edb9-157">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2edb9-157">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="2edb9-158">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="2edb9-158">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="2edb9-159">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="2edb9-159">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

