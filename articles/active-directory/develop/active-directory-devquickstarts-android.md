---
title: Azure AD Android Getting Started | Microsoft Docs
description: How to build an Android application that integrates with Azure AD for sign-in and calls Azure AD protected APIs by using OAuth.
services: active-directory
documentationcenter: android
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 21f16a9be780a06ccb073b44435bef45308ab85c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564601"
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="ad9a4-103">Integrate Azure AD into an Android app</span><span class="sxs-lookup"><span data-stu-id="ad9a4-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ad9a4-104">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-104">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="ad9a4-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="ad9a4-106">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-106">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="ad9a4-107">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-107">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="ad9a4-108">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-108">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="ad9a4-109">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-109">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="ad9a4-110">Gets a user's to-do list.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-110">Gets a user's to-do list.</span></span>
* <span data-ttu-id="ad9a4-111">Signs out users.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-111">Signs out users.</span></span>

<span data-ttu-id="ad9a4-112">To get started, you need an Azure AD tenant in which you can create users and register an application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-112">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="ad9a4-113">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-113">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

> [!TIP]
> <span data-ttu-id="ad9a4-114">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-114">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="ad9a4-115">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-115">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="ad9a4-116">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-116">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="ad9a4-117">Step 1: Download and run the Node.js REST API TODO sample server</span><span class="sxs-lookup"><span data-stu-id="ad9a4-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="ad9a4-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="ad9a4-119">This is a prerequisite for the Quick Start.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="ad9a4-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="ad9a4-121">Step 2: Register your web API with your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="ad9a4-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="ad9a4-122">Active Directory supports adding two types of applications:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="ad9a4-123">Web APIs that offer services to users</span><span class="sxs-lookup"><span data-stu-id="ad9a4-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="ad9a4-124">Applications (running either on the web or on a device) that access those web APIs</span><span class="sxs-lookup"><span data-stu-id="ad9a4-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="ad9a4-125">In this step, you're registering the web API that you're running locally for testing this sample.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="ad9a4-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="ad9a4-127">Azure AD can help protect any endpoint.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="ad9a4-128">We're assuming that you're registering the TODO REST API referenced earlier.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="ad9a4-129">But this works for any web API that you want Azure Active Directory to help protect.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="ad9a4-130">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ad9a4-131">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-131">On the top bar, click your account.</span></span> <span data-ttu-id="ad9a4-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="ad9a4-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ad9a4-134">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ad9a4-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="ad9a4-136">For the sign-on URL, enter the base URL for the sample.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="ad9a4-137">By default, this is `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="ad9a4-138">Click **OK** to complete the registration.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="ad9a4-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="ad9a4-140">You'll need this later when configuring your application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="ad9a4-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="ad9a4-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="ad9a4-143">Step 3: Register the sample Android Native Client application</span><span class="sxs-lookup"><span data-stu-id="ad9a4-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="ad9a4-144">You must register your web application in this sample.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-144">You must register your web application in this sample.</span></span> <span data-ttu-id="ad9a4-145">This allows your application to communicate with the just-registered web API.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="ad9a4-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="ad9a4-147">That's part of the security of the model.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-147">That's part of the security of the model.</span></span>

