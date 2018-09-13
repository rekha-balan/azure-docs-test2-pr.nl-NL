---
title: What are access controls in Azure Active Directory conditional access? | Microsoft Docs
description: Learn how access controls in Azure Active Directory conditional access work.
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
ms.date: 08/28/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 050ccff8501a22526e9382a620258b0f846efe5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965533"
---
# <a name="what-are-access-controls-in-azure-active-directory-conditional-access"></a><span data-ttu-id="bfd9f-105">What are access controls in Azure Active Directory conditional access?</span><span class="sxs-lookup"><span data-stu-id="bfd9f-105">What are access controls in Azure Active Directory conditional access?</span></span> 

<span data-ttu-id="bfd9f-106">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-106">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users access your cloud apps.</span></span> <span data-ttu-id="bfd9f-107">In a conditional access policy, you define the response ("do this") to the reason for triggering your policy ("when this happens").</span><span class="sxs-lookup"><span data-stu-id="bfd9f-107">In a conditional access policy, you define the response ("do this") to the reason for triggering your policy ("when this happens").</span></span> 

![Control](./media/controls/10.png)


<span data-ttu-id="bfd9f-109">In the context of conditional access,</span><span class="sxs-lookup"><span data-stu-id="bfd9f-109">In the context of conditional access,</span></span> 

- <span data-ttu-id="bfd9f-110">"**When this happens**" is called **conditions**</span><span class="sxs-lookup"><span data-stu-id="bfd9f-110">"**When this happens**" is called **conditions**</span></span>

- <span data-ttu-id="bfd9f-111">"**Then do this**" is called **access controls**</span><span class="sxs-lookup"><span data-stu-id="bfd9f-111">"**Then do this**" is called **access controls**</span></span>


<span data-ttu-id="bfd9f-112">The combination of a condition statement with your controls represents a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-112">The combination of a condition statement with your controls represents a conditional access policy.</span></span>

![Control](./media/controls/61.png)

<span data-ttu-id="bfd9f-114">Each control is either a requirement that must be fulfilled by the person or system signing in, or a restriction on what the user can do after signing in.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-114">Each control is either a requirement that must be fulfilled by the person or system signing in, or a restriction on what the user can do after signing in.</span></span> 

<span data-ttu-id="bfd9f-115">There are two types of controls:</span><span class="sxs-lookup"><span data-stu-id="bfd9f-115">There are two types of controls:</span></span> 

- <span data-ttu-id="bfd9f-116">**Grant controls** - To gate access</span><span class="sxs-lookup"><span data-stu-id="bfd9f-116">**Grant controls** - To gate access</span></span>

- <span data-ttu-id="bfd9f-117">**Session controls** - To restrict access within a session</span><span class="sxs-lookup"><span data-stu-id="bfd9f-117">**Session controls** - To restrict access within a session</span></span>

<span data-ttu-id="bfd9f-118">This topic explains the various controls that are available in Azure AD conditional access.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-118">This topic explains the various controls that are available in Azure AD conditional access.</span></span> 

## <a name="grant-controls"></a><span data-ttu-id="bfd9f-119">Grant controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-119">Grant controls</span></span>

<span data-ttu-id="bfd9f-120">With grant controls, you can either block access altogether or allow access with additional requirements by selecting the desired controls.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-120">With grant controls, you can either block access altogether or allow access with additional requirements by selecting the desired controls.</span></span> <span data-ttu-id="bfd9f-121">For multiple controls, you can require:</span><span class="sxs-lookup"><span data-stu-id="bfd9f-121">For multiple controls, you can require:</span></span>

- <span data-ttu-id="bfd9f-122">All selected controls to be fulfilled (*AND*)</span><span class="sxs-lookup"><span data-stu-id="bfd9f-122">All selected controls to be fulfilled (*AND*)</span></span> 
- <span data-ttu-id="bfd9f-123">One selected control to be fulfilled (*OR*)</span><span class="sxs-lookup"><span data-stu-id="bfd9f-123">One selected control to be fulfilled (*OR*)</span></span>

![Control](./media/controls/17.png)



### <a name="multi-factor-authentication"></a><span data-ttu-id="bfd9f-125">Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="bfd9f-125">Multi-factor authentication</span></span>

