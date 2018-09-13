---
title: Azure Active Directory conditional access settings reference | Microsoft Docs
description: Get an overview of the supported settings in an Azure Active Directory conditional access policy.
services: active-directory.
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/11/2018
ms.author: markvi
ms.reviewer: spunukol
ms.openlocfilehash: 6010ea7f4997e4604e72cdf4a993956ab76b1ef2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968153"
---
# <a name="azure-active-directory-conditional-access-settings-reference"></a><span data-ttu-id="79e84-103">Azure Active Directory conditional access settings reference</span><span class="sxs-lookup"><span data-stu-id="79e84-103">Azure Active Directory conditional access settings reference</span></span>

<span data-ttu-id="79e84-104">You can use [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md) to control how authorized users can access your resources.</span><span class="sxs-lookup"><span data-stu-id="79e84-104">You can use [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md) to control how authorized users can access your resources.</span></span>   

<span data-ttu-id="79e84-105">This article provides you with support information for the following configuration options in a conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="79e84-105">This article provides you with support information for the following configuration options in a conditional access policy:</span></span> 

- <span data-ttu-id="79e84-106">Cloud applications assignments</span><span class="sxs-lookup"><span data-stu-id="79e84-106">Cloud applications assignments</span></span>

- <span data-ttu-id="79e84-107">Device platform condition</span><span class="sxs-lookup"><span data-stu-id="79e84-107">Device platform condition</span></span> 

- <span data-ttu-id="79e84-108">Client applications condition</span><span class="sxs-lookup"><span data-stu-id="79e84-108">Client applications condition</span></span>

- <span data-ttu-id="79e84-109">Approved client application requirement</span><span class="sxs-lookup"><span data-stu-id="79e84-109">Approved client application requirement</span></span>


<span data-ttu-id="79e84-110">If this is not the information you are looking for, please leave a comment at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="79e84-110">If this is not the information you are looking for, please leave a comment at the end of this article.</span></span>

## <a name="cloud-apps-assignments"></a><span data-ttu-id="79e84-111">Cloud apps assignments</span><span class="sxs-lookup"><span data-stu-id="79e84-111">Cloud apps assignments</span></span>

