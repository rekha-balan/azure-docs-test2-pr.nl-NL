---
title: How to enable cross-app SSO on iOS using ADAL | Microsoft Docs
description: 'How to use the features of the ADAL SDK to enable Single Sign On across your applications. '
services: active-directory
documentationcenter: ''
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: d56fbe4fb1a3ff58a13588f21903211383b86855
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562895"
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="a6955-103">How to enable cross-app SSO on iOS using ADAL</span><span class="sxs-lookup"><span data-stu-id="a6955-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="a6955-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span><span class="sxs-lookup"><span data-stu-id="a6955-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="a6955-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span><span class="sxs-lookup"><span data-stu-id="a6955-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="a6955-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span><span class="sxs-lookup"><span data-stu-id="a6955-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="a6955-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span><span class="sxs-lookup"><span data-stu-id="a6955-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="a6955-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span><span class="sxs-lookup"><span data-stu-id="a6955-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="a6955-109">This walkthrough applies to:</span><span class="sxs-lookup"><span data-stu-id="a6955-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="a6955-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6955-110">Azure Active Directory</span></span>
* <span data-ttu-id="a6955-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="a6955-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="a6955-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a6955-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="a6955-113">Azure Active Directory Conditional Access</span><span class="sxs-lookup"><span data-stu-id="a6955-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="a6955-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="a6955-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="a6955-115">SSO Concepts in the Microsoft Identity Platform</span><span class="sxs-lookup"><span data-stu-id="a6955-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="a6955-116">Microsoft Identity Brokers</span><span class="sxs-lookup"><span data-stu-id="a6955-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="a6955-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span><span class="sxs-lookup"><span data-stu-id="a6955-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="a6955-118">We call these **brokers**.</span><span class="sxs-lookup"><span data-stu-id="a6955-118">We call these **brokers**.</span></span> <span data-ttu-id="a6955-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span><span class="sxs-lookup"><span data-stu-id="a6955-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="a6955-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span><span class="sxs-lookup"><span data-stu-id="a6955-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="a6955-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="a6955-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="a6955-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span><span class="sxs-lookup"><span data-stu-id="a6955-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="a6955-123">Patterns for logging in on mobile devices</span><span class="sxs-lookup"><span data-stu-id="a6955-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="a6955-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span><span class="sxs-lookup"><span data-stu-id="a6955-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="a6955-125">Non-broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="a6955-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="a6955-126">Broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="a6955-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="a6955-127">Non-broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="a6955-127">Non-broker assisted logins</span></span>
<span data-ttu-id="a6955-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span><span class="sxs-lookup"><span data-stu-id="a6955-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="a6955-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span><span class="sxs-lookup"><span data-stu-id="a6955-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="a6955-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span><span class="sxs-lookup"><span data-stu-id="a6955-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="a6955-131">These logins have the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a6955-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="a6955-132">User experience exists entirely within the application.</span><span class="sxs-lookup"><span data-stu-id="a6955-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="a6955-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span><span class="sxs-lookup"><span data-stu-id="a6955-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="a6955-134">Control around the experience of logging in is provided to the application before and after sign-in.</span><span class="sxs-lookup"><span data-stu-id="a6955-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="a6955-135">These logins have the following drawbacks:</span><span class="sxs-lookup"><span data-stu-id="a6955-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="a6955-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span><span class="sxs-lookup"><span data-stu-id="a6955-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="a6955-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span><span class="sxs-lookup"><span data-stu-id="a6955-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="a6955-138">Your application can't support certificate-based authentication for business users.</span><span class="sxs-lookup"><span data-stu-id="a6955-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="a6955-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span><span class="sxs-lookup"><span data-stu-id="a6955-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="a6955-140">Broker assisted logins</span><span class="sxs-lookup"><span data-stu-id="a6955-140">Broker assisted logins</span></span>
<span data-ttu-id="a6955-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="a6955-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="a6955-142">This means that your applications rely on the broker to sign users in.</span><span class="sxs-lookup"><span data-stu-id="a6955-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="a6955-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span><span class="sxs-lookup"><span data-stu-id="a6955-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="a6955-144">An example of this type of application is the Azure Authenticator application on iOS.</span><span class="sxs-lookup"><span data-stu-id="a6955-144">An example of this type of application is the Azure Authenticator application on iOS.</span></span> <span data-ttu-id="a6955-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span><span class="sxs-lookup"><span data-stu-id="a6955-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="a6955-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span><span class="sxs-lookup"><span data-stu-id="a6955-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="a6955-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span><span class="sxs-lookup"><span data-stu-id="a6955-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="a6955-148">The Microsoft Identity platform uses the same pattern.</span><span class="sxs-lookup"><span data-stu-id="a6955-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="a6955-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Azure Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span><span class="sxs-lookup"><span data-stu-id="a6955-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Azure Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="a6955-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span><span class="sxs-lookup"><span data-stu-id="a6955-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="a6955-151">How the broker gets invoked</span><span class="sxs-lookup"><span data-stu-id="a6955-151">How the broker gets invoked</span></span>
<span data-ttu-id="a6955-152">If a compatible broker is installed on the device, like the Azure Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="a6955-152">If a compatible broker is installed on the device, like the Azure Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="a6955-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span><span class="sxs-lookup"><span data-stu-id="a6955-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="a6955-154">How we ensure the application is valid</span><span class="sxs-lookup"><span data-stu-id="a6955-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="a6955-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span><span class="sxs-lookup"><span data-stu-id="a6955-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="a6955-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span><span class="sxs-lookup"><span data-stu-id="a6955-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="a6955-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a6955-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="a6955-158">**How developers should craft this redirect URI is discussed in detail below.**</span><span class="sxs-lookup"><span data-stu-id="a6955-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="a6955-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="a6955-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="a6955-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span><span class="sxs-lookup"><span data-stu-id="a6955-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="a6955-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span><span class="sxs-lookup"><span data-stu-id="a6955-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="a6955-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span><span class="sxs-lookup"><span data-stu-id="a6955-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="a6955-163">This check ensures that only the application registered by the developer receives tokens.</span><span class="sxs-lookup"><span data-stu-id="a6955-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="a6955-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span><span class="sxs-lookup"><span data-stu-id="a6955-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="a6955-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span><span class="sxs-lookup"><span data-stu-id="a6955-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="a6955-166">These logins have the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a6955-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="a6955-167">User experiences SSO across all their applications no matter the vendor.</span><span class="sxs-lookup"><span data-stu-id="a6955-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="a6955-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span><span class="sxs-lookup"><span data-stu-id="a6955-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="a6955-169">Your application can support certificate-based authentication for business users.</span><span class="sxs-lookup"><span data-stu-id="a6955-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="a6955-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span><span class="sxs-lookup"><span data-stu-id="a6955-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="a6955-171">These logins have the following drawbacks:</span><span class="sxs-lookup"><span data-stu-id="a6955-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="a6955-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span><span class="sxs-lookup"><span data-stu-id="a6955-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="a6955-173">Loss of the ability to manage the login experience for your customers within your application.</span><span class="sxs-lookup"><span data-stu-id="a6955-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="a6955-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span><span class="sxs-lookup"><span data-stu-id="a6955-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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

