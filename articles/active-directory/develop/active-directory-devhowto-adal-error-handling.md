---
title: Error handling best practices for Azure Active Directory Authentication Library (ADAL) clients
description: Provides error handling guidance and best practices for ADAL client applications.
services: active-directory
documentationcenter: ''
author: danieldobalian
manager: mtillman
ms.author: celested
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.custom: ''
ms.openlocfilehash: b28e1931b9f615ae0eebe40b101f1959e9fcb40a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867243"
---
# <a name="error-handling-best-practices-for-azure-active-directory-authentication-library-adal-clients"></a><span data-ttu-id="0556f-103">Error handling best practices for Azure Active Directory Authentication Library (ADAL) clients</span><span class="sxs-lookup"><span data-stu-id="0556f-103">Error handling best practices for Azure Active Directory Authentication Library (ADAL) clients</span></span>

<span data-ttu-id="0556f-104">This article provides guidance on the type of errors that developers may encounter, when using ADAL to authenticate users.</span><span class="sxs-lookup"><span data-stu-id="0556f-104">This article provides guidance on the type of errors that developers may encounter, when using ADAL to authenticate users.</span></span> <span data-ttu-id="0556f-105">When using ADAL, there are several cases where a developer may need to step in and handle errors.</span><span class="sxs-lookup"><span data-stu-id="0556f-105">When using ADAL, there are several cases where a developer may need to step in and handle errors.</span></span> <span data-ttu-id="0556f-106">Proper error handling ensures a great end-user experience, and limits the number of times the end user needs to sign in.</span><span class="sxs-lookup"><span data-stu-id="0556f-106">Proper error handling ensures a great end-user experience, and limits the number of times the end user needs to sign in.</span></span>

<span data-ttu-id="0556f-107">In this article, we explore the specific cases for each platform supported by ADAL, and how your application can handle each case properly.</span><span class="sxs-lookup"><span data-stu-id="0556f-107">In this article, we explore the specific cases for each platform supported by ADAL, and how your application can handle each case properly.</span></span> <span data-ttu-id="0556f-108">The error guidance is split into two broader categories, based on the token acquisition patterns provided by ADAL APIs:</span><span class="sxs-lookup"><span data-stu-id="0556f-108">The error guidance is split into two broader categories, based on the token acquisition patterns provided by ADAL APIs:</span></span>

- <span data-ttu-id="0556f-109">**AcquireTokenSilent**: Client attempts to get a token silently (no UI), and may fail if ADAL is unsuccessful.</span><span class="sxs-lookup"><span data-stu-id="0556f-109">**AcquireTokenSilent**: Client attempts to get a token silently (no UI), and may fail if ADAL is unsuccessful.</span></span> 
- <span data-ttu-id="0556f-110">**AcquireToken**: Client can attempt silent acquisition, but can also perform interactive requests that require sign-in.</span><span class="sxs-lookup"><span data-stu-id="0556f-110">**AcquireToken**: Client can attempt silent acquisition, but can also perform interactive requests that require sign-in.</span></span>

