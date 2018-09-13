---
title: Set a custom home page for published apps by using Azure AD Application Proxy | Microsoft Docs
description: Covers the basics about Azure AD Application Proxy connectors
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/08/2017
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 10bcb3c0c4842202f95cdc1fff30d12b7a8fbbc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965733"
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="62d13-103">Set a custom home page for published apps by using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="62d13-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="62d13-104">This article discusses how to configure apps to direct users to a custom home page.</span><span class="sxs-lookup"><span data-stu-id="62d13-104">This article discusses how to configure apps to direct users to a custom home page.</span></span> <span data-ttu-id="62d13-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span><span class="sxs-lookup"><span data-stu-id="62d13-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not the page your users should see first.</span></span> <span data-ttu-id="62d13-106">Set a custom home page so that your users go to the right page when they access the apps.</span><span class="sxs-lookup"><span data-stu-id="62d13-106">Set a custom home page so that your users go to the right page when they access the apps.</span></span> <span data-ttu-id="62d13-107">Your users will see the custom home page that you set, whether they access the app from the Azure Active Directory Access Panel or the Office 365 app launcher.</span><span class="sxs-lookup"><span data-stu-id="62d13-107">Your users will see the custom home page that you set, whether they access the app from the Azure Active Directory Access Panel or the Office 365 app launcher.</span></span>

<span data-ttu-id="62d13-108">When users launch the app, they're directed by default to the root domain URL for the published app.</span><span class="sxs-lookup"><span data-stu-id="62d13-108">When users launch the app, they're directed by default to the root domain URL for the published app.</span></span> <span data-ttu-id="62d13-109">The landing page is typically set as the home page URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-109">The landing page is typically set as the home page URL.</span></span> <span data-ttu-id="62d13-110">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span><span class="sxs-lookup"><span data-stu-id="62d13-110">Use the Azure AD PowerShell module to define custom home page URLs when you want app users to land on a specific page within the app.</span></span> 

<span data-ttu-id="62d13-111">Here's one example of why a company would set a custom home page:</span><span class="sxs-lookup"><span data-stu-id="62d13-111">Here's one example of why a company would set a custom home page:</span></span>
- <span data-ttu-id="62d13-112">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span><span class="sxs-lookup"><span data-stu-id="62d13-112">Inside your corporate network, users go to *https://ExpenseApp/login/login.aspx* to sign in and access your app.</span></span>
- <span data-ttu-id="62d13-113">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-113">Because you have other assets like images that Application Proxy needs to access at the top level of the folder structure, you publish the app with *https://ExpenseApp* as the internal URL.</span></span>
- <span data-ttu-id="62d13-114">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign-in page.</span><span class="sxs-lookup"><span data-stu-id="62d13-114">The default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users to the sign-in page.</span></span>  
- <span data-ttu-id="62d13-115">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-115">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as the home page URL.</span></span> 