<span data-ttu-id="a6955-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span><span class="sxs-lookup"><span data-stu-id="a6955-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="a6955-176">Enabling cross-app SSO using ADAL</span><span class="sxs-lookup"><span data-stu-id="a6955-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="a6955-177">Here we use the ADAL iOS SDK to:</span><span class="sxs-lookup"><span data-stu-id="a6955-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="a6955-178">Turn on non-broker assisted SSO for your suite of apps</span><span class="sxs-lookup"><span data-stu-id="a6955-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="a6955-179">Turn on support for broker-assisted SSO</span><span class="sxs-lookup"><span data-stu-id="a6955-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="a6955-180">Turning on SSO for non-broker assisted SSO</span><span class="sxs-lookup"><span data-stu-id="a6955-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="a6955-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span><span class="sxs-lookup"><span data-stu-id="a6955-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="a6955-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span><span class="sxs-lookup"><span data-stu-id="a6955-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="a6955-183">To enable SSO across applications you own you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="a6955-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="a6955-184">Ensure all your applications user the same Client ID or Application ID.</span><span class="sxs-lookup"><span data-stu-id="a6955-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="a6955-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span><span class="sxs-lookup"><span data-stu-id="a6955-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="a6955-186">Request the same keychain entitlement for each of your applications.</span><span class="sxs-lookup"><span data-stu-id="a6955-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="a6955-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span><span class="sxs-lookup"><span data-stu-id="a6955-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="a6955-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span><span class="sxs-lookup"><span data-stu-id="a6955-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="a6955-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span><span class="sxs-lookup"><span data-stu-id="a6955-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="a6955-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span><span class="sxs-lookup"><span data-stu-id="a6955-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="a6955-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span><span class="sxs-lookup"><span data-stu-id="a6955-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="a6955-192">The answer is with the **Redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="a6955-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="a6955-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span><span class="sxs-lookup"><span data-stu-id="a6955-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="a6955-194">Each app in your suite will have a different redirect URI.</span><span class="sxs-lookup"><span data-stu-id="a6955-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="a6955-195">An example of how this looks is below:</span><span class="sxs-lookup"><span data-stu-id="a6955-195">An example of how this looks is below:</span></span>

<span data-ttu-id="a6955-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="a6955-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="a6955-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="a6955-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="a6955-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="a6955-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="a6955-199">....</span><span class="sxs-lookup"><span data-stu-id="a6955-199">....</span></span>