> [!TIP]
> <span data-ttu-id="0556f-111">It's a good idea to log all errors and exceptions when using ADAL and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0556f-111">It's a good idea to log all errors and exceptions when using ADAL and Azure AD.</span></span> <span data-ttu-id="0556f-112">Logs are not only helpful for understanding the overall health of your application, but are also important when debugging broader problems.</span><span class="sxs-lookup"><span data-stu-id="0556f-112">Logs are not only helpful for understanding the overall health of your application, but are also important when debugging broader problems.</span></span> <span data-ttu-id="0556f-113">While your application may recover from certain errors, they may hint at broader design problems that require code changes in order to resolve.</span><span class="sxs-lookup"><span data-stu-id="0556f-113">While your application may recover from certain errors, they may hint at broader design problems that require code changes in order to resolve.</span></span> 
> 
> <span data-ttu-id="0556f-114">When implementing the error conditions covered in this document, you should log the error code and description for the reasons discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="0556f-114">When implementing the error conditions covered in this document, you should log the error code and description for the reasons discussed earlier.</span></span> <span data-ttu-id="0556f-115">See the [Error and logging reference](#error-and-logging-reference) for examples of logging code.</span><span class="sxs-lookup"><span data-stu-id="0556f-115">See the [Error and logging reference](#error-and-logging-reference) for examples of logging code.</span></span> 
>

## <a name="acquiretokensilent"></a><span data-ttu-id="0556f-116">AcquireTokenSilent</span><span class="sxs-lookup"><span data-stu-id="0556f-116">AcquireTokenSilent</span></span>

<span data-ttu-id="0556f-117">AcquireTokenSilent attempts to get a token with the guarantee that the end user does not see a User Interface (UI).</span><span class="sxs-lookup"><span data-stu-id="0556f-117">AcquireTokenSilent attempts to get a token with the guarantee that the end user does not see a User Interface (UI).</span></span> <span data-ttu-id="0556f-118">There are several cases where silent acquisition may fail, and needs to be handled through interactive requests or by a default handler.</span><span class="sxs-lookup"><span data-stu-id="0556f-118">There are several cases where silent acquisition may fail, and needs to be handled through interactive requests or by a default handler.</span></span> <span data-ttu-id="0556f-119">We dive into the specifics of when and how to employ each case in the sections that follow.</span><span class="sxs-lookup"><span data-stu-id="0556f-119">We dive into the specifics of when and how to employ each case in the sections that follow.</span></span>

<span data-ttu-id="0556f-120">There is a set of errors generated by the operating system, which may require error handling specific to the application.</span><span class="sxs-lookup"><span data-stu-id="0556f-120">There is a set of errors generated by the operating system, which may require error handling specific to the application.</span></span> <span data-ttu-id="0556f-121">For more information, see "Operating System" errors section in [Error and logging reference](#error-and-logging-reference).</span><span class="sxs-lookup"><span data-stu-id="0556f-121">For more information, see "Operating System" errors section in [Error and logging reference](#error-and-logging-reference).</span></span> 

### <a name="application-scenarios"></a><span data-ttu-id="0556f-122">Application scenarios</span><span class="sxs-lookup"><span data-stu-id="0556f-122">Application scenarios</span></span>

- <span data-ttu-id="0556f-123">[Native client](developer-glossary.md#native-client) applications (iOS, Android, .NET Desktop, or Xamarin)</span><span class="sxs-lookup"><span data-stu-id="0556f-123">[Native client](developer-glossary.md#native-client) applications (iOS, Android, .NET Desktop, or Xamarin)</span></span>
- <span data-ttu-id="0556f-124">[Web client](developer-glossary.md#web-client) applications calling a [resource](developer-glossary.md#resource-server) (.NET)</span><span class="sxs-lookup"><span data-stu-id="0556f-124">[Web client](developer-glossary.md#web-client) applications calling a [resource](developer-glossary.md#resource-server) (.NET)</span></span>

### <a name="error-cases-and-actionable-steps"></a><span data-ttu-id="0556f-125">Error cases and actionable steps</span><span class="sxs-lookup"><span data-stu-id="0556f-125">Error cases and actionable steps</span></span>

<span data-ttu-id="0556f-126">Fundamentally, there are two cases of AcquireTokenSilent errors:</span><span class="sxs-lookup"><span data-stu-id="0556f-126">Fundamentally, there are two cases of AcquireTokenSilent errors:</span></span>

| <span data-ttu-id="0556f-127">Case</span><span class="sxs-lookup"><span data-stu-id="0556f-127">Case</span></span> | <span data-ttu-id="0556f-128">Description</span><span class="sxs-lookup"><span data-stu-id="0556f-128">Description</span></span> |
|------|-------------|
| <span data-ttu-id="0556f-129">**Case 1**: Error is resolvable with an interactive sign-in</span><span class="sxs-lookup"><span data-stu-id="0556f-129">**Case 1**: Error is resolvable with an interactive sign-in</span></span> | <span data-ttu-id="0556f-130">For errors caused by a lack of valid tokens, an interactive request is necessary.</span><span class="sxs-lookup"><span data-stu-id="0556f-130">For errors caused by a lack of valid tokens, an interactive request is necessary.</span></span> <span data-ttu-id="0556f-131">Specifically, cache lookup and an invalid/expired refresh token require an AcquireToken call to resolve.</span><span class="sxs-lookup"><span data-stu-id="0556f-131">Specifically, cache lookup and an invalid/expired refresh token require an AcquireToken call to resolve.</span></span><br><br><span data-ttu-id="0556f-132">In these cases, the end user needs to be prompted to sign in.</span><span class="sxs-lookup"><span data-stu-id="0556f-132">In these cases, the end user needs to be prompted to sign in.</span></span> <span data-ttu-id="0556f-133">The application can choose to do an interactive request immediately, after end-user interaction (such as hitting a sign-in button), or later.</span><span class="sxs-lookup"><span data-stu-id="0556f-133">The application can choose to do an interactive request immediately, after end-user interaction (such as hitting a sign-in button), or later.</span></span> <span data-ttu-id="0556f-134">The choice depends on the desired behavior of the application.</span><span class="sxs-lookup"><span data-stu-id="0556f-134">The choice depends on the desired behavior of the application.</span></span><br><br><span data-ttu-id="0556f-135">See the code in the following section for this specific case and the errors that diagnose it.</span><span class="sxs-lookup"><span data-stu-id="0556f-135">See the code in the following section for this specific case and the errors that diagnose it.</span></span>|
| <span data-ttu-id="0556f-136">**Case 2**: Error is not resolvable with an interactive sign-in</span><span class="sxs-lookup"><span data-stu-id="0556f-136">**Case 2**: Error is not resolvable with an interactive sign-in</span></span> | <span data-ttu-id="0556f-137">For network and transient/temporary errors, or other failures, performing an interactive AcquireToken request does not resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="0556f-137">For network and transient/temporary errors, or other failures, performing an interactive AcquireToken request does not resolve the issue.</span></span> <span data-ttu-id="0556f-138">Unnecessary interactive sign-in prompts can also frustrate end users.</span><span class="sxs-lookup"><span data-stu-id="0556f-138">Unnecessary interactive sign-in prompts can also frustrate end users.</span></span> <span data-ttu-id="0556f-139">ADAL automatically attempts a single retry for most errors on AcquireTokenSilent failures.</span><span class="sxs-lookup"><span data-stu-id="0556f-139">ADAL automatically attempts a single retry for most errors on AcquireTokenSilent failures.</span></span><br><br><span data-ttu-id="0556f-140">The client application can also attempt a retry at some later point, but when and how to do it is dependent on the application behavior and desired end-user experience.</span><span class="sxs-lookup"><span data-stu-id="0556f-140">The client application can also attempt a retry at some later point, but when and how to do it is dependent on the application behavior and desired end-user experience.</span></span> <span data-ttu-id="0556f-141">For example, the application can do an AcquireTokenSilent retry after a few minutes, or in response to some end-user action.</span><span class="sxs-lookup"><span data-stu-id="0556f-141">For example, the application can do an AcquireTokenSilent retry after a few minutes, or in response to some end-user action.</span></span> <span data-ttu-id="0556f-142">An immediate retry will result in the application being throttled, and should not be attempted.</span><span class="sxs-lookup"><span data-stu-id="0556f-142">An immediate retry will result in the application being throttled, and should not be attempted.</span></span><br><br><span data-ttu-id="0556f-143">A subsequent retry failing with the same error does not mean the client should do an interactive request using AcquireToken, as it does not resolve the error.</span><span class="sxs-lookup"><span data-stu-id="0556f-143">A subsequent retry failing with the same error does not mean the client should do an interactive request using AcquireToken, as it does not resolve the error.</span></span><br><br><span data-ttu-id="0556f-144">See the code in the following section for this specific case and the errors that diagnose it.</span><span class="sxs-lookup"><span data-stu-id="0556f-144">See the code in the following section for this specific case and the errors that diagnose it.</span></span> |

### <a name="net"></a><span data-ttu-id="0556f-145">.NET</span><span class="sxs-lookup"><span data-stu-id="0556f-145">.NET</span></span>

<span data-ttu-id="0556f-146">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-146">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-147">acquireTokenSilentAsync(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-147">acquireTokenSilentAsync(…)</span></span>
- <span data-ttu-id="0556f-148">acquireTokenSilentSync(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-148">acquireTokenSilentSync(…)</span></span> 
- <span data-ttu-id="0556f-149">[deprecated] acquireTokenSilent(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-149">[deprecated] acquireTokenSilent(…)</span></span>
- <span data-ttu-id="0556f-150">[deprecated] acquireTokenByRefreshToken(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-150">[deprecated] acquireTokenByRefreshToken(…)</span></span> 

<span data-ttu-id="0556f-151">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-151">Your code would be implemented as follows:</span></span>

```csharp
try{
    AcquireTokenSilentAsync(…);
} 

catch (AdalSilentTokenAcquisitionException e) {
    // Exception: AdalSilentTokenAcquisitionException
    // Caused when there are no tokens in the cache or a required refresh failed. 

    // Action: Case 1, resolvable with an interactive request. 
} 

catch(AdalServiceException e) {
    // Exception: AdalServiceException 
    // Represents an error produced by the STS. 
    // e.ErrorCode contains the error code and description, which can be used for debugging. 
    // NOTE: Do not code a dependency on the contents of the error description, as it can change over time.

    // Action: Case 2, not resolvable with an interactive request.
    // Attempt retry after a timed interval or user action.
} 
    
catch (AdalException e) {
    // Exception: AdalException 
    // Represents a library exception generated by ADAL .NET. 
    // e.ErrorCode contains the error code. 

    // Action: Case 2, not resolvable with an interactive request.
    // Attempt retry after a timed interval or user action.
    // Example Error: network_not_available, default case.
}
```

### <a name="android"></a><span data-ttu-id="0556f-152">Android</span><span class="sxs-lookup"><span data-stu-id="0556f-152">Android</span></span>

<span data-ttu-id="0556f-153">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-153">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-154">acquireTokenSilentSync(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-154">acquireTokenSilentSync(…)</span></span>
- <span data-ttu-id="0556f-155">acquireTokenSilentAsync(...)</span><span class="sxs-lookup"><span data-stu-id="0556f-155">acquireTokenSilentAsync(...)</span></span>
- <span data-ttu-id="0556f-156">[deprecated] acquireTokenSilent(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-156">[deprecated] acquireTokenSilent(…)</span></span>

<span data-ttu-id="0556f-157">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-157">Your code would be implemented as follows:</span></span>

```java
// *Inside callback*
public void onError(Exception e) {

    if (e instanceof AuthenticationException) {
        // Exception: AdalException
        // Represents a library exception generated by ADAL Android.
        // Error Code: e.getCode().

        // Errors: ADALError.ERROR_SILENT_REQUEST,
        // ADALError.AUTH_REFRESH_FAILED_PROMPT_NOT_ALLOWED,
        // ADALError.INVALID_TOKEN_CACHE_ITEM
        // Description: Request failed due to no tokens in
        // cache or failed a required refresh. 

        // Action: Case 1, resolvable with an interactive request. 

        // Action: Case 2, not resolvable with an interactive request.
        // Attempt retry after a timed interval or user action.
        // Example Errors: default case,
        // DEVICE_CONNECTION_IS_NOT_AVAILABLE, 
        // BROKER_AUTHENTICATOR_ERROR_GETAUTHTOKEN,
    }
}
```

### <a name="ios"></a><span data-ttu-id="0556f-158">iOS</span><span class="sxs-lookup"><span data-stu-id="0556f-158">iOS</span></span>

<span data-ttu-id="0556f-159">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-159">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-160">acquireTokenSilentWithResource(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-160">acquireTokenSilentWithResource(…)</span></span>

<span data-ttu-id="0556f-161">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-161">Your code would be implemented as follows:</span></span>

```objc
[context acquireTokenSilentWithResource:[ARGS], completionBlock:^(ADAuthenticationResult *result) {
    if (result.status == AD_FAILED) {
        if ([error.domain isEqualToString:ADAuthenticationErrorDomain]){
            // Exception: AD_FAILED 
            // Represents a library error generated by ADAL Objective-C.
            // Error Code: result.error.code

            // Errors: AD_ERROR_SERVER_REFRESH_TOKEN_REJECTED, AD_ERROR_CACHE_NO_REFRESH_TOKEN
            // Description: No tokens in cache or failed a required token refresh failed. 
            // Action: Case 1, resolvable with an interactive request. 

            // Error: AD_ERROR_CACHE_MULTIPLE_USERS
            // Description: There was ambiguity in the silent request resulting in multiple cache items.
            // Action: Special Case, application should perform another silent request and specify the user using ADUserIdentifier. 
            // Can be caused in cases of a multi-user application. 

            // Action: Case 2, not resolvable with an interactive request.
            // Attempt retry after some time or user action.
            // Example Errors: default case,
            // AD_ERROR_CACHE_BAD_FORMAT
        }
    }
}]
```

## <a name="acquiretoken"></a><span data-ttu-id="0556f-162">AcquireToken</span><span class="sxs-lookup"><span data-stu-id="0556f-162">AcquireToken</span></span>

<span data-ttu-id="0556f-163">AcquireToken is the default ADAL method used to get tokens.</span><span class="sxs-lookup"><span data-stu-id="0556f-163">AcquireToken is the default ADAL method used to get tokens.</span></span> <span data-ttu-id="0556f-164">In cases where user identity is required, AcquireToken attempts to get a token silently first, then displays UI if necessary (unless PromptBehavior.Never is passed).</span><span class="sxs-lookup"><span data-stu-id="0556f-164">In cases where user identity is required, AcquireToken attempts to get a token silently first, then displays UI if necessary (unless PromptBehavior.Never is passed).</span></span> <span data-ttu-id="0556f-165">In cases where application identity is required, AcquireToken attempts to get a token, but doesn't show UI as there is no end user.</span><span class="sxs-lookup"><span data-stu-id="0556f-165">In cases where application identity is required, AcquireToken attempts to get a token, but doesn't show UI as there is no end user.</span></span> 

<span data-ttu-id="0556f-166">When handling AcquireToken errors, error handling is dependent on the platform and scenario the application is trying to achieve.</span><span class="sxs-lookup"><span data-stu-id="0556f-166">When handling AcquireToken errors, error handling is dependent on the platform and scenario the application is trying to achieve.</span></span> 

<span data-ttu-id="0556f-167">The operating system can also generate a set of errors, which require error handling dependent on the specific application.</span><span class="sxs-lookup"><span data-stu-id="0556f-167">The operating system can also generate a set of errors, which require error handling dependent on the specific application.</span></span> <span data-ttu-id="0556f-168">For more information, see "Operating System errors" in [Error and logging reference](#error-and-logging-reference).</span><span class="sxs-lookup"><span data-stu-id="0556f-168">For more information, see "Operating System errors" in [Error and logging reference](#error-and-logging-reference).</span></span> 

### <a name="application-scenarios"></a><span data-ttu-id="0556f-169">Application scenarios</span><span class="sxs-lookup"><span data-stu-id="0556f-169">Application scenarios</span></span>

- <span data-ttu-id="0556f-170">Native client applications (iOS, Android, .NET Desktop, or Xamarin)</span><span class="sxs-lookup"><span data-stu-id="0556f-170">Native client applications (iOS, Android, .NET Desktop, or Xamarin)</span></span>
- <span data-ttu-id="0556f-171">Web applications that call a resource API (.NET)</span><span class="sxs-lookup"><span data-stu-id="0556f-171">Web applications that call a resource API (.NET)</span></span>
- <span data-ttu-id="0556f-172">Single Page Applications (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="0556f-172">Single Page Applications (JavaScript)</span></span>
- <span data-ttu-id="0556f-173">Service-to-Service applications (.NET, Java)</span><span class="sxs-lookup"><span data-stu-id="0556f-173">Service-to-Service applications (.NET, Java)</span></span>
  - <span data-ttu-id="0556f-174">All scenarios, including on-behalf-of</span><span class="sxs-lookup"><span data-stu-id="0556f-174">All scenarios, including on-behalf-of</span></span>
  - <span data-ttu-id="0556f-175">On-Behalf-of specific scenarios</span><span class="sxs-lookup"><span data-stu-id="0556f-175">On-Behalf-of specific scenarios</span></span>

### <a name="error-cases-and-actionable-steps-native-client-applications"></a><span data-ttu-id="0556f-176">Error cases and actionable steps: Native client applications</span><span class="sxs-lookup"><span data-stu-id="0556f-176">Error cases and actionable steps: Native client applications</span></span>

<span data-ttu-id="0556f-177">If you're building a native client application, there are a few error handling cases to consider which relate to network issues, transient failures, and other platform-specific errors.</span><span class="sxs-lookup"><span data-stu-id="0556f-177">If you're building a native client application, there are a few error handling cases to consider which relate to network issues, transient failures, and other platform-specific errors.</span></span> <span data-ttu-id="0556f-178">In most cases, an application shouldn’t perform immediate retries, but rather wait for end-user interaction that prompts a sign-in.</span><span class="sxs-lookup"><span data-stu-id="0556f-178">In most cases, an application shouldn’t perform immediate retries, but rather wait for end-user interaction that prompts a sign-in.</span></span> 

<span data-ttu-id="0556f-179">There are a few special cases in which a single retry may resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="0556f-179">There are a few special cases in which a single retry may resolve the issue.</span></span> <span data-ttu-id="0556f-180">For example, when a user needs to enable data on a device, or completed the Azure AD broker download after the initial failure.</span><span class="sxs-lookup"><span data-stu-id="0556f-180">For example, when a user needs to enable data on a device, or completed the Azure AD broker download after the initial failure.</span></span> 

<span data-ttu-id="0556f-181">In cases of failure, an application can present UI to allow the end user to perform some interaction that prompts a retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-181">In cases of failure, an application can present UI to allow the end user to perform some interaction that prompts a retry.</span></span> <span data-ttu-id="0556f-182">For instance, if the device failed for an offline error, a "Try to Sign in again" button prompting an AcquireToken retry rather than immediately retrying the failure.</span><span class="sxs-lookup"><span data-stu-id="0556f-182">For instance, if the device failed for an offline error, a "Try to Sign in again" button prompting an AcquireToken retry rather than immediately retrying the failure.</span></span> 

<span data-ttu-id="0556f-183">Error handling in native applications can be defined by two cases:</span><span class="sxs-lookup"><span data-stu-id="0556f-183">Error handling in native applications can be defined by two cases:</span></span>

|  |  |
|------|-------------|
| <span data-ttu-id="0556f-184">**Case 1**:</span><span class="sxs-lookup"><span data-stu-id="0556f-184">**Case 1**:</span></span><br><span data-ttu-id="0556f-185">Non-Retryable Error (most cases)</span><span class="sxs-lookup"><span data-stu-id="0556f-185">Non-Retryable Error (most cases)</span></span> | <span data-ttu-id="0556f-186">1. Do not attempt immediate retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-186">1. Do not attempt immediate retry.</span></span> <span data-ttu-id="0556f-187">Present the end-user UI based on the specific error that invokes a retry ("Try to Sign in again", "Download Azure AD broker application", etc).</span><span class="sxs-lookup"><span data-stu-id="0556f-187">Present the end-user UI based on the specific error that invokes a retry ("Try to Sign in again", "Download Azure AD broker application", etc).</span></span> |
| <span data-ttu-id="0556f-188">**Case 2**:</span><span class="sxs-lookup"><span data-stu-id="0556f-188">**Case 2**:</span></span><br><span data-ttu-id="0556f-189">Retryable Error</span><span class="sxs-lookup"><span data-stu-id="0556f-189">Retryable Error</span></span> | <span data-ttu-id="0556f-190">1. Perform a single retry as the end user may have entered a state that results in a success.</span><span class="sxs-lookup"><span data-stu-id="0556f-190">1. Perform a single retry as the end user may have entered a state that results in a success.</span></span><br><br><span data-ttu-id="0556f-191">2. If retry fails, present the end-user UI based on the specific error that invokes a retry ("Try to Sign in again", "Download Azure AD broker app", etc.).</span><span class="sxs-lookup"><span data-stu-id="0556f-191">2. If retry fails, present the end-user UI based on the specific error that invokes a retry ("Try to Sign in again", "Download Azure AD broker app", etc.).</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="0556f-192">If a user account is passed to ADAL in a silent call and fails, the subsequent interactive request allows the end user to sign in using a different account.</span><span class="sxs-lookup"><span data-stu-id="0556f-192">If a user account is passed to ADAL in a silent call and fails, the subsequent interactive request allows the end user to sign in using a different account.</span></span> <span data-ttu-id="0556f-193">After a successful AcquireToken using a user account, the application must verify the signed-in user matches the applications's local user object.</span><span class="sxs-lookup"><span data-stu-id="0556f-193">After a successful AcquireToken using a user account, the application must verify the signed-in user matches the applications's local user object.</span></span> <span data-ttu-id="0556f-194">A mismatch does not generate an exception (except in Objective C), but should be considered in cases where a user is known locally before the authentication requests (like a failed silent call).</span><span class="sxs-lookup"><span data-stu-id="0556f-194">A mismatch does not generate an exception (except in Objective C), but should be considered in cases where a user is known locally before the authentication requests (like a failed silent call).</span></span>
>

#### <a name="net"></a><span data-ttu-id="0556f-195">.NET</span><span class="sxs-lookup"><span data-stu-id="0556f-195">.NET</span></span>

<span data-ttu-id="0556f-196">The following guidance provides examples for error handling in conjunction with all non-silent AcquireToken(…) ADAL methods, *except*:</span><span class="sxs-lookup"><span data-stu-id="0556f-196">The following guidance provides examples for error handling in conjunction with all non-silent AcquireToken(…) ADAL methods, *except*:</span></span> 

- <span data-ttu-id="0556f-197">AcquireTokenAsync(…, IClientAssertionCertification, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-197">AcquireTokenAsync(…, IClientAssertionCertification, …)</span></span>
- <span data-ttu-id="0556f-198">AcquireTokenAsync(…,ClientCredential, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-198">AcquireTokenAsync(…,ClientCredential, …)</span></span>
- <span data-ttu-id="0556f-199">AcquireTokenAsync(…,ClientAssertion, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-199">AcquireTokenAsync(…,ClientAssertion, …)</span></span>
- <span data-ttu-id="0556f-200">AcquireTokenAsync(…,UserAssertion,…)</span><span class="sxs-lookup"><span data-stu-id="0556f-200">AcquireTokenAsync(…,UserAssertion,…)</span></span>   

<span data-ttu-id="0556f-201">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-201">Your code would be implemented as follows:</span></span>

```csharp
try {
    AcquireTokenAsync(…);
} 
    
catch(AdalServiceException e) {
    // Exception: AdalServiceException 
    // Represents an error produced by the STS. 
    // e.ErrorCode contains the error code and description, which can be used for debugging. 
    // NOTE: Do not code a dependency on the contents of the error description, as it can change over time.
    
    // Design time consideration: Certain errors may be caused at development and exposed through this exception. 
    // Looking inside the description will give more guidance on resolving the specific issue. 

    // Action: Case 1: Non-Retryable 
    // Do not perform an immediate retry. Only retry after user action. 
    // Example Errors: default case

    } 

catch (AdalException e) {
    // Exception: AdalException 
    // Represents a library exception generated by ADAL .NET.
    // e.ErrorCode contains the error code

    // Action: Case 1, Non-Retryable 
    // Do not perform an immediate retry. Only retry after user action. 
    // Example Errors: network_not_available, default case
}
```

> [!NOTE]
> <span data-ttu-id="0556f-202">ADAL .NET has an extra consideration as it supports PromptBehavior.Never, which has behavior like AcquireTokenSilent.</span><span class="sxs-lookup"><span data-stu-id="0556f-202">ADAL .NET has an extra consideration as it supports PromptBehavior.Never, which has behavior like AcquireTokenSilent.</span></span>
>

<span data-ttu-id="0556f-203">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-203">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-204">acquireToken(…, PromptBehavior.Never)</span><span class="sxs-lookup"><span data-stu-id="0556f-204">acquireToken(…, PromptBehavior.Never)</span></span>

<span data-ttu-id="0556f-205">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-205">Your code would be implemented as follows:</span></span>

```csharp
    try {acquireToken(…, PromptBehavior.Never);
    } 

catch(AdalServiceException e) {
    // Exception: AdalServiceException represents 
    // Represents an error produced by the STS. 
    // e.ErrorCode contains the error code and description, which can be used for debugging. 
    // NOTE: Do not code a dependency on the contents of the error description, as it can change over time.

    // Action: Case 1: Non-Retryable 
    // Do not perform an immediate retry. Only retry after user action. 
    // Example Errors: default case

} catch (AdalException e) {
    // Error Code: e.ErrorCode == "user_interaction_required"
    // Description: user_interaction_required indicates the silent request failed 
    // in a way that's resolvable with an interactive request.
    // Action: Resolvable with an interactive request. 

    // Action: Case 1, Non-Retryable 
    // Do not perform an immediate retry. Only retry after user action. 
    // Example Errors: network_not_available, default case
}
```

#### <a name="android"></a><span data-ttu-id="0556f-206">Android</span><span class="sxs-lookup"><span data-stu-id="0556f-206">Android</span></span>

<span data-ttu-id="0556f-207">The following guidance provides examples for error handling in conjunction with all non-silent AcquireToken(…) ADAL methods.</span><span class="sxs-lookup"><span data-stu-id="0556f-207">The following guidance provides examples for error handling in conjunction with all non-silent AcquireToken(…) ADAL methods.</span></span> 

<span data-ttu-id="0556f-208">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-208">Your code would be implemented as follows:</span></span>

```java
AcquireTokenAsync(…);

// *Inside callback*
public void onError(Exception e) {
    if (e instanceof AuthenticationException) {
        // Exception: AdalException 
        // Represents a library exception generated by ADAL Android.
        // Error Code: e.getCode();

        // Error: ADALError.BROKER_APP_INSTALLATION_STARTED
        // Description: Broker app not installed, user will be prompted to download the app. 

        // Action: Case 2, Retriable Error 
        // Perform a single retry. If that fails, only try again after user action. 

        // Action: Case 1, Non-Retriable 
        // Do not perform an immediate retry. Only retry after user action. 
        // Example Errors: default case, DEVICE_CONNECTION_IS_NOT_AVAILABLE
    }
}
```

#### <a name="ios"></a><span data-ttu-id="0556f-209">iOS</span><span class="sxs-lookup"><span data-stu-id="0556f-209">iOS</span></span>

<span data-ttu-id="0556f-210">The following guidance provides examples for error handling in conjunction with all non-silent AcquireToken(…) ADAL methods.</span><span class="sxs-lookup"><span data-stu-id="0556f-210">The following guidance provides examples for error handling in conjunction with all non-silent AcquireToken(…) ADAL methods.</span></span> 

<span data-ttu-id="0556f-211">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-211">Your code would be implemented as follows:</span></span>

```objc
[context acquireTokenWithResource:[ARGS], completionBlock:^(ADAuthenticationResult *result) {
    if (result.status == AD_FAILED) {
        if ([error.domain isEqualToString:ADAuthenticationErrorDomain]){
            // Exception: AD_FAILED 
            // Represents a library error generated by ADAL ObjC.
            // Error Code: result.error.code 

            // Error: AD_ERROR_SERVER_WRONG_USER
            // Description: App passed a user into ADAL and the end user signed in with a different account. 
            // Action: Case 1, Non-retriable (as is) and up to the application on how to handle this case. 
            // It can attempt a new request without specifying the user, or use UI to clarify the user account to sign in. 

            // Action: Case 1, Non-Retriable 
            // Do not perform an immediate retry. Only retry after user action. 
            // Example Errors: default case
        }
    }
}]
```

### <a name="error-cases-and-actionable-steps-web-applications-that-call-a-resource-api-net"></a><span data-ttu-id="0556f-212">Error cases and actionable steps: Web applications that call a resource API (.NET)</span><span class="sxs-lookup"><span data-stu-id="0556f-212">Error cases and actionable steps: Web applications that call a resource API (.NET)</span></span>

<span data-ttu-id="0556f-213">If you're building a .NET web app that calls gets a token using an authorization code for a resource, the only code required is a default handler for the generic case.</span><span class="sxs-lookup"><span data-stu-id="0556f-213">If you're building a .NET web app that calls gets a token using an authorization code for a resource, the only code required is a default handler for the generic case.</span></span> 

<span data-ttu-id="0556f-214">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-214">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-215">AcquireTokenByAuthorizationCodeAsync(…)</span><span class="sxs-lookup"><span data-stu-id="0556f-215">AcquireTokenByAuthorizationCodeAsync(…)</span></span>

<span data-ttu-id="0556f-216">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-216">Your code would be implemented as follows:</span></span>

```csharp
try {
    AcquireTokenByAuthorizationCodeAsync(…);
} 

catch (AdalException e) {
    // Exception: AdalException
    // Represents a library exception generated by ADAL .NET.
    // Error Code: e.ErrorCode

    // Action: Do not perform an immediate retry. Only try again after user action or wait until much later. 
    // Example Errors: default case
}
```

### <a name="error-cases-and-actionable-steps-single-page-applications-adaljs"></a><span data-ttu-id="0556f-217">Error cases and actionable steps: Single Page Applications (adal.js)</span><span class="sxs-lookup"><span data-stu-id="0556f-217">Error cases and actionable steps: Single Page Applications (adal.js)</span></span>

<span data-ttu-id="0556f-218">If you're building a single page application using adal.js with AcquireToken, the error handling code is similar to that of a typical silent call.</span><span class="sxs-lookup"><span data-stu-id="0556f-218">If you're building a single page application using adal.js with AcquireToken, the error handling code is similar to that of a typical silent call.</span></span> <span data-ttu-id="0556f-219">Specifically in adal.js, AcquireToken never shows a UI.</span><span class="sxs-lookup"><span data-stu-id="0556f-219">Specifically in adal.js, AcquireToken never shows a UI.</span></span> 

<span data-ttu-id="0556f-220">A failed AcquireToken has the following cases:</span><span class="sxs-lookup"><span data-stu-id="0556f-220">A failed AcquireToken has the following cases:</span></span>

|  |  |
|------|-------------|
| <span data-ttu-id="0556f-221">**Case 1**:</span><span class="sxs-lookup"><span data-stu-id="0556f-221">**Case 1**:</span></span><br><span data-ttu-id="0556f-222">Resolvable with an interactive request</span><span class="sxs-lookup"><span data-stu-id="0556f-222">Resolvable with an interactive request</span></span> | <span data-ttu-id="0556f-223">1. If login() fails, do not perform immediate retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-223">1. If login() fails, do not perform immediate retry.</span></span> <span data-ttu-id="0556f-224">Only retry after user action prompts a retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-224">Only retry after user action prompts a retry.</span></span>|
| <span data-ttu-id="0556f-225">**Case 2**:</span><span class="sxs-lookup"><span data-stu-id="0556f-225">**Case 2**:</span></span><br><span data-ttu-id="0556f-226">Not Resolvable with an interactive request.</span><span class="sxs-lookup"><span data-stu-id="0556f-226">Not Resolvable with an interactive request.</span></span> <span data-ttu-id="0556f-227">Error is retryable.</span><span class="sxs-lookup"><span data-stu-id="0556f-227">Error is retryable.</span></span> | <span data-ttu-id="0556f-228">1. Perform a single retry as the end user major have entered a state that results in a success.</span><span class="sxs-lookup"><span data-stu-id="0556f-228">1. Perform a single retry as the end user major have entered a state that results in a success.</span></span><br><br><span data-ttu-id="0556f-229">2. If retry fails, present the end user with an action based on the specific error that can invoke a retry ("Try to Sign in again").</span><span class="sxs-lookup"><span data-stu-id="0556f-229">2. If retry fails, present the end user with an action based on the specific error that can invoke a retry ("Try to Sign in again").</span></span> |
| <span data-ttu-id="0556f-230">**Case 3**:</span><span class="sxs-lookup"><span data-stu-id="0556f-230">**Case 3**:</span></span><br><span data-ttu-id="0556f-231">Not Resolvable with an interactive request.</span><span class="sxs-lookup"><span data-stu-id="0556f-231">Not Resolvable with an interactive request.</span></span> <span data-ttu-id="0556f-232">Error is not retryable.</span><span class="sxs-lookup"><span data-stu-id="0556f-232">Error is not retryable.</span></span> | <span data-ttu-id="0556f-233">1. Do not attempt immediate retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-233">1. Do not attempt immediate retry.</span></span> <span data-ttu-id="0556f-234">Present the end user with an action based on the specific error that can invoke a retry ("Try to Sign in again").</span><span class="sxs-lookup"><span data-stu-id="0556f-234">Present the end user with an action based on the specific error that can invoke a retry ("Try to Sign in again").</span></span> |

<span data-ttu-id="0556f-235">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-235">Your code would be implemented as follows:</span></span>

```javascript
AuthContext.acquireToken(…, function(error, errorDesc, token) {
    if (error || errorDesc) {
        // Represents any token acquisition failure that occurred. 
        // Error Code: error.indexOf("<ERROR_STRING>")

        // Errors: if (error.indexOf("interaction_required"))
        //         if (error.indexOf("login required"))
        // Description: ADAL wasn't able to silently acquire a token because of expire or fresh session. 
        // Action: Case 1, Resolvable with an interactive login() request. 

        // Error: if (error.indexOf("Token Renewal Failed")) 
        // Description: Timeout when refreshing the token.
        // Action: Case 2, Not resolvable interactively, error is retriable.
        // Perform a single retry. Only try again after user action.

        // Action: Case 3, Not resolvable interactively, error is not retriable. 
        // Do not perform an immediate retry. Only retry after user action.
        // Example Errors: default case
    }
}
```

### <a name="error-cases-and-actionable-steps-service-to-service-applications-net-only"></a><span data-ttu-id="0556f-236">Error cases and actionable steps: service-to-service applications (.NET only)</span><span class="sxs-lookup"><span data-stu-id="0556f-236">Error cases and actionable steps: service-to-service applications (.NET only)</span></span>

<span data-ttu-id="0556f-237">If you're building a service-to-service application that uses AcquireToken, there are a few key errors your code must handle.</span><span class="sxs-lookup"><span data-stu-id="0556f-237">If you're building a service-to-service application that uses AcquireToken, there are a few key errors your code must handle.</span></span> <span data-ttu-id="0556f-238">The only recourse to failure is to return the error back to the calling app (for on-behalf-of cases) or apply a retry strategy.</span><span class="sxs-lookup"><span data-stu-id="0556f-238">The only recourse to failure is to return the error back to the calling app (for on-behalf-of cases) or apply a retry strategy.</span></span> 

#### <a name="all-scenarios"></a><span data-ttu-id="0556f-239">All scenarios</span><span class="sxs-lookup"><span data-stu-id="0556f-239">All scenarios</span></span>

<span data-ttu-id="0556f-240">For *all* service-to-service application scenarios, including on-behalf-of:</span><span class="sxs-lookup"><span data-stu-id="0556f-240">For *all* service-to-service application scenarios, including on-behalf-of:</span></span>

- <span data-ttu-id="0556f-241">Do not attempt an immediate retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-241">Do not attempt an immediate retry.</span></span> <span data-ttu-id="0556f-242">ADAL attempts a single retry for certain failed requests.</span><span class="sxs-lookup"><span data-stu-id="0556f-242">ADAL attempts a single retry for certain failed requests.</span></span> 
- <span data-ttu-id="0556f-243">Only continue retrying after a user or app action is prompts a retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-243">Only continue retrying after a user or app action is prompts a retry.</span></span> <span data-ttu-id="0556f-244">For example, a daemon application that does work on some set interval should wait until the next interval to retry.</span><span class="sxs-lookup"><span data-stu-id="0556f-244">For example, a daemon application that does work on some set interval should wait until the next interval to retry.</span></span>

<span data-ttu-id="0556f-245">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-245">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-246">AcquireTokenAsync(…, IClientAssertionCertification, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-246">AcquireTokenAsync(…, IClientAssertionCertification, …)</span></span>
- <span data-ttu-id="0556f-247">AcquireTokenAsync(…,ClientCredential, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-247">AcquireTokenAsync(…,ClientCredential, …)</span></span>
- <span data-ttu-id="0556f-248">AcquireTokenAsync(…,ClientAssertion, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-248">AcquireTokenAsync(…,ClientAssertion, …)</span></span>
- <span data-ttu-id="0556f-249">AcquireTokenAsync(…,UserAssertion, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-249">AcquireTokenAsync(…,UserAssertion, …)</span></span>

<span data-ttu-id="0556f-250">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-250">Your code would be implemented as follows:</span></span>

```csharp
try {
    AcquireTokenAsync(…);
} 

catch (AdalException e) {
    // Exception: AdalException
    // Represents a library exception generated by ADAL .NET.
    // Error Code: e.ErrorCode

    // Action: Do not perform an immediate retry. Only try again after user action (if applicable) or wait until much later. 
    // Example Errors: default case
}  
```

#### <a name="on-behalf-of-scenarios"></a><span data-ttu-id="0556f-251">On-behalf-of scenarios</span><span class="sxs-lookup"><span data-stu-id="0556f-251">On-behalf-of scenarios</span></span>

<span data-ttu-id="0556f-252">For *on-behalf-of* service-to-service application scenarios.</span><span class="sxs-lookup"><span data-stu-id="0556f-252">For *on-behalf-of* service-to-service application scenarios.</span></span>

<span data-ttu-id="0556f-253">The following guidance provides examples for error handling in conjunction with ADAL methods:</span><span class="sxs-lookup"><span data-stu-id="0556f-253">The following guidance provides examples for error handling in conjunction with ADAL methods:</span></span> 

- <span data-ttu-id="0556f-254">AcquireTokenAsync(…, UserAssertion, …)</span><span class="sxs-lookup"><span data-stu-id="0556f-254">AcquireTokenAsync(…, UserAssertion, …)</span></span>

<span data-ttu-id="0556f-255">Your code would be implemented as follows:</span><span class="sxs-lookup"><span data-stu-id="0556f-255">Your code would be implemented as follows:</span></span>

```csharp
try {
AcquireTokenAsync(…);
} 

catch (AdalServiceException e) {
    // Exception: AdalServiceException 
    // Represents an error produced by the STS. 
    // e.ErrorCode contains the error code and description, which can be used for debugging. 
    // NOTE: Do not code a dependency on the contents of the error description, as it can change over time.

    // Error: On-Behalf-Of Error Handler
    if (e.ErrorCode == "interaction_required") {
        // Description: The client needs to perform some action due to a config from admin. 
        // Action: Capture `claims` parameter inside ex.InnerException.InnerException.
        // Generate HTTP error 403 with claims, throw back HTTP error to client.
        // Wait for client to retry. 
    }
} 
        
catch (AdalException e) {
    // Exception: AdalException 
    // Represents a library exception generated by ADAL .NET.
    // Error Code: e.ErrorCode

    // Action: Do not perform an immediate retry. Only try again after user action (if applicable) or wait until much later. 
    // Example Error: default case
}
```

<span data-ttu-id="0556f-256">We've built a [complete sample](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) that demonstrates this scenario.</span><span class="sxs-lookup"><span data-stu-id="0556f-256">We've built a [complete sample](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) that demonstrates this scenario.</span></span>

## <a name="error-and-logging-reference"></a><span data-ttu-id="0556f-257">Error and logging reference</span><span class="sxs-lookup"><span data-stu-id="0556f-257">Error and logging reference</span></span>

### <a name="logging-personal-identifiable-information-pii--organizational-identifiable-information-oii"></a><span data-ttu-id="0556f-258">Logging Personal Identifiable Information (PII) & Organizational Identifiable Information (OII)</span><span class="sxs-lookup"><span data-stu-id="0556f-258">Logging Personal Identifiable Information (PII) & Organizational Identifiable Information (OII)</span></span>
<span data-ttu-id="0556f-259">By default, ADAL logging does not capture or log any PII or OII.</span><span class="sxs-lookup"><span data-stu-id="0556f-259">By default, ADAL logging does not capture or log any PII or OII.</span></span> <span data-ttu-id="0556f-260">The library allows app developers to turn this on through a setter in the Logger class.</span><span class="sxs-lookup"><span data-stu-id="0556f-260">The library allows app developers to turn this on through a setter in the Logger class.</span></span> <span data-ttu-id="0556f-261">By turning on PII or OII, the app takes responsibility for safely handling highly-sensitive data and complying with any regulatory requirements.</span><span class="sxs-lookup"><span data-stu-id="0556f-261">By turning on PII or OII, the app takes responsibility for safely handling highly-sensitive data and complying with any regulatory requirements.</span></span>

### <a name="net"></a><span data-ttu-id="0556f-262">.NET</span><span class="sxs-lookup"><span data-stu-id="0556f-262">.NET</span></span>

#### <a name="adal-library-errors"></a><span data-ttu-id="0556f-263">ADAL library errors</span><span class="sxs-lookup"><span data-stu-id="0556f-263">ADAL library errors</span></span>

<span data-ttu-id="0556f-264">To explore specific ADAL errors, the source code in the [azure-activedirectory-library-for-dotnet repository](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/8f6d560fbede2247ec0e217a21f6929d4375dcaa/src/ADAL.PCL/Utilities/Constants.cs#L58) is the best error reference.</span><span class="sxs-lookup"><span data-stu-id="0556f-264">To explore specific ADAL errors, the source code in the [azure-activedirectory-library-for-dotnet repository](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/8f6d560fbede2247ec0e217a21f6929d4375dcaa/src/ADAL.PCL/Utilities/Constants.cs#L58) is the best error reference.</span></span>

#### <a name="guidance-for-error-logging-code"></a><span data-ttu-id="0556f-265">Guidance for error logging code</span><span class="sxs-lookup"><span data-stu-id="0556f-265">Guidance for error logging code</span></span>

<span data-ttu-id="0556f-266">ADAL .NET logging changes depending on the platform being worked on.</span><span class="sxs-lookup"><span data-stu-id="0556f-266">ADAL .NET logging changes depending on the platform being worked on.</span></span> <span data-ttu-id="0556f-267">Refer to the [Logging wiki](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/wiki/Logging-in-ADAL.Net) for code on how to enable logging.</span><span class="sxs-lookup"><span data-stu-id="0556f-267">Refer to the [Logging wiki](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/wiki/Logging-in-ADAL.Net) for code on how to enable logging.</span></span>

### <a name="android"></a><span data-ttu-id="0556f-268">Android</span><span class="sxs-lookup"><span data-stu-id="0556f-268">Android</span></span>

#### <a name="adal-library-errors"></a><span data-ttu-id="0556f-269">ADAL library errors</span><span class="sxs-lookup"><span data-stu-id="0556f-269">ADAL library errors</span></span>

<span data-ttu-id="0556f-270">To explore specific ADAL errors, the source code in the [azure-activedirectory-library-for-android repository](https://github.com/AzureAD/azure-activedirectory-library-for-android/blob/dev/adal/src/main/java/com/microsoft/aad/adal/ADALError.java#L33) is the best error reference.</span><span class="sxs-lookup"><span data-stu-id="0556f-270">To explore specific ADAL errors, the source code in the [azure-activedirectory-library-for-android repository](https://github.com/AzureAD/azure-activedirectory-library-for-android/blob/dev/adal/src/main/java/com/microsoft/aad/adal/ADALError.java#L33) is the best error reference.</span></span>

#### <a name="operating-system-errors"></a><span data-ttu-id="0556f-271">Operating System errors</span><span class="sxs-lookup"><span data-stu-id="0556f-271">Operating System errors</span></span>

<span data-ttu-id="0556f-272">Android OS errors are exposed through AuthenticationException in ADAL, are identifiable as "SERVER_INVALID_REQUEST", and can be further granular through the error descriptions.</span><span class="sxs-lookup"><span data-stu-id="0556f-272">Android OS errors are exposed through AuthenticationException in ADAL, are identifiable as "SERVER_INVALID_REQUEST", and can be further granular through the error descriptions.</span></span> 

<span data-ttu-id="0556f-273">For a full list of common errors and what steps to take when your app or end users encounter them, refer to the [ADAL Android Wiki](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki).</span><span class="sxs-lookup"><span data-stu-id="0556f-273">For a full list of common errors and what steps to take when your app or end users encounter them, refer to the [ADAL Android Wiki](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki).</span></span> 

#### <a name="guidance-for-error-logging-code"></a><span data-ttu-id="0556f-274">Guidance for error logging code</span><span class="sxs-lookup"><span data-stu-id="0556f-274">Guidance for error logging code</span></span>

```java
// 1. Configure Logger
Logger.getInstance().setExternalLogger(new ILogger() {    
    @Override   
    public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) { 
    // …
    // You can write this to logfile depending on level or errorcode. 
    writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);    
    }
}

// 2. Set the log level
Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

// By default, the `Logger` does not capture any PII or OII

// PII or OII will be logged
Logger.getInstance().setEnablePII(true);

// To STOP logging PII or OII, use the following setter
Logger.getInstance().setEnablePII(false);


// 3. Send logs to logcat.
adb logcat > "C:\logmsg\logfile.txt";
```

### <a name="ios"></a><span data-ttu-id="0556f-275">iOS</span><span class="sxs-lookup"><span data-stu-id="0556f-275">iOS</span></span>

#### <a name="adal-library-errors"></a><span data-ttu-id="0556f-276">ADAL library errors</span><span class="sxs-lookup"><span data-stu-id="0556f-276">ADAL library errors</span></span>

<span data-ttu-id="0556f-277">To explore specific ADAL errors, the source code in the [azure-activedirectory-library-for-objc repository](https://github.com/AzureAD/azure-activedirectory-library-for-objc/blob/dev/ADAL/src/ADAuthenticationError.m#L295) is the best error reference.</span><span class="sxs-lookup"><span data-stu-id="0556f-277">To explore specific ADAL errors, the source code in the [azure-activedirectory-library-for-objc repository](https://github.com/AzureAD/azure-activedirectory-library-for-objc/blob/dev/ADAL/src/ADAuthenticationError.m#L295) is the best error reference.</span></span>

#### <a name="operating-system-errors"></a><span data-ttu-id="0556f-278">Operating System errors</span><span class="sxs-lookup"><span data-stu-id="0556f-278">Operating System errors</span></span>

<span data-ttu-id="0556f-279">iOS errors may arise during sign-in when users use web views, and the nature of authentication.</span><span class="sxs-lookup"><span data-stu-id="0556f-279">iOS errors may arise during sign-in when users use web views, and the nature of authentication.</span></span> <span data-ttu-id="0556f-280">This can be caused by conditions such as SSL errors, timeouts, or network errors:</span><span class="sxs-lookup"><span data-stu-id="0556f-280">This can be caused by conditions such as SSL errors, timeouts, or network errors:</span></span>

- <span data-ttu-id="0556f-281">For Entitlement Sharing, logins are not persistent and the cache appears empty.</span><span class="sxs-lookup"><span data-stu-id="0556f-281">For Entitlement Sharing, logins are not persistent and the cache appears empty.</span></span> <span data-ttu-id="0556f-282">You can resolve by adding the following line of code to the keychain: `[[ADAuthenticationSettings sharedInstance] setSharedCacheKeychainGroup:nil];`</span><span class="sxs-lookup"><span data-stu-id="0556f-282">You can resolve by adding the following line of code to the keychain: `[[ADAuthenticationSettings sharedInstance] setSharedCacheKeychainGroup:nil];`</span></span>
- <span data-ttu-id="0556f-283">For the NsUrlDomain set of errors, the action changes depending on the app logic.</span><span class="sxs-lookup"><span data-stu-id="0556f-283">For the NsUrlDomain set of errors, the action changes depending on the app logic.</span></span> <span data-ttu-id="0556f-284">See the [NSURLErrorDomain reference documentation](https://developer.apple.com/documentation/foundation/nsurlerrordomain#declarations) for specific instances that can be handled.</span><span class="sxs-lookup"><span data-stu-id="0556f-284">See the [NSURLErrorDomain reference documentation](https://developer.apple.com/documentation/foundation/nsurlerrordomain#declarations) for specific instances that can be handled.</span></span>
- <span data-ttu-id="0556f-285">See [ADAL Obj-C Common Issues](https://github.com/AzureAD/azure-activedirectory-library-for-objc#adauthenticationerror) for the list of common errors maintained by the ADAL Objective-C team.</span><span class="sxs-lookup"><span data-stu-id="0556f-285">See [ADAL Obj-C Common Issues](https://github.com/AzureAD/azure-activedirectory-library-for-objc#adauthenticationerror) for the list of common errors maintained by the ADAL Objective-C team.</span></span>

#### <a name="guidance-for-error-logging-code"></a><span data-ttu-id="0556f-286">Guidance for error logging code</span><span class="sxs-lookup"><span data-stu-id="0556f-286">Guidance for error logging code</span></span>

```objc
// 1. Enable NSLogging
[ADLogger setNSLogging:YES];

// 2. Set the log level (if you want verbose)
[ADLogger setLevel:ADAL_LOG_LEVEL_VERBOSE];

// 3. Set up a callback block to simply print out
[ADLogger setLogCallBack:^(ADAL_LOG_LEVEL logLevel, NSString *message, NSString *additionalInformation, NSInteger errorCode, NSDictionary *userInfo) {
     NSString* log = [NSString stringWithFormat:@"%@ %@", message, additionalInformation];    
     NSLog(@"%@", log);
}];
```

### <a name="guidance-for-error-logging-code---javascript"></a><span data-ttu-id="0556f-287">Guidance for error logging code - JavaScript</span><span class="sxs-lookup"><span data-stu-id="0556f-287">Guidance for error logging code - JavaScript</span></span> 

```javascript
0: Error1: Warning2: Info3: Verbose
window.Logging = {
    level: 3,
    log: function (message) {
        console.log(message);
    }
};
```
## <a name="related-content"></a><span data-ttu-id="0556f-288">Related content</span><span class="sxs-lookup"><span data-stu-id="0556f-288">Related content</span></span>

* <span data-ttu-id="0556f-289">[Azure AD Developer's Guide][AAD-Dev-Guide]</span><span class="sxs-lookup"><span data-stu-id="0556f-289">[Azure AD Developer's Guide][AAD-Dev-Guide]</span></span>
* <span data-ttu-id="0556f-290">[Azure AD Authentication Libraries][AAD-Auth-Libraries]</span><span class="sxs-lookup"><span data-stu-id="0556f-290">[Azure AD Authentication Libraries][AAD-Auth-Libraries]</span></span>
* <span data-ttu-id="0556f-291">[Azure AD Authentication Scenarios][AAD-Auth-Scenarios]</span><span class="sxs-lookup"><span data-stu-id="0556f-291">[Azure AD Authentication Scenarios][AAD-Auth-Scenarios]</span></span>
* <span data-ttu-id="0556f-292">[Integrating Applications with Azure Active Directory][AAD-Integrating-Apps]</span><span class="sxs-lookup"><span data-stu-id="0556f-292">[Integrating Applications with Azure Active Directory][AAD-Integrating-Apps]</span></span>

<span data-ttu-id="0556f-293">Use the comments section that follows, to provide feedback and help us refine and shape our content.</span><span class="sxs-lookup"><span data-stu-id="0556f-293">Use the comments section that follows, to provide feedback and help us refine and shape our content.</span></span>

<span data-ttu-id="0556f-294">[![Sign in button][AAD-Sign-In]][AAD-Sign-In]
<!--Reference style links --> [AAD-Auth-Libraries]: ./active-directory-authentication-libraries.md [AAD-Auth-Scenarios]:authentication-scenarios.md [AAD-Dev-Guide]:azure-ad-developers-guide.md [AAD-Integrating-Apps]:quickstart-v1-integrate-apps-with-azure-ad.md [AZURE-portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="0556f-294">[![Sign in button][AAD-Sign-In]][AAD-Sign-In]
<!--Reference style links --> [AAD-Auth-Libraries]: ./active-directory-authentication-libraries.md [AAD-Auth-Scenarios]:authentication-scenarios.md [AAD-Dev-Guide]:azure-ad-developers-guide.md [AAD-Integrating-Apps]:quickstart-v1-integrate-apps-with-azure-ad.md [AZURE-portal]: https://portal.azure.com</span></span>

<!--Image references-->
[AAD-Sign-In]:./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png

