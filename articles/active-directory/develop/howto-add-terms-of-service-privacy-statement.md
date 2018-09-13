---
title: Terms of Service and privacy statement for Azure AD apps | Microsoft Docs
description: Learn how you can configure the terms of service and privacy statement for apps registered to use Azure AD.
services: active-directory
documentationcenter: dev-center-name
author: CelesteDG
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/23/2018
ms.author: celested
ms.reviwer: lenalepa, sureshja
ms.custom: aaddev
ms.openlocfilehash: cb05139241f92eb930a99c387e2f06cabac35caf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855775"
---
# <a name="terms-of-service-and-privacy-statement-for-registered-azure-active-directory-apps"></a><span data-ttu-id="475f8-103">Terms of service and privacy statement for registered Azure Active Directory apps</span><span class="sxs-lookup"><span data-stu-id="475f8-103">Terms of service and privacy statement for registered Azure Active Directory apps</span></span>

<span data-ttu-id="475f8-104">Developers who build and manage apps that integrate with Azure Active Directory (Azure AD) and Microsoft accounts should include links to the app's terms of service and privacy statement.</span><span class="sxs-lookup"><span data-stu-id="475f8-104">Developers who build and manage apps that integrate with Azure Active Directory (Azure AD) and Microsoft accounts should include links to the app's terms of service and privacy statement.</span></span> <span data-ttu-id="475f8-105">The terms of service and privacy statement are surfaced to users through the user consent experience.</span><span class="sxs-lookup"><span data-stu-id="475f8-105">The terms of service and privacy statement are surfaced to users through the user consent experience.</span></span> <span data-ttu-id="475f8-106">They help your users know that they can trust your app.</span><span class="sxs-lookup"><span data-stu-id="475f8-106">They help your users know that they can trust your app.</span></span> <span data-ttu-id="475f8-107">The terms of service and privacy statement are especially critical for user-facing multi-tenant apps--apps that are used by multiple directories or are available to any Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="475f8-107">The terms of service and privacy statement are especially critical for user-facing multi-tenant apps--apps that are used by multiple directories or are available to any Microsoft account.</span></span>

<span data-ttu-id="475f8-108">You are responsible for creating the terms of service and privacy statement documents for your app, and for providing the URLs to these documents.</span><span class="sxs-lookup"><span data-stu-id="475f8-108">You are responsible for creating the terms of service and privacy statement documents for your app, and for providing the URLs to these documents.</span></span> <span data-ttu-id="475f8-109">For multi-tenant apps that fail to provide these links, the user consent experience for your app will show an alert, which may discourage users from consenting to your app.</span><span class="sxs-lookup"><span data-stu-id="475f8-109">For multi-tenant apps that fail to provide these links, the user consent experience for your app will show an alert, which may discourage users from consenting to your app.</span></span>

> [!NOTE]
> * <span data-ttu-id="475f8-110">Single-tenant apps will not show an alert.</span><span class="sxs-lookup"><span data-stu-id="475f8-110">Single-tenant apps will not show an alert.</span></span>
> * <span data-ttu-id="475f8-111">If one or both of the two links are missing, your app will show an alert.</span><span class="sxs-lookup"><span data-stu-id="475f8-111">If one or both of the two links are missing, your app will show an alert.</span></span>

## <a name="user-consent-experience"></a><span data-ttu-id="475f8-112">User consent experience</span><span class="sxs-lookup"><span data-stu-id="475f8-112">User consent experience</span></span>

<span data-ttu-id="475f8-113">The following examples show the user consent experience when the terms of service and privacy statement are configured and when these links are not configured.</span><span class="sxs-lookup"><span data-stu-id="475f8-113">The following examples show the user consent experience when the terms of service and privacy statement are configured and when these links are not configured.</span></span>

![Screenshots with and without a privacy statement and terms of service provided](./media/howto-add-terms-of-service-privacy-statement/user-consent-exp-privacy-statement-terms-service.png)

## <a name="formatting-links-to-the-terms-of-service-and-privacy-statement-documents"></a><span data-ttu-id="475f8-115">Formatting links to the terms of service and privacy statement documents</span><span class="sxs-lookup"><span data-stu-id="475f8-115">Formatting links to the terms of service and privacy statement documents</span></span>

<span data-ttu-id="475f8-116">Before you add links to your app's terms of service and privacy statement documents, make sure the URLs follow these guidelines.</span><span class="sxs-lookup"><span data-stu-id="475f8-116">Before you add links to your app's terms of service and privacy statement documents, make sure the URLs follow these guidelines.</span></span>

