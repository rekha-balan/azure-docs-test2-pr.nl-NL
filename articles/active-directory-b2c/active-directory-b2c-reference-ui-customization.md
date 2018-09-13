---
title: 'Azure Active Directory B2C: User interface (UI) customization | Microsoft Docs'
description: A topic on the user interface (UI) customization features in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: c995e0de46c67c5c5d243739b2d36266267bdade
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564035"
---
# <a name="azure-active-directory-b2c-customize-the-azure-ad-b2c-user-interface-ui"></a><span data-ttu-id="9c690-103">Azure Active Directory B2C: Customize the Azure AD B2C user interface (UI)</span><span class="sxs-lookup"><span data-stu-id="9c690-103">Azure Active Directory B2C: Customize the Azure AD B2C user interface (UI)</span></span>
<span data-ttu-id="9c690-104">User experience is paramount in a consumer-facing application.</span><span class="sxs-lookup"><span data-stu-id="9c690-104">User experience is paramount in a consumer-facing application.</span></span> <span data-ttu-id="9c690-105">It is the difference between a good application and a great one, and between merely active consumers and truly engaged ones.</span><span class="sxs-lookup"><span data-stu-id="9c690-105">It is the difference between a good application and a great one, and between merely active consumers and truly engaged ones.</span></span> <span data-ttu-id="9c690-106">Azure Active Directory (Azure AD) B2C lets you customize consumer sign-up, sign-in (*see note below*), profile editing, and  password reset pages with pixel-perfect control.</span><span class="sxs-lookup"><span data-stu-id="9c690-106">Azure Active Directory (Azure AD) B2C lets you customize consumer sign-up, sign-in (*see note below*), profile editing, and  password reset pages with pixel-perfect control.</span></span>

> [!NOTE]
> <span data-ttu-id="9c690-107">Currently, local account sign-in pages, its accompaning password reset pages and verification emails can be customized only by using the [company branding feature](../active-directory/active-directory-add-company-branding.md) and not by the mechanisms described in this article.</span><span class="sxs-lookup"><span data-stu-id="9c690-107">Currently, local account sign-in pages, its accompaning password reset pages and verification emails can be customized only by using the [company branding feature](../active-directory/active-directory-add-company-branding.md) and not by the mechanisms described in this article.</span></span>
> 
> 

<span data-ttu-id="9c690-108">In this article, you will read about:</span><span class="sxs-lookup"><span data-stu-id="9c690-108">In this article, you will read about:</span></span>

* <span data-ttu-id="9c690-109">The page user interface (UI) customization feature.</span><span class="sxs-lookup"><span data-stu-id="9c690-109">The page user interface (UI) customization feature.</span></span>
* <span data-ttu-id="9c690-110">A tool that will help you test the page UI customization feature using our sample content.</span><span class="sxs-lookup"><span data-stu-id="9c690-110">A tool that will help you test the page UI customization feature using our sample content.</span></span>
* <span data-ttu-id="9c690-111">The core UI elements in each type of page.</span><span class="sxs-lookup"><span data-stu-id="9c690-111">The core UI elements in each type of page.</span></span>
* <span data-ttu-id="9c690-112">Best practices when exercising this feature.</span><span class="sxs-lookup"><span data-stu-id="9c690-112">Best practices when exercising this feature.</span></span>

## <a name="the-page-ui-customization-feature"></a><span data-ttu-id="9c690-113">The page UI customization feature</span><span class="sxs-lookup"><span data-stu-id="9c690-113">The page UI customization feature</span></span>
<span data-ttu-id="9c690-114">With the page UI customization feature, you can customize the look and feel of consumer sign-up, sign-in, password reset and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span><span class="sxs-lookup"><span data-stu-id="9c690-114">With the page UI customization feature, you can customize the look and feel of consumer sign-up, sign-in, password reset and profile-editing pages (by configuring [policies](active-directory-b2c-reference-policies.md)).</span></span> <span data-ttu-id="9c690-115">Your consumers will have seamless experiences when navigating between your application and pages served by Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="9c690-115">Your consumers will have seamless experiences when navigating between your application and pages served by Azure AD B2C.</span></span>

<span data-ttu-id="9c690-116">Unlike other services where UI options are limited or are only available via APIs, Azure AD B2C uses a modern (and simpler) approach to page UI customization.</span><span class="sxs-lookup"><span data-stu-id="9c690-116">Unlike other services where UI options are limited or are only available via APIs, Azure AD B2C uses a modern (and simpler) approach to page UI customization.</span></span>

