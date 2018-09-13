---
title: You can't get there from here on the Azure portal from a Windows device| Microsoft Docs
description: Learn where you can't get there from here comes from and what you could check to avoid running into this dialog.
services: active-directory
keywords: device-based conditional access, device registration, enable device registration, device registration and MDM
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: markvi
ms.openlocfilehash: da22bc938e468d7be95e8afd26309973104fde8a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551478"
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="63ff0-104">You can't get there from here on a Windows device</span><span class="sxs-lookup"><span data-stu-id="63ff0-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="63ff0-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span><span class="sxs-lookup"><span data-stu-id="63ff0-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="63ff0-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span><span class="sxs-lookup"><span data-stu-id="63ff0-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access to your organization's resources under certain conditions.</span></span> <span data-ttu-id="63ff0-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span><span class="sxs-lookup"><span data-stu-id="63ff0-107">While it might be necessary to contact helpdesk or your administrator to get this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="63ff0-108">If you are using a **Windows** device, you should check the following:</span><span class="sxs-lookup"><span data-stu-id="63ff0-108">If you are using a **Windows** device, you should check the following:</span></span>

- <span data-ttu-id="63ff0-109">Are you using a supported browser?</span><span class="sxs-lookup"><span data-stu-id="63ff0-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="63ff0-110">Are you running a supported version of Windows on your device?</span><span class="sxs-lookup"><span data-stu-id="63ff0-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="63ff0-111">Is your device compliant?</span><span class="sxs-lookup"><span data-stu-id="63ff0-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="63ff0-112">Supported browser</span><span class="sxs-lookup"><span data-stu-id="63ff0-112">Supported browser</span></span>

<span data-ttu-id="63ff0-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span><span class="sxs-lookup"><span data-stu-id="63ff0-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="63ff0-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span><span class="sxs-lookup"><span data-stu-id="63ff0-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="63ff0-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span><span class="sxs-lookup"><span data-stu-id="63ff0-115">You can easily identify whether you can't access a resource due to an unsupported browser by looking at the details section of the error page:</span></span>

