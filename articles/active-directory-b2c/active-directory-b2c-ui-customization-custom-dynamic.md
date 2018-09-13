---
title: Customize the Azure Active Directory B2C user interface (UI) dynamically by using custom policies | Microsoft Docs
description: Support multiple branding experiences with HTML5/CSS content that changes dynamically at runtime.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 09/20/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 4e7cc47bddf3663cbc1c8bb5c4470020a84073e4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966412"
---
# <a name="azure-active-directory-b2c-configure-the-ui-with-dynamic-content-by-using-custom-policies"></a><span data-ttu-id="6c539-103">Azure Active Directory B2C: Configure the UI with dynamic content by using custom policies</span><span class="sxs-lookup"><span data-stu-id="6c539-103">Azure Active Directory B2C: Configure the UI with dynamic content by using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6c539-104">By using Azure Active Directory B2C (Azure AD B2C) custom policies, you can send a parameter in a query string.</span><span class="sxs-lookup"><span data-stu-id="6c539-104">By using Azure Active Directory B2C (Azure AD B2C) custom policies, you can send a parameter in a query string.</span></span> <span data-ttu-id="6c539-105">By passing the parameter to your HTML endpoint, you can dynamically change the page content.</span><span class="sxs-lookup"><span data-stu-id="6c539-105">By passing the parameter to your HTML endpoint, you can dynamically change the page content.</span></span> <span data-ttu-id="6c539-106">For example, you can change the background image on the Azure AD B2C sign-up or sign-in page, based on a parameter that you pass from your web or mobile application.</span><span class="sxs-lookup"><span data-stu-id="6c539-106">For example, you can change the background image on the Azure AD B2C sign-up or sign-in page, based on a parameter that you pass from your web or mobile application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6c539-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c539-107">Prerequisites</span></span>
<span data-ttu-id="6c539-108">This article focuses on how to customize the Azure AD B2C user interface with *dynamic content* by using custom policies.</span><span class="sxs-lookup"><span data-stu-id="6c539-108">This article focuses on how to customize the Azure AD B2C user interface with *dynamic content* by using custom policies.</span></span> <span data-ttu-id="6c539-109">To get started, see [UI customization in a custom policy](active-directory-b2c-ui-customization-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6c539-109">To get started, see [UI customization in a custom policy](active-directory-b2c-ui-customization-custom.md).</span></span> 

>[!NOTE]
><span data-ttu-id="6c539-110">The Azure AD B2C article, [Configure UI customization in a custom policy](active-directory-b2c-ui-customization-custom.md), discusses the following fundamentals:</span><span class="sxs-lookup"><span data-stu-id="6c539-110">The Azure AD B2C article, [Configure UI customization in a custom policy](active-directory-b2c-ui-customization-custom.md), discusses the following fundamentals:</span></span>
> * <span data-ttu-id="6c539-111">The page user interface (UI) customization feature.</span><span class="sxs-lookup"><span data-stu-id="6c539-111">The page user interface (UI) customization feature.</span></span>
> * <span data-ttu-id="6c539-112">Essential tools for testing the page UI customization feature by using our sample content.</span><span class="sxs-lookup"><span data-stu-id="6c539-112">Essential tools for testing the page UI customization feature by using our sample content.</span></span>
> * <span data-ttu-id="6c539-113">The core UI elements of each page type.</span><span class="sxs-lookup"><span data-stu-id="6c539-113">The core UI elements of each page type.</span></span>
> * <span data-ttu-id="6c539-114">Best practices for applying this feature.</span><span class="sxs-lookup"><span data-stu-id="6c539-114">Best practices for applying this feature.</span></span>

## <a name="add-a-link-to-html5css-templates-to-your-user-journey"></a><span data-ttu-id="6c539-115">Add a link to HTML5/CSS templates to your user journey</span><span class="sxs-lookup"><span data-stu-id="6c539-115">Add a link to HTML5/CSS templates to your user journey</span></span>

<span data-ttu-id="6c539-116">In a custom policy, a content definition defines the HTML5 page URI that is used for a specified UI step (for example, the sign-in or sign-up pages).</span><span class="sxs-lookup"><span data-stu-id="6c539-116">In a custom policy, a content definition defines the HTML5 page URI that is used for a specified UI step (for example, the sign-in or sign-up pages).</span></span> <span data-ttu-id="6c539-117">The base policy defines the default look and feel by pointing to a URI of HTML5 files (in the CSS).</span><span class="sxs-lookup"><span data-stu-id="6c539-117">The base policy defines the default look and feel by pointing to a URI of HTML5 files (in the CSS).</span></span> <span data-ttu-id="6c539-118">In the extension policy, you can modify the look and feel by overriding the LoadUri for the HTML5 file.</span><span class="sxs-lookup"><span data-stu-id="6c539-118">In the extension policy, you can modify the look and feel by overriding the LoadUri for the HTML5 file.</span></span> <span data-ttu-id="6c539-119">Content definitions contain URLs to external content that is defined by crafting HTML5/CSS files, as appropriate.</span><span class="sxs-lookup"><span data-stu-id="6c539-119">Content definitions contain URLs to external content that is defined by crafting HTML5/CSS files, as appropriate.</span></span> 

<span data-ttu-id="6c539-120">The `ContentDefinitions` section contains a series of `ContentDefinition` XML elements.</span><span class="sxs-lookup"><span data-stu-id="6c539-120">The `ContentDefinitions` section contains a series of `ContentDefinition` XML elements.</span></span> <span data-ttu-id="6c539-121">The ID attribute of the `ContentDefinition` element specifies the type of page that relates to the content definition.</span><span class="sxs-lookup"><span data-stu-id="6c539-121">The ID attribute of the `ContentDefinition` element specifies the type of page that relates to the content definition.</span></span> <span data-ttu-id="6c539-122">That is, the element defines the context that a custom HTML5/CSS template is going to apply.</span><span class="sxs-lookup"><span data-stu-id="6c539-122">That is, the element defines the context that a custom HTML5/CSS template is going to apply.</span></span> <span data-ttu-id="6c539-123">The following table describes the set of content definition IDs that are recognized by the IEF engine, and the page types that relate to them.</span><span class="sxs-lookup"><span data-stu-id="6c539-123">The following table describes the set of content definition IDs that are recognized by the IEF engine, and the page types that relate to them.</span></span>

| <span data-ttu-id="6c539-124">Content definition ID</span><span class="sxs-lookup"><span data-stu-id="6c539-124">Content definition ID</span></span> | <span data-ttu-id="6c539-125">Default HTML5 template</span><span class="sxs-lookup"><span data-stu-id="6c539-125">Default HTML5 template</span></span>| <span data-ttu-id="6c539-126">Description</span><span class="sxs-lookup"><span data-stu-id="6c539-126">Description</span></span> | 
|-----------------------|--------|-------------|
| <span data-ttu-id="6c539-127">*api.error*</span><span class="sxs-lookup"><span data-stu-id="6c539-127">*api.error*</span></span> | [<span data-ttu-id="6c539-128">exception.cshtml</span><span class="sxs-lookup"><span data-stu-id="6c539-128">exception.cshtml</span></span>](https://login.microsoftonline.com/static/tenant/default/exception.cshtml) | <span data-ttu-id="6c539-129">**Error page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-129">**Error page**.</span></span> <span data-ttu-id="6c539-130">This page is displayed when an exception or an error is encountered.</span><span class="sxs-lookup"><span data-stu-id="6c539-130">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="6c539-131">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="6c539-131">*api.idpselections*</span></span> | [<span data-ttu-id="6c539-132">idpSelector.cshtml</span><span class="sxs-lookup"><span data-stu-id="6c539-132">idpSelector.cshtml</span></span>](https://login.microsoftonline.com/static/tenant/default/idpSelector.cshtml) | <span data-ttu-id="6c539-133">**Identity provider selection page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-133">**Identity provider selection page**.</span></span> <span data-ttu-id="6c539-134">This page lists identity providers that users can choose from during sign-in.</span><span class="sxs-lookup"><span data-stu-id="6c539-134">This page lists identity providers that users can choose from during sign-in.</span></span> <span data-ttu-id="6c539-135">The options are usually enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="6c539-135">The options are usually enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="6c539-136">*api.idpselections.signup*</span><span class="sxs-lookup"><span data-stu-id="6c539-136">*api.idpselections.signup*</span></span> | [<span data-ttu-id="6c539-137">idpSelector.cshtml</span><span class="sxs-lookup"><span data-stu-id="6c539-137">idpSelector.cshtml</span></span>](https://login.microsoftonline.com/static/tenant/default/idpSelector.cshtml) | <span data-ttu-id="6c539-138">**Identity provider selection for sign-up**.</span><span class="sxs-lookup"><span data-stu-id="6c539-138">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="6c539-139">This page lists identity providers that users can choose from during sign-up.</span><span class="sxs-lookup"><span data-stu-id="6c539-139">This page lists identity providers that users can choose from during sign-up.</span></span> <span data-ttu-id="6c539-140">The options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="6c539-140">The options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="6c539-141">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="6c539-141">*api.localaccountpasswordreset*</span></span> | [<span data-ttu-id="6c539-142">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="6c539-142">selfasserted.html</span></span>](https://login.microsoftonline.com/static/tenant/default/selfAsserted.cshtml) | <span data-ttu-id="6c539-143">**Forgot password page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-143">**Forgot password page**.</span></span> <span data-ttu-id="6c539-144">This page contains a form that users must complete to initiate a password reset.</span><span class="sxs-lookup"><span data-stu-id="6c539-144">This page contains a form that users must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="6c539-145">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="6c539-145">*api.localaccountsignin*</span></span> | [<span data-ttu-id="6c539-146">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="6c539-146">selfasserted.html</span></span>](https://login.microsoftonline.com/static/tenant/default/selfAsserted.cshtml) | <span data-ttu-id="6c539-147">**Local account sign-in page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-147">**Local account sign-in page**.</span></span> <span data-ttu-id="6c539-148">This page contains a form for signing in with a local account that's based on an email address or a user name.</span><span class="sxs-lookup"><span data-stu-id="6c539-148">This page contains a form for signing in with a local account that's based on an email address or a user name.</span></span> <span data-ttu-id="6c539-149">The form can contain a text input box and password entry box.</span><span class="sxs-lookup"><span data-stu-id="6c539-149">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="6c539-150">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="6c539-150">*api.localaccountsignup*</span></span> | [<span data-ttu-id="6c539-151">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="6c539-151">selfasserted.html</span></span>](https://login.microsoftonline.com/static/tenant/default/selfAsserted.cshtml) | <span data-ttu-id="6c539-152">**Local account sign up page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-152">**Local account sign up page**.</span></span> <span data-ttu-id="6c539-153">This page contains a form for signing up for a local account that's based on an email address or a user name.</span><span class="sxs-lookup"><span data-stu-id="6c539-153">This page contains a form for signing up for a local account that's based on an email address or a user name.</span></span> <span data-ttu-id="6c539-154">The form can contain various input controls, such as: a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span><span class="sxs-lookup"><span data-stu-id="6c539-154">The form can contain various input controls, such as: a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="6c539-155">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="6c539-155">*api.phonefactor*</span></span> | [<span data-ttu-id="6c539-156">multifactor-1.0.0.cshtml</span><span class="sxs-lookup"><span data-stu-id="6c539-156">multifactor-1.0.0.cshtml</span></span>](https://login.microsoftonline.com/static/tenant/default/multifactor-1.0.0.cshtml) | <span data-ttu-id="6c539-157">**Multi-factor authentication page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-157">**Multi-factor authentication page**.</span></span> <span data-ttu-id="6c539-158">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span><span class="sxs-lookup"><span data-stu-id="6c539-158">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="6c539-159">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="6c539-159">*api.selfasserted*</span></span> | [<span data-ttu-id="6c539-160">selfasserted.html</span><span class="sxs-lookup"><span data-stu-id="6c539-160">selfasserted.html</span></span>](https://login.microsoftonline.com/static/tenant/default/selfAsserted.cshtml) | <span data-ttu-id="6c539-161">**Social account sign-up page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-161">**Social account sign-up page**.</span></span> <span data-ttu-id="6c539-162">This page contains a form that users must complete when they sign up by using an existing account from a social identity provider.</span><span class="sxs-lookup"><span data-stu-id="6c539-162">This page contains a form that users must complete when they sign up by using an existing account from a social identity provider.</span></span> <span data-ttu-id="6c539-163">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span><span class="sxs-lookup"><span data-stu-id="6c539-163">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="6c539-164">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="6c539-164">*api.selfasserted.profileupdate*</span></span> | [<span data-ttu-id="6c539-165">updateprofile.html</span><span class="sxs-lookup"><span data-stu-id="6c539-165">updateprofile.html</span></span>](https://login.microsoftonline.com/static/tenant/default/updateProfile.cshtml) | <span data-ttu-id="6c539-166">**Profile update page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-166">**Profile update page**.</span></span> <span data-ttu-id="6c539-167">This page contains a form that users can access to update their profile.</span><span class="sxs-lookup"><span data-stu-id="6c539-167">This page contains a form that users can access to update their profile.</span></span> <span data-ttu-id="6c539-168">This page is similar to the social account sign-up page, except for the password entry fields.</span><span class="sxs-lookup"><span data-stu-id="6c539-168">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="6c539-169">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="6c539-169">*api.signuporsignin*</span></span> | [<span data-ttu-id="6c539-170">unified.html</span><span class="sxs-lookup"><span data-stu-id="6c539-170">unified.html</span></span>](https://login.microsoftonline.com/static/tenant/default/unified.cshtml) | <span data-ttu-id="6c539-171">**Unified sign-up or sign-in page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-171">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="6c539-172">This page handles the user sign-up and sign-in process.</span><span class="sxs-lookup"><span data-stu-id="6c539-172">This page handles the user sign-up and sign-in process.</span></span> <span data-ttu-id="6c539-173">Users can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="6c539-173">Users can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="serving-dynamic-content"></a><span data-ttu-id="6c539-174">Serving dynamic content</span><span class="sxs-lookup"><span data-stu-id="6c539-174">Serving dynamic content</span></span>
<span data-ttu-id="6c539-175">In the [Configure UI customization in a custom policy](active-directory-b2c-ui-customization-custom.md) article, you upload HTML5 files to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="6c539-175">In the [Configure UI customization in a custom policy](active-directory-b2c-ui-customization-custom.md) article, you upload HTML5 files to Azure Blob storage.</span></span> <span data-ttu-id="6c539-176">Those HTML5 files are static and render the same HTML content for each request.</span><span class="sxs-lookup"><span data-stu-id="6c539-176">Those HTML5 files are static and render the same HTML content for each request.</span></span> 

<span data-ttu-id="6c539-177">In this article, you use an ASP.NET web app, which can accept query string parameters and respond accordingly.</span><span class="sxs-lookup"><span data-stu-id="6c539-177">In this article, you use an ASP.NET web app, which can accept query string parameters and respond accordingly.</span></span> 

<span data-ttu-id="6c539-178">In this walkthrough, you:</span><span class="sxs-lookup"><span data-stu-id="6c539-178">In this walkthrough, you:</span></span>
* <span data-ttu-id="6c539-179">Create an ASP.NET Core web application that hosts your HTML5 templates.</span><span class="sxs-lookup"><span data-stu-id="6c539-179">Create an ASP.NET Core web application that hosts your HTML5 templates.</span></span> 
* <span data-ttu-id="6c539-180">Add a custom HTML5 template, _unified.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="6c539-180">Add a custom HTML5 template, _unified.cshtml_.</span></span> 
* <span data-ttu-id="6c539-181">Publish your web app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6c539-181">Publish your web app to Azure App Service.</span></span> 
* <span data-ttu-id="6c539-182">Set cross-origin resource sharing (CORS) for your web app.</span><span class="sxs-lookup"><span data-stu-id="6c539-182">Set cross-origin resource sharing (CORS) for your web app.</span></span>
* <span data-ttu-id="6c539-183">Override the `LoadUri` elements to point to your HTML5 file.</span><span class="sxs-lookup"><span data-stu-id="6c539-183">Override the `LoadUri` elements to point to your HTML5 file.</span></span>

## <a name="step-1-create-an-aspnet-web-app"></a><span data-ttu-id="6c539-184">Step 1: Create an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="6c539-184">Step 1: Create an ASP.NET web app</span></span>

1. <span data-ttu-id="6c539-185">In Visual Studio, create a project by selecting **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="6c539-185">In Visual Studio, create a project by selecting **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="6c539-186">In the **New Project** window, select **Visual C#** > **Web** > **ASP.NET Core Web Application (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="6c539-186">In the **New Project** window, select **Visual C#** > **Web** > **ASP.NET Core Web Application (.NET Core)**.</span></span>

3. <span data-ttu-id="6c539-187">Name the application (for example, *Contoso.AADB2C.UI*), and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c539-187">Name the application (for example, *Contoso.AADB2C.UI*), and then select **OK**.</span></span>

    ![Create new Visual Studio project](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-create-project1.png)

4. <span data-ttu-id="6c539-189">Select the **Web Application** template.</span><span class="sxs-lookup"><span data-stu-id="6c539-189">Select the **Web Application** template.</span></span>

5. <span data-ttu-id="6c539-190">Set the authentication to **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="6c539-190">Set the authentication to **No Authentication**.</span></span>

    ![Select Web Application template](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-create-project2.png)

6. <span data-ttu-id="6c539-192">Select **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="6c539-192">Select **OK** to create the project.</span></span>

## <a name="step-2-create-mvc-view"></a><span data-ttu-id="6c539-193">Step 2: Create MVC view</span><span class="sxs-lookup"><span data-stu-id="6c539-193">Step 2: Create MVC view</span></span>
### <a name="step-21-download-the-b2c-built-in-html5-template"></a><span data-ttu-id="6c539-194">Step 2.1: Download the B2C built-in HTML5 template</span><span class="sxs-lookup"><span data-stu-id="6c539-194">Step 2.1: Download the B2C built-in HTML5 template</span></span>
<span data-ttu-id="6c539-195">Your custom HTML5 template is based on the Azure AD B2C built-in HTML5 template.</span><span class="sxs-lookup"><span data-stu-id="6c539-195">Your custom HTML5 template is based on the Azure AD B2C built-in HTML5 template.</span></span> <span data-ttu-id="6c539-196">You can download the [unified.html file](https://login.microsoftonline.com/static/tenant/default/unified.cshtml) or download the template from [starter pack](https://github.com/AzureADQuickStarts/B2C-AzureBlobStorage-Client/tree/master/sample_templates/wingtip).</span><span class="sxs-lookup"><span data-stu-id="6c539-196">You can download the [unified.html file](https://login.microsoftonline.com/static/tenant/default/unified.cshtml) or download the template from [starter pack](https://github.com/AzureADQuickStarts/B2C-AzureBlobStorage-Client/tree/master/sample_templates/wingtip).</span></span> <span data-ttu-id="6c539-197">You use this HTML5 file to create a unified sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="6c539-197">You use this HTML5 file to create a unified sign-up or sign-in page.</span></span>

### <a name="step-22-add-the-mvc-view"></a><span data-ttu-id="6c539-198">Step 2.2: Add the MVC view</span><span class="sxs-lookup"><span data-stu-id="6c539-198">Step 2.2: Add the MVC view</span></span>
1. <span data-ttu-id="6c539-199">Right-click the Views/Home folder, and then **Add** > **New Item**.</span><span class="sxs-lookup"><span data-stu-id="6c539-199">Right-click the Views/Home folder, and then **Add** > **New Item**.</span></span>

    ![Add MVC new item](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-add-view1.png)

2. <span data-ttu-id="6c539-201">In the **Add New Item - Contoso.AADB2C.UI** window, select **Web > ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6c539-201">In the **Add New Item - Contoso.AADB2C.UI** window, select **Web > ASP.NET**.</span></span>

3. <span data-ttu-id="6c539-202">Select **MVC View Page**.</span><span class="sxs-lookup"><span data-stu-id="6c539-202">Select **MVC View Page**.</span></span>

4. <span data-ttu-id="6c539-203">In the **Name** box, change the name to **unified.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="6c539-203">In the **Name** box, change the name to **unified.cshtml**.</span></span>

5. <span data-ttu-id="6c539-204">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6c539-204">Select **Add**.</span></span>

    ![Add MVC view](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-add-view2.png)

6. <span data-ttu-id="6c539-206">If the *unified.cshtml* file is not open already, double-click the file to open it, and then clear the file contents.</span><span class="sxs-lookup"><span data-stu-id="6c539-206">If the *unified.cshtml* file is not open already, double-click the file to open it, and then clear the file contents.</span></span>

7. <span data-ttu-id="6c539-207">For this walkthrough, we remove the reference to layout-page.</span><span class="sxs-lookup"><span data-stu-id="6c539-207">For this walkthrough, we remove the reference to layout-page.</span></span> <span data-ttu-id="6c539-208">Add the following code snippet to _unified.cshtml_:</span><span class="sxs-lookup"><span data-stu-id="6c539-208">Add the following code snippet to _unified.cshtml_:</span></span>

    ```csharp
    @{
        Layout = null;
    }
    ```

8. <span data-ttu-id="6c539-209">Open the _unified.cshtml_ file you downloaded from Azure AD B2C built-in HTML5 template.</span><span class="sxs-lookup"><span data-stu-id="6c539-209">Open the _unified.cshtml_ file you downloaded from Azure AD B2C built-in HTML5 template.</span></span>

9. <span data-ttu-id="6c539-210">Replace the single at signs (@) with double at signs (@@).</span><span class="sxs-lookup"><span data-stu-id="6c539-210">Replace the single at signs (@) with double at signs (@@).</span></span>

10. <span data-ttu-id="6c539-211">Copy the content of the file and paste it below the Layout definition.</span><span class="sxs-lookup"><span data-stu-id="6c539-211">Copy the content of the file and paste it below the Layout definition.</span></span> <span data-ttu-id="6c539-212">Your code should look like:</span><span class="sxs-lookup"><span data-stu-id="6c539-212">Your code should look like:</span></span>

    ![unified.cshtml file after adding the HTML5](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-edit-view1.png)

### <a name="step-23-change-the-background-image"></a><span data-ttu-id="6c539-214">Step 2.3: Change the background image</span><span class="sxs-lookup"><span data-stu-id="6c539-214">Step 2.3: Change the background image</span></span>

<span data-ttu-id="6c539-215">Locate the `<img>` element that contains the `ID` value *background_background_image*, and then replace the `src` value with **https://kbdevstorage1.blob.core.windows.net/asset-blobs/19889_en_1** or any other background image you want to use.</span><span class="sxs-lookup"><span data-stu-id="6c539-215">Locate the `<img>` element that contains the `ID` value *background_background_image*, and then replace the `src` value with **https://kbdevstorage1.blob.core.windows.net/asset-blobs/19889_en_1** or any other background image you want to use.</span></span>

![Change the page background](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-add-static-background.png)

### <a name="step-24-add-your-view-to-the-mvc-controller"></a><span data-ttu-id="6c539-217">Step 2.4: Add your view to the MVC controller</span><span class="sxs-lookup"><span data-stu-id="6c539-217">Step 2.4: Add your view to the MVC controller</span></span>

1. <span data-ttu-id="6c539-218">Open **Controllers\HomeController.cs**, and add following method:</span><span class="sxs-lookup"><span data-stu-id="6c539-218">Open **Controllers\HomeController.cs**, and add following method:</span></span> 

    ```C
    public IActionResult unified()
    {
        return View();
    }
    ```
    <span data-ttu-id="6c539-219">This code specifies that the method should use a *View* template file to render a response to the browser.</span><span class="sxs-lookup"><span data-stu-id="6c539-219">This code specifies that the method should use a *View* template file to render a response to the browser.</span></span> <span data-ttu-id="6c539-220">Because we don't explicitly specify the name of the *View* template file, MVC defaults to using the _unified.cshtml_ View file in the */Views/Home* folder.</span><span class="sxs-lookup"><span data-stu-id="6c539-220">Because we don't explicitly specify the name of the *View* template file, MVC defaults to using the _unified.cshtml_ View file in the */Views/Home* folder.</span></span>
    
    <span data-ttu-id="6c539-221">After you add the _unified_ method, your code should look like:</span><span class="sxs-lookup"><span data-stu-id="6c539-221">After you add the _unified_ method, your code should look like:</span></span>
    
    ![Change the controller to render the view](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-controller-view.png)

2. <span data-ttu-id="6c539-223">Debug your web app, and make sure that the _unified_ page is accessible (for example, `http://localhost:<Port number>/Home/unified`).</span><span class="sxs-lookup"><span data-stu-id="6c539-223">Debug your web app, and make sure that the _unified_ page is accessible (for example, `http://localhost:<Port number>/Home/unified`).</span></span>

### <a name="step-25-publish-to-azure"></a><span data-ttu-id="6c539-224">Step 2.5: Publish to Azure</span><span class="sxs-lookup"><span data-stu-id="6c539-224">Step 2.5: Publish to Azure</span></span>
1. <span data-ttu-id="6c539-225">In **Solution Explorer**, right-click the **Contoso.AADB2C.UI** project, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="6c539-225">In **Solution Explorer**, right-click the **Contoso.AADB2C.UI** project, and then select **Publish**.</span></span>

    ![Publish to Microsoft Azure App Service](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-publish1.png)

2. <span data-ttu-id="6c539-227">Select the **Microsoft Azure App Service** tile, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="6c539-227">Select the **Microsoft Azure App Service** tile, and then select **Publish**.</span></span>

    ![Create new Microsoft Azure App Service](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-publish2.png)

    <span data-ttu-id="6c539-229">The **Create App Service** window opens.</span><span class="sxs-lookup"><span data-stu-id="6c539-229">The **Create App Service** window opens.</span></span> <span data-ttu-id="6c539-230">In it you can begin to create all the necessary Azure resources to run the ASP.NET web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c539-230">In it you can begin to create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6c539-231">For more information about publishing, see [Create an ASP.NET web app in Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet#publish-to-azure).</span><span class="sxs-lookup"><span data-stu-id="6c539-231">For more information about publishing, see [Create an ASP.NET web app in Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet#publish-to-azure).</span></span>

3. <span data-ttu-id="6c539-232">In the **Web App Name** box, type a unique app name (valid characters are a-z, A-Z, 0-9, and the hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="6c539-232">In the **Web App Name** box, type a unique app name (valid characters are a-z, A-Z, 0-9, and the hyphen (-).</span></span> <span data-ttu-id="6c539-233">The URL of the web app is `http://<app_name>.azurewebsites.NET`, where `<app_name>` is your web app name.</span><span class="sxs-lookup"><span data-stu-id="6c539-233">The URL of the web app is `http://<app_name>.azurewebsites.NET`, where `<app_name>` is your web app name.</span></span> <span data-ttu-id="6c539-234">You can accept the automatically generated name, which is unique.</span><span class="sxs-lookup"><span data-stu-id="6c539-234">You can accept the automatically generated name, which is unique.</span></span>

4. <span data-ttu-id="6c539-235">Select **Create** to start creating the Azure resources.</span><span class="sxs-lookup"><span data-stu-id="6c539-235">Select **Create** to start creating the Azure resources.</span></span>

    ![Provide App Service properties](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-publish3.png)

    <span data-ttu-id="6c539-237">After the creation process is complete, the wizard publishes the ASP.NET web app to Azure and then launches the app in the default browser.</span><span class="sxs-lookup"><span data-stu-id="6c539-237">After the creation process is complete, the wizard publishes the ASP.NET web app to Azure and then launches the app in the default browser.</span></span>

5. <span data-ttu-id="6c539-238">Copy the URL of the _unified_ page (for example, _https://<app_name>.azurewebsites.net/home/unified_).</span><span class="sxs-lookup"><span data-stu-id="6c539-238">Copy the URL of the _unified_ page (for example, _https://<app_name>.azurewebsites.net/home/unified_).</span></span>

## <a name="step-3-configure-cors-in-azure-app-service"></a><span data-ttu-id="6c539-239">Step 3: Configure CORS in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6c539-239">Step 3: Configure CORS in Azure App Service</span></span>
1. <span data-ttu-id="6c539-240">In the [Azure portal](https://portal.azure.com/), Select **App Services**, and then select the name of your API app.</span><span class="sxs-lookup"><span data-stu-id="6c539-240">In the [Azure portal](https://portal.azure.com/), Select **App Services**, and then select the name of your API app.</span></span>

    ![Select API app in the Azure portal](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-CORS1.png)

2. <span data-ttu-id="6c539-242">In the **Settings** section, under **API** section, select **CORS**.</span><span class="sxs-lookup"><span data-stu-id="6c539-242">In the **Settings** section, under **API** section, select **CORS**.</span></span>

    ![Select CORS settings](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-CORS2.png)

3. <span data-ttu-id="6c539-244">In the **CORS** window, in the **Allowed Origins** box, do either of the following:</span><span class="sxs-lookup"><span data-stu-id="6c539-244">In the **CORS** window, in the **Allowed Origins** box, do either of the following:</span></span>

    * <span data-ttu-id="6c539-245">Enter the URL or URLs that you want to allow JavaScript calls to come from.</span><span class="sxs-lookup"><span data-stu-id="6c539-245">Enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>
    * <span data-ttu-id="6c539-246">Enter an asterisk (\*) to specify that all origin domains are accepted.</span><span class="sxs-lookup"><span data-stu-id="6c539-246">Enter an asterisk (\*) to specify that all origin domains are accepted.</span></span>

4. <span data-ttu-id="6c539-247">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6c539-247">Select **Save**.</span></span>

    ![The CORS window](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-CORS3.png)

    <span data-ttu-id="6c539-249">After you select **Save**, the API app accepts JavaScript calls from the specified URLs.</span><span class="sxs-lookup"><span data-stu-id="6c539-249">After you select **Save**, the API app accepts JavaScript calls from the specified URLs.</span></span> 

## <a name="step-4-html5-template-validation"></a><span data-ttu-id="6c539-250">Step 4: HTML5 template validation</span><span class="sxs-lookup"><span data-stu-id="6c539-250">Step 4: HTML5 template validation</span></span>
<span data-ttu-id="6c539-251">Your HTML5 template is ready to use.</span><span class="sxs-lookup"><span data-stu-id="6c539-251">Your HTML5 template is ready to use.</span></span> <span data-ttu-id="6c539-252">However, it is not available in the `ContentDefinition` code.</span><span class="sxs-lookup"><span data-stu-id="6c539-252">However, it is not available in the `ContentDefinition` code.</span></span> <span data-ttu-id="6c539-253">Before you can add `ContentDefinition` to your custom policy, ensure that:</span><span class="sxs-lookup"><span data-stu-id="6c539-253">Before you can add `ContentDefinition` to your custom policy, ensure that:</span></span>
* <span data-ttu-id="6c539-254">Your content is HTML5 compliant and accessible.</span><span class="sxs-lookup"><span data-stu-id="6c539-254">Your content is HTML5 compliant and accessible.</span></span>
* <span data-ttu-id="6c539-255">Your content server is enabled for CORS.</span><span class="sxs-lookup"><span data-stu-id="6c539-255">Your content server is enabled for CORS.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6c539-256">To verify that the site where you're hosting your content has enabled CORS and can test CORS requests, go to the [test-cors.org](http://test-cors.org/) website.</span><span class="sxs-lookup"><span data-stu-id="6c539-256">To verify that the site where you're hosting your content has enabled CORS and can test CORS requests, go to the [test-cors.org](http://test-cors.org/) website.</span></span> 

* <span data-ttu-id="6c539-257">Your served content is secure over **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="6c539-257">Your served content is secure over **HTTPS**.</span></span>
* <span data-ttu-id="6c539-258">You are using *absolute URLS*, such as *https://yourdomain/content*, for all links, CSS content, and images.</span><span class="sxs-lookup"><span data-stu-id="6c539-258">You are using *absolute URLS*, such as *https://yourdomain/content*, for all links, CSS content, and images.</span></span>

## <a name="step-5-configure-your-content-definition"></a><span data-ttu-id="6c539-259">Step 5: Configure your content definition</span><span class="sxs-lookup"><span data-stu-id="6c539-259">Step 5: Configure your content definition</span></span>
<span data-ttu-id="6c539-260">To configure `ContentDefinition`, do the following:</span><span class="sxs-lookup"><span data-stu-id="6c539-260">To configure `ContentDefinition`, do the following:</span></span>
1. <span data-ttu-id="6c539-261">Open the base file of your policy (for example, *TrustFrameworkBase.xml*).</span><span class="sxs-lookup"><span data-stu-id="6c539-261">Open the base file of your policy (for example, *TrustFrameworkBase.xml*).</span></span>

2. <span data-ttu-id="6c539-262">Search for the `<ContentDefinitions>` element, and then copy the entire contents of the `<ContentDefinitions>` node.</span><span class="sxs-lookup"><span data-stu-id="6c539-262">Search for the `<ContentDefinitions>` element, and then copy the entire contents of the `<ContentDefinitions>` node.</span></span>

3. <span data-ttu-id="6c539-263">Open the extension file (for example, *TrustFrameworkExtensions.xml*) and then search for the `<BuildingBlocks>` element.</span><span class="sxs-lookup"><span data-stu-id="6c539-263">Open the extension file (for example, *TrustFrameworkExtensions.xml*) and then search for the `<BuildingBlocks>` element.</span></span> <span data-ttu-id="6c539-264">If the element doesn't exist, add it.</span><span class="sxs-lookup"><span data-stu-id="6c539-264">If the element doesn't exist, add it.</span></span>

4. <span data-ttu-id="6c539-265">Paste the entire contents of the `<ContentDefinitions>` node that you copied as a child of the `<BuildingBlocks>` element.</span><span class="sxs-lookup"><span data-stu-id="6c539-265">Paste the entire contents of the `<ContentDefinitions>` node that you copied as a child of the `<BuildingBlocks>` element.</span></span> 

5. <span data-ttu-id="6c539-266">Search for the `<ContentDefinition>` node that contains `Id="api.signuporsignin"` in the XML that you copied.</span><span class="sxs-lookup"><span data-stu-id="6c539-266">Search for the `<ContentDefinition>` node that contains `Id="api.signuporsignin"` in the XML that you copied.</span></span>

6. <span data-ttu-id="6c539-267">Change the value of `LoadUri` from _~/tenant/default/unified_ to _https://<app_name>.azurewebsites.net/home/unified_.</span><span class="sxs-lookup"><span data-stu-id="6c539-267">Change the value of `LoadUri` from _~/tenant/default/unified_ to _https://<app_name>.azurewebsites.net/home/unified_.</span></span>  
    <span data-ttu-id="6c539-268">Your custom policy should look like the following:</span><span class="sxs-lookup"><span data-stu-id="6c539-268">Your custom policy should look like the following:</span></span>
    
    ![Your content definition](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-content-definition.png)

## <a name="step-6-upload-the-policy-to-your-tenant"></a><span data-ttu-id="6c539-270">Step 6: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="6c539-270">Step 6: Upload the policy to your tenant</span></span>
1. <span data-ttu-id="6c539-271">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="6c539-271">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span></span>

2. <span data-ttu-id="6c539-272">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="6c539-272">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="6c539-273">Select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="6c539-273">Select **All Policies**.</span></span>

4. <span data-ttu-id="6c539-274">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="6c539-274">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="6c539-275">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="6c539-275">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="6c539-276">Upload the *TrustFrameworkExtensions.xml* file, and ensure that it passes validation.</span><span class="sxs-lookup"><span data-stu-id="6c539-276">Upload the *TrustFrameworkExtensions.xml* file, and ensure that it passes validation.</span></span>

## <a name="step-7-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="6c539-277">Step 7: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="6c539-277">Step 7: Test the custom policy by using Run Now</span></span>
1. <span data-ttu-id="6c539-278">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="6c539-278">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6c539-279">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="6c539-279">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="6c539-280">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="6c539-280">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

2. <span data-ttu-id="6c539-281">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="6c539-281">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>  
    <span data-ttu-id="6c539-282">You should be able to see your custom HTML5 with the background that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="6c539-282">You should be able to see your custom HTML5 with the background that you created earlier.</span></span>

    ![Your sign-up or sign-in policy](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-demo1.png)

## <a name="step-8-add-dynamic-content"></a><span data-ttu-id="6c539-284">Step 8: Add dynamic content</span><span class="sxs-lookup"><span data-stu-id="6c539-284">Step 8: Add dynamic content</span></span>
<span data-ttu-id="6c539-285">Change the background based on query string parameter named _campaignId_.</span><span class="sxs-lookup"><span data-stu-id="6c539-285">Change the background based on query string parameter named _campaignId_.</span></span> <span data-ttu-id="6c539-286">Your RP application (web and mobile apps) sends the parameter to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6c539-286">Your RP application (web and mobile apps) sends the parameter to Azure AD B2C.</span></span> <span data-ttu-id="6c539-287">Your policy reads the parameter and sends its value to your HTML5 template.</span><span class="sxs-lookup"><span data-stu-id="6c539-287">Your policy reads the parameter and sends its value to your HTML5 template.</span></span> 

### <a name="step-81-add-a-content-definition-parameter"></a><span data-ttu-id="6c539-288">Step 8.1: Add a content definition parameter</span><span class="sxs-lookup"><span data-stu-id="6c539-288">Step 8.1: Add a content definition parameter</span></span>

<span data-ttu-id="6c539-289">Add the `ContentDefinitionParameters` element by doing the following:</span><span class="sxs-lookup"><span data-stu-id="6c539-289">Add the `ContentDefinitionParameters` element by doing the following:</span></span>
1. <span data-ttu-id="6c539-290">Open the *SignUpOrSignin* file of your policy (for example, *SignUpOrSignin.xml*).</span><span class="sxs-lookup"><span data-stu-id="6c539-290">Open the *SignUpOrSignin* file of your policy (for example, *SignUpOrSignin.xml*).</span></span>

2. <span data-ttu-id="6c539-291">Search for the `<DefaultUserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="6c539-291">Search for the `<DefaultUserJourney>` node.</span></span> 

3. <span data-ttu-id="6c539-292">In the `<DefaultUserJourney>` node, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="6c539-292">In the `<DefaultUserJourney>` node, add the following XML snippet:</span></span>  

    ```XML
    <UserJourneyBehaviors>
        <ContentDefinitionParameters>
            <Parameter Name="campaignId">{OAUTH-KV:campaignId}</Parameter>
        </ContentDefinitionParameters>
    </UserJourneyBehaviors>
    ```

### <a name="step-82-change-your-code-to-accept-a-query-string-parameter-and-replace-the-background-image"></a><span data-ttu-id="6c539-293">Step 8.2: Change your code to accept a query string parameter, and replace the background image</span><span class="sxs-lookup"><span data-stu-id="6c539-293">Step 8.2: Change your code to accept a query string parameter, and replace the background image</span></span>
<span data-ttu-id="6c539-294">Modify the HomeController `unified` method to accept the campaignId parameter.</span><span class="sxs-lookup"><span data-stu-id="6c539-294">Modify the HomeController `unified` method to accept the campaignId parameter.</span></span> <span data-ttu-id="6c539-295">The method then checks the parameter's value and sets the `ViewData["background"]` variable accordingly.</span><span class="sxs-lookup"><span data-stu-id="6c539-295">The method then checks the parameter's value and sets the `ViewData["background"]` variable accordingly.</span></span>

1. <span data-ttu-id="6c539-296">Open the *Controllers\HomeController.cs* file, and then change the `unified` method by adding the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="6c539-296">Open the *Controllers\HomeController.cs* file, and then change the `unified` method by adding the following code snippet:</span></span>

    ```csharp
    public IActionResult unified(string campaignId)
    {
        // If campaign ID is Hawaii, show Hawaii background
        if (campaignId != null && campaignId.ToLower() == "hawaii")
        {
            ViewData["background"] = "https://kbdevstorage1.blob.core.windows.net/asset-blobs/19889_en_1";
        }
        // If campaign ID is Tokyo, show Tokyo background
        else if (campaignId != null && campaignId.ToLower() == "tokyo")
        {
            ViewData["background"] = "https://kbdevstorage1.blob.core.windows.net/asset-blobs/19666_en_1";
        }
        // Default background
        else
        {
            ViewData["background"] = "https://kbdevstorage1.blob.core.windows.net/asset-blobs/18983_en_1";
        }

        return View();
    }

    ```

2. <span data-ttu-id="6c539-297">Locate the `<img>` element with ID `background_background_image`, and replace the `src` value with `@ViewData["background"]`.</span><span class="sxs-lookup"><span data-stu-id="6c539-297">Locate the `<img>` element with ID `background_background_image`, and replace the `src` value with `@ViewData["background"]`.</span></span>

    ![Change the page background](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-add-dynamic-background.png)

### <a name="83-upload-the-changes-and-publish-your-policy"></a><span data-ttu-id="6c539-299">8.3: Upload the changes and publish your policy</span><span class="sxs-lookup"><span data-stu-id="6c539-299">8.3: Upload the changes and publish your policy</span></span>
1. <span data-ttu-id="6c539-300">Publish your Visual Studio project to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6c539-300">Publish your Visual Studio project to Azure App Service.</span></span>

2. <span data-ttu-id="6c539-301">Upload the *SignUpOrSignin.xml* policy to Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6c539-301">Upload the *SignUpOrSignin.xml* policy to Azure AD B2C.</span></span>

3. <span data-ttu-id="6c539-302">Open **B2C_1A_signup_signin**, the RP custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="6c539-302">Open **B2C_1A_signup_signin**, the RP custom policy that you uploaded, and then select **Run now**.</span></span>  
    <span data-ttu-id="6c539-303">You should see the same background image that was previously displayed.</span><span class="sxs-lookup"><span data-stu-id="6c539-303">You should see the same background image that was previously displayed.</span></span>

4. <span data-ttu-id="6c539-304">Copy the URL from the browser's address bar.</span><span class="sxs-lookup"><span data-stu-id="6c539-304">Copy the URL from the browser's address bar.</span></span>

5. <span data-ttu-id="6c539-305">Add the _campaignId_ query string parameter to the URI.</span><span class="sxs-lookup"><span data-stu-id="6c539-305">Add the _campaignId_ query string parameter to the URI.</span></span> <span data-ttu-id="6c539-306">For example, add `&campaignId=hawaii`, as shown in following image:</span><span class="sxs-lookup"><span data-stu-id="6c539-306">For example, add `&campaignId=hawaii`, as shown in following image:</span></span>

    ![Change the page background](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-campaignId-param.png)

6. <span data-ttu-id="6c539-308">Select **Enter** to display the Hawaii background image.</span><span class="sxs-lookup"><span data-stu-id="6c539-308">Select **Enter** to display the Hawaii background image.</span></span>

    ![Change the page background](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-demo2.png)

7. <span data-ttu-id="6c539-310">Change the value to *Tokyo*, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6c539-310">Change the value to *Tokyo*, and then select **Enter**.</span></span>  
    <span data-ttu-id="6c539-311">The browser displays the Tokyo background.</span><span class="sxs-lookup"><span data-stu-id="6c539-311">The browser displays the Tokyo background.</span></span>

    ![Change the page background](media/active-directory-b2c-ui-customization-custom-dynamic/aadb2c-ief-ui-customization-demo3.png)

## <a name="step-9-change-the-rest-of-the-user-journey"></a><span data-ttu-id="6c539-313">Step 9: Change the rest of the user journey</span><span class="sxs-lookup"><span data-stu-id="6c539-313">Step 9: Change the rest of the user journey</span></span>
<span data-ttu-id="6c539-314">If you select the **Sign up now** link on the sign-in page, the browser displays the default background image, not the image you defined.</span><span class="sxs-lookup"><span data-stu-id="6c539-314">If you select the **Sign up now** link on the sign-in page, the browser displays the default background image, not the image you defined.</span></span> <span data-ttu-id="6c539-315">This behavior arises because you've changed only the sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="6c539-315">This behavior arises because you've changed only the sign-up or sign-in page.</span></span> <span data-ttu-id="6c539-316">To change the rest of the Self-Assert content definitions:</span><span class="sxs-lookup"><span data-stu-id="6c539-316">To change the rest of the Self-Assert content definitions:</span></span>
1. <span data-ttu-id="6c539-317">Go back to "Step 2," and do the following:</span><span class="sxs-lookup"><span data-stu-id="6c539-317">Go back to "Step 2," and do the following:</span></span>

    <span data-ttu-id="6c539-318">a.</span><span class="sxs-lookup"><span data-stu-id="6c539-318">a.</span></span> <span data-ttu-id="6c539-319">Download the *selfasserted* file.</span><span class="sxs-lookup"><span data-stu-id="6c539-319">Download the *selfasserted* file.</span></span>

    <span data-ttu-id="6c539-320">b.</span><span class="sxs-lookup"><span data-stu-id="6c539-320">b.</span></span> <span data-ttu-id="6c539-321">Copy the file content.</span><span class="sxs-lookup"><span data-stu-id="6c539-321">Copy the file content.</span></span>

    <span data-ttu-id="6c539-322">c.</span><span class="sxs-lookup"><span data-stu-id="6c539-322">c.</span></span> <span data-ttu-id="6c539-323">Create a new view, *selfasserted*.</span><span class="sxs-lookup"><span data-stu-id="6c539-323">Create a new view, *selfasserted*.</span></span>

    <span data-ttu-id="6c539-324">d.</span><span class="sxs-lookup"><span data-stu-id="6c539-324">d.</span></span> <span data-ttu-id="6c539-325">Add *selfasserted* to the **Home** controller.</span><span class="sxs-lookup"><span data-stu-id="6c539-325">Add *selfasserted* to the **Home** controller.</span></span>

2. <span data-ttu-id="6c539-326">Go back to "Step 4," and do the following:</span><span class="sxs-lookup"><span data-stu-id="6c539-326">Go back to "Step 4," and do the following:</span></span> 

    <span data-ttu-id="6c539-327">a.</span><span class="sxs-lookup"><span data-stu-id="6c539-327">a.</span></span> <span data-ttu-id="6c539-328">In your extension policy, find the `<ContentDefinition>` node that contains `Id="api.selfasserted"`, `Id="api.localaccountsignup"`, and `Id="api.localaccountpasswordreset"`.</span><span class="sxs-lookup"><span data-stu-id="6c539-328">In your extension policy, find the `<ContentDefinition>` node that contains `Id="api.selfasserted"`, `Id="api.localaccountsignup"`, and `Id="api.localaccountpasswordreset"`.</span></span>

    <span data-ttu-id="6c539-329">b.</span><span class="sxs-lookup"><span data-stu-id="6c539-329">b.</span></span> <span data-ttu-id="6c539-330">Set the `LoadUri` attribute to your *selfasserted* URI.</span><span class="sxs-lookup"><span data-stu-id="6c539-330">Set the `LoadUri` attribute to your *selfasserted* URI.</span></span>

3. <span data-ttu-id="6c539-331">Go back to "Step 8.2," and change your code to accept query string parameters, but this time to the *selfasserted* function.</span><span class="sxs-lookup"><span data-stu-id="6c539-331">Go back to "Step 8.2," and change your code to accept query string parameters, but this time to the *selfasserted* function.</span></span> 

4. <span data-ttu-id="6c539-332">Upload the *TrustFrameworkExtensions.xml* policy, and ensure that it passes validation.</span><span class="sxs-lookup"><span data-stu-id="6c539-332">Upload the *TrustFrameworkExtensions.xml* policy, and ensure that it passes validation.</span></span>

5. <span data-ttu-id="6c539-333">Run the policy test, and then select **Sign up now** to see the result.</span><span class="sxs-lookup"><span data-stu-id="6c539-333">Run the policy test, and then select **Sign up now** to see the result.</span></span>

## <a name="optional-download-the-complete-policy-files-and-code"></a><span data-ttu-id="6c539-334">(Optional) Download the complete policy files and code</span><span class="sxs-lookup"><span data-stu-id="6c539-334">(Optional) Download the complete policy files and code</span></span>
* <span data-ttu-id="6c539-335">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="6c539-335">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="6c539-336">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-ui-customization).</span><span class="sxs-lookup"><span data-stu-id="6c539-336">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-ui-customization).</span></span>
* <span data-ttu-id="6c539-337">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-ui-customization).</span><span class="sxs-lookup"><span data-stu-id="6c539-337">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-ui-customization).</span></span>