<span data-ttu-id="79e84-112">With conditional access policies, you control how your users access your [cloud apps](conditions.md#cloud-apps).</span><span class="sxs-lookup"><span data-stu-id="79e84-112">With conditional access policies, you control how your users access your [cloud apps](conditions.md#cloud-apps).</span></span> <span data-ttu-id="79e84-113">When you configure a conditional access policy, you need to select at least one cloud app.</span><span class="sxs-lookup"><span data-stu-id="79e84-113">When you configure a conditional access policy, you need to select at least one cloud app.</span></span> 

![Select the cloud apps for your policy](./media/technical-reference/09.png)


### <a name="microsoft-cloud-applications"></a><span data-ttu-id="79e84-115">Microsoft cloud applications</span><span class="sxs-lookup"><span data-stu-id="79e84-115">Microsoft cloud applications</span></span>

<span data-ttu-id="79e84-116">You can assign a conditional access policy to the following cloud apps from Microsoft:</span><span class="sxs-lookup"><span data-stu-id="79e84-116">You can assign a conditional access policy to the following cloud apps from Microsoft:</span></span>

- <span data-ttu-id="79e84-117">Azure Information Protection - [Learn more](/azure/information-protection/faqs#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)</span><span class="sxs-lookup"><span data-stu-id="79e84-117">Azure Information Protection - [Learn more](/azure/information-protection/faqs#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work)</span></span>

- <span data-ttu-id="79e84-118">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="79e84-118">Azure RemoteApp</span></span>

- <span data-ttu-id="79e84-119">Microsoft Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="79e84-119">Microsoft Dynamics 365</span></span>

- <span data-ttu-id="79e84-120">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="79e84-120">Microsoft Office 365 Yammer</span></span>

- <span data-ttu-id="79e84-121">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="79e84-121">Microsoft Office 365 Exchange Online</span></span>

- <span data-ttu-id="79e84-122">Microsoft Office 365 SharePoint Online (includes OneDrive for Business and Project Online)</span><span class="sxs-lookup"><span data-stu-id="79e84-122">Microsoft Office 365 SharePoint Online (includes OneDrive for Business and Project Online)</span></span>

- <span data-ttu-id="79e84-123">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="79e84-123">Microsoft Power BI</span></span> 

- <span data-ttu-id="79e84-124">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="79e84-124">Azure DevOps</span></span>

- <span data-ttu-id="79e84-125">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="79e84-125">Microsoft Teams</span></span>


### <a name="other-applications"></a><span data-ttu-id="79e84-126">Other applications</span><span class="sxs-lookup"><span data-stu-id="79e84-126">Other applications</span></span> 

<span data-ttu-id="79e84-127">In addition to the Microsoft cloud apps, you can assign a conditional access policy to the following types of cloud apps:</span><span class="sxs-lookup"><span data-stu-id="79e84-127">In addition to the Microsoft cloud apps, you can assign a conditional access policy to the following types of cloud apps:</span></span>

- <span data-ttu-id="79e84-128">Azure AD-connected applications</span><span class="sxs-lookup"><span data-stu-id="79e84-128">Azure AD-connected applications</span></span>

- <span data-ttu-id="79e84-129">Pre-integrated federated software as a service (SaaS) application</span><span class="sxs-lookup"><span data-stu-id="79e84-129">Pre-integrated federated software as a service (SaaS) application</span></span>

- <span data-ttu-id="79e84-130">Applications that use password single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="79e84-130">Applications that use password single sign-on (SSO)</span></span>

- <span data-ttu-id="79e84-131">Line-of-business applications</span><span class="sxs-lookup"><span data-stu-id="79e84-131">Line-of-business applications</span></span>

- <span data-ttu-id="79e84-132">Applications that use Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="79e84-132">Applications that use Azure AD Application Proxy</span></span>


## <a name="device-platform-condition"></a><span data-ttu-id="79e84-133">Device platform condition</span><span class="sxs-lookup"><span data-stu-id="79e84-133">Device platform condition</span></span>

<span data-ttu-id="79e84-134">In a conditional access policy, you can configure the device platform condition to tie the policy to the operating system on a client.</span><span class="sxs-lookup"><span data-stu-id="79e84-134">In a conditional access policy, you can configure the device platform condition to tie the policy to the operating system on a client.</span></span> <span data-ttu-id="79e84-135">Azure AD conditional access supports the following device platforms:</span><span class="sxs-lookup"><span data-stu-id="79e84-135">Azure AD conditional access supports the following device platforms:</span></span>

- <span data-ttu-id="79e84-136">Android</span><span class="sxs-lookup"><span data-stu-id="79e84-136">Android</span></span>

- <span data-ttu-id="79e84-137">iOS</span><span class="sxs-lookup"><span data-stu-id="79e84-137">iOS</span></span>

- <span data-ttu-id="79e84-138">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="79e84-138">Windows Phone</span></span>

- <span data-ttu-id="79e84-139">Windows</span><span class="sxs-lookup"><span data-stu-id="79e84-139">Windows</span></span>

- <span data-ttu-id="79e84-140">macOS</span><span class="sxs-lookup"><span data-stu-id="79e84-140">macOS</span></span>


![Tie the access policy to the client OS](./media/technical-reference/41.png)





## <a name="client-apps-condition"></a><span data-ttu-id="79e84-142">Client apps condition</span><span class="sxs-lookup"><span data-stu-id="79e84-142">Client apps condition</span></span> 

<span data-ttu-id="79e84-143">In your conditional access policy, you can configure the [client apps](conditions.md#client-apps) condition to tie the policy to the client app that has initiated an access attempt.</span><span class="sxs-lookup"><span data-stu-id="79e84-143">In your conditional access policy, you can configure the [client apps](conditions.md#client-apps) condition to tie the policy to the client app that has initiated an access attempt.</span></span> <span data-ttu-id="79e84-144">Set the client apps condition to grant or block access when an access attempt is made from the following types of client apps:</span><span class="sxs-lookup"><span data-stu-id="79e84-144">Set the client apps condition to grant or block access when an access attempt is made from the following types of client apps:</span></span>

- <span data-ttu-id="79e84-145">Browser</span><span class="sxs-lookup"><span data-stu-id="79e84-145">Browser</span></span>
- <span data-ttu-id="79e84-146">Mobile apps and desktop apps</span><span class="sxs-lookup"><span data-stu-id="79e84-146">Mobile apps and desktop apps</span></span>

![Control access for client apps](./media/technical-reference/03.png)

### <a name="supported-browsers"></a><span data-ttu-id="79e84-148">Supported browsers</span><span class="sxs-lookup"><span data-stu-id="79e84-148">Supported browsers</span></span> 

<span data-ttu-id="79e84-149">In your conditional access policy, you can select **Browsers** as client app.</span><span class="sxs-lookup"><span data-stu-id="79e84-149">In your conditional access policy, you can select **Browsers** as client app.</span></span>

![Control access for supported browsers](./media/technical-reference/05.png)

<span data-ttu-id="79e84-151">This setting works with all browsers.</span><span class="sxs-lookup"><span data-stu-id="79e84-151">This setting works with all browsers.</span></span> <span data-ttu-id="79e84-152">However, to satisfy a device policy, like a compliant device requirement, the following operating systems and browsers are supported:</span><span class="sxs-lookup"><span data-stu-id="79e84-152">However, to satisfy a device policy, like a compliant device requirement, the following operating systems and browsers are supported:</span></span>


| <span data-ttu-id="79e84-153">OS</span><span class="sxs-lookup"><span data-stu-id="79e84-153">OS</span></span>                     | <span data-ttu-id="79e84-154">Browsers</span><span class="sxs-lookup"><span data-stu-id="79e84-154">Browsers</span></span>                            | <span data-ttu-id="79e84-155">Support</span><span class="sxs-lookup"><span data-stu-id="79e84-155">Support</span></span>     |
| :--                    | :--                                 | :-:         |
| <span data-ttu-id="79e84-156">Windows 10</span><span class="sxs-lookup"><span data-stu-id="79e84-156">Windows 10</span></span>             | <span data-ttu-id="79e84-157">Internet Explorer, Edge, Chrome</span><span class="sxs-lookup"><span data-stu-id="79e84-157">Internet Explorer, Edge, Chrome</span></span>     | ![Check][1] |
| <span data-ttu-id="79e84-159">Windows 8 / 8.1</span><span class="sxs-lookup"><span data-stu-id="79e84-159">Windows 8 / 8.1</span></span>        | <span data-ttu-id="79e84-160">Internet Explorer, Chrome</span><span class="sxs-lookup"><span data-stu-id="79e84-160">Internet Explorer, Chrome</span></span>           | ![Check][1] |
| <span data-ttu-id="79e84-162">Windows 7</span><span class="sxs-lookup"><span data-stu-id="79e84-162">Windows 7</span></span>              | <span data-ttu-id="79e84-163">Internet Explorer, Chrome</span><span class="sxs-lookup"><span data-stu-id="79e84-163">Internet Explorer, Chrome</span></span>           | ![Check][1] |
| <span data-ttu-id="79e84-165">iOS</span><span class="sxs-lookup"><span data-stu-id="79e84-165">iOS</span></span>                    | <span data-ttu-id="79e84-166">Safari, Intune Managed Browser</span><span class="sxs-lookup"><span data-stu-id="79e84-166">Safari, Intune Managed Browser</span></span>      | ![Check][1] |
| <span data-ttu-id="79e84-168">Android</span><span class="sxs-lookup"><span data-stu-id="79e84-168">Android</span></span>                | <span data-ttu-id="79e84-169">Chrome, Intune Managed Browser</span><span class="sxs-lookup"><span data-stu-id="79e84-169">Chrome, Intune Managed Browser</span></span>      | ![Check][1] |
| <span data-ttu-id="79e84-171">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="79e84-171">Windows Phone</span></span>          | <span data-ttu-id="79e84-172">Internet Explorer, Edge</span><span class="sxs-lookup"><span data-stu-id="79e84-172">Internet Explorer, Edge</span></span>             | ![Check][1] |
| <span data-ttu-id="79e84-174">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="79e84-174">Windows Server 2016</span></span>    | <span data-ttu-id="79e84-175">Internet Explorer, Edge</span><span class="sxs-lookup"><span data-stu-id="79e84-175">Internet Explorer, Edge</span></span>             | ![Check][1] |
| <span data-ttu-id="79e84-177">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="79e84-177">Windows Server 2016</span></span>    | <span data-ttu-id="79e84-178">Chrome</span><span class="sxs-lookup"><span data-stu-id="79e84-178">Chrome</span></span>                              | <span data-ttu-id="79e84-179">Coming soon</span><span class="sxs-lookup"><span data-stu-id="79e84-179">Coming soon</span></span> |
| <span data-ttu-id="79e84-180">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="79e84-180">Windows Server 2012 R2</span></span> | <span data-ttu-id="79e84-181">Internet Explorer, Chrome</span><span class="sxs-lookup"><span data-stu-id="79e84-181">Internet Explorer, Chrome</span></span>           | ![Check][1] |
| <span data-ttu-id="79e84-183">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="79e84-183">Windows Server 2008 R2</span></span> | <span data-ttu-id="79e84-184">Internet Explorer, Chrome</span><span class="sxs-lookup"><span data-stu-id="79e84-184">Internet Explorer, Chrome</span></span>           | ![Check][1] |
| <span data-ttu-id="79e84-186">macOS</span><span class="sxs-lookup"><span data-stu-id="79e84-186">macOS</span></span>                  | <span data-ttu-id="79e84-187">Chrome, Safari</span><span class="sxs-lookup"><span data-stu-id="79e84-187">Chrome, Safari</span></span>                      | ![Check][1] |



#### <a name="chrome-support"></a><span data-ttu-id="79e84-189">Chrome support</span><span class="sxs-lookup"><span data-stu-id="79e84-189">Chrome support</span></span>

<span data-ttu-id="79e84-190">For Chrome support in **Windows 10 Creators Update (version 1703)** or later, install [this extension](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).</span><span class="sxs-lookup"><span data-stu-id="79e84-190">For Chrome support in **Windows 10 Creators Update (version 1703)** or later, install [this extension](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).</span></span>

<span data-ttu-id="79e84-191">To automatically deploy this extension to Chrome browsers, create the following registry key:</span><span class="sxs-lookup"><span data-stu-id="79e84-191">To automatically deploy this extension to Chrome browsers, create the following registry key:</span></span>

|    |    |
|--- | ---|
|<span data-ttu-id="79e84-192">Path</span><span class="sxs-lookup"><span data-stu-id="79e84-192">Path</span></span> | <span data-ttu-id="79e84-193">HKEY_LOCAL_MACHINE\Software\Policies\Google\Chrome\ExtensionInstallForcelist</span><span class="sxs-lookup"><span data-stu-id="79e84-193">HKEY_LOCAL_MACHINE\Software\Policies\Google\Chrome\ExtensionInstallForcelist</span></span> |
|<span data-ttu-id="79e84-194">Name</span><span class="sxs-lookup"><span data-stu-id="79e84-194">Name</span></span> | <span data-ttu-id="79e84-195">1</span><span class="sxs-lookup"><span data-stu-id="79e84-195">1</span></span> |
|<span data-ttu-id="79e84-196">Type</span><span class="sxs-lookup"><span data-stu-id="79e84-196">Type</span></span> | <span data-ttu-id="79e84-197">REG_SZ (String)</span><span class="sxs-lookup"><span data-stu-id="79e84-197">REG_SZ (String)</span></span> |
|<span data-ttu-id="79e84-198">Data</span><span class="sxs-lookup"><span data-stu-id="79e84-198">Data</span></span> | <span data-ttu-id="79e84-199">ppnbnpeolgkicgegkbkbjmhlideopiji;https://clients2.google.com/service/update2/crx</span><span class="sxs-lookup"><span data-stu-id="79e84-199">ppnbnpeolgkicgegkbkbjmhlideopiji;https://clients2.google.com/service/update2/crx</span></span>

<span data-ttu-id="79e84-200">For Chrome support in **Windows 8.1 and 7**, create the following registry key:</span><span class="sxs-lookup"><span data-stu-id="79e84-200">For Chrome support in **Windows 8.1 and 7**, create the following registry key:</span></span>

|    |    |
|--- | ---|
|<span data-ttu-id="79e84-201">Path</span><span class="sxs-lookup"><span data-stu-id="79e84-201">Path</span></span> | <span data-ttu-id="79e84-202">HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\AutoSelectCertificateForUrls</span><span class="sxs-lookup"><span data-stu-id="79e84-202">HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\AutoSelectCertificateForUrls</span></span> |
|<span data-ttu-id="79e84-203">Name</span><span class="sxs-lookup"><span data-stu-id="79e84-203">Name</span></span> | <span data-ttu-id="79e84-204">1</span><span class="sxs-lookup"><span data-stu-id="79e84-204">1</span></span> |
|<span data-ttu-id="79e84-205">Type</span><span class="sxs-lookup"><span data-stu-id="79e84-205">Type</span></span> | <span data-ttu-id="79e84-206">REG_SZ (String)</span><span class="sxs-lookup"><span data-stu-id="79e84-206">REG_SZ (String)</span></span> |
|<span data-ttu-id="79e84-207">Data</span><span class="sxs-lookup"><span data-stu-id="79e84-207">Data</span></span> | <span data-ttu-id="79e84-208">{"pattern":"https://device.login.microsoftonline.com","filter":{"ISSUER":{"CN":"MS-Organization-Access"}}}</span><span class="sxs-lookup"><span data-stu-id="79e84-208">{"pattern":"https://device.login.microsoftonline.com","filter":{"ISSUER":{"CN":"MS-Organization-Access"}}}</span></span>|

<span data-ttu-id="79e84-209">These browsers support device authentication, allowing the device to be identified and validated against a policy.</span><span class="sxs-lookup"><span data-stu-id="79e84-209">These browsers support device authentication, allowing the device to be identified and validated against a policy.</span></span> <span data-ttu-id="79e84-210">The device check fails if the browser is running in private mode.</span><span class="sxs-lookup"><span data-stu-id="79e84-210">The device check fails if the browser is running in private mode.</span></span> 


### <a name="supported-mobile-applications-and-desktop-clients"></a><span data-ttu-id="79e84-211">Supported mobile applications and desktop clients</span><span class="sxs-lookup"><span data-stu-id="79e84-211">Supported mobile applications and desktop clients</span></span>

<span data-ttu-id="79e84-212">In your conditional access policy, you can select **Mobile apps and desktop clients** as client app.</span><span class="sxs-lookup"><span data-stu-id="79e84-212">In your conditional access policy, you can select **Mobile apps and desktop clients** as client app.</span></span>


![Control access for supported mobile apps or desktop clients](./media/technical-reference/06.png)


<span data-ttu-id="79e84-214">This setting has an impact on access attempts made from the following mobile apps and desktop clients:</span><span class="sxs-lookup"><span data-stu-id="79e84-214">This setting has an impact on access attempts made from the following mobile apps and desktop clients:</span></span> 


|<span data-ttu-id="79e84-215">Client apps</span><span class="sxs-lookup"><span data-stu-id="79e84-215">Client apps</span></span>|<span data-ttu-id="79e84-216">Target Service</span><span class="sxs-lookup"><span data-stu-id="79e84-216">Target Service</span></span>|<span data-ttu-id="79e84-217">Platform</span><span class="sxs-lookup"><span data-stu-id="79e84-217">Platform</span></span>|
|---|---|---|
|<span data-ttu-id="79e84-218">Azure Remote app</span><span class="sxs-lookup"><span data-stu-id="79e84-218">Azure Remote app</span></span>|<span data-ttu-id="79e84-219">Azure Remote App service</span><span class="sxs-lookup"><span data-stu-id="79e84-219">Azure Remote App service</span></span>|<span data-ttu-id="79e84-220">Windows 10, Windows 8.1, Windows 7, iOS, Android, and Mac OS X</span><span class="sxs-lookup"><span data-stu-id="79e84-220">Windows 10, Windows 8.1, Windows 7, iOS, Android, and Mac OS X</span></span>|
|<span data-ttu-id="79e84-221">Dynamics CRM app</span><span class="sxs-lookup"><span data-stu-id="79e84-221">Dynamics CRM app</span></span>|<span data-ttu-id="79e84-222">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="79e84-222">Dynamics CRM</span></span>|<span data-ttu-id="79e84-223">Windows 10, Windows 8.1, iOS, and Android</span><span class="sxs-lookup"><span data-stu-id="79e84-223">Windows 10, Windows 8.1, iOS, and Android</span></span>|
|<span data-ttu-id="79e84-224">Mail/Calendar/People app, Outlook 2016, Outlook 2013 (with modern authentication)</span><span class="sxs-lookup"><span data-stu-id="79e84-224">Mail/Calendar/People app, Outlook 2016, Outlook 2013 (with modern authentication)</span></span>|<span data-ttu-id="79e84-225">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="79e84-225">Office 365 Exchange Online</span></span>|<span data-ttu-id="79e84-226">Windows 10</span><span class="sxs-lookup"><span data-stu-id="79e84-226">Windows 10</span></span>|
|<span data-ttu-id="79e84-227">MFA and location policy for apps.</span><span class="sxs-lookup"><span data-stu-id="79e84-227">MFA and location policy for apps.</span></span> <span data-ttu-id="79e84-228">Device based policies are not supported.</span><span class="sxs-lookup"><span data-stu-id="79e84-228">Device based policies are not supported.</span></span> |<span data-ttu-id="79e84-229">Any My Apps app service</span><span class="sxs-lookup"><span data-stu-id="79e84-229">Any My Apps app service</span></span>|<span data-ttu-id="79e84-230">Android and iOS</span><span class="sxs-lookup"><span data-stu-id="79e84-230">Android and iOS</span></span>|
|<span data-ttu-id="79e84-231">Microsoft Teams Services - this controls all services that support Microsoft Teams and all its Client Apps - Windows Desktop, iOS, Android, WP, and web client</span><span class="sxs-lookup"><span data-stu-id="79e84-231">Microsoft Teams Services - this controls all services that support Microsoft Teams and all its Client Apps - Windows Desktop, iOS, Android, WP, and web client</span></span>|<span data-ttu-id="79e84-232">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="79e84-232">Microsoft Teams</span></span>|<span data-ttu-id="79e84-233">Windows 10, Windows 8.1, Windows 7, iOS, Android and macOS</span><span class="sxs-lookup"><span data-stu-id="79e84-233">Windows 10, Windows 8.1, Windows 7, iOS, Android and macOS</span></span> |
|<span data-ttu-id="79e84-234">Office 2016 apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span><span class="sxs-lookup"><span data-stu-id="79e84-234">Office 2016 apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))</span></span>|<span data-ttu-id="79e84-235">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="79e84-235">Office 365 SharePoint Online</span></span>|<span data-ttu-id="79e84-236">Windows 8.1, Windows 7</span><span class="sxs-lookup"><span data-stu-id="79e84-236">Windows 8.1, Windows 7</span></span>|
|<span data-ttu-id="79e84-237">Office 2016 apps, Universal Office apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office Groups support is planned for the future, SharePoint app support is planned for the future</span><span class="sxs-lookup"><span data-stu-id="79e84-237">Office 2016 apps, Universal Office apps, Office 2013 (with modern authentication), OneDrive sync client (see [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), Office Groups support is planned for the future, SharePoint app support is planned for the future</span></span>|<span data-ttu-id="79e84-238">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="79e84-238">Office 365 SharePoint Online</span></span>|<span data-ttu-id="79e84-239">Windows 10</span><span class="sxs-lookup"><span data-stu-id="79e84-239">Windows 10</span></span>|
|<span data-ttu-id="79e84-240">Office 2016 for macOS (Word, Excel, PowerPoint, OneNote only).</span><span class="sxs-lookup"><span data-stu-id="79e84-240">Office 2016 for macOS (Word, Excel, PowerPoint, OneNote only).</span></span> <span data-ttu-id="79e84-241">OneDrive for Business support planned for the future</span><span class="sxs-lookup"><span data-stu-id="79e84-241">OneDrive for Business support planned for the future</span></span>|<span data-ttu-id="79e84-242">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="79e84-242">Office 365 SharePoint Online</span></span>|<span data-ttu-id="79e84-243">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="79e84-243">Mac OS X</span></span>|
|<span data-ttu-id="79e84-244">Office mobile apps</span><span class="sxs-lookup"><span data-stu-id="79e84-244">Office mobile apps</span></span>|<span data-ttu-id="79e84-245">Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="79e84-245">Office 365 SharePoint Online</span></span>|<span data-ttu-id="79e84-246">Android, iOS</span><span class="sxs-lookup"><span data-stu-id="79e84-246">Android, iOS</span></span>|
|<span data-ttu-id="79e84-247">Office Yammer app</span><span class="sxs-lookup"><span data-stu-id="79e84-247">Office Yammer app</span></span>|<span data-ttu-id="79e84-248">Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="79e84-248">Office 365 Yammer</span></span>|<span data-ttu-id="79e84-249">Windows 10, iOS, Android</span><span class="sxs-lookup"><span data-stu-id="79e84-249">Windows 10, iOS, Android</span></span>|
|<span data-ttu-id="79e84-250">Outlook 2016 (Office for macOS)</span><span class="sxs-lookup"><span data-stu-id="79e84-250">Outlook 2016 (Office for macOS)</span></span>|<span data-ttu-id="79e84-251">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="79e84-251">Office 365 Exchange Online</span></span>|<span data-ttu-id="79e84-252">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="79e84-252">Mac OS X</span></span>|
|<span data-ttu-id="79e84-253">Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span><span class="sxs-lookup"><span data-stu-id="79e84-253">Outlook 2016, Outlook 2013 (with modern authentication), Skype for Business (with modern authentication)</span></span>|<span data-ttu-id="79e84-254">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="79e84-254">Office 365 Exchange Online</span></span>|<span data-ttu-id="79e84-255">Windows 8.1, Windows 7</span><span class="sxs-lookup"><span data-stu-id="79e84-255">Windows 8.1, Windows 7</span></span>|
|<span data-ttu-id="79e84-256">Outlook mobile app</span><span class="sxs-lookup"><span data-stu-id="79e84-256">Outlook mobile app</span></span>|<span data-ttu-id="79e84-257">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="79e84-257">Office 365 Exchange Online</span></span>|<span data-ttu-id="79e84-258">Android, iOS</span><span class="sxs-lookup"><span data-stu-id="79e84-258">Android, iOS</span></span>|
|<span data-ttu-id="79e84-259">PowerBI app</span><span class="sxs-lookup"><span data-stu-id="79e84-259">PowerBI app</span></span>|<span data-ttu-id="79e84-260">PowerBI service</span><span class="sxs-lookup"><span data-stu-id="79e84-260">PowerBI service</span></span>|<span data-ttu-id="79e84-261">Windows 10, Windows 8.1, Windows 7, Android and iOS</span><span class="sxs-lookup"><span data-stu-id="79e84-261">Windows 10, Windows 8.1, Windows 7, Android and iOS</span></span>|
|<span data-ttu-id="79e84-262">Skype for Business</span><span class="sxs-lookup"><span data-stu-id="79e84-262">Skype for Business</span></span>|<span data-ttu-id="79e84-263">Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="79e84-263">Office 365 Exchange Online</span></span>|<span data-ttu-id="79e84-264">Android, IOS</span><span class="sxs-lookup"><span data-stu-id="79e84-264">Android, IOS</span></span> |
|<span data-ttu-id="79e84-265">Azure DevOps app</span><span class="sxs-lookup"><span data-stu-id="79e84-265">Azure DevOps app</span></span>|<span data-ttu-id="79e84-266">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="79e84-266">Azure DevOps</span></span>|<span data-ttu-id="79e84-267">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span><span class="sxs-lookup"><span data-stu-id="79e84-267">Windows 10, Windows 8.1, Windows 7, iOS, and Android</span></span>|



## <a name="approved-client-app-requirement"></a><span data-ttu-id="79e84-268">Approved client app requirement</span><span class="sxs-lookup"><span data-stu-id="79e84-268">Approved client app requirement</span></span> 

<span data-ttu-id="79e84-269">In your conditional access policy, you can require that an access attempt to the selected cloud apps needs to be made from an approved client app.</span><span class="sxs-lookup"><span data-stu-id="79e84-269">In your conditional access policy, you can require that an access attempt to the selected cloud apps needs to be made from an approved client app.</span></span> 

![Control access for approved client apps](./media/technical-reference/21.png)

<span data-ttu-id="79e84-271">This setting applies to the following client apps:</span><span class="sxs-lookup"><span data-stu-id="79e84-271">This setting applies to the following client apps:</span></span>


- <span data-ttu-id="79e84-272">Microsoft Intune Managed Browser</span><span class="sxs-lookup"><span data-stu-id="79e84-272">Microsoft Intune Managed Browser</span></span>
- <span data-ttu-id="79e84-273">Microsoft PowerBI</span><span class="sxs-lookup"><span data-stu-id="79e84-273">Microsoft PowerBI</span></span>
- <span data-ttu-id="79e84-274">Microsoft Invoicing</span><span class="sxs-lookup"><span data-stu-id="79e84-274">Microsoft Invoicing</span></span>
- <span data-ttu-id="79e84-275">Microsoft Launcher</span><span class="sxs-lookup"><span data-stu-id="79e84-275">Microsoft Launcher</span></span>
- <span data-ttu-id="79e84-276">Microsoft Azure Information Protection</span><span class="sxs-lookup"><span data-stu-id="79e84-276">Microsoft Azure Information Protection</span></span>
- <span data-ttu-id="79e84-277">Microsoft Excel</span><span class="sxs-lookup"><span data-stu-id="79e84-277">Microsoft Excel</span></span>
- <span data-ttu-id="79e84-278">Microsoft Kaizala</span><span class="sxs-lookup"><span data-stu-id="79e84-278">Microsoft Kaizala</span></span> 
- <span data-ttu-id="79e84-279">Microsoft OneDrive</span><span class="sxs-lookup"><span data-stu-id="79e84-279">Microsoft OneDrive</span></span>
- <span data-ttu-id="79e84-280">Microsoft OneNote</span><span class="sxs-lookup"><span data-stu-id="79e84-280">Microsoft OneNote</span></span>
- <span data-ttu-id="79e84-281">Microsoft Outlook</span><span class="sxs-lookup"><span data-stu-id="79e84-281">Microsoft Outlook</span></span>
- <span data-ttu-id="79e84-282">Microsoft Planner</span><span class="sxs-lookup"><span data-stu-id="79e84-282">Microsoft Planner</span></span>
- <span data-ttu-id="79e84-283">Microsoft PowerPoint</span><span class="sxs-lookup"><span data-stu-id="79e84-283">Microsoft PowerPoint</span></span>
- <span data-ttu-id="79e84-284">Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="79e84-284">Microsoft SharePoint</span></span>
- <span data-ttu-id="79e84-285">Microsoft Skype for Business</span><span class="sxs-lookup"><span data-stu-id="79e84-285">Microsoft Skype for Business</span></span>
- <span data-ttu-id="79e84-286">Microsoft StaffHub</span><span class="sxs-lookup"><span data-stu-id="79e84-286">Microsoft StaffHub</span></span>
- <span data-ttu-id="79e84-287">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="79e84-287">Microsoft Teams</span></span>
- <span data-ttu-id="79e84-288">Microsoft Visio</span><span class="sxs-lookup"><span data-stu-id="79e84-288">Microsoft Visio</span></span>
- <span data-ttu-id="79e84-289">Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="79e84-289">Microsoft Word</span></span>



<span data-ttu-id="79e84-290">**Remarks**</span><span class="sxs-lookup"><span data-stu-id="79e84-290">**Remarks**</span></span>

- <span data-ttu-id="79e84-291">The approved client apps support the Intune mobile application management feature.</span><span class="sxs-lookup"><span data-stu-id="79e84-291">The approved client apps support the Intune mobile application management feature.</span></span>

- <span data-ttu-id="79e84-292">The **Require approved client app** requirement:</span><span class="sxs-lookup"><span data-stu-id="79e84-292">The **Require approved client app** requirement:</span></span>

    - <span data-ttu-id="79e84-293">Only supports the iOS and Android for [device platform condition](#device-platforms-condition).</span><span class="sxs-lookup"><span data-stu-id="79e84-293">Only supports the iOS and Android for [device platform condition](#device-platforms-condition).</span></span>


## <a name="next-steps"></a><span data-ttu-id="79e84-294">Next steps</span><span class="sxs-lookup"><span data-stu-id="79e84-294">Next steps</span></span>

- <span data-ttu-id="79e84-295">For an overview of conditional access, see [What is conditional access in Azure Active Directory?](../active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="79e84-295">For an overview of conditional access, see [What is conditional access in Azure Active Directory?](../active-directory-conditional-access-azure-portal.md)</span></span>
- <span data-ttu-id="79e84-296">If you are ready to configure conditional access policies in your environment, see the [recommended practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="79e84-296">If you are ready to configure conditional access policies in your environment, see the [recommended practices for conditional access in Azure Active Directory](best-practices.md).</span></span>



<!--Image references-->
[1]: ./media/technical-reference/01.png


