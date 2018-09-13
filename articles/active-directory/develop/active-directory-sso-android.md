---
title: How to enable cross-app SSO on Android using ADAL | Microsoft Docs
description: 'How to use the features of the ADAL SDK to enable Single Sign On across your applications. '
services: active-directory
documentationcenter: ''
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: d070cc164469f0bfccedcf80e419d7d22caa4083
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669474"
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="fb10b-103">How to enable cross-app SSO on Android using ADAL</span><span class="sxs-lookup"><span data-stu-id="fb10b-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="fb10b-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span><span class="sxs-lookup"><span data-stu-id="fb10b-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="fb10b-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span><span class="sxs-lookup"><span data-stu-id="fb10b-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="fb10b-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span><span class="sxs-lookup"><span data-stu-id="fb10b-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="fb10b-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span><span class="sxs-lookup"><span data-stu-id="fb10b-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="fb10b-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span><span class="sxs-lookup"><span data-stu-id="fb10b-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="fb10b-109">This walkthrough applies to:</span><span class="sxs-lookup"><span data-stu-id="fb10b-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="fb10b-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb10b-110">Azure Active Directory</span></span>
* <span data-ttu-id="fb10b-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="fb10b-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="fb10b-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fb10b-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="fb10b-113">Azure Active Directory Conditional Access</span><span class="sxs-lookup"><span data-stu-id="fb10b-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="fb10b-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="fb10b-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="fb10b-115">SSO Concepts in the Microsoft Identity Platform</span><span class="sxs-lookup"><span data-stu-id="fb10b-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="fb10b-116">Microsoft Identity Brokers</span><span class="sxs-lookup"><span data-stu-id="fb10b-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="fb10b-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span><span class="sxs-lookup"><span data-stu-id="fb10b-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="fb10b-118">We call these **brokers**.</span><span class="sxs-lookup"><span data-stu-id="fb10b-118">We call these **brokers**.</span></span> <span data-ttu-id="fb10b-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span><span class="sxs-lookup"><span data-stu-id="fb10b-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="fb10b-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span><span class="sxs-lookup"><span data-stu-id="fb10b-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="fb10b-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="fb10b-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="fb10b-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span><span class="sxs-lookup"><span data-stu-id="fb10b-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="fb10b-123">Patterns for logging in on mobile devices</span><span class="sxs-lookup"><span data-stu-id="fb10b-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="fb10b-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span><span class="sxs-lookup"><span data-stu-id="fb10b-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="fb10b-125">Non-broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="fb10b-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="fb10b-126">Broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="fb10b-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="fb10b-127">Non-broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="fb10b-127">Non-broker assisted logins</span></span>
<span data-ttu-id="fb10b-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="fb10b-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span><span class="sxs-lookup"><span data-stu-id="fb10b-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="fb10b-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span><span class="sxs-lookup"><span data-stu-id="fb10b-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="fb10b-131">These logins have the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fb10b-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="fb10b-132">User experience exists entirely within the application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="fb10b-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span><span class="sxs-lookup"><span data-stu-id="fb10b-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="fb10b-134">Control around the experience of logging in is provided to the application before and after sign-in.</span><span class="sxs-lookup"><span data-stu-id="fb10b-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="fb10b-135">These logins have the following drawbacks:</span><span class="sxs-lookup"><span data-stu-id="fb10b-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="fb10b-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span><span class="sxs-lookup"><span data-stu-id="fb10b-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="fb10b-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span><span class="sxs-lookup"><span data-stu-id="fb10b-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="fb10b-138">Your application can't support certificate-based authentication for business users.</span><span class="sxs-lookup"><span data-stu-id="fb10b-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="fb10b-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span><span class="sxs-lookup"><span data-stu-id="fb10b-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="fb10b-140">Broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="fb10b-140">Broker assisted logins</span></span>
<span data-ttu-id="fb10b-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="fb10b-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="fb10b-142">This means that your applications rely on the broker to sign users in.</span><span class="sxs-lookup"><span data-stu-id="fb10b-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="fb10b-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span><span class="sxs-lookup"><span data-stu-id="fb10b-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="fb10b-144">An example of this type of application is the Azure Authenticator application on iOS.</span><span class="sxs-lookup"><span data-stu-id="fb10b-144">An example of this type of application is the Azure Authenticator application on iOS.</span></span> <span data-ttu-id="fb10b-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="fb10b-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="fb10b-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span><span class="sxs-lookup"><span data-stu-id="fb10b-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="fb10b-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="fb10b-148">The Microsoft Identity platform uses the same pattern.</span><span class="sxs-lookup"><span data-stu-id="fb10b-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="fb10b-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Azure Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span><span class="sxs-lookup"><span data-stu-id="fb10b-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Azure Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="fb10b-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span><span class="sxs-lookup"><span data-stu-id="fb10b-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="fb10b-151">How the broker gets invoked</span><span class="sxs-lookup"><span data-stu-id="fb10b-151">How the broker gets invoked</span></span>
<span data-ttu-id="fb10b-152">If a compatible broker is installed on the device, like the Azure Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="fb10b-152">If a compatible broker is installed on the device, like the Azure Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="fb10b-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span><span class="sxs-lookup"><span data-stu-id="fb10b-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="fb10b-154">How we ensure the application is valid</span><span class="sxs-lookup"><span data-stu-id="fb10b-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="fb10b-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span><span class="sxs-lookup"><span data-stu-id="fb10b-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="fb10b-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="fb10b-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fb10b-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="fb10b-158">**How developers should craft this redirect URI is discussed in detail below.**</span><span class="sxs-lookup"><span data-stu-id="fb10b-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="fb10b-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span><span class="sxs-lookup"><span data-stu-id="fb10b-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="fb10b-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span><span class="sxs-lookup"><span data-stu-id="fb10b-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="fb10b-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span><span class="sxs-lookup"><span data-stu-id="fb10b-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="fb10b-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span><span class="sxs-lookup"><span data-stu-id="fb10b-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="fb10b-163">This check ensures that only the application registered by the developer receives tokens.</span><span class="sxs-lookup"><span data-stu-id="fb10b-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="fb10b-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span><span class="sxs-lookup"><span data-stu-id="fb10b-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="fb10b-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span><span class="sxs-lookup"><span data-stu-id="fb10b-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="fb10b-166">These logins have the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fb10b-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="fb10b-167">User experiences SSO across all their applications no matter the vendor.</span><span class="sxs-lookup"><span data-stu-id="fb10b-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="fb10b-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span><span class="sxs-lookup"><span data-stu-id="fb10b-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="fb10b-169">Your application can support certificate-based authentication for business users.</span><span class="sxs-lookup"><span data-stu-id="fb10b-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="fb10b-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span><span class="sxs-lookup"><span data-stu-id="fb10b-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="fb10b-171">These logins have the following drawbacks:</span><span class="sxs-lookup"><span data-stu-id="fb10b-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="fb10b-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span><span class="sxs-lookup"><span data-stu-id="fb10b-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="fb10b-173">Loss of the ability to manage the login experience for your customers within your application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="fb10b-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span><span class="sxs-lookup"><span data-stu-id="fb10b-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="fb10b-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span><span class="sxs-lookup"><span data-stu-id="fb10b-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="fb10b-176">Enabling cross-app SSO using ADAL</span><span class="sxs-lookup"><span data-stu-id="fb10b-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="fb10b-177">Here we use the ADAL Android SDK to:</span><span class="sxs-lookup"><span data-stu-id="fb10b-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="fb10b-178">Turn on non-broker assisted SSO for your suite of apps</span><span class="sxs-lookup"><span data-stu-id="fb10b-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="fb10b-179">Turn on support for broker-assisted SSO</span><span class="sxs-lookup"><span data-stu-id="fb10b-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="fb10b-180">Turning on SSO for non-broker assisted SSO</span><span class="sxs-lookup"><span data-stu-id="fb10b-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="fb10b-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span><span class="sxs-lookup"><span data-stu-id="fb10b-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="fb10b-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span><span class="sxs-lookup"><span data-stu-id="fb10b-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="fb10b-183">To enable SSO across applications you own you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="fb10b-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="fb10b-184">Ensure all your applications user the same Client ID or Application ID.</span><span class="sxs-lookup"><span data-stu-id="fb10b-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="fb10b-185">Ensure all your applications have the same SharedUserID set.</span><span class="sxs-lookup"><span data-stu-id="fb10b-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="fb10b-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span><span class="sxs-lookup"><span data-stu-id="fb10b-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="fb10b-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span><span class="sxs-lookup"><span data-stu-id="fb10b-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="fb10b-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span><span class="sxs-lookup"><span data-stu-id="fb10b-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="fb10b-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span><span class="sxs-lookup"><span data-stu-id="fb10b-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="fb10b-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span><span class="sxs-lookup"><span data-stu-id="fb10b-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="fb10b-191">The answer is with the **Redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="fb10b-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="fb10b-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span><span class="sxs-lookup"><span data-stu-id="fb10b-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="fb10b-193">Each app in your suite will have a different redirect URI.</span><span class="sxs-lookup"><span data-stu-id="fb10b-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="fb10b-194">An example of how this looks is below:</span><span class="sxs-lookup"><span data-stu-id="fb10b-194">An example of how this looks is below:</span></span>

