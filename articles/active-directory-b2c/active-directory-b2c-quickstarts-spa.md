---
title: Quickstart - Set up sign-in for a single-page app using Azure Active Directory B2C | Microsoft Docs
description: Run a sample single-page application that uses Azure Active Directory B2C to provide account sign-in.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: quickstart
ms.date: 7/13/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 155cdaf51ac5725a315259a0d809ba644f64110c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868759"
---
# <a name="quickstart-set-up-sign-in-for-a-single-page-app-using-azure-active-directory-b2c"></a><span data-ttu-id="547d6-103">Quickstart: Set up sign-in for a single-page app using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="547d6-103">Quickstart: Set up sign-in for a single-page app using Azure Active Directory B2C</span></span>

<span data-ttu-id="547d6-104">Azure Active Directory (Azure AD) B2C provides cloud identity management to keep your application, business, and customers protected.</span><span class="sxs-lookup"><span data-stu-id="547d6-104">Azure Active Directory (Azure AD) B2C provides cloud identity management to keep your application, business, and customers protected.</span></span> <span data-ttu-id="547d6-105">Azure AD B2C enables your apps to authenticate to social accounts, and enterprise accounts using open standard protocols.</span><span class="sxs-lookup"><span data-stu-id="547d6-105">Azure AD B2C enables your apps to authenticate to social accounts, and enterprise accounts using open standard protocols.</span></span>

<span data-ttu-id="547d6-106">In this quickstart, you use an Azure AD B2C enabled sample single-page app to sign in using a social identity provider and call an Azure AD B2C protected web API.</span><span class="sxs-lookup"><span data-stu-id="547d6-106">In this quickstart, you use an Azure AD B2C enabled sample single-page app to sign in using a social identity provider and call an Azure AD B2C protected web API.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="547d6-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="547d6-107">Prerequisites</span></span>

* <span data-ttu-id="547d6-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="547d6-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span></span>
* <span data-ttu-id="547d6-109">Install [Node.js](https://nodejs.org/en/download/)</span><span class="sxs-lookup"><span data-stu-id="547d6-109">Install [Node.js](https://nodejs.org/en/download/)</span></span>
* <span data-ttu-id="547d6-110">A Facebook account.</span><span class="sxs-lookup"><span data-stu-id="547d6-110">A Facebook account.</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="547d6-111">Download the sample</span><span class="sxs-lookup"><span data-stu-id="547d6-111">Download the sample</span></span>

<span data-ttu-id="547d6-112">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp/archive/master.zip) or clone the sample web app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="547d6-112">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp/archive/master.zip) or clone the sample web app from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp.git
```

## <a name="run-the-sample-application"></a><span data-ttu-id="547d6-113">Run the sample application</span><span class="sxs-lookup"><span data-stu-id="547d6-113">Run the sample application</span></span>

<span data-ttu-id="547d6-114">To run this sample from the Node.js command prompt:</span><span class="sxs-lookup"><span data-stu-id="547d6-114">To run this sample from the Node.js command prompt:</span></span> 

```
cd active-directory-b2c-javascript-msal-singlepageapp
npm install && npm update
node server.js
```

<span data-ttu-id="547d6-115">The Node.js app outputs the port number it's listening on at localhost.</span><span class="sxs-lookup"><span data-stu-id="547d6-115">The Node.js app outputs the port number it's listening on at localhost.</span></span>

```
Listening on port 6420...
```

<span data-ttu-id="547d6-116">Browse to the app's URL `http://localhost:6420` in a web browser.</span><span class="sxs-lookup"><span data-stu-id="547d6-116">Browse to the app's URL `http://localhost:6420` in a web browser.</span></span>

![Sample app in browser](media/active-directory-b2c-quickstarts-spa/sample-app-spa.png)

## <a name="create-an-account"></a><span data-ttu-id="547d6-118">Create an account</span><span class="sxs-lookup"><span data-stu-id="547d6-118">Create an account</span></span>

<span data-ttu-id="547d6-119">Click the **Login** button to start the Azure AD B2C **Sign Up or Sign In** workflow based on an Azure AD B2C policy.</span><span class="sxs-lookup"><span data-stu-id="547d6-119">Click the **Login** button to start the Azure AD B2C **Sign Up or Sign In** workflow based on an Azure AD B2C policy.</span></span> 

<span data-ttu-id="547d6-120">The sample is intended to support several sign-up options including creating a local account using an email address.</span><span class="sxs-lookup"><span data-stu-id="547d6-120">The sample is intended to support several sign-up options including creating a local account using an email address.</span></span> <span data-ttu-id="547d6-121">For this quickstart, use a Facebook account.</span><span class="sxs-lookup"><span data-stu-id="547d6-121">For this quickstart, use a Facebook account.</span></span> 

