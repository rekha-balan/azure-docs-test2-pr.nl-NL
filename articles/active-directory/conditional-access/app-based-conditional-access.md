---
title: Azure Active Directory app-based conditional access | Microsoft Docs
description: Learn how Azure Active Directory app-based conditional access works.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/13/2018
ms.author: markvi
ms.reviewer: spunukol
ms.openlocfilehash: f34fc4c41094292db9bed1294ee7b26ec04c96c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867067"
---
# <a name="azure-active-directory-app-based-conditional-access"></a><span data-ttu-id="6b50b-104">Azure Active Directory app-based conditional access</span><span class="sxs-lookup"><span data-stu-id="6b50b-104">Azure Active Directory app-based conditional access</span></span>  

<span data-ttu-id="6b50b-105">Your employees use mobile devices for both personal and work tasks.</span><span class="sxs-lookup"><span data-stu-id="6b50b-105">Your employees use mobile devices for both personal and work tasks.</span></span> <span data-ttu-id="6b50b-106">While making sure your employees can be productive, you also want to prevent data loss.</span><span class="sxs-lookup"><span data-stu-id="6b50b-106">While making sure your employees can be productive, you also want to prevent data loss.</span></span> <span data-ttu-id="6b50b-107">With Azure Active Directory (Azure AD) app-based conditional access, you can restrict access to your cloud apps to client apps that can protect your corporate data.</span><span class="sxs-lookup"><span data-stu-id="6b50b-107">With Azure Active Directory (Azure AD) app-based conditional access, you can restrict access to your cloud apps to client apps that can protect your corporate data.</span></span>  

<span data-ttu-id="6b50b-108">This topic explains how to configure Azure AD app-based conditional access.</span><span class="sxs-lookup"><span data-stu-id="6b50b-108">This topic explains how to configure Azure AD app-based conditional access.</span></span>

## <a name="overview"></a><span data-ttu-id="6b50b-109">Overview</span><span class="sxs-lookup"><span data-stu-id="6b50b-109">Overview</span></span>

