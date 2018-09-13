---
title: Unexpected application in my applications list | Microsoft Docs
description: How to see all applications in your tenant and understand how applications appear in your All Applications list under Enterprise Applications
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: 754a06cc8bb9cc6e660e2ac5f01ef2c40176eb05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965705"
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="220e6-103">Unexpected application in my applications list</span><span class="sxs-lookup"><span data-stu-id="220e6-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="220e6-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span><span class="sxs-lookup"><span data-stu-id="220e6-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="220e6-105">How to see all applications in your tenant</span><span class="sxs-lookup"><span data-stu-id="220e6-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="220e6-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span><span class="sxs-lookup"><span data-stu-id="220e6-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="220e6-107">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="220e6-107">Follow these steps:</span></span>

1.  <span data-ttu-id="220e6-108">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="220e6-108">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="220e6-109">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="220e6-109">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="220e6-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="220e6-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="220e6-111">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="220e6-111">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="220e6-112">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="220e6-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="220e6-113">click the use the **Filter** control at the top of the **All Applications List**.</span><span class="sxs-lookup"><span data-stu-id="220e6-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="220e6-114">On the **Filter** pane, set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="220e6-114">On the **Filter** pane, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="220e6-115">Why does a specific application appear in my all applications list?</span><span class="sxs-lookup"><span data-stu-id="220e6-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="220e6-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span><span class="sxs-lookup"><span data-stu-id="220e6-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="220e6-117">Service Principal objects can appear in this list in a various ways:</span><span class="sxs-lookup"><span data-stu-id="220e6-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="220e6-118">When you add any application from the application gallery, including:</span><span class="sxs-lookup"><span data-stu-id="220e6-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="220e6-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD</span><span class="sxs-lookup"><span data-stu-id="220e6-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD</span></span>

   2. <span data-ttu-id="220e6-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally</span><span class="sxs-lookup"><span data-stu-id="220e6-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally</span></span>

   3. <span data-ttu-id="220e6-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet</span><span class="sxs-lookup"><span data-stu-id="220e6-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet</span></span>

   4. <span data-ttu-id="220e6-122">**Non-Gallery Applications** – Bring your own applications!</span><span class="sxs-lookup"><span data-stu-id="220e6-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="220e6-123">Any web link you want, or any application that renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM that you wish to integrate for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="220e6-123">Any web link you want, or any application that renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM that you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="220e6-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="220e6-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="220e6-125">One example is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="220e6-125">One example is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="220e6-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="220e6-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

4.  <span data-ttu-id="220e6-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)</span><span class="sxs-lookup"><span data-stu-id="220e6-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)</span></span>

5.  <span data-ttu-id="220e6-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)</span><span class="sxs-lookup"><span data-stu-id="220e6-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)</span></span>

6.  <span data-ttu-id="220e6-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)</span><span class="sxs-lookup"><span data-stu-id="220e6-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)</span></span>

7.  <span data-ttu-id="220e6-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0)</span><span class="sxs-lookup"><span data-stu-id="220e6-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0)</span></span>

8.  <span data-ttu-id="220e6-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant</span><span class="sxs-lookup"><span data-stu-id="220e6-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant</span></span>

9.  <span data-ttu-id="220e6-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant</span><span class="sxs-lookup"><span data-stu-id="220e6-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant</span></span>

10. <span data-ttu-id="220e6-133">When you enable certain services that store data in your tenant.</span><span class="sxs-lookup"><span data-stu-id="220e6-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="220e6-134">One example is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span><span class="sxs-lookup"><span data-stu-id="220e6-134">One example is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="220e6-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="220e6-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="220e6-136">I want to remove a specific user’s or group’s assignment to an application</span><span class="sxs-lookup"><span data-stu-id="220e6-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="220e6-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="220e6-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="220e6-138">I want to disable all access to an application for every user</span><span class="sxs-lookup"><span data-stu-id="220e6-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="220e6-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="220e6-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="220e6-140">I want to delete an application entirely</span><span class="sxs-lookup"><span data-stu-id="220e6-140">I want to delete an application entirely</span></span>

<span data-ttu-id="220e6-141">To **delete an application**, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="220e6-141">To **delete an application**, follow these steps:</span></span>

1.  <span data-ttu-id="220e6-142">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="220e6-142">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="220e6-143">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="220e6-143">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="220e6-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="220e6-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="220e6-145">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="220e6-145">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="220e6-146">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="220e6-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="220e6-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="220e6-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="220e6-148">Select the application you want to delete.</span><span class="sxs-lookup"><span data-stu-id="220e6-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="220e6-149">Once the application loads, click **Delete** icon from the top application’s **Overview** pane.</span><span class="sxs-lookup"><span data-stu-id="220e6-149">Once the application loads, click **Delete** icon from the top application’s **Overview** pane.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="220e6-150">I want to disable all future user consent operations to any application</span><span class="sxs-lookup"><span data-stu-id="220e6-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="220e6-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span><span class="sxs-lookup"><span data-stu-id="220e6-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="220e6-152">Administrators can still consent on user’s behalves.</span><span class="sxs-lookup"><span data-stu-id="220e6-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="220e6-153">To learn more about application consent, and why you may or may not want to consent, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="220e6-153">To learn more about application consent, and why you may or may not want to consent, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="220e6-154">To **disable all future user consent operations in your entire directory**, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="220e6-154">To **disable all future user consent operations in your entire directory**, follow these steps:</span></span>

1.  <span data-ttu-id="220e6-155">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="220e6-155">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="220e6-156">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="220e6-156">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="220e6-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="220e6-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="220e6-158">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="220e6-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="220e6-159">click **User settings**.</span><span class="sxs-lookup"><span data-stu-id="220e6-159">click **User settings**.</span></span>

6.  <span data-ttu-id="220e6-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="220e6-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="220e6-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="220e6-161">Next steps</span></span>
[<span data-ttu-id="220e6-162">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="220e6-162">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
