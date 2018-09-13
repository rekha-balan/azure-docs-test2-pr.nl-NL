---
title: Unexpected application in my applications list | Microsoft Docs
description: How to see all applications in your tenant and understand how applications appear in your All Applications list under Enterprise Applications
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 569a8db4266182122e9da175840484473e9106e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670458"
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="58f82-103">Unexpected application in my applications list</span><span class="sxs-lookup"><span data-stu-id="58f82-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="58f82-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span><span class="sxs-lookup"><span data-stu-id="58f82-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="58f82-105">How to see all applications in your tenant</span><span class="sxs-lookup"><span data-stu-id="58f82-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="58f82-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span><span class="sxs-lookup"><span data-stu-id="58f82-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="58f82-107">To do this, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="58f82-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="58f82-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="58f82-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="58f82-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="58f82-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="58f82-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="58f82-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="58f82-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="58f82-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="58f82-112">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="58f82-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="58f82-113">click the use the **Filter** control at the top of the **All Applications List**.</span><span class="sxs-lookup"><span data-stu-id="58f82-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="58f82-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="58f82-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="58f82-115">Why does a specific application appear in my all applications list?</span><span class="sxs-lookup"><span data-stu-id="58f82-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="58f82-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span><span class="sxs-lookup"><span data-stu-id="58f82-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="58f82-117">Service Principal objects can appear in this list in a various ways:</span><span class="sxs-lookup"><span data-stu-id="58f82-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="58f82-118">When you add any application from the application gallery, including:</span><span class="sxs-lookup"><span data-stu-id="58f82-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="58f82-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58f82-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="58f82-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span><span class="sxs-lookup"><span data-stu-id="58f82-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="58f82-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span><span class="sxs-lookup"><span data-stu-id="58f82-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="58f82-122">**Non-Gallery Applications** – Bring your own applications!</span><span class="sxs-lookup"><span data-stu-id="58f82-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="58f82-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58f82-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="58f82-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58f82-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="58f82-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="58f82-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="58f82-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="58f82-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="58f82-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="58f82-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="58f82-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="58f82-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="58f82-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span><span class="sxs-lookup"><span data-stu-id="58f82-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="58f82-130">When you create a service principal object using the [Azure AD PowerShell Module](https://docs.microsoft.com/powershell/azuread/v2/azureactivedirectory).</span><span class="sxs-lookup"><span data-stu-id="58f82-130">When you create a service principal object using the [Azure AD PowerShell Module](https://docs.microsoft.com/powershell/azuread/v2/azureactivedirectory).</span></span>

8.  <span data-ttu-id="58f82-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span><span class="sxs-lookup"><span data-stu-id="58f82-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="58f82-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span><span class="sxs-lookup"><span data-stu-id="58f82-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="58f82-133">When you enable certain services that store data in your tenant.</span><span class="sxs-lookup"><span data-stu-id="58f82-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="58f82-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span><span class="sxs-lookup"><span data-stu-id="58f82-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="58f82-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="58f82-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="58f82-136">I want to remove a specific user’s or group’s assignment to an application</span><span class="sxs-lookup"><span data-stu-id="58f82-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="58f82-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="58f82-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="58f82-138">I want to disable all access to an application for every user</span><span class="sxs-lookup"><span data-stu-id="58f82-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="58f82-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span><span class="sxs-lookup"><span data-stu-id="58f82-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="58f82-140">I want to delete an application entirely</span><span class="sxs-lookup"><span data-stu-id="58f82-140">I want to delete an application entirely</span></span>

<span data-ttu-id="58f82-141">To **delete an application**, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="58f82-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="58f82-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="58f82-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="58f82-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="58f82-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="58f82-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="58f82-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="58f82-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="58f82-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="58f82-146">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="58f82-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="58f82-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="58f82-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="58f82-148">Select the application you want to delete.</span><span class="sxs-lookup"><span data-stu-id="58f82-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="58f82-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span><span class="sxs-lookup"><span data-stu-id="58f82-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="58f82-150">I want to disable all future user consent operations to any application</span><span class="sxs-lookup"><span data-stu-id="58f82-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="58f82-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span><span class="sxs-lookup"><span data-stu-id="58f82-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="58f82-152">Administrators can still consent on user’s behalves.</span><span class="sxs-lookup"><span data-stu-id="58f82-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="58f82-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="58f82-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="58f82-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span><span class="sxs-lookup"><span data-stu-id="58f82-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="58f82-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="58f82-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="58f82-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="58f82-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="58f82-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="58f82-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="58f82-158">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="58f82-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="58f82-159">click **User settings**.</span><span class="sxs-lookup"><span data-stu-id="58f82-159">click **User settings**.</span></span>

6.  <span data-ttu-id="58f82-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="58f82-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58f82-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="58f82-161">Next steps</span></span>
[<span data-ttu-id="58f82-162">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58f82-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
