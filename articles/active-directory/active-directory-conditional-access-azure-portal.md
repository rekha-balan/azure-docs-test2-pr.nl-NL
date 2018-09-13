---
title: Azure Active Directory conditional access | Microsoft Docs
description: Use conditional access control in Azure Active Directory to check for specific conditions when authenticating for access to applications.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/06/2017
ms.author: markvi
ms.openlocfilehash: 6ef390284758602df5886eea8ebc24b09f32acaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554356"
---
# <a name="conditional-access-in-azure-active-directory---preview"></a><span data-ttu-id="41912-104">Conditional access in Azure Active Directory - preview</span><span class="sxs-lookup"><span data-stu-id="41912-104">Conditional access in Azure Active Directory - preview</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](active-directory-conditional-access-azure-portal.md)
> * [Azure classic portal](active-directory-conditional-access.md)


<span data-ttu-id="41912-107">The behavior outlined in this topic is currently in [preview](active-directory-preview-explainer.md).</span><span class="sxs-lookup"><span data-stu-id="41912-107">The behavior outlined in this topic is currently in [preview](active-directory-preview-explainer.md).</span></span>

<span data-ttu-id="41912-108">In a mobile first, cloud first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span><span class="sxs-lookup"><span data-stu-id="41912-108">In a mobile first, cloud first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="41912-109">With the proliferation of devices (including BYOD), work off corporate networks, and 3rd party SaaS apps, IT professionals are faced with two opposing goals:</span><span class="sxs-lookup"><span data-stu-id="41912-109">With the proliferation of devices (including BYOD), work off corporate networks, and 3rd party SaaS apps, IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="41912-110">Empower the end users to be productive wherever and whenever</span><span class="sxs-lookup"><span data-stu-id="41912-110">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="41912-111">Protect the corporate assets at any time</span><span class="sxs-lookup"><span data-stu-id="41912-111">Protect the corporate assets at any time</span></span>

<span data-ttu-id="41912-112">To improve productivity, Azure Active Directory provides your users with a broad range of options to access your corporate assets.</span><span class="sxs-lookup"><span data-stu-id="41912-112">To improve productivity, Azure Active Directory provides your users with a broad range of options to access your corporate assets.</span></span> <span data-ttu-id="41912-113">With application access management, Azure Active Directory enables you to ensure that only *the right people* can access your applications.</span><span class="sxs-lookup"><span data-stu-id="41912-113">With application access management, Azure Active Directory enables you to ensure that only *the right people* can access your applications.</span></span> <span data-ttu-id="41912-114">What if you want to have more control over how the right people are accessing your resources under certain conditions?</span><span class="sxs-lookup"><span data-stu-id="41912-114">What if you want to have more control over how the right people are accessing your resources under certain conditions?</span></span> <span data-ttu-id="41912-115">What if you even have conditions under which you want to block access to certain apps even for the *right people*?</span><span class="sxs-lookup"><span data-stu-id="41912-115">What if you even have conditions under which you want to block access to certain apps even for the *right people*?</span></span> <span data-ttu-id="41912-116">For example, it might be OK for you if the right people are accessing certain apps from a trusted network; however, you might not want them to access these apps from a network you don't trust.</span><span class="sxs-lookup"><span data-stu-id="41912-116">For example, it might be OK for you if the right people are accessing certain apps from a trusted network; however, you might not want them to access these apps from a network you don't trust.</span></span> <span data-ttu-id="41912-117">You can address these questions using conditional access.</span><span class="sxs-lookup"><span data-stu-id="41912-117">You can address these questions using conditional access.</span></span>

<span data-ttu-id="41912-118">Conditional access is a capability of Azure Active Directory that enables you to enforce controls on the access to apps in your environment based on specific conditions.</span><span class="sxs-lookup"><span data-stu-id="41912-118">Conditional access is a capability of Azure Active Directory that enables you to enforce controls on the access to apps in your environment based on specific conditions.</span></span> <span data-ttu-id="41912-119">With controls, you can either tie additional requirements to the access or you can block it.</span><span class="sxs-lookup"><span data-stu-id="41912-119">With controls, you can either tie additional requirements to the access or you can block it.</span></span> <span data-ttu-id="41912-120">The implementation of conditional access is based on policies.</span><span class="sxs-lookup"><span data-stu-id="41912-120">The implementation of conditional access is based on policies.</span></span> <span data-ttu-id="41912-121">A policy-based approach simplifies your configuration experience because it follows the way you think about your access requirements.</span><span class="sxs-lookup"><span data-stu-id="41912-121">A policy-based approach simplifies your configuration experience because it follows the way you think about your access requirements.</span></span>  