<span data-ttu-id="63ff0-116">!["You can't get there from here" message for unsupported browsers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="63ff0-116">!["You can't get there from here" message for unsupported browsers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="63ff0-117">The only remediation is to use a browser that the application supports for your device platform.</span><span class="sxs-lookup"><span data-stu-id="63ff0-117">The only remediation is to use a browser that the application supports for your device platform.</span></span> <span data-ttu-id="63ff0-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers).</span><span class="sxs-lookup"><span data-stu-id="63ff0-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="63ff0-119">Supported versions of Windows</span><span class="sxs-lookup"><span data-stu-id="63ff0-119">Supported versions of Windows</span></span>

<span data-ttu-id="63ff0-120">The following must be true about the Windows operating system on your device:</span><span class="sxs-lookup"><span data-stu-id="63ff0-120">The following must be true about the Windows operating system on your device:</span></span> 

- <span data-ttu-id="63ff0-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span><span class="sxs-lookup"><span data-stu-id="63ff0-121">If you are running a Windows desktop operating system on your device, it needs to be Windows 7 or later.</span></span>
- <span data-ttu-id="63ff0-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="63ff0-122">If you are running a Windows server operating system on your device, it needs to be Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="63ff0-123">Compliant device</span><span class="sxs-lookup"><span data-stu-id="63ff0-123">Compliant device</span></span>

<span data-ttu-id="63ff0-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span><span class="sxs-lookup"><span data-stu-id="63ff0-124">Your administrator might have configured a conditional access policy that allows access to your organization's resources only from compliant devices.</span></span> <span data-ttu-id="63ff0-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="63ff0-125">To be compliant, your device must be either joined to your on-premises Active Directory or joined to your Azure Active Directory.</span></span>

<span data-ttu-id="63ff0-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span><span class="sxs-lookup"><span data-stu-id="63ff0-126">You can easily identify whether you can't access a resource due to a device that is not compliant by looking at the details section of the error page:</span></span>
 
<span data-ttu-id="63ff0-127">!["You can't get there from here" messages for unregistered devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="63ff0-127">!["You can't get there from here" messages for unregistered devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="63ff0-128">Is your device joined to an on-premises Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63ff0-128">Is your device joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="63ff0-129">**If your device is joined to an on-premises Active Directory in your organization:**</span><span class="sxs-lookup"><span data-stu-id="63ff0-129">**If your device is joined to an on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="63ff0-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span><span class="sxs-lookup"><span data-stu-id="63ff0-130">Make sure that you sign in to Windows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="63ff0-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="63ff0-131">Connect to your corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="63ff0-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span><span class="sxs-lookup"><span data-stu-id="63ff0-132">After you are connected, press the Windows logo key + the L key to lock your Windows session.</span></span>
4. <span data-ttu-id="63ff0-133">Unlock your Windows session by entering your work account credentials.</span><span class="sxs-lookup"><span data-stu-id="63ff0-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="63ff0-134">Wait for a minute, and then try again to access the application or service.</span><span class="sxs-lookup"><span data-stu-id="63ff0-134">Wait for a minute, and then try again to access the application or service.</span></span>
6. <span data-ttu-id="63ff0-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span><span class="sxs-lookup"><span data-stu-id="63ff0-135">If you see the same page, click the **More details** link, and then contact your administrator with the details.</span></span>


### <a name="is-your-device-not-joined-to-an-on-premises-active-directory"></a><span data-ttu-id="63ff0-136">Is your device not joined to an on-premises Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63ff0-136">Is your device not joined to an on-premises Active Directory?</span></span>

<span data-ttu-id="63ff0-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span><span class="sxs-lookup"><span data-stu-id="63ff0-137">If your device is not joined to an on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="63ff0-138">Run Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="63ff0-138">Run Azure AD Join</span></span>
* <span data-ttu-id="63ff0-139">Add your work or school account to Windows</span><span class="sxs-lookup"><span data-stu-id="63ff0-139">Add your work or school account to Windows</span></span>

<span data-ttu-id="63ff0-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="63ff0-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="63ff0-141">If your device:</span><span class="sxs-lookup"><span data-stu-id="63ff0-141">If your device:</span></span>

- <span data-ttu-id="63ff0-142">Belongs to your organization, you should run Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="63ff0-142">Belongs to your organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="63ff0-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span><span class="sxs-lookup"><span data-stu-id="63ff0-143">Is a personal device or a Windows phone, you should add your work or school account to Windows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="63ff0-144">Azure AD Join on Windows 10</span><span class="sxs-lookup"><span data-stu-id="63ff0-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="63ff0-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span><span class="sxs-lookup"><span data-stu-id="63ff0-145">The steps to join your device to Azure AD are tied the version of Windows 10 you are running on it.</span></span> <span data-ttu-id="63ff0-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span><span class="sxs-lookup"><span data-stu-id="63ff0-146">To determine the version of your Windows 10 operating system, run the **winver** command:</span></span> 

![Windows version](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="63ff0-148">**Windows 10 Anniversary Update (Version 1607):**</span><span class="sxs-lookup"><span data-stu-id="63ff0-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="63ff0-149">Open the **Settings** app.</span><span class="sxs-lookup"><span data-stu-id="63ff0-149">Open the **Settings** app.</span></span>
2. <span data-ttu-id="63ff0-150">Click **Accounts** > **Access work or school**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="63ff0-151">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-151">Click **Connect**.</span></span>
4. <span data-ttu-id="63ff0-152">Click **Join this device to Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-152">Click **Join this device to Azure AD**.</span></span>
5. <span data-ttu-id="63ff0-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span><span class="sxs-lookup"><span data-stu-id="63ff0-153">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
6. <span data-ttu-id="63ff0-154">Sign out, and then sign in with your work account.</span><span class="sxs-lookup"><span data-stu-id="63ff0-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="63ff0-155">Try again to access the application.</span><span class="sxs-lookup"><span data-stu-id="63ff0-155">Try again to access the application.</span></span>

<span data-ttu-id="63ff0-156">**Windows 10 November 2015 Update (Version 1511):**</span><span class="sxs-lookup"><span data-stu-id="63ff0-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="63ff0-157">Open the **Settings** app.</span><span class="sxs-lookup"><span data-stu-id="63ff0-157">Open the **Settings** app.</span></span>
2. <span data-ttu-id="63ff0-158">Click **System** > **About**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="63ff0-159">Click **Join Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="63ff0-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span><span class="sxs-lookup"><span data-stu-id="63ff0-160">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="63ff0-161">Sign out, and then sign in with your work account (your Azure AD account).</span><span class="sxs-lookup"><span data-stu-id="63ff0-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="63ff0-162">Try again to access the application.</span><span class="sxs-lookup"><span data-stu-id="63ff0-162">Try again to access the application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="63ff0-163">Workplace Join on Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="63ff0-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="63ff0-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="63ff0-164">If your device is not domain-joined and runs Windows 8.1, to do a Workplace Join and enroll in Microsoft Intune, do the following steps:</span></span>

1. <span data-ttu-id="63ff0-165">Open **PC Settings**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="63ff0-166">Click **Network** > **Workplace**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="63ff0-167">Click **Join**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-167">Click **Join**.</span></span>
4. <span data-ttu-id="63ff0-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span><span class="sxs-lookup"><span data-stu-id="63ff0-168">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="63ff0-169">Click **Turn on**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="63ff0-170">Try again to access the application.</span><span class="sxs-lookup"><span data-stu-id="63ff0-170">Try again to access the application.</span></span>



#### <a name="add-your-work-or-school-account-to-windows"></a><span data-ttu-id="63ff0-171">Add your work or school account to Windows</span><span class="sxs-lookup"><span data-stu-id="63ff0-171">Add your work or school account to Windows</span></span> 


<span data-ttu-id="63ff0-172">**Windows 10 Anniversary Update (Version 1607):**</span><span class="sxs-lookup"><span data-stu-id="63ff0-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="63ff0-173">Open the **Settings** app.</span><span class="sxs-lookup"><span data-stu-id="63ff0-173">Open the **Settings** app.</span></span>
2. <span data-ttu-id="63ff0-174">Click **Accounts** > **Access work or school**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="63ff0-175">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-175">Click **Connect**.</span></span>
4. <span data-ttu-id="63ff0-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span><span class="sxs-lookup"><span data-stu-id="63ff0-176">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="63ff0-177">Try again to access the application.</span><span class="sxs-lookup"><span data-stu-id="63ff0-177">Try again to access the application.</span></span>


<span data-ttu-id="63ff0-178">**Windows 10 November 2015 Update (Version 1511):**</span><span class="sxs-lookup"><span data-stu-id="63ff0-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="63ff0-179">Open the **Settings** app.</span><span class="sxs-lookup"><span data-stu-id="63ff0-179">Open the **Settings** app.</span></span>
2. <span data-ttu-id="63ff0-180">Click **Accounts** > **Your accounts**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="63ff0-181">Click **Add work or school account**.</span><span class="sxs-lookup"><span data-stu-id="63ff0-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="63ff0-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span><span class="sxs-lookup"><span data-stu-id="63ff0-182">Authenticate to your organization, provide multi-factor authentication if prompted, and then follow the steps that are shown.</span></span>
5. <span data-ttu-id="63ff0-183">Try again to access the application.</span><span class="sxs-lookup"><span data-stu-id="63ff0-183">Try again to access the application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="63ff0-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="63ff0-184">Next steps</span></span>
[<span data-ttu-id="63ff0-185">Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="63ff0-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)