<span data-ttu-id="9c690-117">Here's how it works: Azure AD B2C runs code in your consumer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/) to load content from a URL that you specify in a policy.</span><span class="sxs-lookup"><span data-stu-id="9c690-117">Here's how it works: Azure AD B2C runs code in your consumer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/) to load content from a URL that you specify in a policy.</span></span> <span data-ttu-id="9c690-118">You can specify different URLs for different pages.</span><span class="sxs-lookup"><span data-stu-id="9c690-118">You can specify different URLs for different pages.</span></span> <span data-ttu-id="9c690-119">The code merges UI elements from Azure AD B2C with the content loaded from your URL, and displays the page to your consumer.</span><span class="sxs-lookup"><span data-stu-id="9c690-119">The code merges UI elements from Azure AD B2C with the content loaded from your URL, and displays the page to your consumer.</span></span> <span data-ttu-id="9c690-120">All you need to do is:</span><span class="sxs-lookup"><span data-stu-id="9c690-120">All you need to do is:</span></span>

1. <span data-ttu-id="9c690-121">Create well-formed HTML5 content with a `<div id="api"></div>` element (needs to be an empty element) located somewhere in the `<body>`.</span><span class="sxs-lookup"><span data-stu-id="9c690-121">Create well-formed HTML5 content with a `<div id="api"></div>` element (needs to be an empty element) located somewhere in the `<body>`.</span></span> <span data-ttu-id="9c690-122">This element marks where the Azure AD B2C content is inserted.</span><span class="sxs-lookup"><span data-stu-id="9c690-122">This element marks where the Azure AD B2C content is inserted.</span></span>
2. <span data-ttu-id="9c690-123">Host your content on an HTTPS endpoint (with CORS allowed).</span><span class="sxs-lookup"><span data-stu-id="9c690-123">Host your content on an HTTPS endpoint (with CORS allowed).</span></span> <span data-ttu-id="9c690-124">Note that you will need to enable both GET and OPTIONS request methods when configuring CORS.</span><span class="sxs-lookup"><span data-stu-id="9c690-124">Note that you will need to enable both GET and OPTIONS request methods when configuring CORS.</span></span>
3. <span data-ttu-id="9c690-125">Style the UI elements that Azure AD B2C inserts in.</span><span class="sxs-lookup"><span data-stu-id="9c690-125">Style the UI elements that Azure AD B2C inserts in.</span></span>