>[!NOTE]
><span data-ttu-id="62d13-116">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](../user-help/active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="62d13-116">When you give users access to published apps, the apps are displayed in the [Azure AD Access Panel](../user-help/active-directory-saas-access-panel-introduction.md) and the [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="62d13-117">Before you start</span><span class="sxs-lookup"><span data-stu-id="62d13-117">Before you start</span></span>

<span data-ttu-id="62d13-118">Before you set the home page URL, keep in mind the following requirements:</span><span class="sxs-lookup"><span data-stu-id="62d13-118">Before you set the home page URL, keep in mind the following requirements:</span></span>

* <span data-ttu-id="62d13-119">Ensure that the path you specify is a subdomain path of the root domain URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-119">Ensure that the path you specify is a subdomain path of the root domain URL.</span></span>

  <span data-ttu-id="62d13-120">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="62d13-120">If the root-domain URL is, for example, https://apps.contoso.com/app1/, the home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="62d13-121">If you make a change to the published app, the change might reset the value of the home page URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-121">If you make a change to the published app, the change might reset the value of the home page URL.</span></span> <span data-ttu-id="62d13-122">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-122">When you update the app in the future, you should recheck and, if necessary, update the home page URL.</span></span>

## <a name="change-the-home-page-in-the-azure-portal"></a><span data-ttu-id="62d13-123">Change the home page in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="62d13-123">Change the home page in the Azure portal</span></span>

1. <span data-ttu-id="62d13-124">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="62d13-124">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="62d13-125">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span><span class="sxs-lookup"><span data-stu-id="62d13-125">Navigate to **Azure Active Directory** > **App registrations** and choose your application from the list.</span></span> 
3. <span data-ttu-id="62d13-126">Select **Properties** from the settings.</span><span class="sxs-lookup"><span data-stu-id="62d13-126">Select **Properties** from the settings.</span></span>
4. <span data-ttu-id="62d13-127">Update the **Home page URL** field with your new path.</span><span class="sxs-lookup"><span data-stu-id="62d13-127">Update the **Home page URL** field with your new path.</span></span> 

   ![Provide new home page URL](./media/application-proxy-configure-custom-home-page/homepage.png)

5. <span data-ttu-id="62d13-129">Select **Save**</span><span class="sxs-lookup"><span data-stu-id="62d13-129">Select **Save**</span></span>

## <a name="change-the-home-page-with-powershell"></a><span data-ttu-id="62d13-130">Change the home page with PowerShell</span><span class="sxs-lookup"><span data-stu-id="62d13-130">Change the home page with PowerShell</span></span>

### <a name="install-the-azure-ad-powershell-module"></a><span data-ttu-id="62d13-131">Install the Azure AD PowerShell module</span><span class="sxs-lookup"><span data-stu-id="62d13-131">Install the Azure AD PowerShell module</span></span>

<span data-ttu-id="62d13-132">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="62d13-132">Before you define a custom home page URL by using PowerShell, install the Azure AD PowerShell module.</span></span> <span data-ttu-id="62d13-133">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span><span class="sxs-lookup"><span data-stu-id="62d13-133">You can download the package from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses the Graph API endpoint.</span></span> 

<span data-ttu-id="62d13-134">To install the package, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="62d13-134">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="62d13-135">Open a standard PowerShell window, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="62d13-135">Open a standard PowerShell window, and then run the following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="62d13-136">If you're running the command as a non-admin, use the `-scope currentuser` option.</span><span class="sxs-lookup"><span data-stu-id="62d13-136">If you're running the command as a non-admin, use the `-scope currentuser` option.</span></span>
2. <span data-ttu-id="62d13-137">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span><span class="sxs-lookup"><span data-stu-id="62d13-137">During the installation, select **Y** to install two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-the-objectid-of-the-app"></a><span data-ttu-id="62d13-138">Find the ObjectID of the app</span><span class="sxs-lookup"><span data-stu-id="62d13-138">Find the ObjectID of the app</span></span>

<span data-ttu-id="62d13-139">Obtain the ObjectID of the app, and then search for the app by its home page.</span><span class="sxs-lookup"><span data-stu-id="62d13-139">Obtain the ObjectID of the app, and then search for the app by its home page.</span></span>

1. <span data-ttu-id="62d13-140">In the same PowerShell window, import the Azure AD module.</span><span class="sxs-lookup"><span data-stu-id="62d13-140">In the same PowerShell window, import the Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="62d13-141">Sign in to the Azure AD module as the tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="62d13-141">Sign in to the Azure AD module as the tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="62d13-142">Find the app based on its home page URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-142">Find the app based on its home page URL.</span></span> <span data-ttu-id="62d13-143">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span><span class="sxs-lookup"><span data-stu-id="62d13-143">You can find the URL in the portal by going to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="62d13-144">This example uses *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="62d13-144">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="62d13-145">You should get a result that's similar to the one shown here.</span><span class="sxs-lookup"><span data-stu-id="62d13-145">You should get a result that's similar to the one shown here.</span></span> <span data-ttu-id="62d13-146">Copy the ObjectID GUID to use in the next section.</span><span class="sxs-lookup"><span data-stu-id="62d13-146">Copy the ObjectID GUID to use in the next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-the-home-page-url"></a><span data-ttu-id="62d13-147">Update the home page URL</span><span class="sxs-lookup"><span data-stu-id="62d13-147">Update the home page URL</span></span>

<span data-ttu-id="62d13-148">Create the home page URL, and update your application with that value.</span><span class="sxs-lookup"><span data-stu-id="62d13-148">Create the home page URL, and update your application with that value.</span></span> <span data-ttu-id="62d13-149">Continue using the same PowerShell window to run these commands.</span><span class="sxs-lookup"><span data-stu-id="62d13-149">Continue using the same PowerShell window to run these commands.</span></span> <span data-ttu-id="62d13-150">Or, if you're using a new PowerShell window, sign in to the Azure AD module again using `Connect-AzureAD`.</span><span class="sxs-lookup"><span data-stu-id="62d13-150">Or, if you're using a new PowerShell window, sign in to the Azure AD module again using `Connect-AzureAD`.</span></span> 

1. <span data-ttu-id="62d13-151">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="62d13-151">Confirm that you have the correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with the ObjectID that you copied in the preceding section.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="62d13-152">Now that you've confirmed the app, you're ready to update the home page, as follows.</span><span class="sxs-lookup"><span data-stu-id="62d13-152">Now that you've confirmed the app, you're ready to update the home page, as follows.</span></span>

2. <span data-ttu-id="62d13-153">Create a blank application object to hold the changes that you want to make.</span><span class="sxs-lookup"><span data-stu-id="62d13-153">Create a blank application object to hold the changes that you want to make.</span></span> <span data-ttu-id="62d13-154">This variable holds the values that you want to update.</span><span class="sxs-lookup"><span data-stu-id="62d13-154">This variable holds the values that you want to update.</span></span> <span data-ttu-id="62d13-155">Nothing is created in this step.</span><span class="sxs-lookup"><span data-stu-id="62d13-155">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="62d13-156">Set the home page URL to the value that you want.</span><span class="sxs-lookup"><span data-stu-id="62d13-156">Set the home page URL to the value that you want.</span></span> <span data-ttu-id="62d13-157">The value must be a subdomain path of the published app.</span><span class="sxs-lookup"><span data-stu-id="62d13-157">The value must be a subdomain path of the published app.</span></span> <span data-ttu-id="62d13-158">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span><span class="sxs-lookup"><span data-stu-id="62d13-158">For example, if you change the home page URL from *https://sharepoint-iddemo.msappproxy.net/* to *https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly to the custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="62d13-159">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span><span class="sxs-lookup"><span data-stu-id="62d13-159">Make the update by using the GUID (ObjectID) that you copied in "Step 1: Find the ObjectID of the app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="62d13-160">To confirm that the change was successful, restart the app.</span><span class="sxs-lookup"><span data-stu-id="62d13-160">To confirm that the change was successful, restart the app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="62d13-161">Any changes that you make to the app might reset the home page URL.</span><span class="sxs-lookup"><span data-stu-id="62d13-161">Any changes that you make to the app might reset the home page URL.</span></span> <span data-ttu-id="62d13-162">If your home page URL resets, repeat the steps in this section to set it back.</span><span class="sxs-lookup"><span data-stu-id="62d13-162">If your home page URL resets, repeat the steps in this section to set it back.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62d13-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="62d13-163">Next steps</span></span>

- [<span data-ttu-id="62d13-164">Enable remote access to SharePoint with Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="62d13-164">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>](application-proxy-integrate-with-sharepoint-server.md)
- [<span data-ttu-id="62d13-165">Enable Application Proxy in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="62d13-165">Enable Application Proxy in the Azure portal</span></span>](application-proxy-enable.md)