<span data-ttu-id="41912-122">Typically, you define your access requirements using statements that are based on the following pattern:</span><span class="sxs-lookup"><span data-stu-id="41912-122">Typically, you define your access requirements using statements that are based on the following pattern:</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/10.png)

<span data-ttu-id="41912-124">When you replace the two occurrences of “*this*” with real-world information, you have an example for a policy statement that probably looks familiar to you:</span><span class="sxs-lookup"><span data-stu-id="41912-124">When you replace the two occurrences of “*this*” with real-world information, you have an example for a policy statement that probably looks familiar to you:</span></span>

<span data-ttu-id="41912-125">*When contractors are trying to access our cloud apps from networks that are not trusted, then block access.*</span><span class="sxs-lookup"><span data-stu-id="41912-125">*When contractors are trying to access our cloud apps from networks that are not trusted, then block access.*</span></span>

<span data-ttu-id="41912-126">The policy statement above highlights the power of conditional access.</span><span class="sxs-lookup"><span data-stu-id="41912-126">The policy statement above highlights the power of conditional access.</span></span> <span data-ttu-id="41912-127">While you can enable contractors to basically access your cloud apps (**who**), with conditional access, you can also define conditions under which the access is possible (**how**).</span><span class="sxs-lookup"><span data-stu-id="41912-127">While you can enable contractors to basically access your cloud apps (**who**), with conditional access, you can also define conditions under which the access is possible (**how**).</span></span>

<span data-ttu-id="41912-128">In the context of Azure Active Directory conditional access,</span><span class="sxs-lookup"><span data-stu-id="41912-128">In the context of Azure Active Directory conditional access,</span></span>

- <span data-ttu-id="41912-129">"**When this happens**" is called **condition statement**</span><span class="sxs-lookup"><span data-stu-id="41912-129">"**When this happens**" is called **condition statement**</span></span>
- <span data-ttu-id="41912-130">"**Then do this**" is called **controls**</span><span class="sxs-lookup"><span data-stu-id="41912-130">"**Then do this**" is called **controls**</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/11.png)

<span data-ttu-id="41912-132">The combination of a condition statement with your controls represents a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="41912-132">The combination of a condition statement with your controls represents a conditional access policy.</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a><span data-ttu-id="41912-134">Controls</span><span class="sxs-lookup"><span data-stu-id="41912-134">Controls</span></span>

<span data-ttu-id="41912-135">In a conditional access policy, controls define what it is that should happen when a condition statement has been satisfied.</span><span class="sxs-lookup"><span data-stu-id="41912-135">In a conditional access policy, controls define what it is that should happen when a condition statement has been satisfied.</span></span>  
<span data-ttu-id="41912-136">With controls, you can either block access or allow access with additional requirements.</span><span class="sxs-lookup"><span data-stu-id="41912-136">With controls, you can either block access or allow access with additional requirements.</span></span>
<span data-ttu-id="41912-137">When you configure a policy that allows access, you need to select at least one requirement.</span><span class="sxs-lookup"><span data-stu-id="41912-137">When you configure a policy that allows access, you need to select at least one requirement.</span></span>   

### <a name="grant-controls"></a><span data-ttu-id="41912-138">Grant controls</span><span class="sxs-lookup"><span data-stu-id="41912-138">Grant controls</span></span>
<span data-ttu-id="41912-139">The current implementation of Azure Active Directory enables you to configure the following grant control requirements:</span><span class="sxs-lookup"><span data-stu-id="41912-139">The current implementation of Azure Active Directory enables you to configure the following grant control requirements:</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/05.png)