## <a name="test-out-the-ui-customization-feature"></a><span data-ttu-id="9c690-126">Test out the UI customization feature</span><span class="sxs-lookup"><span data-stu-id="9c690-126">Test out the UI customization feature</span></span>
<span data-ttu-id="9c690-127">If you want to try out the UI customization feature by using our sample HTML and CSS content, we've provided you [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c690-127">If you want to try out the UI customization feature by using our sample HTML and CSS content, we've provided you [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures sample content on your Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="9c690-128">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as the content is hosted on a publicly-available HTTPS endpoint (with CORS allowed), you are good to go.</span><span class="sxs-lookup"><span data-stu-id="9c690-128">You can host your UI content anywhere: on web servers, CDNs, AWS S3, file sharing systems, etc. As long as the content is hosted on a publicly-available HTTPS endpoint (with CORS allowed), you are good to go.</span></span> <span data-ttu-id="9c690-129">We are using Azure Blob storage for illustrative purposes only.</span><span class="sxs-lookup"><span data-stu-id="9c690-129">We are using Azure Blob storage for illustrative purposes only.</span></span>
> 
> 

### <a name="the-most-basic-html-content-for-testing"></a><span data-ttu-id="9c690-130">The most basic HTML content for testing</span><span class="sxs-lookup"><span data-stu-id="9c690-130">The most basic HTML content for testing</span></span>
<span data-ttu-id="9c690-131">Shown below is the most basic HTML content that you can use to test this capability.</span><span class="sxs-lookup"><span data-stu-id="9c690-131">Shown below is the most basic HTML content that you can use to test this capability.</span></span> <span data-ttu-id="9c690-132">Use the same helper tool provided earlier to upload and configure this content on your Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="9c690-132">Use the same helper tool provided earlier to upload and configure this content on your Azure Blob storage.</span></span> <span data-ttu-id="9c690-133">You can then verify that the basic, non-stylized buttons & form fields on each page are displayed and functional.</span><span class="sxs-lookup"><span data-stu-id="9c690-133">You can then verify that the basic, non-stylized buttons & form fields on each page are displayed and functional.</span></span>

```HTML

<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>    <!-- IMP: This element is intentionally empty; don't enter anything here -->
    </body>
</html>

```

## <a name="the-core-ui-elements-in-each-type-of-page"></a><span data-ttu-id="9c690-134">The core UI elements in each type of page</span><span class="sxs-lookup"><span data-stu-id="9c690-134">The core UI elements in each type of page</span></span>
<span data-ttu-id="9c690-135">In the following sections, you will find examples of HTML5 fragments that Azure AD B2C merges into the `<div id="api"></div>` element located in your content.</span><span class="sxs-lookup"><span data-stu-id="9c690-135">In the following sections, you will find examples of HTML5 fragments that Azure AD B2C merges into the `<div id="api"></div>` element located in your content.</span></span> <span data-ttu-id="9c690-136">**Do not insert these fragments in your HTML 5 content.**</span><span class="sxs-lookup"><span data-stu-id="9c690-136">**Do not insert these fragments in your HTML 5 content.**</span></span> <span data-ttu-id="9c690-137">The Azure AD B2C service inserts them in at run-time.</span><span class="sxs-lookup"><span data-stu-id="9c690-137">The Azure AD B2C service inserts them in at run-time.</span></span> <span data-ttu-id="9c690-138">Use these examples to design your own style sheets.</span><span class="sxs-lookup"><span data-stu-id="9c690-138">Use these examples to design your own style sheets.</span></span>

### <a name="azure-ad-b2c-content-inserted-into-the-identity-provider-selection-page"></a><span data-ttu-id="9c690-139">Azure AD B2C content inserted into the "Identity provider selection page"</span><span class="sxs-lookup"><span data-stu-id="9c690-139">Azure AD B2C content inserted into the "Identity provider selection page"</span></span>
<span data-ttu-id="9c690-140">This page contains a list of identity providers that the user can choose from during sign-up or sign-in.</span><span class="sxs-lookup"><span data-stu-id="9c690-140">This page contains a list of identity providers that the user can choose from during sign-up or sign-in.</span></span> <span data-ttu-id="9c690-141">These are either social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span><span class="sxs-lookup"><span data-stu-id="9c690-141">These are either social identity providers such as Facebook and Google+, or local accounts (based on email address or user name).</span></span>

```HTML

<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>

```

### <a name="azure-ad-b2c-content-inserted-into-the-local-account-sign-up-page"></a><span data-ttu-id="9c690-142">Azure AD B2C content inserted into the "Local account sign-up page"</span><span class="sxs-lookup"><span data-stu-id="9c690-142">Azure AD B2C content inserted into the "Local account sign-up page"</span></span>
<span data-ttu-id="9c690-143">This page contains a sign-up form that the user has to fill in when signing up for a local account that is based on an email address or a user name.</span><span class="sxs-lookup"><span data-stu-id="9c690-143">This page contains a sign-up form that the user has to fill in when signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="9c690-144">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span><span class="sxs-lookup"><span data-stu-id="9c690-144">The form can contain different input controls such as text input box, password entry box, radio button, single-select drop-down boxes, and multi-select check boxes.</span></span>

```HTML

<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing the following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">The password entry fields do not match. Please enter the same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent to your inbox. Please copy it to the input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need to send new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used to contact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of the following: Lowercase characters, uppercase characters, digits (0-9), and one or more of the following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('The postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>

```

### <a name="azure-ad-b2c-content-inserted-into-the-social-account-sign-up-page"></a><span data-ttu-id="9c690-145">Azure AD B2C content inserted into the ""Social account sign-up page"</span><span class="sxs-lookup"><span data-stu-id="9c690-145">Azure AD B2C content inserted into the ""Social account sign-up page"</span></span>
<span data-ttu-id="9c690-146">This page contains a sign-up form that the consumer has to fill in when signing up using an existing account from a social identity provider such as Facebook or Google+.</span><span class="sxs-lookup"><span data-stu-id="9c690-146">This page contains a sign-up form that the consumer has to fill in when signing up using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="9c690-147">This page is similar to the local account sign-up page (shown in the previous section) with the exception of the password entry fields.</span><span class="sxs-lookup"><span data-stu-id="9c690-147">This page is similar to the local account sign-up page (shown in the previous section) with the exception of the password entry fields.</span></span>

### <a name="azure-ad-b2c-content-inserted-into-the-unified-sign-up-or-sign-in-page"></a><span data-ttu-id="9c690-148">Azure AD B2C content inserted into the "Unified sign-up or sign-in page"</span><span class="sxs-lookup"><span data-stu-id="9c690-148">Azure AD B2C content inserted into the "Unified sign-up or sign-in page"</span></span>
<span data-ttu-id="9c690-149">This page handles both sign-up & sign-in of consumers, who can use social identity providers such as Facebook or Google+, or local accounts.</span><span class="sxs-lookup"><span data-stu-id="9c690-149">This page handles both sign-up & sign-in of consumers, who can use social identity providers such as Facebook or Google+, or local accounts.</span></span>

```HTML

<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>

```

### <a name="azure-ad-b2c-content-inserted-into-the-multi-factor-authentication-page"></a><span data-ttu-id="9c690-150">Azure AD B2C content inserted into the "Multi-factor authentication page"</span><span class="sxs-lookup"><span data-stu-id="9c690-150">Azure AD B2C content inserted into the "Multi-factor authentication page"</span></span>
<span data-ttu-id="9c690-151">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span><span class="sxs-lookup"><span data-stu-id="9c690-151">On this page, users can verify their phone numbers (using text or voice) during sign-up or sign-in.</span></span>

```HTML

<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone to authenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>

```

### <a name="azure-ad-b2c-content-inserted-into-the-error-page"></a><span data-ttu-id="9c690-152">Azure AD B2C content inserted into the ""Error page"</span><span class="sxs-lookup"><span data-stu-id="9c690-152">Azure AD B2C content inserted into the ""Error page"</span></span>
```HTML

<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if the problem persists feel free to contact us. In the meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting the remote resource.</div>
    </div>
</div>

```

## <a name="things-to-remember-when-building-your-own-content"></a><span data-ttu-id="9c690-153">Things to remember when building your own content</span><span class="sxs-lookup"><span data-stu-id="9c690-153">Things to remember when building your own content</span></span>
<span data-ttu-id="9c690-154">If you are planning to use the page UI customization feature, review the following best practices:</span><span class="sxs-lookup"><span data-stu-id="9c690-154">If you are planning to use the page UI customization feature, review the following best practices:</span></span>

* <span data-ttu-id="9c690-155">Don't copy the Azure AD B2C's default content and attempt to modify it.</span><span class="sxs-lookup"><span data-stu-id="9c690-155">Don't copy the Azure AD B2C's default content and attempt to modify it.</span></span> <span data-ttu-id="9c690-156">It is best to build your HTML5 content from scratch and to use default content as reference.</span><span class="sxs-lookup"><span data-stu-id="9c690-156">It is best to build your HTML5 content from scratch and to use default content as reference.</span></span>
* <span data-ttu-id="9c690-157">In all the pages (except the Error pages) served by the Sign-in, Sign-up and Profile-editing policies, style sheets that you provide will have to override the default style sheets that we add into these pages in the <head> fragments.</span><span class="sxs-lookup"><span data-stu-id="9c690-157">In all the pages (except the Error pages) served by the Sign-in, Sign-up and Profile-editing policies, style sheets that you provide will have to override the default style sheets that we add into these pages in the <head> fragments.</span></span> <span data-ttu-id="9c690-158">In all the pages served by the Sign-up or Sign-in and Password reset policies, and the Error pages on all policies, you will have to provide all the styling yourself.</span><span class="sxs-lookup"><span data-stu-id="9c690-158">In all the pages served by the Sign-up or Sign-in and Password reset policies, and the Error pages on all policies, you will have to provide all the styling yourself.</span></span>
* <span data-ttu-id="9c690-159">For security reasons, we don't allow you to include any JavaScript in your content.</span><span class="sxs-lookup"><span data-stu-id="9c690-159">For security reasons, we don't allow you to include any JavaScript in your content.</span></span> <span data-ttu-id="9c690-160">Most of what you need should be available out of the box.</span><span class="sxs-lookup"><span data-stu-id="9c690-160">Most of what you need should be available out of the box.</span></span> <span data-ttu-id="9c690-161">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) to request new functionality.</span><span class="sxs-lookup"><span data-stu-id="9c690-161">If not, use [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) to request new functionality.</span></span>
* <span data-ttu-id="9c690-162">Supported browser versions:</span><span class="sxs-lookup"><span data-stu-id="9c690-162">Supported browser versions:</span></span>
  * <span data-ttu-id="9c690-163">Internet Explorer 11, 10, Edge</span><span class="sxs-lookup"><span data-stu-id="9c690-163">Internet Explorer 11, 10, Edge</span></span>
  * <span data-ttu-id="9c690-164">Limited support for Internet Explorer 9, 8</span><span class="sxs-lookup"><span data-stu-id="9c690-164">Limited support for Internet Explorer 9, 8</span></span>
  * <span data-ttu-id="9c690-165">Google Chrome 42.0 and above</span><span class="sxs-lookup"><span data-stu-id="9c690-165">Google Chrome 42.0 and above</span></span>
  * <span data-ttu-id="9c690-166">Mozilla Firefox 38.0 and above</span><span class="sxs-lookup"><span data-stu-id="9c690-166">Mozilla Firefox 38.0 and above</span></span>