<span data-ttu-id="6b50b-110">With [Azure AD conditional access](overview.md), you can fine-tune how authorized users can access your resources.</span><span class="sxs-lookup"><span data-stu-id="6b50b-110">With [Azure AD conditional access](overview.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="6b50b-111">For example, you can limit the access to your cloud apps to trusted devices.</span><span class="sxs-lookup"><span data-stu-id="6b50b-111">For example, you can limit the access to your cloud apps to trusted devices.</span></span>

<span data-ttu-id="6b50b-112">You can use [Intune app protection policies](https://docs.microsoft.com/intune/app-protection-policy) to help protect your company’s data.</span><span class="sxs-lookup"><span data-stu-id="6b50b-112">You can use [Intune app protection policies](https://docs.microsoft.com/intune/app-protection-policy) to help protect your company’s data.</span></span> <span data-ttu-id="6b50b-113">Intune app protection policies don't require mobile-device management (MDM) solution, which enables you to protect your company’s data with or without enrolling devices in a device management solution.</span><span class="sxs-lookup"><span data-stu-id="6b50b-113">Intune app protection policies don't require mobile-device management (MDM) solution, which enables you to protect your company’s data with or without enrolling devices in a device management solution.</span></span>

<span data-ttu-id="6b50b-114">Azure Active Directory app-based conditional access enables you limit access to your cloud apps to client apps that support Intune app protection policies.</span><span class="sxs-lookup"><span data-stu-id="6b50b-114">Azure Active Directory app-based conditional access enables you limit access to your cloud apps to client apps that support Intune app protection policies.</span></span> <span data-ttu-id="6b50b-115">For example, you can restrict access to Exchange Online to the Outlook app.</span><span class="sxs-lookup"><span data-stu-id="6b50b-115">For example, you can restrict access to Exchange Online to the Outlook app.</span></span>

<span data-ttu-id="6b50b-116">In the conditional access terminology, these client apps are known as **approved client apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-116">In the conditional access terminology, these client apps are known as **approved client apps**.</span></span>  


![Conditional access](./media/app-based-conditional-access/05.png)


<span data-ttu-id="6b50b-118">For a list of approved client apps, see [approved client app requirement](technical-reference.md#approved-client-app-requirement).</span><span class="sxs-lookup"><span data-stu-id="6b50b-118">For a list of approved client apps, see [approved client app requirement](technical-reference.md#approved-client-app-requirement).</span></span>


<span data-ttu-id="6b50b-119">You can combine app-based conditional access policies with other policies such as [device-based conditional access policies](require-managed-devices.md) to provide flexibility in how to protect data for both personal and corporate devices.</span><span class="sxs-lookup"><span data-stu-id="6b50b-119">You can combine app-based conditional access policies with other policies such as [device-based conditional access policies](require-managed-devices.md) to provide flexibility in how to protect data for both personal and corporate devices.</span></span>

 


## <a name="before-you-begin"></a><span data-ttu-id="6b50b-120">Before you begin</span><span class="sxs-lookup"><span data-stu-id="6b50b-120">Before you begin</span></span>

<span data-ttu-id="6b50b-121">This topic assumes that you are familiar with:</span><span class="sxs-lookup"><span data-stu-id="6b50b-121">This topic assumes that you are familiar with:</span></span>

- <span data-ttu-id="6b50b-122">The [approved client app requirement](technical-reference.md#approved-client-app-requirement) technical reference.</span><span class="sxs-lookup"><span data-stu-id="6b50b-122">The [approved client app requirement](technical-reference.md#approved-client-app-requirement) technical reference.</span></span>


- <span data-ttu-id="6b50b-123">The basic concepts of [conditional access in Azure Active Directory](overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b50b-123">The basic concepts of [conditional access in Azure Active Directory](overview.md).</span></span>

- <span data-ttu-id="6b50b-124">How to [configure a conditional access policy](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="6b50b-124">How to [configure a conditional access policy](app-based-mfa.md).</span></span>

- <span data-ttu-id="6b50b-125">The [migration of conditional access policies](best-practices.md#policy-migration).</span><span class="sxs-lookup"><span data-stu-id="6b50b-125">The [migration of conditional access policies](best-practices.md#policy-migration).</span></span>
 

## <a name="prerequisites"></a><span data-ttu-id="6b50b-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6b50b-126">Prerequisites</span></span>

<span data-ttu-id="6b50b-127">To create an app-based conditional access policy, you must have an Enterprise Mobility + Security or an Azure Active Directory premium subscription, and the users must be licensed for EMS or Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b50b-127">To create an app-based conditional access policy, you must have an Enterprise Mobility + Security or an Azure Active Directory premium subscription, and the users must be licensed for EMS or Azure AD.</span></span> 


## <a name="exchange-online-policy"></a><span data-ttu-id="6b50b-128">Exchange Online policy</span><span class="sxs-lookup"><span data-stu-id="6b50b-128">Exchange Online policy</span></span> 

<span data-ttu-id="6b50b-129">This scenario consists of an app-based conditional access policy for access to Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="6b50b-129">This scenario consists of an app-based conditional access policy for access to Exchange Online.</span></span>


### <a name="scenario-playbook"></a><span data-ttu-id="6b50b-130">Scenario playbook</span><span class="sxs-lookup"><span data-stu-id="6b50b-130">Scenario playbook</span></span>

<span data-ttu-id="6b50b-131">This scenario assumes that a user:</span><span class="sxs-lookup"><span data-stu-id="6b50b-131">This scenario assumes that a user:</span></span>

- <span data-ttu-id="6b50b-132">Configures email using a native mail application on iOS or Android to connect to Exchange</span><span class="sxs-lookup"><span data-stu-id="6b50b-132">Configures email using a native mail application on iOS or Android to connect to Exchange</span></span>

- <span data-ttu-id="6b50b-133">Receives an email that indicates that access is only available using Outlook app</span><span class="sxs-lookup"><span data-stu-id="6b50b-133">Receives an email that indicates that access is only available using Outlook app</span></span>

- <span data-ttu-id="6b50b-134">Downloads the application with the link</span><span class="sxs-lookup"><span data-stu-id="6b50b-134">Downloads the application with the link</span></span>

- <span data-ttu-id="6b50b-135">Opens the Outlook application and signs in with the Azure AD credentials</span><span class="sxs-lookup"><span data-stu-id="6b50b-135">Opens the Outlook application and signs in with the Azure AD credentials</span></span>

- <span data-ttu-id="6b50b-136">Is prompted to install either Authenticator (iOS) or Company Portal (Android) to continue</span><span class="sxs-lookup"><span data-stu-id="6b50b-136">Is prompted to install either Authenticator (iOS) or Company Portal (Android) to continue</span></span>

- <span data-ttu-id="6b50b-137">Installs the application and can return to the Outlook app to continue</span><span class="sxs-lookup"><span data-stu-id="6b50b-137">Installs the application and can return to the Outlook app to continue</span></span>

- <span data-ttu-id="6b50b-138">Is prompted to register a device</span><span class="sxs-lookup"><span data-stu-id="6b50b-138">Is prompted to register a device</span></span>

- <span data-ttu-id="6b50b-139">Is able to access email</span><span class="sxs-lookup"><span data-stu-id="6b50b-139">Is able to access email</span></span>

<span data-ttu-id="6b50b-140">Any Intune app protection policies are activated at the time the access corporate data and may prompt the user to restart the application, use an additional PIN etc (if configured for the application and platform).</span><span class="sxs-lookup"><span data-stu-id="6b50b-140">Any Intune app protection policies are activated at the time the access corporate data and may prompt the user to restart the application, use an additional PIN etc (if configured for the application and platform).</span></span>

### <a name="configuration"></a><span data-ttu-id="6b50b-141">Configuration</span><span class="sxs-lookup"><span data-stu-id="6b50b-141">Configuration</span></span> 

<span data-ttu-id="6b50b-142">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online**</span><span class="sxs-lookup"><span data-stu-id="6b50b-142">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online**</span></span>

<span data-ttu-id="6b50b-143">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-143">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/01.png)

1. <span data-ttu-id="6b50b-145">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-145">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-146">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-146">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>

3. <span data-ttu-id="6b50b-147">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-147">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/07.png)

4. <span data-ttu-id="6b50b-149">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**:</span><span class="sxs-lookup"><span data-stu-id="6b50b-149">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**:</span></span>

    <span data-ttu-id="6b50b-150">a.</span><span class="sxs-lookup"><span data-stu-id="6b50b-150">a.</span></span> <span data-ttu-id="6b50b-151">As **Device platforms**, select **Android** and **iOS**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-151">As **Device platforms**, select **Android** and **iOS**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/03.png)

    <span data-ttu-id="6b50b-153">b.</span><span class="sxs-lookup"><span data-stu-id="6b50b-153">b.</span></span> <span data-ttu-id="6b50b-154">As **Client apps**, select **Mobile apps and desktop apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-154">As **Client apps**, select **Mobile apps and desktop apps**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/04.png)

5. <span data-ttu-id="6b50b-156">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-156">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span></span>

    ![Conditional access](./media/app-based-conditional-access/05.png)
 

<span data-ttu-id="6b50b-158">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-158">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span></span>

<span data-ttu-id="6b50b-159">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-159">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/06.png)

1. <span data-ttu-id="6b50b-161">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-161">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-162">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-162">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>


3. <span data-ttu-id="6b50b-163">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-163">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/07.png)

4. <span data-ttu-id="6b50b-165">**Conditions:** As **Conditions**, you need to configure **Client apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-165">**Conditions:** As **Conditions**, you need to configure **Client apps**.</span></span> 

    <span data-ttu-id="6b50b-166">a.</span><span class="sxs-lookup"><span data-stu-id="6b50b-166">a.</span></span> <span data-ttu-id="6b50b-167">As **Client apps**, select **Exchange Active Sync**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-167">As **Client apps**, select **Exchange Active Sync**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/08.png)

    <span data-ttu-id="6b50b-169">b.</span><span class="sxs-lookup"><span data-stu-id="6b50b-169">b.</span></span> <span data-ttu-id="6b50b-170">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-170">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span></span>

    ![Conditional access](./media/app-based-conditional-access/05.png)


<span data-ttu-id="6b50b-172">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span><span class="sxs-lookup"><span data-stu-id="6b50b-172">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span></span>


![Conditional access](./media/app-based-conditional-access/09.png)

<span data-ttu-id="6b50b-174">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span><span class="sxs-lookup"><span data-stu-id="6b50b-174">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span></span>


## <a name="exchange-online-and-sharepoint-online-policy"></a><span data-ttu-id="6b50b-175">Exchange Online and SharePoint Online policy</span><span class="sxs-lookup"><span data-stu-id="6b50b-175">Exchange Online and SharePoint Online policy</span></span>

<span data-ttu-id="6b50b-176">This scenario consists of a conditional access with mobile app management policy for access to Exchange Online and SharePoint Online with approved apps.</span><span class="sxs-lookup"><span data-stu-id="6b50b-176">This scenario consists of a conditional access with mobile app management policy for access to Exchange Online and SharePoint Online with approved apps.</span></span>

### <a name="scenario-playbook"></a><span data-ttu-id="6b50b-177">Scenario playbook</span><span class="sxs-lookup"><span data-stu-id="6b50b-177">Scenario playbook</span></span>

<span data-ttu-id="6b50b-178">This scenario assumes that a user:</span><span class="sxs-lookup"><span data-stu-id="6b50b-178">This scenario assumes that a user:</span></span>

- <span data-ttu-id="6b50b-179">Tries to use the SharePoint app to connect and also to view their corporate sites</span><span class="sxs-lookup"><span data-stu-id="6b50b-179">Tries to use the SharePoint app to connect and also to view their corporate sites</span></span>

- <span data-ttu-id="6b50b-180">Attempt to sign-in with the same credentials as the Outlook app credentials</span><span class="sxs-lookup"><span data-stu-id="6b50b-180">Attempt to sign-in with the same credentials as the Outlook app credentials</span></span>

- <span data-ttu-id="6b50b-181">Does not have to re-register and can get access to the resources</span><span class="sxs-lookup"><span data-stu-id="6b50b-181">Does not have to re-register and can get access to the resources</span></span>


### <a name="configuration"></a><span data-ttu-id="6b50b-182">Configuration</span><span class="sxs-lookup"><span data-stu-id="6b50b-182">Configuration</span></span>

<span data-ttu-id="6b50b-183">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online and SharePoint Online**</span><span class="sxs-lookup"><span data-stu-id="6b50b-183">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online and SharePoint Online**</span></span>

<span data-ttu-id="6b50b-184">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-184">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/71.png)

1. <span data-ttu-id="6b50b-186">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-186">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-187">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-187">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>


3. <span data-ttu-id="6b50b-188">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online** and **Office 365 SharePoint Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-188">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online** and **Office 365 SharePoint Online**.</span></span> 

    ![Conditional access](./media/app-based-conditional-access/02.png)

4. <span data-ttu-id="6b50b-190">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**:</span><span class="sxs-lookup"><span data-stu-id="6b50b-190">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**:</span></span>

    <span data-ttu-id="6b50b-191">a.</span><span class="sxs-lookup"><span data-stu-id="6b50b-191">a.</span></span> <span data-ttu-id="6b50b-192">As **Device platforms**, select **Android** and **iOS**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-192">As **Device platforms**, select **Android** and **iOS**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/03.png)

    <span data-ttu-id="6b50b-194">b.</span><span class="sxs-lookup"><span data-stu-id="6b50b-194">b.</span></span> <span data-ttu-id="6b50b-195">As **Client apps**, select **Mobile apps and desktop apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-195">As **Client apps**, select **Mobile apps and desktop apps**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/04.png)

5. <span data-ttu-id="6b50b-197">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-197">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span></span>

    ![Conditional access](./media/app-based-conditional-access/05.png)




<span data-ttu-id="6b50b-199">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-199">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span></span>

<span data-ttu-id="6b50b-200">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-200">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/06.png)

1. <span data-ttu-id="6b50b-202">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-202">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-203">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-203">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>

3. <span data-ttu-id="6b50b-204">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-204">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span></span> <span data-ttu-id="6b50b-205">Online</span><span class="sxs-lookup"><span data-stu-id="6b50b-205">Online</span></span> 

    ![Conditional access](./media/app-based-conditional-access/07.png)

4. <span data-ttu-id="6b50b-207">**Conditions:** As **Conditions**, you need to configure **Client apps**:</span><span class="sxs-lookup"><span data-stu-id="6b50b-207">**Conditions:** As **Conditions**, you need to configure **Client apps**:</span></span>

    <span data-ttu-id="6b50b-208">a.</span><span class="sxs-lookup"><span data-stu-id="6b50b-208">a.</span></span> <span data-ttu-id="6b50b-209">As **Client apps**, select **Exchange Active Sync**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-209">As **Client apps**, select **Exchange Active Sync**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/08.png)

    <span data-ttu-id="6b50b-211">b.</span><span class="sxs-lookup"><span data-stu-id="6b50b-211">b.</span></span> <span data-ttu-id="6b50b-212">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-212">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span></span>

    ![Conditional access](./media/app-based-conditional-access/05.png)




<span data-ttu-id="6b50b-214">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span><span class="sxs-lookup"><span data-stu-id="6b50b-214">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span></span>


![Conditional access](./media/app-based-conditional-access/09.png)

<span data-ttu-id="6b50b-216">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span><span class="sxs-lookup"><span data-stu-id="6b50b-216">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span></span>


## <a name="app-based-or-compliant-device-policy-for-exchange-online-and-sharepoint-online"></a><span data-ttu-id="6b50b-217">App-based or compliant device policy for Exchange Online and SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6b50b-217">App-based or compliant device policy for Exchange Online and SharePoint Online</span></span>

<span data-ttu-id="6b50b-218">This scenario consists of an app-based or compliant device conditional access policy for access to Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="6b50b-218">This scenario consists of an app-based or compliant device conditional access policy for access to Exchange Online.</span></span>


### <a name="scenario-playbook"></a><span data-ttu-id="6b50b-219">Scenario playbook</span><span class="sxs-lookup"><span data-stu-id="6b50b-219">Scenario playbook</span></span>

<span data-ttu-id="6b50b-220">This scenario assumes that:</span><span class="sxs-lookup"><span data-stu-id="6b50b-220">This scenario assumes that:</span></span>
 
- <span data-ttu-id="6b50b-221">Some user are already enrolled (with or without corporate devices)</span><span class="sxs-lookup"><span data-stu-id="6b50b-221">Some user are already enrolled (with or without corporate devices)</span></span>

- <span data-ttu-id="6b50b-222">Users who are not enrolled and registered with Azure AD using an app protected application need to register a device to access resources</span><span class="sxs-lookup"><span data-stu-id="6b50b-222">Users who are not enrolled and registered with Azure AD using an app protected application need to register a device to access resources</span></span>

- <span data-ttu-id="6b50b-223">Enrolled users using the app protected application don't have to re-register the device</span><span class="sxs-lookup"><span data-stu-id="6b50b-223">Enrolled users using the app protected application don't have to re-register the device</span></span>


### <a name="configuration"></a><span data-ttu-id="6b50b-224">Configuration</span><span class="sxs-lookup"><span data-stu-id="6b50b-224">Configuration</span></span>

<span data-ttu-id="6b50b-225">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online and SharePoint Online**</span><span class="sxs-lookup"><span data-stu-id="6b50b-225">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online and SharePoint Online**</span></span>

<span data-ttu-id="6b50b-226">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-226">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/62.png)

1. <span data-ttu-id="6b50b-228">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-228">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-229">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-229">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>

3. <span data-ttu-id="6b50b-230">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online** and **Office 365 SharePoint Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-230">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online** and **Office 365 SharePoint Online**.</span></span> 

     ![Conditional access](./media/app-based-conditional-access/02.png)

4. <span data-ttu-id="6b50b-232">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-232">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**.</span></span> 
 
    <span data-ttu-id="6b50b-233">a.</span><span class="sxs-lookup"><span data-stu-id="6b50b-233">a.</span></span> <span data-ttu-id="6b50b-234">As **Device platforms**, select **Android** and **iOS**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-234">As **Device platforms**, select **Android** and **iOS**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/03.png)

    <span data-ttu-id="6b50b-236">b.</span><span class="sxs-lookup"><span data-stu-id="6b50b-236">b.</span></span> <span data-ttu-id="6b50b-237">As **Client apps**, select **Mobile apps and desktop apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-237">As **Client apps**, select **Mobile apps and desktop apps**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/04.png)

5. <span data-ttu-id="6b50b-239">As **Access controls**, you need to have the following selected:</span><span class="sxs-lookup"><span data-stu-id="6b50b-239">As **Access controls**, you need to have the following selected:</span></span>

    - <span data-ttu-id="6b50b-240">**Require device to be marked as compliant**</span><span class="sxs-lookup"><span data-stu-id="6b50b-240">**Require device to be marked as compliant**</span></span>

    - <span data-ttu-id="6b50b-241">**Require approved client app (preview)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-241">**Require approved client app (preview)**</span></span>

    - <span data-ttu-id="6b50b-242">**Require one of the selected controls**</span><span class="sxs-lookup"><span data-stu-id="6b50b-242">**Require one of the selected controls**</span></span>   
 
    ![Conditional access](./media/app-based-conditional-access/11.png)



<span data-ttu-id="6b50b-244">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-244">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span></span>

<span data-ttu-id="6b50b-245">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-245">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/61.png)

1. <span data-ttu-id="6b50b-247">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-247">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-248">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-248">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>

3. <span data-ttu-id="6b50b-249">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-249">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span></span> 

    ![Conditional access](./media/app-based-conditional-access/07.png)

4. <span data-ttu-id="6b50b-251">**Conditions:** As **Conditions**, you need to configure **Client apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-251">**Conditions:** As **Conditions**, you need to configure **Client apps**.</span></span> 

    <span data-ttu-id="6b50b-252">As \**Client apps*, select **Exchange Active Sync**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-252">As \**Client apps*, select **Exchange Active Sync**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/08.png)

5. <span data-ttu-id="6b50b-254">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-254">As **Access controls**, you need to have **Require approved client app (preview)** selected.</span></span>
 
    ![Conditional access](./media/app-based-conditional-access/11.png)




<span data-ttu-id="6b50b-256">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span><span class="sxs-lookup"><span data-stu-id="6b50b-256">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span></span>


![Conditional access](./media/app-based-conditional-access/09.png)

<span data-ttu-id="6b50b-258">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span><span class="sxs-lookup"><span data-stu-id="6b50b-258">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span></span>





## <a name="app-based-and-compliant-device-policy-for-exchange-online-and-sharepoint-online"></a><span data-ttu-id="6b50b-259">App-based and compliant device policy for Exchange Online and SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6b50b-259">App-based and compliant device policy for Exchange Online and SharePoint Online</span></span>

<span data-ttu-id="6b50b-260">This scenario consists of an app-based and compliant device conditional access policy for access to Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="6b50b-260">This scenario consists of an app-based and compliant device conditional access policy for access to Exchange Online.</span></span>


### <a name="scenario-playbook"></a><span data-ttu-id="6b50b-261">Scenario playbook</span><span class="sxs-lookup"><span data-stu-id="6b50b-261">Scenario playbook</span></span>

<span data-ttu-id="6b50b-262">This scenario assumes that a user:</span><span class="sxs-lookup"><span data-stu-id="6b50b-262">This scenario assumes that a user:</span></span>
 
-   <span data-ttu-id="6b50b-263">Configures email using a native mail application on iOS or Android to connect to Exchange</span><span class="sxs-lookup"><span data-stu-id="6b50b-263">Configures email using a native mail application on iOS or Android to connect to Exchange</span></span>
-   <span data-ttu-id="6b50b-264">Receives an email that indicates that access requires your device to be enrolled</span><span class="sxs-lookup"><span data-stu-id="6b50b-264">Receives an email that indicates that access requires your device to be enrolled</span></span>
-   <span data-ttu-id="6b50b-265">Downloads the company portal and signs in to company portal</span><span class="sxs-lookup"><span data-stu-id="6b50b-265">Downloads the company portal and signs in to company portal</span></span>
-   <span data-ttu-id="6b50b-266">Checks mail and is asked to use the Outlook app</span><span class="sxs-lookup"><span data-stu-id="6b50b-266">Checks mail and is asked to use the Outlook app</span></span>
-   <span data-ttu-id="6b50b-267">Downloads the Outlook app</span><span class="sxs-lookup"><span data-stu-id="6b50b-267">Downloads the Outlook app</span></span>
-   <span data-ttu-id="6b50b-268">Opens the Outlook app and enters the credentials used in the enrollment</span><span class="sxs-lookup"><span data-stu-id="6b50b-268">Opens the Outlook app and enters the credentials used in the enrollment</span></span>
-   <span data-ttu-id="6b50b-269">User is able to access email</span><span class="sxs-lookup"><span data-stu-id="6b50b-269">User is able to access email</span></span>

<span data-ttu-id="6b50b-270">Any Intune app protection policies are activated at the time of access to the corporate data and may prompt the user to restart the application, use an additional PIN etc. (if configured for the application and platform)</span><span class="sxs-lookup"><span data-stu-id="6b50b-270">Any Intune app protection policies are activated at the time of access to the corporate data and may prompt the user to restart the application, use an additional PIN etc. (if configured for the application and platform)</span></span>


### <a name="configuration"></a><span data-ttu-id="6b50b-271">Configuration</span><span class="sxs-lookup"><span data-stu-id="6b50b-271">Configuration</span></span>

<span data-ttu-id="6b50b-272">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online and SharePoint Online**</span><span class="sxs-lookup"><span data-stu-id="6b50b-272">**Step 1 - Configure an Azure AD conditional access policy for Exchange Online and SharePoint Online**</span></span>

<span data-ttu-id="6b50b-273">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-273">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/62.png)

1. <span data-ttu-id="6b50b-275">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-275">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-276">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-276">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>

3. <span data-ttu-id="6b50b-277">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online** and **Office 365 SharePoint Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-277">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online** and **Office 365 SharePoint Online**.</span></span> 

     ![Conditional access](./media/app-based-conditional-access/02.png)

4. <span data-ttu-id="6b50b-279">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-279">**Conditions:** As **Conditions**, you need to configure **Device platforms** and **Client apps**.</span></span> 
 
    <span data-ttu-id="6b50b-280">a.</span><span class="sxs-lookup"><span data-stu-id="6b50b-280">a.</span></span> <span data-ttu-id="6b50b-281">As **Device platforms**, select **Android** and **iOS**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-281">As **Device platforms**, select **Android** and **iOS**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/03.png)

    <span data-ttu-id="6b50b-283">b.</span><span class="sxs-lookup"><span data-stu-id="6b50b-283">b.</span></span> <span data-ttu-id="6b50b-284">As **Client apps**, select **Mobile apps and desktop apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-284">As **Client apps**, select **Mobile apps and desktop apps**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/04.png)

5. <span data-ttu-id="6b50b-286">As **Access controls**, you need to have the following selected:</span><span class="sxs-lookup"><span data-stu-id="6b50b-286">As **Access controls**, you need to have the following selected:</span></span>

    - <span data-ttu-id="6b50b-287">**Require device to be marked as compliant**</span><span class="sxs-lookup"><span data-stu-id="6b50b-287">**Require device to be marked as compliant**</span></span>

    - <span data-ttu-id="6b50b-288">**Require approved client app (preview)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-288">**Require approved client app (preview)**</span></span>

    - <span data-ttu-id="6b50b-289">**Require all the selected controls**</span><span class="sxs-lookup"><span data-stu-id="6b50b-289">**Require all the selected controls**</span></span>   
 
    ![Conditional access](./media/app-based-conditional-access/13.png)



<span data-ttu-id="6b50b-291">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-291">**Step 2 - Configure an Azure AD conditional access policy for Exchange Online with Active Sync (EAS)**</span></span>

<span data-ttu-id="6b50b-292">For the conditional access policy in this step, you need to configure the following components:</span><span class="sxs-lookup"><span data-stu-id="6b50b-292">For the conditional access policy in this step, you need to configure the following components:</span></span>

![Conditional access](./media/app-based-conditional-access/61.png)

1. <span data-ttu-id="6b50b-294">The **Name** of your conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="6b50b-294">The **Name** of your conditional access policy.</span></span>

2. <span data-ttu-id="6b50b-295">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span><span class="sxs-lookup"><span data-stu-id="6b50b-295">**Users and groups**: Each conditional access policy must have at least one user or group selected.</span></span>

3. <span data-ttu-id="6b50b-296">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-296">**Cloud apps:** As cloud apps, you need to select **Office 365 Exchange Online**.</span></span> 

    ![Conditional access](./media/app-based-conditional-access/07.png)

4. <span data-ttu-id="6b50b-298">**Conditions:** As **Conditions**, you need to configure **Client apps**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-298">**Conditions:** As **Conditions**, you need to configure **Client apps**.</span></span> 

    <span data-ttu-id="6b50b-299">As **Client apps**, select **Exchange Active Sync**.</span><span class="sxs-lookup"><span data-stu-id="6b50b-299">As **Client apps**, select **Exchange Active Sync**.</span></span>

    ![Conditional access](./media/app-based-conditional-access/08.png)

5. <span data-ttu-id="6b50b-301">As **Access controls**, you need to have the following selected:</span><span class="sxs-lookup"><span data-stu-id="6b50b-301">As **Access controls**, you need to have the following selected:</span></span>

    - <span data-ttu-id="6b50b-302">**Require device to be marked as compliant**</span><span class="sxs-lookup"><span data-stu-id="6b50b-302">**Require device to be marked as compliant**</span></span>

    - <span data-ttu-id="6b50b-303">**Require approved client app (preview)**</span><span class="sxs-lookup"><span data-stu-id="6b50b-303">**Require approved client app (preview)**</span></span>

    - <span data-ttu-id="6b50b-304">**Require all the selected controls**</span><span class="sxs-lookup"><span data-stu-id="6b50b-304">**Require all the selected controls**</span></span>   
 
    ![Conditional access](./media/app-based-conditional-access/64.png)




<span data-ttu-id="6b50b-306">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span><span class="sxs-lookup"><span data-stu-id="6b50b-306">**Step 3 - Configure Intune app protection policy for iOS and Android client applications**</span></span>


![Conditional access](./media/app-based-conditional-access/09.png)

<span data-ttu-id="6b50b-308">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span><span class="sxs-lookup"><span data-stu-id="6b50b-308">See [Protect apps and data with Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune) for more information.</span></span>






## <a name="next-steps"></a><span data-ttu-id="6b50b-309">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b50b-309">Next steps</span></span>

<span data-ttu-id="6b50b-310">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="6b50b-310">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

<span data-ttu-id="6b50b-311">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="6b50b-311">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 