<span data-ttu-id="bfd9f-126">You can use this control to require multi-factor authentication to access the specified cloud app.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-126">You can use this control to require multi-factor authentication to access the specified cloud app.</span></span> <span data-ttu-id="bfd9f-127">This control supports the following multi-factor providers:</span><span class="sxs-lookup"><span data-stu-id="bfd9f-127">This control supports the following multi-factor providers:</span></span> 

- <span data-ttu-id="bfd9f-128">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="bfd9f-128">Azure Multi-Factor Authentication</span></span> 

- <span data-ttu-id="bfd9f-129">An on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-129">An on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span></span>
 
<span data-ttu-id="bfd9f-130">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access to the primary credentials of a valid user.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-130">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access to the primary credentials of a valid user.</span></span>



### <a name="compliant-device"></a><span data-ttu-id="bfd9f-131">Compliant device</span><span class="sxs-lookup"><span data-stu-id="bfd9f-131">Compliant device</span></span>

<span data-ttu-id="bfd9f-132">You can configure conditional access policies that are device-based.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-132">You can configure conditional access policies that are device-based.</span></span> <span data-ttu-id="bfd9f-133">The objective of a device-based conditional access policy is to grant access to the configured resources only from [managed devices](require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-133">The objective of a device-based conditional access policy is to grant access to the configured resources only from [managed devices](require-managed-devices.md).</span></span> <span data-ttu-id="bfd9f-134">Requiring a compliant device is one option you have to define what a managed device is.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-134">Requiring a compliant device is one option you have to define what a managed device is.</span></span> <span data-ttu-id="bfd9f-135">If this option is selected, your conditional access policy grants access to access attempts made with devices that are [registered](../devices/overview.md) to your Azure Active Directory and are marked as compliant by Intune (for any device OS) or by your third-party MDM system for Windows 10 devices.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-135">If this option is selected, your conditional access policy grants access to access attempts made with devices that are [registered](../devices/overview.md) to your Azure Active Directory and are marked as compliant by Intune (for any device OS) or by your third-party MDM system for Windows 10 devices.</span></span> <span data-ttu-id="bfd9f-136">Third-party MDM systems for device OS types other than Windows 10 are not supported.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-136">Third-party MDM systems for device OS types other than Windows 10 are not supported.</span></span>