<span data-ttu-id="fb10b-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="fb10b-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="fb10b-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="fb10b-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="fb10b-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="fb10b-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="fb10b-198">....</span><span class="sxs-lookup"><span data-stu-id="fb10b-198">....</span></span>

<span data-ttu-id="fb10b-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span><span class="sxs-lookup"><span data-stu-id="fb10b-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="fb10b-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span><span class="sxs-lookup"><span data-stu-id="fb10b-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="fb10b-201">Step 2: Configuring shared storage in Android</span><span class="sxs-lookup"><span data-stu-id="fb10b-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="fb10b-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="fb10b-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="fb10b-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span><span class="sxs-lookup"><span data-stu-id="fb10b-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="fb10b-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span><span class="sxs-lookup"><span data-stu-id="fb10b-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="fb10b-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="fb10b-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span><span class="sxs-lookup"><span data-stu-id="fb10b-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="fb10b-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span><span class="sxs-lookup"><span data-stu-id="fb10b-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="fb10b-208">That's it!</span><span class="sxs-lookup"><span data-stu-id="fb10b-208">That's it!</span></span> <span data-ttu-id="fb10b-209">The Microsoft Identity SDK will now share credentials across all your applications.</span><span class="sxs-lookup"><span data-stu-id="fb10b-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="fb10b-210">The user list will also be shared across application instances.</span><span class="sxs-lookup"><span data-stu-id="fb10b-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="fb10b-211">Turning on SSO for broker assisted SSO</span><span class="sxs-lookup"><span data-stu-id="fb10b-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="fb10b-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span><span class="sxs-lookup"><span data-stu-id="fb10b-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="fb10b-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="fb10b-214">The steps to follow are:</span><span class="sxs-lookup"><span data-stu-id="fb10b-214">The steps to follow are:</span></span>