- <span data-ttu-id="41912-141">**Multi-factor Authentication** - You can require strong authentication through multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="41912-141">**Multi-factor Authentication** - You can require strong authentication through multi-factor authentication.</span></span> <span data-ttu-id="41912-142">As provider, you can use Azure Multi-Factor or an on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="41912-142">As provider, you can use Azure Multi-Factor or an on-premises multi-factor authentication provider, combined with Active Directory Federation Services (AD FS).</span></span> <span data-ttu-id="41912-143">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access to the credentials of a valid user.</span><span class="sxs-lookup"><span data-stu-id="41912-143">Using multi-factor authentication helps protect resources from being accessed by an unauthorized user who might have gained access to the credentials of a valid user.</span></span>

- <span data-ttu-id="41912-144">**Compliant device** - You can set conditional access policies at the device level.</span><span class="sxs-lookup"><span data-stu-id="41912-144">**Compliant device** - You can set conditional access policies at the device level.</span></span> <span data-ttu-id="41912-145">You might set up a policy to only enable computers that are compliant, or mobile devices that are enrolled in a mobile device management application, can access your organization's resources.</span><span class="sxs-lookup"><span data-stu-id="41912-145">You might set up a policy to only enable computers that are compliant, or mobile devices that are enrolled in a mobile device management application, can access your organization's resources.</span></span> <span data-ttu-id="41912-146">For example, you can use Intune to check device compliance, and then report it to Azure AD for enforcement when the user attempts to access an application.</span><span class="sxs-lookup"><span data-stu-id="41912-146">For example, you can use Intune to check device compliance, and then report it to Azure AD for enforcement when the user attempts to access an application.</span></span> <span data-ttu-id="41912-147">For detailed guidance about how to use Intune to protect apps and data, see Protect apps and data with Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="41912-147">For detailed guidance about how to use Intune to protect apps and data, see Protect apps and data with Microsoft Intune.</span></span> <span data-ttu-id="41912-148">You also can use Intune to enforce data protection for lost or stolen devices.</span><span class="sxs-lookup"><span data-stu-id="41912-148">You also can use Intune to enforce data protection for lost or stolen devices.</span></span> <span data-ttu-id="41912-149">For more information, see Help protect your data with full or selective wipe using Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="41912-149">For more information, see Help protect your data with full or selective wipe using Microsoft Intune.</span></span>

