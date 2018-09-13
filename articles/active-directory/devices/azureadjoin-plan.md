---
title: Usage scenarios and deployment considerations for Azure AD Join| Microsoft Docs
description: Explains how administrators can set up Azure AD Join for their end users (employees, students, other users). It also discusses the different real-world scenarios for using Azure AD Join.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
tags: azure-classic-portal
ms.component: devices
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2018
ms.author: markvi
ms.openlocfilehash: a145b4184fbebd9c4f447face1c47bec20c0ec32
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864919"
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="acfa6-104">Usage scenarios and deployment considerations for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="acfa6-104">Usage scenarios and deployment considerations for Azure AD Join</span></span>
## <a name="usage-scenarios-for-azure-ad-join"></a><span data-ttu-id="acfa6-105">Usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="acfa6-105">Usage scenarios for Azure AD Join</span></span>
### <a name="scenario-1-businesses-largely-in-the-cloud"></a><span data-ttu-id="acfa6-106">Scenario 1: Businesses largely in the cloud</span><span class="sxs-lookup"><span data-stu-id="acfa6-106">Scenario 1: Businesses largely in the cloud</span></span>
<span data-ttu-id="acfa6-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span><span class="sxs-lookup"><span data-stu-id="acfa6-107">Azure Active Directory Join (Azure AD Join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon.</span></span> <span data-ttu-id="acfa6-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span><span class="sxs-lookup"><span data-stu-id="acfa6-108">You can use an account that you have created in Azure AD to sign in to Windows 10.</span></span> <span data-ttu-id="acfa6-109">Through [the first run experience (FRX) process](azuread-joined-devices-frx.md), or by joining Azure AD from [the settings menu](../user-help/device-management-azuread-joined-devices-setup.md), your users can join their machines to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acfa6-109">Through [the first run experience (FRX) process](azuread-joined-devices-frx.md), or by joining Azure AD from [the settings menu](../user-help/device-management-azuread-joined-devices-setup.md), your users can join their machines to Azure AD.</span></span>  <span data-ttu-id="acfa6-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span><span class="sxs-lookup"><span data-stu-id="acfa6-110">Your users can also enjoy single sign-on (SSO) access to  cloud resources like Office 365, either in their browsers or in Office applications.</span></span>

### <a name="scenario-2-educational-institutions"></a><span data-ttu-id="acfa6-111">Scenario 2: Educational institutions</span><span class="sxs-lookup"><span data-stu-id="acfa6-111">Scenario 2: Educational institutions</span></span>
<span data-ttu-id="acfa6-112">Educational institutions usually have two user types: faculty and students.</span><span class="sxs-lookup"><span data-stu-id="acfa6-112">Educational institutions usually have two user types: faculty and students.</span></span> <span data-ttu-id="acfa6-113">Faculty members are considered longer-term members of the organization.</span><span class="sxs-lookup"><span data-stu-id="acfa6-113">Faculty members are considered longer-term members of the organization.</span></span> <span data-ttu-id="acfa6-114">Creating on-premises accounts for them is desirable.</span><span class="sxs-lookup"><span data-stu-id="acfa6-114">Creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="acfa6-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acfa6-115">But students are shorter-term members of the organization and  their accounts can be managed in Azure AD.</span></span> <span data-ttu-id="acfa6-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span><span class="sxs-lookup"><span data-stu-id="acfa6-116">This means that directory scale can be pushed to the cloud instead of being stored on-premises.</span></span> <span data-ttu-id="acfa6-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span><span class="sxs-lookup"><span data-stu-id="acfa6-117">It also means that students  will be able to sign in to Windows with their Azure AD accounts and get access to Office 365 resources in Office applications.</span></span>

### <a name="scenario-3-retail-businesses"></a><span data-ttu-id="acfa6-118">Scenario 3: Retail businesses</span><span class="sxs-lookup"><span data-stu-id="acfa6-118">Scenario 3: Retail businesses</span></span>
<span data-ttu-id="acfa6-119">Retail businesses have seasonal workers and long-term employees.</span><span class="sxs-lookup"><span data-stu-id="acfa6-119">Retail businesses have seasonal workers and long-term employees.</span></span> <span data-ttu-id="acfa6-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span><span class="sxs-lookup"><span data-stu-id="acfa6-120">You typically create on-premises accounts and use domain-joined machines for longer-term full-time employees.</span></span> <span data-ttu-id="acfa6-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span><span class="sxs-lookup"><span data-stu-id="acfa6-121">But seasonal workers are shorter-term members of the organization, and it's desirable to manage their accounts where user licenses can be more easily moved around.</span></span> <span data-ttu-id="acfa6-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span><span class="sxs-lookup"><span data-stu-id="acfa6-122">When you create their user accounts in the cloud with Office 365 licenses, these users get the benefits of signing in to Windows and Office applications with an Azure AD account, while you maintain more flexibility with their licenses after they leave.</span></span>

### <a name="scenario-4-additional-scenarios"></a><span data-ttu-id="acfa6-123">Scenario 4: Additional scenarios</span><span class="sxs-lookup"><span data-stu-id="acfa6-123">Scenario 4: Additional scenarios</span></span>
<span data-ttu-id="acfa6-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="acfa6-124">Along with the benefits discussed earlier, you  benefit from having your users join their devices to Azure AD because of a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on to Azure AD and on-premises resources.</span></span>  

