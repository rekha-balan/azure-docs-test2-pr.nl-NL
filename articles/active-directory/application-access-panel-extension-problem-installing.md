---
title: Problem installing the application access panel browser extension | Microsoft Docs
description: How to fix common errors encountered when installing the access panel browser extension
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
ms.openlocfilehash: 40ace51c4ba74039b3a5d5997acdf2da7b98b4a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669434"
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="72f6b-103">Problem installing the application access panel browser extension</span><span class="sxs-lookup"><span data-stu-id="72f6b-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="72f6b-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="72f6b-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="72f6b-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="72f6b-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="72f6b-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="72f6b-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="72f6b-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span><span class="sxs-lookup"><span data-stu-id="72f6b-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="72f6b-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="72f6b-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="72f6b-109">Meeting browser requirements for the Access Panel</span><span class="sxs-lookup"><span data-stu-id="72f6b-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="72f6b-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span><span class="sxs-lookup"><span data-stu-id="72f6b-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="72f6b-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span><span class="sxs-lookup"><span data-stu-id="72f6b-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="72f6b-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="72f6b-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="72f6b-113">For password-based SSO, the end user’s browsers can be:</span><span class="sxs-lookup"><span data-stu-id="72f6b-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="72f6b-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span><span class="sxs-lookup"><span data-stu-id="72f6b-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="72f6b-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span><span class="sxs-lookup"><span data-stu-id="72f6b-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="72f6b-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span><span class="sxs-lookup"><span data-stu-id="72f6b-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

<span data-ttu-id="72f6b-117">**Note**: The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span><span class="sxs-lookup"><span data-stu-id="72f6b-117">**Note**: The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="72f6b-118">How to install the Access Panel Browser extension</span><span class="sxs-lookup"><span data-stu-id="72f6b-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="72f6b-119">To install the Access Panel Browser extension, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="72f6b-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="72f6b-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72f6b-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="72f6b-121">click a **password-SSO application** in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="72f6b-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="72f6b-122">In the prompt asking to install the software, select **Install Now**.</span><span class="sxs-lookup"><span data-stu-id="72f6b-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="72f6b-123">Based on your browser you be directed to the download link.</span><span class="sxs-lookup"><span data-stu-id="72f6b-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="72f6b-124">**Add** the extension to your browser.</span><span class="sxs-lookup"><span data-stu-id="72f6b-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="72f6b-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span><span class="sxs-lookup"><span data-stu-id="72f6b-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="72f6b-126">Once installed, **restart** your browser session.</span><span class="sxs-lookup"><span data-stu-id="72f6b-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="72f6b-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span><span class="sxs-lookup"><span data-stu-id="72f6b-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="72f6b-128">You may also download the extension for Chrome and Firefox from the direct links below:</span><span class="sxs-lookup"><span data-stu-id="72f6b-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="72f6b-129">Chrome Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="72f6b-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="72f6b-130">Firefox Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="72f6b-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="72f6b-131">Setting up a group policy for Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="72f6b-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="72f6b-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span><span class="sxs-lookup"><span data-stu-id="72f6b-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="72f6b-133">The prerequisites include:</span><span class="sxs-lookup"><span data-stu-id="72f6b-133">The prerequisites include:</span></span>

-   <span data-ttu-id="72f6b-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span><span class="sxs-lookup"><span data-stu-id="72f6b-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="72f6b-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span><span class="sxs-lookup"><span data-stu-id="72f6b-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="72f6b-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="72f6b-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="72f6b-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="72f6b-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="72f6b-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span><span class="sxs-lookup"><span data-stu-id="72f6b-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="72f6b-139">Troubleshoot the Access Panel in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="72f6b-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="72f6b-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span><span class="sxs-lookup"><span data-stu-id="72f6b-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="72f6b-141">If these troubleshooting steps do not resolve the issue</span><span class="sxs-lookup"><span data-stu-id="72f6b-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="72f6b-142">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="72f6b-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="72f6b-143">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="72f6b-143">Correlation error ID</span></span>

-   <span data-ttu-id="72f6b-144">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="72f6b-144">UPN (user email address)</span></span>

-   <span data-ttu-id="72f6b-145">TenantID</span><span class="sxs-lookup"><span data-stu-id="72f6b-145">TenantID</span></span>

-   <span data-ttu-id="72f6b-146">Browser type</span><span class="sxs-lookup"><span data-stu-id="72f6b-146">Browser type</span></span>

-   <span data-ttu-id="72f6b-147">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="72f6b-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="72f6b-148">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="72f6b-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="72f6b-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="72f6b-149">Next steps</span></span>
[<span data-ttu-id="72f6b-150">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72f6b-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