<span data-ttu-id="ad9a4-148">We're assuming that you're registering the sample application referenced earlier.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="ad9a4-149">But this procedure works for any app that you're developing.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="ad9a4-150">You might wonder why you're putting both an application and a web API in one tenant.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="ad9a4-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="ad9a4-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="ad9a4-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="ad9a4-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="ad9a4-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="ad9a4-156">This is usually the case if you're developing an application just for your own company to use.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="ad9a4-157">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ad9a4-158">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-158">On the top bar, click your account.</span></span> <span data-ttu-id="ad9a4-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="ad9a4-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ad9a4-161">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ad9a4-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="ad9a4-163">For the redirect URI, enter `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="ad9a4-164">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-164">Click **Finish**.</span></span>
7. <span data-ttu-id="ad9a4-165">From the application page, find the application ID value and copy it.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="ad9a4-166">You'll need this later when configuring your application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="ad9a4-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="ad9a4-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="ad9a4-169">To build with Maven, you can use pom.xml at the top level:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="ad9a4-170">Clone this repo into a directory of your choice:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="ad9a4-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="ad9a4-172">Set up the emulator with SDK 19.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="ad9a4-173">Go to the root folder where you cloned the repo.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="ad9a4-174">Run this command: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="ad9a4-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="ad9a4-175">Change the directory to the Quick Start sample: `cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="ad9a4-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="ad9a4-176">Run this command: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="ad9a4-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="ad9a4-177">You should see the app starting.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-177">You should see the app starting.</span></span>
8. <span data-ttu-id="ad9a4-178">Enter test user credentials to try.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="ad9a4-179">JAR packages will be submitted beside the AAR package.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="ad9a4-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span><span class="sxs-lookup"><span data-stu-id="ad9a4-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="ad9a4-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="ad9a4-182">You can use the source code to import this library into Eclipse and link to your application.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="ad9a4-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="ad9a4-184">Option 1: Source Zip</span><span class="sxs-lookup"><span data-stu-id="ad9a4-184">Option 1: Source Zip</span></span>
<span data-ttu-id="ad9a4-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="ad9a4-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="ad9a4-187">Option 2: Source via Git</span><span class="sxs-lookup"><span data-stu-id="ad9a4-187">Option 2: Source via Git</span></span>
<span data-ttu-id="ad9a4-188">To get the source code of the SDK via Git, type:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="ad9a4-189">Option 3: Binaries via Gradle</span><span class="sxs-lookup"><span data-stu-id="ad9a4-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="ad9a4-190">You can get the binaries from the Maven central repo.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="ad9a4-191">The AAR package can be included as follows in your project in Android Studio:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="ad9a4-192">Option 4: AAR via Maven</span><span class="sxs-lookup"><span data-stu-id="ad9a4-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="ad9a4-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="ad9a4-194">Option 5: JAR package inside the libs folder</span><span class="sxs-lookup"><span data-stu-id="ad9a4-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="ad9a4-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="ad9a4-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="ad9a4-197">Step 5: Add references to Android ADAL to your project</span><span class="sxs-lookup"><span data-stu-id="ad9a4-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="ad9a4-198">Add a reference to your project and specify it as an Android library.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="ad9a4-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="ad9a4-200">Add the project dependency for debugging into your project settings.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="ad9a4-201">Update your project's AndroidManifest.xml file to include:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-201">Update your project's AndroidManifest.xml file to include:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="ad9a4-202">Create an instance of AuthenticationContext at your main activity.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="ad9a4-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="ad9a4-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.windows.net/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.windows.net/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="ad9a4-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="ad9a4-206">To ask for a token, define a callback:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-206">To ask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="ad9a4-207">Finally, ask for a token by using that callback:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="ad9a4-208">Here's an explanation of the parameters:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="ad9a4-209">*resource* is required and is the resource you're trying to access.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="ad9a4-210">*clientid* is required and comes from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="ad9a4-211">*RedirectUri* is not required to be provided for the acquireToken call.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="ad9a4-212">You can set it up as your package name.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="ad9a4-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="ad9a4-214">*callback* is called after the authorization code is exchanged for a token.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="ad9a4-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="ad9a4-216">*acquireTokenSilent* is optional.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="ad9a4-217">You can call it to handle caching and token refresh.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="ad9a4-218">It also provides the sync version.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-218">It also provides the sync version.</span></span> <span data-ttu-id="ad9a4-219">It accepts *userId* as a parameter.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="ad9a4-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="ad9a4-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="ad9a4-222">Important information</span><span class="sxs-lookup"><span data-stu-id="ad9a4-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="ad9a4-223">Customization</span><span class="sxs-lookup"><span data-stu-id="ad9a4-223">Customization</span></span>
<span data-ttu-id="ad9a4-224">Your application resources can overwrite library project resources.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="ad9a4-225">This happens when your app is being built.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-225">This happens when your app is being built.</span></span> <span data-ttu-id="ad9a4-226">For this reason, you can customize authentication activity layout the way you want.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="ad9a4-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="ad9a4-228">Broker</span><span class="sxs-lookup"><span data-stu-id="ad9a4-228">Broker</span></span>
<span data-ttu-id="ad9a4-229">The Microsoft Intune Company Portal app provides the broker component.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="ad9a4-230">The account is created in AccountManager.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-230">The account is created in AccountManager.</span></span> <span data-ttu-id="ad9a4-231">The account type is "com.microsoft.workaccount."</span><span class="sxs-lookup"><span data-stu-id="ad9a4-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="ad9a4-232">AccountManager allows only a single SSO account.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="ad9a4-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="ad9a4-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="ad9a4-235">You can skip the broker user with:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="ad9a4-236">You need to register a special RedirectUri for broker usage.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="ad9a4-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="ad9a4-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="ad9a4-239">The signature is related to your signing certificates.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="ad9a4-240">The current broker model is for one user.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-240">The current broker model is for one user.</span></span> <span data-ttu-id="ad9a4-241">AuthenticationContext provides the API method to get the broker user.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="ad9a4-242">Your app manifest should have the following permissions to use AccountManager accounts.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="ad9a4-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="ad9a4-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="ad9a4-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="ad9a4-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="ad9a4-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="ad9a4-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="ad9a4-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="ad9a4-247">Authority URL and AD FS</span><span class="sxs-lookup"><span data-stu-id="ad9a4-247">Authority URL and AD FS</span></span>
<span data-ttu-id="ad9a4-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="ad9a4-249">The authority URL needs an STS instance and a [tenant name](https://login.windows.net/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-249">The authority URL needs an STS instance and a [tenant name](https://login.windows.net/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="ad9a4-250">Querying cache items</span><span class="sxs-lookup"><span data-stu-id="ad9a4-250">Querying cache items</span></span>
<span data-ttu-id="ad9a4-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="ad9a4-252">You can get the current cache from AuthenticationContext by using:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="ad9a4-253">You can also provide your cache implementation, if you want to customize it.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="ad9a4-254">Prompt behavior</span><span class="sxs-lookup"><span data-stu-id="ad9a4-254">Prompt behavior</span></span>
<span data-ttu-id="ad9a4-255">ADAL provides an option to specify prompt behavior.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="ad9a4-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="ad9a4-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="ad9a4-258">Silent token request from cache and refresh</span><span class="sxs-lookup"><span data-stu-id="ad9a4-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="ad9a4-259">A silent token request does not use the UI pop-up and does not require an activity.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="ad9a4-260">It returns a token from the cache if available.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="ad9a4-261">If the token is expired, this method tries to refresh it.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="ad9a4-262">If the refresh token is expired or failed, it returns AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="ad9a4-263">You can also make a sync call by using this method.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="ad9a4-264">You can set null to callback or use acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="ad9a4-265">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="ad9a4-265">Diagnostics</span></span>
<span data-ttu-id="ad9a4-266">These are the primary sources of information for diagnosing issues:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="ad9a4-267">Exceptions</span><span class="sxs-lookup"><span data-stu-id="ad9a4-267">Exceptions</span></span>
* <span data-ttu-id="ad9a4-268">Logs</span><span class="sxs-lookup"><span data-stu-id="ad9a4-268">Logs</span></span>
* <span data-ttu-id="ad9a4-269">Network traces</span><span class="sxs-lookup"><span data-stu-id="ad9a4-269">Network traces</span></span>

<span data-ttu-id="ad9a4-270">Note that correlation IDs are central to the diagnostics in the library.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="ad9a4-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="ad9a4-272">If you don't set a correlation ID, ADAL will generate a random one.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="ad9a4-273">All log messages and network calls will then be stamped with the correlation ID.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="ad9a4-274">The self-generated ID changes on each request.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="ad9a4-275">Exceptions</span><span class="sxs-lookup"><span data-stu-id="ad9a4-275">Exceptions</span></span>
<span data-ttu-id="ad9a4-276">Exceptions are the first diagnostic.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="ad9a4-277">We try to provide helpful error messages.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="ad9a4-278">If you find one that is not helpful, please file an issue and let us know.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="ad9a4-279">Include device information such as model and SDK number.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="ad9a4-280">Logs</span><span class="sxs-lookup"><span data-stu-id="ad9a4-280">Logs</span></span>
<span data-ttu-id="ad9a4-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="ad9a4-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="ad9a4-283">Messages can be written to a custom log file, as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="ad9a4-284">Unfortunately, there is no standard way of getting logs from a device.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="ad9a4-285">There are some services that can help you with this.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-285">There are some services that can help you with this.</span></span> <span data-ttu-id="ad9a4-286">You can also invent your own, such as sending the file to a server.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="ad9a4-287">These are the logging levels:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-287">These are the logging levels:</span></span>
* <span data-ttu-id="ad9a4-288">Error (exceptions)</span><span class="sxs-lookup"><span data-stu-id="ad9a4-288">Error (exceptions)</span></span>
* <span data-ttu-id="ad9a4-289">Warn (warning)</span><span class="sxs-lookup"><span data-stu-id="ad9a4-289">Warn (warning)</span></span>
* <span data-ttu-id="ad9a4-290">Info (information purposes)</span><span class="sxs-lookup"><span data-stu-id="ad9a4-290">Info (information purposes)</span></span>
* <span data-ttu-id="ad9a4-291">Verbose (more details)</span><span class="sxs-lookup"><span data-stu-id="ad9a4-291">Verbose (more details)</span></span>

<span data-ttu-id="ad9a4-292">You set the log level like this:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="ad9a4-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="ad9a4-294">You can get a log to a file from logcat as follows:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="ad9a4-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="ad9a4-296">Network traces</span><span class="sxs-lookup"><span data-stu-id="ad9a4-296">Network traces</span></span>
<span data-ttu-id="ad9a4-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="ad9a4-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="ad9a4-299">Fiddler is the easiest HTTP tracing tool.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="ad9a4-300">Use the following links to set it up to correctly record ADAL network traffic.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="ad9a4-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="ad9a4-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="ad9a4-303">If you're using production accounts, do not share these traces with third parties.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="ad9a4-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="ad9a4-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="ad9a4-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="ad9a4-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="ad9a4-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="ad9a4-307">Dialog mode</span><span class="sxs-lookup"><span data-stu-id="ad9a4-307">Dialog mode</span></span>
<span data-ttu-id="ad9a4-308">The acquireToken method without activity supports a dialog prompt.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="ad9a4-309">Encryption</span><span class="sxs-lookup"><span data-stu-id="ad9a4-309">Encryption</span></span>
<span data-ttu-id="ad9a4-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="ad9a4-311">You can look at the StorageHelper class to see the details.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="ad9a4-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="ad9a4-313">ADAL uses that for API 18 and higher.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="ad9a4-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="ad9a4-315">OAuth2 bearer challenge</span><span class="sxs-lookup"><span data-stu-id="ad9a4-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="ad9a4-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="ad9a4-317">Session cookies in WebView</span><span class="sxs-lookup"><span data-stu-id="ad9a4-317">Session cookies in WebView</span></span>
<span data-ttu-id="ad9a4-318">Android WebView does not clear session cookies after the app is closed.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="ad9a4-319">You can handle that by using this sample code:</span><span class="sxs-lookup"><span data-stu-id="ad9a4-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="ad9a4-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="ad9a4-321">Resource overrides</span><span class="sxs-lookup"><span data-stu-id="ad9a4-321">Resource overrides</span></span>
<span data-ttu-id="ad9a4-322">The ADAL library includes English strings for ProgressDialog messages.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="ad9a4-323">Your application should overwrite them if you want localized strings.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="ad9a4-324">NTLM dialog box</span><span class="sxs-lookup"><span data-stu-id="ad9a4-324">NTLM dialog box</span></span>
<span data-ttu-id="ad9a4-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="ad9a4-326">You can customize the layout and strings for the dialog box.</span><span class="sxs-lookup"><span data-stu-id="ad9a4-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="ad9a4-327">Cross-app SSO</span><span class="sxs-lookup"><span data-stu-id="ad9a4-327">Cross-app SSO</span></span>
<span data-ttu-id="ad9a4-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="ad9a4-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