## <a name="deployment-considerations-for-azure-ad-join"></a><span data-ttu-id="acfa6-125">Deployment considerations for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="acfa6-125">Deployment considerations for Azure AD Join</span></span>
### <a name="enable-your-users-to-join-a-company-owned-device-directly-to-azure-ad"></a><span data-ttu-id="acfa6-126">Enable your users to join a company-owned device directly to Azure AD</span><span class="sxs-lookup"><span data-stu-id="acfa6-126">Enable your users to join a company-owned device directly to Azure AD</span></span>
<span data-ttu-id="acfa6-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span><span class="sxs-lookup"><span data-stu-id="acfa6-127">Enterprises can provide cloud-only accounts to partner companies and organizations.</span></span> <span data-ttu-id="acfa6-128">These partners can then easily access company apps and resources with single sign-on.</span><span class="sxs-lookup"><span data-stu-id="acfa6-128">These partners can then easily access company apps and resources with single sign-on.</span></span> <span data-ttu-id="acfa6-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span><span class="sxs-lookup"><span data-stu-id="acfa6-129">This scenario is applicable to users who access resources primarily in the cloud, such as Office 365 or SaaS apps that rely on Azure AD for authentication.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="acfa6-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="acfa6-130">Prerequisites</span></span>
<span data-ttu-id="acfa6-131">**At the enterprise level (administrator)**</span><span class="sxs-lookup"><span data-stu-id="acfa6-131">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="acfa6-132">Azure subscription with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acfa6-132">Azure subscription with Azure Active Directory</span></span>  

<span data-ttu-id="acfa6-133">**At the user level**</span><span class="sxs-lookup"><span data-stu-id="acfa6-133">**At the user level**</span></span>

* <span data-ttu-id="acfa6-134">Windows 10 (Professional and Enterprise editions)</span><span class="sxs-lookup"><span data-stu-id="acfa6-134">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="acfa6-135">Administrator tasks</span><span class="sxs-lookup"><span data-stu-id="acfa6-135">Administrator tasks</span></span>
* [<span data-ttu-id="acfa6-136">Set up device registration</span><span class="sxs-lookup"><span data-stu-id="acfa6-136">Set up device registration</span></span>](device-management-azure-portal.md)

### <a name="user-tasks"></a><span data-ttu-id="acfa6-137">User tasks</span><span class="sxs-lookup"><span data-stu-id="acfa6-137">User tasks</span></span>
* [<span data-ttu-id="acfa6-138">Set up a new Windows 10 device with Azure AD during setup</span><span class="sxs-lookup"><span data-stu-id="acfa6-138">Set up a new Windows 10 device with Azure AD during setup</span></span>](azuread-joined-devices-frx.md)
* [<span data-ttu-id="acfa6-139">Set up a Windows 10 device with Azure AD from the settings menu</span><span class="sxs-lookup"><span data-stu-id="acfa6-139">Set up a Windows 10 device with Azure AD from the settings menu</span></span>](../user-help/device-management-azuread-registered-devices-windows10-setup.md)
* [<span data-ttu-id="acfa6-140">Join a personal Windows 10 device to your organization</span><span class="sxs-lookup"><span data-stu-id="acfa6-140">Join a personal Windows 10 device to your organization</span></span>](../user-help/device-management-azuread-joined-devices-setup.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a><span data-ttu-id="acfa6-141">Enable BYOD in your organization for Windows 10</span><span class="sxs-lookup"><span data-stu-id="acfa6-141">Enable BYOD in your organization for Windows 10</span></span>
<span data-ttu-id="acfa6-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span><span class="sxs-lookup"><span data-stu-id="acfa6-142">You can set up your users and employees to use their personal Windows devices (BYOD) to access company apps and resources.</span></span> <span data-ttu-id="acfa6-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span><span class="sxs-lookup"><span data-stu-id="acfa6-143">Your users can add their Azure AD accounts (work or school accounts) to a personal Windows device to access resources in a secure and compliant fashion.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="acfa6-144">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="acfa6-144">Prerequisites</span></span>
<span data-ttu-id="acfa6-145">**At the enterprise level (administrator)**</span><span class="sxs-lookup"><span data-stu-id="acfa6-145">**At the enterprise level (administrator)**</span></span>

* <span data-ttu-id="acfa6-146">Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="acfa6-146">Azure AD subscription</span></span>

<span data-ttu-id="acfa6-147">**At the user level**</span><span class="sxs-lookup"><span data-stu-id="acfa6-147">**At the user level**</span></span>

* <span data-ttu-id="acfa6-148">Windows 10 (Professional and Enterprise editions)</span><span class="sxs-lookup"><span data-stu-id="acfa6-148">Windows 10 (Professional and Enterprise editions)</span></span>

### <a name="administrator-tasks"></a><span data-ttu-id="acfa6-149">Administrator tasks</span><span class="sxs-lookup"><span data-stu-id="acfa6-149">Administrator tasks</span></span>
* [<span data-ttu-id="acfa6-150">Set up device registration</span><span class="sxs-lookup"><span data-stu-id="acfa6-150">Set up device registration</span></span>](device-management-azure-portal.md)

### <a name="user-tasks"></a><span data-ttu-id="acfa6-151">User tasks</span><span class="sxs-lookup"><span data-stu-id="acfa6-151">User tasks</span></span>
* [<span data-ttu-id="acfa6-152">Join a personal Windows 10 device to your organization</span><span class="sxs-lookup"><span data-stu-id="acfa6-152">Join a personal Windows 10 device to your organization</span></span>](../user-help/device-management-azuread-joined-devices-setup.md)

## <a name="next-steps"></a><span data-ttu-id="acfa6-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="acfa6-153">Next steps</span></span>

- [<span data-ttu-id="acfa6-154">Device management</span><span class="sxs-lookup"><span data-stu-id="acfa6-154">Device management</span></span>](overview.md)