| <span data-ttu-id="475f8-117">Guideline</span><span class="sxs-lookup"><span data-stu-id="475f8-117">Guideline</span></span>     | <span data-ttu-id="475f8-118">Description</span><span class="sxs-lookup"><span data-stu-id="475f8-118">Description</span></span>                           |
|---------------|---------------------------------------|
| <span data-ttu-id="475f8-119">Format</span><span class="sxs-lookup"><span data-stu-id="475f8-119">Format</span></span>        | <span data-ttu-id="475f8-120">Valid URL</span><span class="sxs-lookup"><span data-stu-id="475f8-120">Valid URL</span></span>                             |
| <span data-ttu-id="475f8-121">Valid schemas</span><span class="sxs-lookup"><span data-stu-id="475f8-121">Valid schemas</span></span> | <span data-ttu-id="475f8-122">HTTP and HTTPS</span><span class="sxs-lookup"><span data-stu-id="475f8-122">HTTP and HTTPS</span></span></br><span data-ttu-id="475f8-123">We recommend HTTPS</span><span class="sxs-lookup"><span data-stu-id="475f8-123">We recommend HTTPS</span></span> |
| <span data-ttu-id="475f8-124">Max length</span><span class="sxs-lookup"><span data-stu-id="475f8-124">Max length</span></span>    | <span data-ttu-id="475f8-125">2048 characters</span><span class="sxs-lookup"><span data-stu-id="475f8-125">2048 characters</span></span>                       |

<span data-ttu-id="475f8-126">Examples: `https://myapp.com/terms-of-service` and `https://myapp.com/privacy-statement`</span><span class="sxs-lookup"><span data-stu-id="475f8-126">Examples: `https://myapp.com/terms-of-service` and `https://myapp.com/privacy-statement`</span></span>

## <a name="adding-links-to-the-terms-of-service-and-privacy-statement"></a><span data-ttu-id="475f8-127">Adding links to the terms of service and privacy statement</span><span class="sxs-lookup"><span data-stu-id="475f8-127">Adding links to the terms of service and privacy statement</span></span>