- <span data-ttu-id="41912-150">**Domain joined device** – You can require the device you have used to connect to Azure Active Directory to be a domain joined device.</span><span class="sxs-lookup"><span data-stu-id="41912-150">**Domain joined device** – You can require the device you have used to connect to Azure Active Directory to be a domain joined device.</span></span> <span data-ttu-id="41912-151">This policy applies to Windows desktops, laptops, and enterprise tablets.</span><span class="sxs-lookup"><span data-stu-id="41912-151">This policy applies to Windows desktops, laptops, and enterprise tablets.</span></span> <span data-ttu-id="41912-152">For more information about how to set up automatic registration of domain-joined devices with Azure AD, see [Automatic device registration with Azure Active Directory for Windows domain-joined devices](active-directory-conditional-access-automatic-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="41912-152">For more information about how to set up automatic registration of domain-joined devices with Azure AD, see [Automatic device registration with Azure Active Directory for Windows domain-joined devices](active-directory-conditional-access-automatic-device-registration.md).</span></span>

<span data-ttu-id="41912-153">If you have more than one requirement selected in a conditional access policy, you can also configure your requirements for applying them.</span><span class="sxs-lookup"><span data-stu-id="41912-153">If you have more than one requirement selected in a conditional access policy, you can also configure your requirements for applying them.</span></span> <span data-ttu-id="41912-154">You can choose to require all of the selected controls or one of them.</span><span class="sxs-lookup"><span data-stu-id="41912-154">You can choose to require all of the selected controls or one of them.</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a><span data-ttu-id="41912-156">Session controls</span><span class="sxs-lookup"><span data-stu-id="41912-156">Session controls</span></span>
<span data-ttu-id="41912-157">Session controls enable limiting experience within a cloud app.</span><span class="sxs-lookup"><span data-stu-id="41912-157">Session controls enable limiting experience within a cloud app.</span></span> <span data-ttu-id="41912-158">The session controls are enforced by cloud apps and rely on additional information provided by Azure AD to the app about the session.</span><span class="sxs-lookup"><span data-stu-id="41912-158">The session controls are enforced by cloud apps and rely on additional information provided by Azure AD to the app about the session.</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a><span data-ttu-id="41912-160">Use app enforced restrictions</span><span class="sxs-lookup"><span data-stu-id="41912-160">Use app enforced restrictions</span></span>
<span data-ttu-id="41912-161">You can use this control to require Azure AD to pass the device information to the cloud app.</span><span class="sxs-lookup"><span data-stu-id="41912-161">You can use this control to require Azure AD to pass the device information to the cloud app.</span></span> <span data-ttu-id="41912-162">This helps the cloud app know if the user is coming from a compliant device or domain joined device.</span><span class="sxs-lookup"><span data-stu-id="41912-162">This helps the cloud app know if the user is coming from a compliant device or domain joined device.</span></span> <span data-ttu-id="41912-163">This control is currently only supported with SharePoint as the cloud app.</span><span class="sxs-lookup"><span data-stu-id="41912-163">This control is currently only supported with SharePoint as the cloud app.</span></span> <span data-ttu-id="41912-164">SharePoint uses the device information to provide users a limited or full experience depending on the device state.</span><span class="sxs-lookup"><span data-stu-id="41912-164">SharePoint uses the device information to provide users a limited or full experience depending on the device state.</span></span>
<span data-ttu-id="41912-165">To learn more about how to require limited access with SharePoint, go [here](https://aka.ms/spolimitedaccessdocs).</span><span class="sxs-lookup"><span data-stu-id="41912-165">To learn more about how to require limited access with SharePoint, go [here](https://aka.ms/spolimitedaccessdocs).</span></span>

## <a name="condition-statement"></a><span data-ttu-id="41912-166">Condition Statement</span><span class="sxs-lookup"><span data-stu-id="41912-166">Condition Statement</span></span>

<span data-ttu-id="41912-167">The previous section has introduced you to supported options to block or restrict access to your resources in form of controls.</span><span class="sxs-lookup"><span data-stu-id="41912-167">The previous section has introduced you to supported options to block or restrict access to your resources in form of controls.</span></span> <span data-ttu-id="41912-168">In a conditional access policy, you define the criteria that need to be met for your controls to be applied in form of a condition statement.</span><span class="sxs-lookup"><span data-stu-id="41912-168">In a conditional access policy, you define the criteria that need to be met for your controls to be applied in form of a condition statement.</span></span>  

<span data-ttu-id="41912-169">You can include the following assignments into your condition statement:</span><span class="sxs-lookup"><span data-stu-id="41912-169">You can include the following assignments into your condition statement:</span></span>

![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/07.png)


- <span data-ttu-id="41912-171">**Who** - In many cases, you want your controls to be applied to a specific set of users.</span><span class="sxs-lookup"><span data-stu-id="41912-171">**Who** - In many cases, you want your controls to be applied to a specific set of users.</span></span> <span data-ttu-id="41912-172">In a condition statement, you can define this set by selecting the users and groups your policy applies to.</span><span class="sxs-lookup"><span data-stu-id="41912-172">In a condition statement, you can define this set by selecting the users and groups your policy applies to.</span></span> <span data-ttu-id="41912-173">If necessary, you can also explicitly exclude a set of users from your policy by exempting them.</span><span class="sxs-lookup"><span data-stu-id="41912-173">If necessary, you can also explicitly exclude a set of users from your policy by exempting them.</span></span>  
<span data-ttu-id="41912-174">By selecting users and groups, you define the scope of users your policy applies to.</span><span class="sxs-lookup"><span data-stu-id="41912-174">By selecting users and groups, you define the scope of users your policy applies to.</span></span>    

    ![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/08.png)



- <span data-ttu-id="41912-176">**What** - Typically, there are certain apps that are running in your environment requiring, from a protection perspective, more attention than others.</span><span class="sxs-lookup"><span data-stu-id="41912-176">**What** - Typically, there are certain apps that are running in your environment requiring, from a protection perspective, more attention than others.</span></span> <span data-ttu-id="41912-177">This affects, for example, apps that have access to sensitive data.</span><span class="sxs-lookup"><span data-stu-id="41912-177">This affects, for example, apps that have access to sensitive data.</span></span>
<span data-ttu-id="41912-178">By selecting cloud apps, you define the scope of cloud apps your policy applies to.</span><span class="sxs-lookup"><span data-stu-id="41912-178">By selecting cloud apps, you define the scope of cloud apps your policy applies to.</span></span> <span data-ttu-id="41912-179">If necessary, you can also explicitly exclude a set of apps from your policy.</span><span class="sxs-lookup"><span data-stu-id="41912-179">If necessary, you can also explicitly exclude a set of apps from your policy.</span></span>

    ![Control](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/09.png)


- <span data-ttu-id="41912-181">**How** - As long as access to your apps is performed under conditions you can control, there might be no need for imposing additional controls on how your cloud apps are accessed by your users.</span><span class="sxs-lookup"><span data-stu-id="41912-181">**How** - As long as access to your apps is performed under conditions you can control, there might be no need for imposing additional controls on how your cloud apps are accessed by your users.</span></span> <span data-ttu-id="41912-182">However, things might look different if access to your cloud apps is performed, for example, from networks that are not trusted or devices that are not compliant.</span><span class="sxs-lookup"><span data-stu-id="41912-182">However, things might look different if access to your cloud apps is performed, for example, from networks that are not trusted or devices that are not compliant.</span></span> <span data-ttu-id="41912-183">In a condition statement, you can define certain access conditions that have additional requirements for how access to your apps is performed.</span><span class="sxs-lookup"><span data-stu-id="41912-183">In a condition statement, you can define certain access conditions that have additional requirements for how access to your apps is performed.</span></span>

    ![Conditions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/01.png)


## <a name="conditions"></a><span data-ttu-id="41912-185">Conditions</span><span class="sxs-lookup"><span data-stu-id="41912-185">Conditions</span></span>

<span data-ttu-id="41912-186">In the current implementation of Azure Active Directory, you can define conditions for the following areas:</span><span class="sxs-lookup"><span data-stu-id="41912-186">In the current implementation of Azure Active Directory, you can define conditions for the following areas:</span></span>


- <span data-ttu-id="41912-187">**Device platforms** – The device platform is characterized by the operating system that is running on your device (Android, iOS, Windows Phone, Windows).</span><span class="sxs-lookup"><span data-stu-id="41912-187">**Device platforms** – The device platform is characterized by the operating system that is running on your device (Android, iOS, Windows Phone, Windows).</span></span> <span data-ttu-id="41912-188">You can define the device platforms that are included as well as device platforms that are exempted from a policy.</span><span class="sxs-lookup"><span data-stu-id="41912-188">You can define the device platforms that are included as well as device platforms that are exempted from a policy.</span></span>  
<span data-ttu-id="41912-189">To use device platforms in the policy, first change the configure toggles to **Yes**, and then select all or individual device platforms the policy applies to.</span><span class="sxs-lookup"><span data-stu-id="41912-189">To use device platforms in the policy, first change the configure toggles to **Yes**, and then select all or individual device platforms the policy applies to.</span></span> <span data-ttu-id="41912-190">If you select individual device platforms, the policy has only an impact on these platforms.</span><span class="sxs-lookup"><span data-stu-id="41912-190">If you select individual device platforms, the policy has only an impact on these platforms.</span></span> <span data-ttu-id="41912-191">In this case, sign-ins to other supported platforms are not impacted by the policy.</span><span class="sxs-lookup"><span data-stu-id="41912-191">In this case, sign-ins to other supported platforms are not impacted by the policy.</span></span>

    ![Conditions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/02.png)

- <span data-ttu-id="41912-193">**Locations** -  The location is identified by the IP address of the client you have used to connect to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="41912-193">**Locations** -  The location is identified by the IP address of the client you have used to connect to Azure Active Directory.</span></span> <span data-ttu-id="41912-194">This condition requires you to be familiar with Trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="41912-194">This condition requires you to be familiar with Trusted IPs.</span></span> <span data-ttu-id="41912-195">Trusted IPs is a feature of multi-factor authentication that enables you to define trusted IP address ranges representing your organization's local intranet.</span><span class="sxs-lookup"><span data-stu-id="41912-195">Trusted IPs is a feature of multi-factor authentication that enables you to define trusted IP address ranges representing your organization's local intranet.</span></span> <span data-ttu-id="41912-196">When you configure a location conditions, Trusted IPs enables you to distinguish between connections made from your organization's network and all other locations.</span><span class="sxs-lookup"><span data-stu-id="41912-196">When you configure a location conditions, Trusted IPs enables you to distinguish between connections made from your organization's network and all other locations.</span></span> <span data-ttu-id="41912-197">For more details, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="41912-197">For more details, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>  
<span data-ttu-id="41912-198">You can either include all locations or all trused IPs and you can exclude all trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="41912-198">You can either include all locations or all trused IPs and you can exclude all trusted IPs.</span></span>

    ![Conditions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/03.png)


- <span data-ttu-id="41912-200">**Client app** - The client app can be either on a generic level the app (web browser, mobile app, desktop client) you have used to connect to Azure Active Directory or you can specifically select Exchange Active Sync.</span><span class="sxs-lookup"><span data-stu-id="41912-200">**Client app** - The client app can be either on a generic level the app (web browser, mobile app, desktop client) you have used to connect to Azure Active Directory or you can specifically select Exchange Active Sync.</span></span>  
<span data-ttu-id="41912-201">Legacy authentication refers to clients using basic authentication such as older Office clients that don’t use modern authentication.</span><span class="sxs-lookup"><span data-stu-id="41912-201">Legacy authentication refers to clients using basic authentication such as older Office clients that don’t use modern authentication.</span></span> <span data-ttu-id="41912-202">Conditional access is currently not supported with legacy authentication.</span><span class="sxs-lookup"><span data-stu-id="41912-202">Conditional access is currently not supported with legacy authentication.</span></span>

    ![Conditions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal/04.png)


## <a name="what-you-should-know"></a><span data-ttu-id="41912-204">What you should know</span><span class="sxs-lookup"><span data-stu-id="41912-204">What you should know</span></span>

### <a name="do-i-need-to-assign-a-user-to-my-policy"></a><span data-ttu-id="41912-205">Do I need to assign a user to my policy?</span><span class="sxs-lookup"><span data-stu-id="41912-205">Do I need to assign a user to my policy?</span></span>

<span data-ttu-id="41912-206">When configuring a conditional access policy, you should at least assign one group to it.</span><span class="sxs-lookup"><span data-stu-id="41912-206">When configuring a conditional access policy, you should at least assign one group to it.</span></span> <span data-ttu-id="41912-207">A conditional access policy that has no users and groups assigned, is never triggered.</span><span class="sxs-lookup"><span data-stu-id="41912-207">A conditional access policy that has no users and groups assigned, is never triggered.</span></span>

<span data-ttu-id="41912-208">When you intend to assign several users and groups to a policy, you should start small by assigning only one user or group, and then test your configuration.</span><span class="sxs-lookup"><span data-stu-id="41912-208">When you intend to assign several users and groups to a policy, you should start small by assigning only one user or group, and then test your configuration.</span></span> <span data-ttu-id="41912-209">If your policy works as expected, you can then add additional assignments to it.</span><span class="sxs-lookup"><span data-stu-id="41912-209">If your policy works as expected, you can then add additional assignments to it.</span></span>  


### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="41912-210">How are assignments evaluated?</span><span class="sxs-lookup"><span data-stu-id="41912-210">How are assignments evaluated?</span></span>

<span data-ttu-id="41912-211">All assignments are logically **ANDed**.</span><span class="sxs-lookup"><span data-stu-id="41912-211">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="41912-212">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span><span class="sxs-lookup"><span data-stu-id="41912-212">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="41912-213">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span><span class="sxs-lookup"><span data-stu-id="41912-213">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="41912-214">Including **All locations**</span><span class="sxs-lookup"><span data-stu-id="41912-214">Including **All locations**</span></span>
- <span data-ttu-id="41912-215">Excluding **All trusted IPs**</span><span class="sxs-lookup"><span data-stu-id="41912-215">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="41912-216">What happens if you have policies in the Azure classic portal and Azure portal configured?</span><span class="sxs-lookup"><span data-stu-id="41912-216">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="41912-217">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span><span class="sxs-lookup"><span data-stu-id="41912-217">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="41912-218">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span><span class="sxs-lookup"><span data-stu-id="41912-218">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="41912-219">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span><span class="sxs-lookup"><span data-stu-id="41912-219">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="41912-220">What happens if I have multiple policies for the same user configured?</span><span class="sxs-lookup"><span data-stu-id="41912-220">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="41912-221">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span><span class="sxs-lookup"><span data-stu-id="41912-221">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="41912-222">Does conditional access work with Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="41912-222">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="41912-223">No, you cannot use Exchange ActiveSync in a conditional access policy at this point.</span><span class="sxs-lookup"><span data-stu-id="41912-223">No, you cannot use Exchange ActiveSync in a conditional access policy at this point.</span></span>


### <a name="what-happens-if-i-require-multi-factor-authentication-or-a-compliant-device"></a><span data-ttu-id="41912-224">What happens if I require multi-factor authentication or a compliant device?</span><span class="sxs-lookup"><span data-stu-id="41912-224">What happens if I require multi-factor authentication or a compliant device?</span></span>

<span data-ttu-id="41912-225">Currently, the user will be prompted for multi-factor authentication irrespective of the device.</span><span class="sxs-lookup"><span data-stu-id="41912-225">Currently, the user will be prompted for multi-factor authentication irrespective of the device.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="41912-226">What you should avoid doing</span><span class="sxs-lookup"><span data-stu-id="41912-226">What you should avoid doing</span></span>

<span data-ttu-id="41912-227">The conditional access framework provides you with a great configuration flexibility.</span><span class="sxs-lookup"><span data-stu-id="41912-227">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="41912-228">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span><span class="sxs-lookup"><span data-stu-id="41912-228">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="41912-229">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="41912-229">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="41912-230">In your environment, you should avoid the following configurations:</span><span class="sxs-lookup"><span data-stu-id="41912-230">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="41912-231">**For all users, all cloud apps:**</span><span class="sxs-lookup"><span data-stu-id="41912-231">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="41912-232">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span><span class="sxs-lookup"><span data-stu-id="41912-232">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="41912-233">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span><span class="sxs-lookup"><span data-stu-id="41912-233">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="41912-234">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span><span class="sxs-lookup"><span data-stu-id="41912-234">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="41912-235">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span><span class="sxs-lookup"><span data-stu-id="41912-235">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="41912-236">**For all users, all cloud apps, all device platforms:**</span><span class="sxs-lookup"><span data-stu-id="41912-236">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="41912-237">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span><span class="sxs-lookup"><span data-stu-id="41912-237">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="41912-238">Common scenarios</span><span class="sxs-lookup"><span data-stu-id="41912-238">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="41912-239">Requiring multi-factor authentication for apps</span><span class="sxs-lookup"><span data-stu-id="41912-239">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="41912-240">Many environments have apps requiring a higher level of protection than the others.</span><span class="sxs-lookup"><span data-stu-id="41912-240">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="41912-241">This is, for example, the case for apps that have access to sensitive data.</span><span class="sxs-lookup"><span data-stu-id="41912-241">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="41912-242">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span><span class="sxs-lookup"><span data-stu-id="41912-242">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="41912-243">Requiring multi-factor authentication for access from networks that are not trusted</span><span class="sxs-lookup"><span data-stu-id="41912-243">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="41912-244">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="41912-244">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="41912-245">However, the main difference is the condition for this requirement.</span><span class="sxs-lookup"><span data-stu-id="41912-245">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="41912-246">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span><span class="sxs-lookup"><span data-stu-id="41912-246">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="41912-247">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span><span class="sxs-lookup"><span data-stu-id="41912-247">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="41912-248">Only trusted devices can access Office 365 services</span><span class="sxs-lookup"><span data-stu-id="41912-248">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="41912-249">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span><span class="sxs-lookup"><span data-stu-id="41912-249">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="41912-250">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span><span class="sxs-lookup"><span data-stu-id="41912-250">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="41912-251">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="41912-251">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="41912-252">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span><span class="sxs-lookup"><span data-stu-id="41912-252">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="41912-253">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span><span class="sxs-lookup"><span data-stu-id="41912-253">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41912-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="41912-254">Next steps</span></span>

<span data-ttu-id="41912-255">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41912-255">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>













