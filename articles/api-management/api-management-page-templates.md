---
title: Page templates in Azure API Management | Microsoft Docs
description: Learn how to customize the content of developer portal pages using a set of templates in Azure API Management.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f9c23978c2d700da45fe21fcd8cdc395059bf27e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563084"
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="c2f0d-103">Page templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c2f0d-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="c2f0d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="c2f0d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="c2f0d-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="c2f0d-107">Sign in</span><span class="sxs-lookup"><span data-stu-id="c2f0d-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="c2f0d-108">Sign up</span><span class="sxs-lookup"><span data-stu-id="c2f0d-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="c2f0d-109">Page not found</span><span class="sxs-lookup"><span data-stu-id="c2f0d-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="c2f0d-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="c2f0d-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="c2f0d-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="c2f0d-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <a name="SignIn"></a> <span data-ttu-id="c2f0d-113">Sign in</span><span class="sxs-lookup"><span data-stu-id="c2f0d-113">Sign in</span></span>  
 <span data-ttu-id="c2f0d-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="c2f0d-115">![Sign In Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-templates/apim-sign-in-page-developer-portal-templates.png "APIM Sign In Page Developer Portal Templates")</span><span class="sxs-lookup"><span data-stu-id="c2f0d-115">![Sign In Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-templates/apim-sign-in-page-developer-portal-templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c2f0d-116">Default template</span><span class="sxs-lookup"><span data-stu-id="c2f0d-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="c2f0d-117">Controls</span><span class="sxs-lookup"><span data-stu-id="c2f0d-117">Controls</span></span>  
 <span data-ttu-id="c2f0d-118">This template may  use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c2f0d-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="c2f0d-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="c2f0d-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="c2f0d-120">providers</span><span class="sxs-lookup"><span data-stu-id="c2f0d-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="c2f0d-121">Data model</span><span class="sxs-lookup"><span data-stu-id="c2f0d-121">Data model</span></span>  
 <span data-ttu-id="c2f0d-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="c2f0d-123">Sample template data</span><span class="sxs-lookup"><span data-stu-id="c2f0d-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <a name="SignUp"></a> <span data-ttu-id="c2f0d-124">Sign up</span><span class="sxs-lookup"><span data-stu-id="c2f0d-124">Sign up</span></span>  
 <span data-ttu-id="c2f0d-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="c2f0d-126">![Sign Up Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-templates/apim-sign-up-page-developer-portal-templates.png "APIM Sign Up Page Developer Portal Templates")</span><span class="sxs-lookup"><span data-stu-id="c2f0d-126">![Sign Up Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-templates/apim-sign-up-page-developer-portal-templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c2f0d-127">Default template</span><span class="sxs-lookup"><span data-stu-id="c2f0d-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="c2f0d-128">Controls</span><span class="sxs-lookup"><span data-stu-id="c2f0d-128">Controls</span></span>  
 <span data-ttu-id="c2f0d-129">This template may  use the following [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c2f0d-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="c2f0d-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="c2f0d-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="c2f0d-131">Data model</span><span class="sxs-lookup"><span data-stu-id="c2f0d-131">Data model</span></span>  
 <span data-ttu-id="c2f0d-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="c2f0d-133">Sample template data</span><span class="sxs-lookup"><span data-stu-id="c2f0d-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <a name="PageNotFound"></a> <span data-ttu-id="c2f0d-134">Page not found</span><span class="sxs-lookup"><span data-stu-id="c2f0d-134">Page not found</span></span>  
 <span data-ttu-id="c2f0d-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="c2f0d-136">![Not Found Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-templates/apim-not-found-page-developer-portal-templates.png "APIM Not Found Page Developer Portal Templates")</span><span class="sxs-lookup"><span data-stu-id="c2f0d-136">![Not Found Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-page-templates/apim-not-found-page-developer-portal-templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="c2f0d-137">Default template</span><span class="sxs-lookup"><span data-stu-id="c2f0d-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="c2f0d-138">Controls</span><span class="sxs-lookup"><span data-stu-id="c2f0d-138">Controls</span></span>  
 <span data-ttu-id="c2f0d-139">This template may  not use any [page controls](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="c2f0d-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="c2f0d-140">Data model</span><span class="sxs-lookup"><span data-stu-id="c2f0d-140">Data model</span></span>  
  
|<span data-ttu-id="c2f0d-141">Property</span><span class="sxs-lookup"><span data-stu-id="c2f0d-141">Property</span></span>|<span data-ttu-id="c2f0d-142">Type</span><span class="sxs-lookup"><span data-stu-id="c2f0d-142">Type</span></span>|<span data-ttu-id="c2f0d-143">Description</span><span class="sxs-lookup"><span data-stu-id="c2f0d-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="c2f0d-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="c2f0d-144">referenceCode</span></span>|<span data-ttu-id="c2f0d-145">string</span><span class="sxs-lookup"><span data-stu-id="c2f0d-145">string</span></span>|<span data-ttu-id="c2f0d-146">Code generated if this page was displayed as the result of an internal error.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="c2f0d-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="c2f0d-147">errorCode</span></span>|<span data-ttu-id="c2f0d-148">string</span><span class="sxs-lookup"><span data-stu-id="c2f0d-148">string</span></span>|<span data-ttu-id="c2f0d-149">Code generated if this page was displayed as the result of an internal error.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="c2f0d-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="c2f0d-150">emailBody</span></span>|<span data-ttu-id="c2f0d-151">string</span><span class="sxs-lookup"><span data-stu-id="c2f0d-151">string</span></span>|<span data-ttu-id="c2f0d-152">Email body generated if this page was displayed as the result of an internal error.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="c2f0d-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="c2f0d-153">requestedUrl</span></span>|<span data-ttu-id="c2f0d-154">string</span><span class="sxs-lookup"><span data-stu-id="c2f0d-154">string</span></span>|<span data-ttu-id="c2f0d-155">The URL requested when the page was not found.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="c2f0d-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="c2f0d-156">referrerUrl</span></span>|<span data-ttu-id="c2f0d-157">string</span><span class="sxs-lookup"><span data-stu-id="c2f0d-157">string</span></span>|<span data-ttu-id="c2f0d-158">The referrer URL to the requested URL.</span><span class="sxs-lookup"><span data-stu-id="c2f0d-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="c2f0d-159">Sample template data</span><span class="sxs-lookup"><span data-stu-id="c2f0d-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="c2f0d-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2f0d-160">Next steps</span></span>
<span data-ttu-id="c2f0d-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c2f0d-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>


