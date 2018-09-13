---
title: Set a custom home page for published apps by using Azure AD Application Proxy | Microsoft Docs
description: Covers the basics about Azure AD Application Proxy connectors
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: kgremban
ms.openlocfilehash: 28f100276511c1ae978466870ff48f885dd53c28
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670303"
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="714d7-103">Set a custom home page for published apps by using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="714d7-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="714d7-104">This article discusses how to configure apps to direct users to a custom home page when they access the apps from the Azure Active Directory (Azure AD) Access Panel and the Office 365 app launcher.</span><span class="sxs-lookup"><span data-stu-id="714d7-104">This article discusses how to configure apps to direct users to a custom home page when they access the apps from the Azure Active Directory (Azure AD) Access Panel and the Office 365 app launcher.</span></span>

>[!NOTE]
><span data-ttu-id="714d7-105">The Application Proxy feature is available only if you upgraded to the Premium or Basic edition of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="714d7-105">The Application Proxy feature is available only if you upgraded to the Premium or Basic edition of Azure Active Directory.</span></span> <span data-ttu-id="714d7-106">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="714d7-106">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

<span data-ttu-id="714d7-107">By using the Azure AD PowerShell module, you can define custom home-page URLs for instances when you want app users to land on a specific page within the app (for example, *https://expenseApp-contoso.msappproxy.net/login/login.aspx*).</span><span class="sxs-lookup"><span data-stu-id="714d7-107">By using the Azure AD PowerShell module, you can define custom home-page URLs for instances when you want app users to land on a specific page within the app (for example, *https://expenseApp-contoso.msappproxy.net/login/login.aspx*).</span></span>

>[!NOTE]
><span data-ttu-id="714d7-108">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="714d7-108">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

<span data-ttu-id="714d7-109">When users launch the app, they're directed by default to the root domain URL for the published app.</span><span class="sxs-lookup"><span data-stu-id="714d7-109">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="714d7-110">The landing page is typically set as the home-page URL.</span><span class="sxs-lookup"><span data-stu-id="714d7-110">The landing page is typically set as the home-page URL.</span></span> <span data-ttu-id="714d7-111">For example, for the back-end app http://ExpenseApp, the URL is published as *https://expenseApp-contoso.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="714d7-111">For example, for the back-end app http://ExpenseApp, the URL is published as *https://expenseApp-contoso.msappproxy.net*.</span></span> <span data-ttu-id="714d7-112">By default, the home-page URL is set as *https://expenseApp-contoso.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="714d7-112">By default, the home-page URL is set as *https://expenseApp-contoso.msappproxy.net*.</span></span>

## <a name="determine-the-home-page-url"></a><span data-ttu-id="714d7-113">Determine the home-page URL</span><span class="sxs-lookup"><span data-stu-id="714d7-113">Determine the home-page URL</span></span>

<span data-ttu-id="714d7-114">Before you set the home-page URL, keep in mind the following:</span><span class="sxs-lookup"><span data-stu-id="714d7-114">Before you set the home-page URL, keep in mind the following:</span></span>

* <span data-ttu-id="714d7-115">Ensure that the path you specify is a subdomain path of the root domain URL.</span><span class="sxs-lookup"><span data-stu-id="714d7-115">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

 <span data-ttu-id="714d7-116">For example, if the published app is accessible from a root-domain URL (for example, https://intranet-contoso.msappproxy.net/), the home-page URL that you configure must start with https://intranet-contoso.msappproxy.net/.</span><span class="sxs-lookup"><span data-stu-id="714d7-116">For example, if the published app is accessible from a root-domain URL (for example, https://intranet-contoso.msappproxy.net/), the home-page URL that you configure must start with https://intranet-contoso.msappproxy.net/.</span></span>

* <span data-ttu-id="714d7-117">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home-page URL that you configure must start with https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="714d7-117">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home-page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="714d7-118">If you make a change to the published app, the change might reset the value of the home-page URL.</span><span class="sxs-lookup"><span data-stu-id="714d7-118">If you make a change to the published app, the change might reset the value of the home-page URL.</span></span> <span data-ttu-id="714d7-119">Therefore, when you decide to update the app, you should recheck and, if necessary, update the home-page URL.</span><span class="sxs-lookup"><span data-stu-id="714d7-119">Therefore, when you decide to update the app, you should recheck and, if necessary, update the home-page URL.</span></span>

<span data-ttu-id="714d7-120">In the next section, you walk through setting up a custom home-page URL for the published app.</span><span class="sxs-lookup"><span data-stu-id="714d7-120">In the next section, you walk through setting up a custom home-page URL for the published app.</span></span> 

## <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="714d7-121">Install the Azure AD PowerShell module</span><span class="sxs-lookup"><span data-stu-id="714d7-121">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="714d7-122">Before you define a custom home-page URL by using PowerShell, install a nonstandard package of the Azure AD PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="714d7-122">Before you define a custom home-page URL by using PowerShell, install a nonstandard package of the Azure AD PowerShell module.</span></span> <span data-ttu-id="714d7-123">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/1.1.23.0), which uses the Graph API endpoint.</span><span class="sxs-lookup"><span data-stu-id="714d7-123">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/1.1.23.0), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="714d7-124">To install the package by using PowerShell, do the following:</span><span class="sxs-lookup"><span data-stu-id="714d7-124">To install the package by using PowerShell, do the following:</span></span>

1. <span data-ttu-id="714d7-125">Open a standard PowerShell window, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="714d7-125">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD -RequiredVersion 1.1.23.0
    ```
    <span data-ttu-id="714d7-126">If you're running the command as a non-admin, use the **-scope currentuser** option.</span><span class="sxs-lookup"><span data-stu-id="714d7-126">If you're running the command as a non-admin, use the **-scope currentuser** option.</span></span>
2. <span data-ttu-id="714d7-127">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span><span class="sxs-lookup"><span data-stu-id="714d7-127">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

## <a name="set-a-custom-home-page-url-by-using-the-azure-ad-powershell-module"></a><span data-ttu-id="714d7-128">Set a custom home-page URL by using the Azure AD PowerShell module</span><span class="sxs-lookup"><span data-stu-id="714d7-128">Set a custom home-page URL by using the Azure AD PowerShell module</span></span>

<span data-ttu-id="714d7-129">Now that you've installed the Azure AD PowerShell module, you're ready to set the home-page URL.</span><span class="sxs-lookup"><span data-stu-id="714d7-129">Now that you've installed the Azure AD PowerShell module, you're ready to set the home-page URL.</span></span> <span data-ttu-id="714d7-130">To do so, follow the instructions in the next two sections.</span><span class="sxs-lookup"><span data-stu-id="714d7-130">To do so, follow the instructions in the next two sections.</span></span>

### <a name="step-1-find-the-objectid-of-the-app"></a><span data-ttu-id="714d7-131">Step 1: Find the ObjectID of the app</span><span class="sxs-lookup"><span data-stu-id="714d7-131">Step 1: Find the ObjectID of the app</span></span>

<span data-ttu-id="714d7-132">Obtain the ObjectID of the app, and then search for the app by its home page.</span><span class="sxs-lookup"><span data-stu-id="714d7-132">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="714d7-133">Open PowerShell, and then import the Azure AD module by using the following command:</span><span class="sxs-lookup"><span data-stu-id="714d7-133">Open PowerShell, and then import the Azure AD module by using the following command:</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="714d7-134">Sign in to the Azure AD module by using the following cmdlet, and then follow the instructions on the screen.</span><span class="sxs-lookup"><span data-stu-id="714d7-134">Sign in to the Azure AD module by using the following cmdlet, and then follow the instructions on the screen.</span></span> <span data-ttu-id="714d7-135">Be sure to sign in as the tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="714d7-135">Be sure to sign in as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="714d7-136">Use this cmdlet to find the app based on the home page that contains *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="714d7-136">Use this cmdlet to find the app based on the home page that contains *sharepoint-iddemo*.</span></span> <span data-ttu-id="714d7-137">To edit the app, replace the following value with the value that works for the app.</span><span class="sxs-lookup"><span data-stu-id="714d7-137">To edit the app, replace the following value with the value that works for the app.</span></span>

    ```
    Get-AzureADApplications | where { $_.Homepage -like “*sharepoint-iddemo*” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="714d7-138">You should get a result that's similar to the one shown here.</span><span class="sxs-lookup"><span data-stu-id="714d7-138">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="714d7-139">Copy the GUID (ObjectID) so that you can use it in "Step 2: Update the home-page URL."</span><span class="sxs-lookup"><span data-stu-id="714d7-139">Copy the GUID (ObjectID) so that you can use it in "Step 2: Update the home-page URL."</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="step-2-update-the-home-page-url"></a><span data-ttu-id="714d7-140">Step 2: Update the home-page URL</span><span class="sxs-lookup"><span data-stu-id="714d7-140">Step 2: Update the home-page URL</span></span>

<span data-ttu-id="714d7-141">In the same PowerShell module that you used in "Step 1: Find the ObjectID of the app," do the following:</span><span class="sxs-lookup"><span data-stu-id="714d7-141">In the same PowerShell module that you used in "Step 1: Find the ObjectID of the app," do the following:</span></span>

1. <span data-ttu-id="714d7-142">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the GUID (ObjectID) that you copied in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="714d7-142">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the GUID (ObjectID) that you copied in the preceding step.</span></span>

    ```
    Get-AzureADApplication -AppObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="714d7-143">Now that you've confirmed the app, you're ready to update the home page, as follows.</span><span class="sxs-lookup"><span data-stu-id="714d7-143">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="714d7-144">Create a blank application object to hold the changes that you want to make.</span><span class="sxs-lookup"><span data-stu-id="714d7-144">Create a blank application object to hold the changes that you want to make.</span></span>  

 >[!NOTE]
 ><span data-ttu-id="714d7-145">This is only a variable to hold the values that you want to update, so nothing has actually been created.</span><span class="sxs-lookup"><span data-stu-id="714d7-145">This is only a variable to hold the values that you want to update, so nothing has actually been created.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="714d7-146">Set the home-page URL to the value that you want.</span><span class="sxs-lookup"><span data-stu-id="714d7-146">Set the home-page URL to the value that you want.</span></span> <span data-ttu-id="714d7-147">The value must be a subdomain path of the published app.</span><span class="sxs-lookup"><span data-stu-id="714d7-147">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="714d7-148">For example, if you change the home-page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users will go directly to the custom home page.</span><span class="sxs-lookup"><span data-stu-id="714d7-148">For example, if you change the home-page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users will go directly to the custom home page.</span></span>

    ```
    $appnew.Homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="714d7-149">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span><span class="sxs-lookup"><span data-stu-id="714d7-149">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -AppObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 - Application $appnew
    ```
5. <span data-ttu-id="714d7-150">To confirm that the change was successful, restart the app.</span><span class="sxs-lookup"><span data-stu-id="714d7-150">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -AppObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="714d7-151">Any changes that you make to the app might reset the home-page URL.</span><span class="sxs-lookup"><span data-stu-id="714d7-151">Any changes that you make to the app might reset the home-page URL.</span></span> <span data-ttu-id="714d7-152">If this happens, repeat the process in "Step 2: Update the home-page URL."</span><span class="sxs-lookup"><span data-stu-id="714d7-152">If this happens, repeat the process in "Step 2: Update the home-page URL."</span></span>

## <a name="next-steps"></a><span data-ttu-id="714d7-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="714d7-153">Next steps</span></span>

- [<span data-ttu-id="714d7-154">Enable remote access to SharePoint with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="714d7-154">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="714d7-155">Enable Application Proxy in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="714d7-155">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