<span data-ttu-id="475f8-128">When the terms of service and privacy statement are ready, you can add links to these documents in your app using one of these methods:</span><span class="sxs-lookup"><span data-stu-id="475f8-128">When the terms of service and privacy statement are ready, you can add links to these documents in your app using one of these methods:</span></span>
* [<span data-ttu-id="475f8-129">Through the Azure portal</span><span class="sxs-lookup"><span data-stu-id="475f8-129">Through the Azure portal</span></span>](#registered-in-azure-portal)
* [<span data-ttu-id="475f8-130">In the Application Registration Portal, or Dev Center</span><span class="sxs-lookup"><span data-stu-id="475f8-130">In the Application Registration Portal, or Dev Center</span></span>](#registered-in-app-reg-portal)
* [<span data-ttu-id="475f8-131">Using the app object JSON</span><span class="sxs-lookup"><span data-stu-id="475f8-131">Using the app object JSON</span></span>](#app-object-json)
* [<span data-ttu-id="475f8-132">Using the MSGraph beta REST API</span><span class="sxs-lookup"><span data-stu-id="475f8-132">Using the MSGraph beta REST API</span></span>](#msgraph-beta-rest-api)

### <a name="registered-in-azure-portal"></a><span data-ttu-id="475f8-133">If you registered your app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="475f8-133">If you registered your app in the Azure portal</span></span>
<span data-ttu-id="475f8-134">Follow these steps if you registered your app in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="475f8-134">Follow these steps if you registered your app in the Azure portal.</span></span>

1. <span data-ttu-id="475f8-135">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="475f8-135">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="475f8-136">Navigate to the **App Registrations** section and select your app.</span><span class="sxs-lookup"><span data-stu-id="475f8-136">Navigate to the **App Registrations** section and select your app.</span></span>
3. <span data-ttu-id="475f8-137">Open the **Properties** section of the app.</span><span class="sxs-lookup"><span data-stu-id="475f8-137">Open the **Properties** section of the app.</span></span>
4. <span data-ttu-id="475f8-138">Fill out the **Terms of Service URL** and **Privacy Statement URL** fields.</span><span class="sxs-lookup"><span data-stu-id="475f8-138">Fill out the **Terms of Service URL** and **Privacy Statement URL** fields.</span></span>
5. <span data-ttu-id="475f8-139">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="475f8-139">Save your changes.</span></span>

![App properties section with terms of service and privacy statement URLs](./media/howto-add-terms-of-service-privacy-statement/azure-portal-terms-service-privacy-statement-urls.png)

### <a name="registered-in-app-reg-portal"></a><span data-ttu-id="475f8-141">If you registered your app in the Application Registration Portal</span><span class="sxs-lookup"><span data-stu-id="475f8-141">If you registered your app in the Application Registration Portal</span></span>
<span data-ttu-id="475f8-142">Follow these steps if you registered your app in the Application Registration Portal or Dev Center.</span><span class="sxs-lookup"><span data-stu-id="475f8-142">Follow these steps if you registered your app in the Application Registration Portal or Dev Center.</span></span>

1. <span data-ttu-id="475f8-143">Sign in to the [Application Registration Portal](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="475f8-143">Sign in to the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
2. <span data-ttu-id="475f8-144">Select your app and scroll to the **Profile** section.</span><span class="sxs-lookup"><span data-stu-id="475f8-144">Select your app and scroll to the **Profile** section.</span></span>
3. <span data-ttu-id="475f8-145">Fill out the **Terms of Service URL** and **Privacy Statement URL** fields.</span><span class="sxs-lookup"><span data-stu-id="475f8-145">Fill out the **Terms of Service URL** and **Privacy Statement URL** fields.</span></span>
4. <span data-ttu-id="475f8-146">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="475f8-146">Save your changes.</span></span>

![App profile section with terms of service and privacy statement URLs](./media/howto-add-terms-of-service-privacy-statement/app-registration-portal-profile-terms-service-privacy-statement-urls.png)

### <a name="app-object-json"></a><span data-ttu-id="475f8-148">Using the app object JSON</span><span class="sxs-lookup"><span data-stu-id="475f8-148">Using the app object JSON</span></span>
<span data-ttu-id="475f8-149">If you prefer to modify the app object JSON directly, you can use the manifest editor in the Azure portal or Application Registration Portal to include links to your app's terms of service and privacy statement.</span><span class="sxs-lookup"><span data-stu-id="475f8-149">If you prefer to modify the app object JSON directly, you can use the manifest editor in the Azure portal or Application Registration Portal to include links to your app's terms of service and privacy statement.</span></span>

```json
    "informationalUrls": { 
        "termsOfService": “<your_terms_of_service_url>”, 
        "privacy": “<your_privacy_statement_url>” 
    }
```

### <a name="msgraph-beta-rest-api"></a><span data-ttu-id="475f8-150">Using the MSGraph beta REST API</span><span class="sxs-lookup"><span data-stu-id="475f8-150">Using the MSGraph beta REST API</span></span>
<span data-ttu-id="475f8-151">To programmatically update all your apps, you can use the MSGraph beta REST API to update all your apps to include links to the terms of service and privacy statement documents.</span><span class="sxs-lookup"><span data-stu-id="475f8-151">To programmatically update all your apps, you can use the MSGraph beta REST API to update all your apps to include links to the terms of service and privacy statement documents.</span></span>

```
PATCH https://graph.microsoft.com/beta/applications/{application id}
{ 
    "appId": "{your application id}", 
    "info": { 
        "termsOfServiceUrl": "<your_terms_of_service_url>", 
        "supportUrl": null, 
        "privacyStatementUrl": "<your_privacy_statement_url>", 
        "marketingUrl": null, 
        "logoUrl": null 
    }
}
```

> [!NOTE]
> * <span data-ttu-id="475f8-152">Be careful not to overwrite any pre-existing values you have assigned to any of these fields: `supportUrl`, `marketingUrl`, and `logoUrl`</span><span class="sxs-lookup"><span data-stu-id="475f8-152">Be careful not to overwrite any pre-existing values you have assigned to any of these fields: `supportUrl`, `marketingUrl`, and `logoUrl`</span></span>
> * <span data-ttu-id="475f8-153">The MSGraph beta REST API will only work when you sign in with an Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="475f8-153">The MSGraph beta REST API will only work when you sign in with an Azure AD account.</span></span> <span data-ttu-id="475f8-154">Personal Microsoft accounts are not supported.</span><span class="sxs-lookup"><span data-stu-id="475f8-154">Personal Microsoft accounts are not supported.</span></span>