<span data-ttu-id="a6955-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span><span class="sxs-lookup"><span data-stu-id="a6955-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="a6955-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span><span class="sxs-lookup"><span data-stu-id="a6955-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="a6955-202">Create keychain sharing between applications</span><span class="sxs-lookup"><span data-stu-id="a6955-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="a6955-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="a6955-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="a6955-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span><span class="sxs-lookup"><span data-stu-id="a6955-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="a6955-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="a6955-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="a6955-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span><span class="sxs-lookup"><span data-stu-id="a6955-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="a6955-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span><span class="sxs-lookup"><span data-stu-id="a6955-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="a6955-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span><span class="sxs-lookup"><span data-stu-id="a6955-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="a6955-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span><span class="sxs-lookup"><span data-stu-id="a6955-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="a6955-210">That's it!</span><span class="sxs-lookup"><span data-stu-id="a6955-210">That's it!</span></span> <span data-ttu-id="a6955-211">The Microsoft Identity SDK will now share credentials across all your applications.</span><span class="sxs-lookup"><span data-stu-id="a6955-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="a6955-212">The user list will also be shared across application instances.</span><span class="sxs-lookup"><span data-stu-id="a6955-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="a6955-213">Turning on SSO for broker assisted SSO</span><span class="sxs-lookup"><span data-stu-id="a6955-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="a6955-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span><span class="sxs-lookup"><span data-stu-id="a6955-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="a6955-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span><span class="sxs-lookup"><span data-stu-id="a6955-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="a6955-216">The steps to follow are:</span><span class="sxs-lookup"><span data-stu-id="a6955-216">The steps to follow are:</span></span>

1. <span data-ttu-id="a6955-217">Enable broker mode in your application code's call to the MS SDK.</span><span class="sxs-lookup"><span data-stu-id="a6955-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="a6955-218">Establish a new redirect URI and provide that to both the app and your app registration.</span><span class="sxs-lookup"><span data-stu-id="a6955-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="a6955-219">Registering a URL Scheme.</span><span class="sxs-lookup"><span data-stu-id="a6955-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="a6955-220">iOS9 Support: Add a permission to your info.plist file.</span><span class="sxs-lookup"><span data-stu-id="a6955-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="a6955-221">Step 1: Enable broker mode in your application</span><span class="sxs-lookup"><span data-stu-id="a6955-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="a6955-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span><span class="sxs-lookup"><span data-stu-id="a6955-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="a6955-223">You do this by setting your credentials type in your code:</span><span class="sxs-lookup"><span data-stu-id="a6955-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="a6955-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span><span class="sxs-lookup"><span data-stu-id="a6955-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="a6955-225">Step 2: Registering a URL Scheme</span><span class="sxs-lookup"><span data-stu-id="a6955-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="a6955-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span><span class="sxs-lookup"><span data-stu-id="a6955-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="a6955-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span><span class="sxs-lookup"><span data-stu-id="a6955-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="a6955-228">This can be in addition to any other app schemes you may have previously registered with your application.</span><span class="sxs-lookup"><span data-stu-id="a6955-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="a6955-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span><span class="sxs-lookup"><span data-stu-id="a6955-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="a6955-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span><span class="sxs-lookup"><span data-stu-id="a6955-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="a6955-231">Below is an example of how this appears in your project configuration.</span><span class="sxs-lookup"><span data-stu-id="a6955-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="a6955-232">You may also do this in XCode as well:</span><span class="sxs-lookup"><span data-stu-id="a6955-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="a6955-233">Step 3: Establish a new redirect URI with your URL Scheme</span><span class="sxs-lookup"><span data-stu-id="a6955-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="a6955-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span><span class="sxs-lookup"><span data-stu-id="a6955-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="a6955-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span><span class="sxs-lookup"><span data-stu-id="a6955-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="a6955-236">This cannot be spoofed by a rogue application.</span><span class="sxs-lookup"><span data-stu-id="a6955-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="a6955-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span><span class="sxs-lookup"><span data-stu-id="a6955-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="a6955-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span><span class="sxs-lookup"><span data-stu-id="a6955-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="a6955-239">Your redirect URI must be in the proper form of:</span><span class="sxs-lookup"><span data-stu-id="a6955-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="a6955-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="a6955-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="a6955-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6955-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="a6955-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="a6955-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="a6955-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span><span class="sxs-lookup"><span data-stu-id="a6955-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="a6955-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span><span class="sxs-lookup"><span data-stu-id="a6955-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="a6955-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="a6955-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="a6955-246">Step 4: iOS9: Add a configuration parameter to your app</span><span class="sxs-lookup"><span data-stu-id="a6955-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="a6955-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span><span class="sxs-lookup"><span data-stu-id="a6955-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="a6955-248">In iOS 9 Apple locked down what schemes an application can query for.</span><span class="sxs-lookup"><span data-stu-id="a6955-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="a6955-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="a6955-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="a6955-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="a6955-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="a6955-251"><array> <string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="a6955-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="a6955-252">You've configured SSO!</span><span class="sxs-lookup"><span data-stu-id="a6955-252">You've configured SSO!</span></span>
<span data-ttu-id="a6955-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span><span class="sxs-lookup"><span data-stu-id="a6955-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