### <a name="sign-up-using-a-social-identity-provider"></a><span data-ttu-id="547d6-122">Sign up using a social identity provider</span><span class="sxs-lookup"><span data-stu-id="547d6-122">Sign up using a social identity provider</span></span>

<span data-ttu-id="547d6-123">Azure AD B2C presents a custom login page for a fictitious brand called Wingtip Toys for the sample web app.</span><span class="sxs-lookup"><span data-stu-id="547d6-123">Azure AD B2C presents a custom login page for a fictitious brand called Wingtip Toys for the sample web app.</span></span> 

1. <span data-ttu-id="547d6-124">To sign up using a social identity provider, click the button of the Facebook identity provider.</span><span class="sxs-lookup"><span data-stu-id="547d6-124">To sign up using a social identity provider, click the button of the Facebook identity provider.</span></span>

    <span data-ttu-id="547d6-125">You authenticate (sign-in) using your social account credentials and authorize the application to read information from your social account.</span><span class="sxs-lookup"><span data-stu-id="547d6-125">You authenticate (sign-in) using your social account credentials and authorize the application to read information from your social account.</span></span> <span data-ttu-id="547d6-126">By granting access, the application can retrieve profile information from the social account such as your name and city.</span><span class="sxs-lookup"><span data-stu-id="547d6-126">By granting access, the application can retrieve profile information from the social account such as your name and city.</span></span> 

2. <span data-ttu-id="547d6-127">Finish the sign-in process for the identity provider by entering your credentials.</span><span class="sxs-lookup"><span data-stu-id="547d6-127">Finish the sign-in process for the identity provider by entering your credentials.</span></span>

    <span data-ttu-id="547d6-128">Your new account profile details are pre-populated with information from your social account.</span><span class="sxs-lookup"><span data-stu-id="547d6-128">Your new account profile details are pre-populated with information from your social account.</span></span> 

3. <span data-ttu-id="547d6-129">Update the Display Name, Job Title, and City fields and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="547d6-129">Update the Display Name, Job Title, and City fields and click **Continue**.</span></span>  <span data-ttu-id="547d6-130">The values you enter are used for your Azure AD B2C user account profile.</span><span class="sxs-lookup"><span data-stu-id="547d6-130">The values you enter are used for your Azure AD B2C user account profile.</span></span>

    <span data-ttu-id="547d6-131">You have successfully created a new Azure AD B2C user account that uses an identity provider.</span><span class="sxs-lookup"><span data-stu-id="547d6-131">You have successfully created a new Azure AD B2C user account that uses an identity provider.</span></span> 

## <a name="access-a-protected-web-api-resource"></a><span data-ttu-id="547d6-132">Access a protected web API resource</span><span class="sxs-lookup"><span data-stu-id="547d6-132">Access a protected web API resource</span></span>

<span data-ttu-id="547d6-133">Click the **Call Web API** button to have your display name returned from the Web API call as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="547d6-133">Click the **Call Web API** button to have your display name returned from the Web API call as a JSON object.</span></span> 

![Web API response](media/active-directory-b2c-quickstarts-spa/call-api-spa.png)

<span data-ttu-id="547d6-135">The sample single-page app includes an Azure AD access token in the request to the protected web API resource to perform the operation to return the JSON object.</span><span class="sxs-lookup"><span data-stu-id="547d6-135">The sample single-page app includes an Azure AD access token in the request to the protected web API resource to perform the operation to return the JSON object.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="547d6-136">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="547d6-136">Clean up resources</span></span>

<span data-ttu-id="547d6-137">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C quickstarts or tutorials.</span><span class="sxs-lookup"><span data-stu-id="547d6-137">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C quickstarts or tutorials.</span></span> <span data-ttu-id="547d6-138">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="547d6-138">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="547d6-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="547d6-139">Next steps</span></span>

<span data-ttu-id="547d6-140">In this quickstart, you used an Azure AD B2C enabled sample ASP.NET app to sign in with a custom login page, sign in with a social identity provider, create an Azure AD B2C account, and call a web API protected by Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="547d6-140">In this quickstart, you used an Azure AD B2C enabled sample ASP.NET app to sign in with a custom login page, sign in with a social identity provider, create an Azure AD B2C account, and call a web API protected by Azure AD B2C.</span></span> 

<span data-ttu-id="547d6-141">The next step is to create your own Azure AD B2C tenant and configure the sample to run using your tenant.</span><span class="sxs-lookup"><span data-stu-id="547d6-141">The next step is to create your own Azure AD B2C tenant and configure the sample to run using your tenant.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="547d6-142">Create an Azure Active Directory B2C tenant in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="547d6-142">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>](tutorial-create-tenant.md)