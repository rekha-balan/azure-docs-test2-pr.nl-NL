---
title: Azure AD Cordova Getting Started | Microsoft Docs
description: How to build a Cordova application that integrates with Azure AD for sign-in and calls Azure AD-protected APIs by using OAuth.
services: active-directory
documentationcenter: ''
author: vibronet
manager: mbaldwin
editor: ''
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.openlocfilehash: 4a80252f139d653ff8788b3c1a6a075448cb48e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553542"
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="c43a5-103">Integrate Azure AD with an Apache Cordova app</span><span class="sxs-lookup"><span data-stu-id="c43a5-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="c43a5-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span><span class="sxs-lookup"><span data-stu-id="c43a5-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="c43a5-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span><span class="sxs-lookup"><span data-stu-id="c43a5-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="c43a5-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c43a5-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="c43a5-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span><span class="sxs-lookup"><span data-stu-id="c43a5-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="c43a5-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span><span class="sxs-lookup"><span data-stu-id="c43a5-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="c43a5-109">With just a few lines of code, authenticate a user and obtain a token.</span><span class="sxs-lookup"><span data-stu-id="c43a5-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="c43a5-110">Use that token to invoke the Graph API to query that directory and display the results.</span><span class="sxs-lookup"><span data-stu-id="c43a5-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="c43a5-111">Use the ADAL token cache to minimize authentication prompts for the user.</span><span class="sxs-lookup"><span data-stu-id="c43a5-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="c43a5-112">To make those improvements, you need to:</span><span class="sxs-lookup"><span data-stu-id="c43a5-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="c43a5-113">Register an application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c43a5-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="c43a5-114">Add code to your app to request tokens.</span><span class="sxs-lookup"><span data-stu-id="c43a5-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="c43a5-115">Add code to use the token for querying the Graph API and display results.</span><span class="sxs-lookup"><span data-stu-id="c43a5-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="c43a5-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span><span class="sxs-lookup"><span data-stu-id="c43a5-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c43a5-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c43a5-117">Prerequisites</span></span>
<span data-ttu-id="c43a5-118">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="c43a5-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="c43a5-119">An Azure AD tenant where you have an account with app development rights.</span><span class="sxs-lookup"><span data-stu-id="c43a5-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="c43a5-120">A development environment that's configured to use Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="c43a5-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="c43a5-121">If you have both already set up, proceed directly to step 1.</span><span class="sxs-lookup"><span data-stu-id="c43a5-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="c43a5-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c43a5-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="c43a5-123">If you don't have Apache Cordova set up on your machine, install the following:</span><span class="sxs-lookup"><span data-stu-id="c43a5-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="c43a5-124">Git</span><span class="sxs-lookup"><span data-stu-id="c43a5-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="c43a5-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="c43a5-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="c43a5-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="c43a5-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="c43a5-127">The preceding installations should work both on the PC and on the Mac.</span><span class="sxs-lookup"><span data-stu-id="c43a5-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="c43a5-128">Each target platform has different prerequisites:</span><span class="sxs-lookup"><span data-stu-id="c43a5-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="c43a5-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="c43a5-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="c43a5-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="c43a5-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="c43a5-131">To build and run an app for iOS:</span><span class="sxs-lookup"><span data-stu-id="c43a5-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="c43a5-132">Install Xcode 6.x or later.</span><span class="sxs-lookup"><span data-stu-id="c43a5-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="c43a5-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="c43a5-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="c43a5-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="c43a5-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="c43a5-135">You can use it to start iOS apps in iOS Simulator from the command line.</span><span class="sxs-lookup"><span data-stu-id="c43a5-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="c43a5-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="c43a5-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="c43a5-137">To build and run an app for Android:</span><span class="sxs-lookup"><span data-stu-id="c43a5-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="c43a5-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span><span class="sxs-lookup"><span data-stu-id="c43a5-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="c43a5-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="c43a5-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="c43a5-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span><span class="sxs-lookup"><span data-stu-id="c43a5-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="c43a5-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span><span class="sxs-lookup"><span data-stu-id="c43a5-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="c43a5-142">*Android 5.0.1 (API 21)* platform SDK</span><span class="sxs-lookup"><span data-stu-id="c43a5-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="c43a5-143">*Android SDK Build Tools* version 19.1.0 or later</span><span class="sxs-lookup"><span data-stu-id="c43a5-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="c43a5-144">*Android Support Repository* (Extras)</span><span class="sxs-lookup"><span data-stu-id="c43a5-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="c43a5-145">The Android SDK doesn't provide any default emulator instance.</span><span class="sxs-lookup"><span data-stu-id="c43a5-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="c43a5-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span><span class="sxs-lookup"><span data-stu-id="c43a5-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="c43a5-147">We recommend an API level of 19 or higher.</span><span class="sxs-lookup"><span data-stu-id="c43a5-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="c43a5-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span><span class="sxs-lookup"><span data-stu-id="c43a5-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="c43a5-149">Step 1: Register an application with Azure AD</span><span class="sxs-lookup"><span data-stu-id="c43a5-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="c43a5-150">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="c43a5-150">This step is optional.</span></span> <span data-ttu-id="c43a5-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span><span class="sxs-lookup"><span data-stu-id="c43a5-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="c43a5-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span><span class="sxs-lookup"><span data-stu-id="c43a5-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="c43a5-153">Azure AD issues tokens to only known applications.</span><span class="sxs-lookup"><span data-stu-id="c43a5-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="c43a5-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span><span class="sxs-lookup"><span data-stu-id="c43a5-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="c43a5-155">To register a new application in your tenant:</span><span class="sxs-lookup"><span data-stu-id="c43a5-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="c43a5-156">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c43a5-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c43a5-157">On the top bar, click your account.</span><span class="sxs-lookup"><span data-stu-id="c43a5-157">On the top bar, click your account.</span></span> <span data-ttu-id="c43a5-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="c43a5-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="c43a5-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c43a5-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c43a5-160">Click **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c43a5-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="c43a5-161">Follow the prompts and create a **Native Client Application**.</span><span class="sxs-lookup"><span data-stu-id="c43a5-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="c43a5-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span><span class="sxs-lookup"><span data-stu-id="c43a5-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="c43a5-163">The **Native Client Application** option must be selected, or the application won't work.)</span><span class="sxs-lookup"><span data-stu-id="c43a5-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="c43a5-164">**Name** describes your application to users.</span><span class="sxs-lookup"><span data-stu-id="c43a5-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="c43a5-165">**Redirect URI** is the URI that's used to return tokens to your app.</span><span class="sxs-lookup"><span data-stu-id="c43a5-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="c43a5-166">Enter **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="c43a5-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="c43a5-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span><span class="sxs-lookup"><span data-stu-id="c43a5-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="c43a5-168">You’ll need this value in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c43a5-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="c43a5-169">You can find it on the application tab of the newly created app.</span><span class="sxs-lookup"><span data-stu-id="c43a5-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="c43a5-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="c43a5-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="c43a5-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="c43a5-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="c43a5-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span><span class="sxs-lookup"><span data-stu-id="c43a5-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="c43a5-173">This enables your application to query the Graph API for users.</span><span class="sxs-lookup"><span data-stu-id="c43a5-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="c43a5-174">Step 2: Clone the sample app repository</span><span class="sxs-lookup"><span data-stu-id="c43a5-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="c43a5-175">From your shell or command line, type the following command:</span><span class="sxs-lookup"><span data-stu-id="c43a5-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="c43a5-176">Step 3: Create the Cordova app</span><span class="sxs-lookup"><span data-stu-id="c43a5-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="c43a5-177">There are multiple ways to create Cordova applications.</span><span class="sxs-lookup"><span data-stu-id="c43a5-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="c43a5-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="c43a5-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="c43a5-179">From your shell or command line, type the following command:</span><span class="sxs-lookup"><span data-stu-id="c43a5-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="c43a5-180">That command creates the folder structure and scaffolding for the Cordova project.</span><span class="sxs-lookup"><span data-stu-id="c43a5-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="c43a5-181">Move to the new DirSearchClient folder:</span><span class="sxs-lookup"><span data-stu-id="c43a5-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="c43a5-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span><span class="sxs-lookup"><span data-stu-id="c43a5-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="c43a5-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="c43a5-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="c43a5-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="c43a5-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="c43a5-185">Add the whitelist plug-in.</span><span class="sxs-lookup"><span data-stu-id="c43a5-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="c43a5-186">This is necessary for invoking the Graph API.</span><span class="sxs-lookup"><span data-stu-id="c43a5-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="c43a5-187">Add all the platforms that you want to support.</span><span class="sxs-lookup"><span data-stu-id="c43a5-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="c43a5-188">To have a working sample, you need to execute at least one of the following commands.</span><span class="sxs-lookup"><span data-stu-id="c43a5-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="c43a5-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span><span class="sxs-lookup"><span data-stu-id="c43a5-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="c43a5-190">Add the ADAL for Cordova plug-in to your project:</span><span class="sxs-lookup"><span data-stu-id="c43a5-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="c43a5-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span><span class="sxs-lookup"><span data-stu-id="c43a5-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="c43a5-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span><span class="sxs-lookup"><span data-stu-id="c43a5-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="c43a5-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span><span class="sxs-lookup"><span data-stu-id="c43a5-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="c43a5-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="c43a5-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="c43a5-195">The only task left for you is to add the logic that implements identity tasks.</span><span class="sxs-lookup"><span data-stu-id="c43a5-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="c43a5-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span><span class="sxs-lookup"><span data-stu-id="c43a5-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="c43a5-197">Those values will be used to construct the token requests later on.</span><span class="sxs-lookup"><span data-stu-id="c43a5-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="c43a5-198">Insert the following snippet at the top of the index.js file:</span><span class="sxs-lookup"><span data-stu-id="c43a5-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.windows.net/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="c43a5-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c43a5-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="c43a5-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c43a5-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="c43a5-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span><span class="sxs-lookup"><span data-stu-id="c43a5-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="c43a5-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span><span class="sxs-lookup"><span data-stu-id="c43a5-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="c43a5-203">Next, add the token request code.</span><span class="sxs-lookup"><span data-stu-id="c43a5-203">Next, add the token request code.</span></span> <span data-ttu-id="c43a5-204">Insert the following snippet between the `search` and `renderData` definitions:</span><span class="sxs-lookup"><span data-stu-id="c43a5-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="c43a5-205">Let's examine that function by breaking it down in its two main parts.</span><span class="sxs-lookup"><span data-stu-id="c43a5-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="c43a5-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span><span class="sxs-lookup"><span data-stu-id="c43a5-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="c43a5-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span><span class="sxs-lookup"><span data-stu-id="c43a5-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="c43a5-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span><span class="sxs-lookup"><span data-stu-id="c43a5-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="c43a5-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span><span class="sxs-lookup"><span data-stu-id="c43a5-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="c43a5-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span><span class="sxs-lookup"><span data-stu-id="c43a5-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="c43a5-211">The second part of the method performs the proper token request.</span><span class="sxs-lookup"><span data-stu-id="c43a5-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="c43a5-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span><span class="sxs-lookup"><span data-stu-id="c43a5-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="c43a5-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span><span class="sxs-lookup"><span data-stu-id="c43a5-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="c43a5-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span><span class="sxs-lookup"><span data-stu-id="c43a5-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="c43a5-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span><span class="sxs-lookup"><span data-stu-id="c43a5-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="c43a5-216">Insert the following snippet below the `authenticate` definition:</span><span class="sxs-lookup"><span data-stu-id="c43a5-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="c43a5-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span><span class="sxs-lookup"><span data-stu-id="c43a5-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="c43a5-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span><span class="sxs-lookup"><span data-stu-id="c43a5-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="c43a5-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span><span class="sxs-lookup"><span data-stu-id="c43a5-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="c43a5-220">Step 5: Run the app</span><span class="sxs-lookup"><span data-stu-id="c43a5-220">Step 5: Run the app</span></span>
<span data-ttu-id="c43a5-221">Your app is finally ready to run.</span><span class="sxs-lookup"><span data-stu-id="c43a5-221">Your app is finally ready to run.</span></span> <span data-ttu-id="c43a5-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span><span class="sxs-lookup"><span data-stu-id="c43a5-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="c43a5-223">You're prompted for authentication.</span><span class="sxs-lookup"><span data-stu-id="c43a5-223">You're prompted for authentication.</span></span> <span data-ttu-id="c43a5-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span><span class="sxs-lookup"><span data-stu-id="c43a5-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="c43a5-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span><span class="sxs-lookup"><span data-stu-id="c43a5-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="c43a5-226">The concrete steps for running the app vary by platform.</span><span class="sxs-lookup"><span data-stu-id="c43a5-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="c43a5-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c43a5-227">Windows 10</span></span>
   <span data-ttu-id="c43a5-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="c43a5-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="c43a5-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="c43a5-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="c43a5-230">During the first run, you might be asked to sign in for a developer license.</span><span class="sxs-lookup"><span data-stu-id="c43a5-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="c43a5-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="c43a5-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="c43a5-232">Windows 8.1 Tablet/PC</span><span class="sxs-lookup"><span data-stu-id="c43a5-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="c43a5-233">During the first run, you might be asked to sign in for a developer license.</span><span class="sxs-lookup"><span data-stu-id="c43a5-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="c43a5-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="c43a5-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="c43a5-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="c43a5-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="c43a5-236">To run on a connected device: `cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="c43a5-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="c43a5-237">To run on the default emulator: `cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="c43a5-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="c43a5-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="c43a5-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="c43a5-239">Android</span><span class="sxs-lookup"><span data-stu-id="c43a5-239">Android</span></span>
   <span data-ttu-id="c43a5-240">To run on a connected device: `cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="c43a5-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="c43a5-241">To run on the default emulator: `cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="c43a5-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="c43a5-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span><span class="sxs-lookup"><span data-stu-id="c43a5-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="c43a5-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="c43a5-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="c43a5-244">iOS</span><span class="sxs-lookup"><span data-stu-id="c43a5-244">iOS</span></span>
   <span data-ttu-id="c43a5-245">To run on a connected device: `cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="c43a5-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="c43a5-246">To run on the default emulator: `cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="c43a5-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="c43a5-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span><span class="sxs-lookup"><span data-stu-id="c43a5-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="c43a5-248">For more information, see the "Prerequisites" section.</span><span class="sxs-lookup"><span data-stu-id="c43a5-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="c43a5-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="c43a5-249">Next steps</span></span>
<span data-ttu-id="c43a5-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="c43a5-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="c43a5-251">You can now move on to more advanced (and more interesting) scenarios.</span><span class="sxs-lookup"><span data-stu-id="c43a5-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="c43a5-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c43a5-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