1. <span data-ttu-id="fb10b-215">Enable broker mode in your application code's call to the MS SDK</span><span class="sxs-lookup"><span data-stu-id="fb10b-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="fb10b-216">Establish a new redirect URI and provide that to both the app and your app registration</span><span class="sxs-lookup"><span data-stu-id="fb10b-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="fb10b-217">Setting up the correct permissions in the Android manifest</span><span class="sxs-lookup"><span data-stu-id="fb10b-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="fb10b-218">Step 1: Enable broker mode in your application</span><span class="sxs-lookup"><span data-stu-id="fb10b-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="fb10b-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span><span class="sxs-lookup"><span data-stu-id="fb10b-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="fb10b-220">You do this by setting your ApplicationSettings type in your code:</span><span class="sxs-lookup"><span data-stu-id="fb10b-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="fb10b-221">Step 2: Establish a new redirect URI with your URL Scheme</span><span class="sxs-lookup"><span data-stu-id="fb10b-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="fb10b-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span><span class="sxs-lookup"><span data-stu-id="fb10b-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="fb10b-223">The Android operating system uses the hash of the certificate in the Google Play store.</span><span class="sxs-lookup"><span data-stu-id="fb10b-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="fb10b-224">This cannot be spoofed by a rogue application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="fb10b-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span><span class="sxs-lookup"><span data-stu-id="fb10b-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="fb10b-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span><span class="sxs-lookup"><span data-stu-id="fb10b-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="fb10b-227">Your redirect URI must be in the proper form of:</span><span class="sxs-lookup"><span data-stu-id="fb10b-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="fb10b-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="fb10b-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="fb10b-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fb10b-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="fb10b-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="fb10b-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="fb10b-231">Step 3: Set up the correct permissions in your application</span><span class="sxs-lookup"><span data-stu-id="fb10b-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="fb10b-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span><span class="sxs-lookup"><span data-stu-id="fb10b-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="fb10b-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span><span class="sxs-lookup"><span data-stu-id="fb10b-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="fb10b-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="fb10b-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="fb10b-235">In particular, these permissions are:</span><span class="sxs-lookup"><span data-stu-id="fb10b-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="fb10b-236">You've configured SSO!</span><span class="sxs-lookup"><span data-stu-id="fb10b-236">You've configured SSO!</span></span>
<span data-ttu-id="fb10b-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span><span class="sxs-lookup"><span data-stu-id="fb10b-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