<span data-ttu-id="bfd9f-137">For more information, see [set up Azure Active Directory device-based conditional access policies](require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-137">For more information, see [set up Azure Active Directory device-based conditional access policies](require-managed-devices.md).</span></span>

### <a name="hybrid-azure-ad-joined-device"></a><span data-ttu-id="bfd9f-138">Hybrid Azure AD joined device</span><span class="sxs-lookup"><span data-stu-id="bfd9f-138">Hybrid Azure AD joined device</span></span>

<span data-ttu-id="bfd9f-139">Requiring a Hybrid Azure AD joined device is another option you have to configure device-based conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-139">Requiring a Hybrid Azure AD joined device is another option you have to configure device-based conditional access policies.</span></span> <span data-ttu-id="bfd9f-140">This requirement refers to Windows desktops, laptops, and enterprise tablets that are joined to an on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-140">This requirement refers to Windows desktops, laptops, and enterprise tablets that are joined to an on-premises Active Directory.</span></span> <span data-ttu-id="bfd9f-141">If this option is selected, your conditional access policy grants access to access attempts made with devices that are joined to your on-premises Active Directory and your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-141">If this option is selected, your conditional access policy grants access to access attempts made with devices that are joined to your on-premises Active Directory and your Azure Active Directory.</span></span>  

<span data-ttu-id="bfd9f-142">For more information, see [set up Azure Active Directory device-based conditional access policies](require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-142">For more information, see [set up Azure Active Directory device-based conditional access policies](require-managed-devices.md).</span></span>





### <a name="approved-client-app"></a><span data-ttu-id="bfd9f-143">Approved client app</span><span class="sxs-lookup"><span data-stu-id="bfd9f-143">Approved client app</span></span>

<span data-ttu-id="bfd9f-144">Because your employees use mobile devices for both personal and work tasks, you might want to have the ability to protect company data accessed using devices even in the case where they are not managed by you.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-144">Because your employees use mobile devices for both personal and work tasks, you might want to have the ability to protect company data accessed using devices even in the case where they are not managed by you.</span></span>
<span data-ttu-id="bfd9f-145">You can use [Intune app protection policies](https://docs.microsoft.com/intune/app-protection-policy) to help protect your company’s data independent of any mobile-device management (MDM) solution.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-145">You can use [Intune app protection policies](https://docs.microsoft.com/intune/app-protection-policy) to help protect your company’s data independent of any mobile-device management (MDM) solution.</span></span>


<span data-ttu-id="bfd9f-146">With approved client apps, you can require a client app that attempts to access your cloud apps to support [Intune app protection policies](https://docs.microsoft.com/intune/app-protection-policy).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-146">With approved client apps, you can require a client app that attempts to access your cloud apps to support [Intune app protection policies](https://docs.microsoft.com/intune/app-protection-policy).</span></span> <span data-ttu-id="bfd9f-147">For example, you can restrict access to Exchange Online to the Outlook app.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-147">For example, you can restrict access to Exchange Online to the Outlook app.</span></span> <span data-ttu-id="bfd9f-148">A conditional access policy that requires approved client apps is  also known as [app-based conditional access policy](app-based-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-148">A conditional access policy that requires approved client apps is  also known as [app-based conditional access policy](app-based-conditional-access.md).</span></span> <span data-ttu-id="bfd9f-149">For a list of supported approved client apps, see [approved client app requirement](technical-reference.md#approved-client-app-requirement).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-149">For a list of supported approved client apps, see [approved client app requirement](technical-reference.md#approved-client-app-requirement).</span></span>


### <a name="terms-of-use"></a><span data-ttu-id="bfd9f-150">Terms of Use</span><span class="sxs-lookup"><span data-stu-id="bfd9f-150">Terms of Use</span></span>

<span data-ttu-id="bfd9f-151">You can require a user in your tenant to consent to the terms of use before being granted access to a resource.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-151">You can require a user in your tenant to consent to the terms of use before being granted access to a resource.</span></span> <span data-ttu-id="bfd9f-152">As an administrator, you can configure and customize terms of use by uploading a PDF document.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-152">As an administrator, you can configure and customize terms of use by uploading a PDF document.</span></span> <span data-ttu-id="bfd9f-153">If a user falls in scope of this control access to an application is only granted if the terms of use have been agreed.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-153">If a user falls in scope of this control access to an application is only granted if the terms of use have been agreed.</span></span> 


### <a name="custom-controls"></a><span data-ttu-id="bfd9f-154">Custom controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-154">Custom controls</span></span> 

<span data-ttu-id="bfd9f-155">You can create custom controls in Conditional Access that redirect your users to a compatible service to satisfy further requirements outside of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-155">You can create custom controls in Conditional Access that redirect your users to a compatible service to satisfy further requirements outside of Azure Active Directory.</span></span> <span data-ttu-id="bfd9f-156">This allows you to use certain external multi-factor authentication and verification providers to enforce Conditional Access rules, or to build your own custom service.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-156">This allows you to use certain external multi-factor authentication and verification providers to enforce Conditional Access rules, or to build your own custom service.</span></span> <span data-ttu-id="bfd9f-157">To satisfy this control, a user’s browser is redirected to the external service, performs any required authentication or validation activities, and is then redirected back to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-157">To satisfy this control, a user’s browser is redirected to the external service, performs any required authentication or validation activities, and is then redirected back to Azure Active Directory.</span></span> <span data-ttu-id="bfd9f-158">If the user was successfully authenticated or validated, the user continues in the Conditional Access flow.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-158">If the user was successfully authenticated or validated, the user continues in the Conditional Access flow.</span></span> 

## <a name="custom-controls"></a><span data-ttu-id="bfd9f-159">Custom controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-159">Custom controls</span></span>

<span data-ttu-id="bfd9f-160">Custom controls are a capability of the Azure Active Directory Premium P1 edition.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-160">Custom controls are a capability of the Azure Active Directory Premium P1 edition.</span></span> <span data-ttu-id="bfd9f-161">When using custom controls, your users are redirected to a compatible service to satisfy further requirements outside of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-161">When using custom controls, your users are redirected to a compatible service to satisfy further requirements outside of Azure Active Directory.</span></span> <span data-ttu-id="bfd9f-162">To satisfy this control, a user’s browser is redirected to the external service, performs any required authentication or validation activities, and is then redirected back to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-162">To satisfy this control, a user’s browser is redirected to the external service, performs any required authentication or validation activities, and is then redirected back to Azure Active Directory.</span></span> <span data-ttu-id="bfd9f-163">Azure Active Directory verifies the response and, if the user was successfully authenticated or validated, the user continues in the conditional access flow.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-163">Azure Active Directory verifies the response and, if the user was successfully authenticated or validated, the user continues in the conditional access flow.</span></span>

<span data-ttu-id="bfd9f-164">These controls allow the use of certain external or custom services as conditional access controls, and generally extend the capabilities of Conditional Access.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-164">These controls allow the use of certain external or custom services as conditional access controls, and generally extend the capabilities of Conditional Access.</span></span>

<span data-ttu-id="bfd9f-165">Providers currently offering a compatible service include:</span><span class="sxs-lookup"><span data-stu-id="bfd9f-165">Providers currently offering a compatible service include:</span></span>

- [<span data-ttu-id="bfd9f-166">Duo Security</span><span class="sxs-lookup"><span data-stu-id="bfd9f-166">Duo Security</span></span>](https://duo.com/docs/azure-ca)

- [<span data-ttu-id="bfd9f-167">Entrust Datacard</span><span class="sxs-lookup"><span data-stu-id="bfd9f-167">Entrust Datacard</span></span>](https://www.entrustdatacard.com/products/authentication/intellitrust)

- <span data-ttu-id="bfd9f-168">RSA</span><span class="sxs-lookup"><span data-stu-id="bfd9f-168">RSA</span></span>

- [<span data-ttu-id="bfd9f-169">Trusona</span><span class="sxs-lookup"><span data-stu-id="bfd9f-169">Trusona</span></span>](https://www.trusona.com/docs/azure-ad-integration-guide)


<span data-ttu-id="bfd9f-170">For more information on those services, contact the providers directly.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-170">For more information on those services, contact the providers directly.</span></span>

### <a name="creating-custom-controls"></a><span data-ttu-id="bfd9f-171">Creating custom controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-171">Creating custom controls</span></span>

<span data-ttu-id="bfd9f-172">To create a custom control, you should first contact the provider that you wish to utilize.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-172">To create a custom control, you should first contact the provider that you wish to utilize.</span></span> <span data-ttu-id="bfd9f-173">Each non-Microsoft provider has its own process and requirements to sign up, subscribe, or otherwise become a part of the service, and to indicate that you wish to integrate with conditional access.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-173">Each non-Microsoft provider has its own process and requirements to sign up, subscribe, or otherwise become a part of the service, and to indicate that you wish to integrate with conditional access.</span></span> <span data-ttu-id="bfd9f-174">At that point, the provider will provide you with a block of data in JSON format.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-174">At that point, the provider will provide you with a block of data in JSON format.</span></span> <span data-ttu-id="bfd9f-175">This data allows the provider and conditional access to work together for your tenant, creates the new control and defines how conditional access can tell if your users have successfully performed verification with the provider.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-175">This data allows the provider and conditional access to work together for your tenant, creates the new control and defines how conditional access can tell if your users have successfully performed verification with the provider.</span></span>

<span data-ttu-id="bfd9f-176">Copy the JSON data and then paste it into the related textbox.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-176">Copy the JSON data and then paste it into the related textbox.</span></span> <span data-ttu-id="bfd9f-177">Do not make any changes to the JSON unless you explicitly understand the change you’re making.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-177">Do not make any changes to the JSON unless you explicitly understand the change you’re making.</span></span> <span data-ttu-id="bfd9f-178">Making any change could break the connection between the provider and Microsoft and potentially lock you and your users out of your accounts.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-178">Making any change could break the connection between the provider and Microsoft and potentially lock you and your users out of your accounts.</span></span>

<span data-ttu-id="bfd9f-179">The option to create a custom control is in the **Manage** section of the **Conditional access** page.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-179">The option to create a custom control is in the **Manage** section of the **Conditional access** page.</span></span>

![Control](./media/controls/82.png)

<span data-ttu-id="bfd9f-181">Clicking **New custom control**, opens a blade with a textbox for the JSON data of your control.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-181">Clicking **New custom control**, opens a blade with a textbox for the JSON data of your control.</span></span>  


![Control](./media/controls/81.png)


### <a name="deleting-custom-controls"></a><span data-ttu-id="bfd9f-183">Deleting custom controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-183">Deleting custom controls</span></span>

<span data-ttu-id="bfd9f-184">To delete a custom control, you must first ensure that it isn’t being used in any conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-184">To delete a custom control, you must first ensure that it isn’t being used in any conditional access policy.</span></span> <span data-ttu-id="bfd9f-185">Once complete:</span><span class="sxs-lookup"><span data-stu-id="bfd9f-185">Once complete:</span></span>

1. <span data-ttu-id="bfd9f-186">Go to the Custom controls list</span><span class="sxs-lookup"><span data-stu-id="bfd9f-186">Go to the Custom controls list</span></span>

2. <span data-ttu-id="bfd9f-187">Click …</span><span class="sxs-lookup"><span data-stu-id="bfd9f-187">Click …</span></span>  

3. <span data-ttu-id="bfd9f-188">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-188">Select **Delete**.</span></span>

### <a name="editing-custom-controls"></a><span data-ttu-id="bfd9f-189">Editing custom controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-189">Editing custom controls</span></span>

<span data-ttu-id="bfd9f-190">To edit a custom control, you must delete the current control and create a new control with the updated information.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-190">To edit a custom control, you must delete the current control and create a new control with the updated information.</span></span>




## <a name="session-controls"></a><span data-ttu-id="bfd9f-191">Session controls</span><span class="sxs-lookup"><span data-stu-id="bfd9f-191">Session controls</span></span>

<span data-ttu-id="bfd9f-192">Session controls enable limited experience within a cloud app.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-192">Session controls enable limited experience within a cloud app.</span></span> <span data-ttu-id="bfd9f-193">The session controls are enforced by cloud apps and rely on additional information provided by Azure AD to the app about the session.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-193">The session controls are enforced by cloud apps and rely on additional information provided by Azure AD to the app about the session.</span></span>

![Control](./media/controls/31.png)

### <a name="use-app-enforced-restrictions"></a><span data-ttu-id="bfd9f-195">Use app enforced restrictions</span><span class="sxs-lookup"><span data-stu-id="bfd9f-195">Use app enforced restrictions</span></span>

<span data-ttu-id="bfd9f-196">You can use this control to require Azure AD to pass the device information to the cloud app.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-196">You can use this control to require Azure AD to pass the device information to the cloud app.</span></span> <span data-ttu-id="bfd9f-197">This helps the cloud app know if the user is coming from a compliant device or domain joined device.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-197">This helps the cloud app know if the user is coming from a compliant device or domain joined device.</span></span> <span data-ttu-id="bfd9f-198">This control is currently only supported with SharePoint as the cloud app.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-198">This control is currently only supported with SharePoint as the cloud app.</span></span> <span data-ttu-id="bfd9f-199">SharePoint uses the device information to provide users a limited or full experience depending on the device state.</span><span class="sxs-lookup"><span data-stu-id="bfd9f-199">SharePoint uses the device information to provide users a limited or full experience depending on the device state.</span></span>
<span data-ttu-id="bfd9f-200">To learn more about how to require limited access with SharePoint, see [control access from unmanaged devices](https://aka.ms/spolimitedaccessdocs).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-200">To learn more about how to require limited access with SharePoint, see [control access from unmanaged devices](https://aka.ms/spolimitedaccessdocs).</span></span>



## <a name="next-steps"></a><span data-ttu-id="bfd9f-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfd9f-201">Next steps</span></span>

- <span data-ttu-id="bfd9f-202">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-202">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

- <span data-ttu-id="bfd9f-203">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="bfd9f-203">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 
