---
title: Debug SAML-based single sign-on - Azure Active Directory | Microsoft Docs
description: Debug SAML-based single sign-on to applications in Azure Active Directory.
services: active-directory
author: CelesteDG
documentationcenter: na
manager: mtillman
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/15/2018
ms.author: celested
ms.custom: aaddev
ms.reviewer: hirsin, dastrock, smalser
ms.openlocfilehash: 388337fa80d174cb17dae12fa9d5f2fbdfe7e737
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968767"
---
# <a name="debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="1d71a-103">Debug SAML-based single sign-on to applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d71a-103">Debug SAML-based single sign-on to applications in Azure Active Directory</span></span>

<span data-ttu-id="1d71a-104">Learn how to find and fix [single sign-on](../manage-apps/what-is-single-sign-on.md) issues for applications in Azure Active Directory (Azure AD) that support [Security Assertion Markup Language (SAML) 2.0](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language).</span><span class="sxs-lookup"><span data-stu-id="1d71a-104">Learn how to find and fix [single sign-on](../manage-apps/what-is-single-sign-on.md) issues for applications in Azure Active Directory (Azure AD) that support [Security Assertion Markup Language (SAML) 2.0](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="1d71a-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1d71a-105">Before you begin</span></span>
<span data-ttu-id="1d71a-106">We recommend installing the [My Apps Secure Sign-in Extension](../user-help/active-directory-saas-access-panel-user-help.md#i-am-having-trouble-installing-the-my-apps-secure-sign-in-extension).</span><span class="sxs-lookup"><span data-stu-id="1d71a-106">We recommend installing the [My Apps Secure Sign-in Extension](../user-help/active-directory-saas-access-panel-user-help.md#i-am-having-trouble-installing-the-my-apps-secure-sign-in-extension).</span></span> <span data-ttu-id="1d71a-107">This browser extension makes it easy to gather the SAML request and SAML response information that you need for resolving issues with single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1d71a-107">This browser extension makes it easy to gather the SAML request and SAML response information that you need for resolving issues with single sign-on.</span></span> <span data-ttu-id="1d71a-108">In case you cannot install the extension, this article shows you how to resolve issues both with and without the extension installed.</span><span class="sxs-lookup"><span data-stu-id="1d71a-108">In case you cannot install the extension, this article shows you how to resolve issues both with and without the extension installed.</span></span>

<span data-ttu-id="1d71a-109">To download and install the My Apps Secure Sign-in Extension, use one of the following links.</span><span class="sxs-lookup"><span data-stu-id="1d71a-109">To download and install the My Apps Secure Sign-in Extension, use one of the following links.</span></span>

- [<span data-ttu-id="1d71a-110">Chrome</span><span class="sxs-lookup"><span data-stu-id="1d71a-110">Chrome</span></span>](https://go.microsoft.com/fwlink/?linkid=866367)
- [<span data-ttu-id="1d71a-111">Edge</span><span class="sxs-lookup"><span data-stu-id="1d71a-111">Edge</span></span>](https://go.microsoft.com/fwlink/?linkid=845176)
- [<span data-ttu-id="1d71a-112">Firefox</span><span class="sxs-lookup"><span data-stu-id="1d71a-112">Firefox</span></span>](https://go.microsoft.com/fwlink/?linkid=866366)


## <a name="test-saml-based-single-sign-on"></a><span data-ttu-id="1d71a-113">Test SAML-based single sign-on</span><span class="sxs-lookup"><span data-stu-id="1d71a-113">Test SAML-based single sign-on</span></span>

<span data-ttu-id="1d71a-114">To test SAML-based single sign-on between AAD and a target application:</span><span class="sxs-lookup"><span data-stu-id="1d71a-114">To test SAML-based single sign-on between AAD and a target application:</span></span>

1.  <span data-ttu-id="1d71a-115">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator or other administrator that is authorized to manage applications.</span><span class="sxs-lookup"><span data-stu-id="1d71a-115">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator or other administrator that is authorized to manage applications.</span></span>
2.  <span data-ttu-id="1d71a-116">In the left blade, click **Azure Active Directory**, and then click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1d71a-116">In the left blade, click **Azure Active Directory**, and then click **Enterprise applications**.</span></span> 
3.  <span data-ttu-id="1d71a-117">From the list of Enterprise Applications, click the application for which you want to test single sign-on, and then from the options on the left click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1d71a-117">From the list of Enterprise Applications, click the application for which you want to test single sign-on, and then from the options on the left click **Single sign-on**.</span></span>
4.  <span data-ttu-id="1d71a-118">To open the SAML-based single sign-on testing experience, in the **Domain and URLs** section click **Test SAML Setting**.</span><span class="sxs-lookup"><span data-stu-id="1d71a-118">To open the SAML-based single sign-on testing experience, in the **Domain and URLs** section click **Test SAML Setting**.</span></span> <span data-ttu-id="1d71a-119">If the Test SAML Setting button is greyed out, you need to fill out and save the required attributes first.</span><span class="sxs-lookup"><span data-stu-id="1d71a-119">If the Test SAML Setting button is greyed out, you need to fill out and save the required attributes first.</span></span>
5.  <span data-ttu-id="1d71a-120">In the **Test single sign-on** blade, use your corporate credentials to sign in to the target application.</span><span class="sxs-lookup"><span data-stu-id="1d71a-120">In the **Test single sign-on** blade, use your corporate credentials to sign in to the target application.</span></span> <span data-ttu-id="1d71a-121">You can sign in as the current user or as a different user.</span><span class="sxs-lookup"><span data-stu-id="1d71a-121">You can sign in as the current user or as a different user.</span></span> <span data-ttu-id="1d71a-122">If you sign in as a different user, a prompt will ask you to authenticate.</span><span class="sxs-lookup"><span data-stu-id="1d71a-122">If you sign in as a different user, a prompt will ask you to authenticate.</span></span>

    ![Test SAML page](./media/howto-v1-debug-saml-sso-issues/testing.png)


<span data-ttu-id="1d71a-124">If you are successfully signed in, the test has passed.</span><span class="sxs-lookup"><span data-stu-id="1d71a-124">If you are successfully signed in, the test has passed.</span></span> <span data-ttu-id="1d71a-125">In this case, Azure AD issued a SAML response token to the application.</span><span class="sxs-lookup"><span data-stu-id="1d71a-125">In this case, Azure AD issued a SAML response token to the application.</span></span> <span data-ttu-id="1d71a-126">The application used the SAML token to successfully sign you in.</span><span class="sxs-lookup"><span data-stu-id="1d71a-126">The application used the SAML token to successfully sign you in.</span></span>

<span data-ttu-id="1d71a-127">If you have an error on the company sign-in page or the application's page, use one of the next sections to resolve the error.</span><span class="sxs-lookup"><span data-stu-id="1d71a-127">If you have an error on the company sign-in page or the application's page, use one of the next sections to resolve the error.</span></span>


## <a name="resolve-a-sign-in-error-on-your-company-sign-in-page"></a><span data-ttu-id="1d71a-128">Resolve a sign-in error on your company sign-in page</span><span class="sxs-lookup"><span data-stu-id="1d71a-128">Resolve a sign-in error on your company sign-in page</span></span>

<span data-ttu-id="1d71a-129">When you try to sign in you might see an error on your company sign-in page.</span><span class="sxs-lookup"><span data-stu-id="1d71a-129">When you try to sign in you might see an error on your company sign-in page.</span></span> 

![Sign-in error](./media/howto-v1-debug-saml-sso-issues/error.png)

<span data-ttu-id="1d71a-131">To debug this error, you need the error message and the SAML request.</span><span class="sxs-lookup"><span data-stu-id="1d71a-131">To debug this error, you need the error message and the SAML request.</span></span> <span data-ttu-id="1d71a-132">The My Apps Secure Sign-in Extension automatically gathers this information and displays resolution guidance on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d71a-132">The My Apps Secure Sign-in Extension automatically gathers this information and displays resolution guidance on Azure AD.</span></span> 

<span data-ttu-id="1d71a-133">To resolve the sign-in error with the MyApps Secure Sign-in Extension installed:</span><span class="sxs-lookup"><span data-stu-id="1d71a-133">To resolve the sign-in error with the MyApps Secure Sign-in Extension installed:</span></span>

1.  <span data-ttu-id="1d71a-134">When an error occurs, the extension redirects you back to the Azure Ad **Test single sign-on** blade.</span><span class="sxs-lookup"><span data-stu-id="1d71a-134">When an error occurs, the extension redirects you back to the Azure Ad **Test single sign-on** blade.</span></span> 
2.  <span data-ttu-id="1d71a-135">On the **Test single sign-on** blade, click **Download the SAML request**.</span><span class="sxs-lookup"><span data-stu-id="1d71a-135">On the **Test single sign-on** blade, click **Download the SAML request**.</span></span> 
3.  <span data-ttu-id="1d71a-136">You should see specific resolution guidance based on the error and the values in the SAML request.</span><span class="sxs-lookup"><span data-stu-id="1d71a-136">You should see specific resolution guidance based on the error and the values in the SAML request.</span></span> <span data-ttu-id="1d71a-137">Review the guidance.</span><span class="sxs-lookup"><span data-stu-id="1d71a-137">Review the guidance.</span></span>

<span data-ttu-id="1d71a-138">To resolve the error without installing MyApps Secure Sign-in Extension:</span><span class="sxs-lookup"><span data-stu-id="1d71a-138">To resolve the error without installing MyApps Secure Sign-in Extension:</span></span>

1. <span data-ttu-id="1d71a-139">Copy the error message at the bottom right corner of the page.</span><span class="sxs-lookup"><span data-stu-id="1d71a-139">Copy the error message at the bottom right corner of the page.</span></span> <span data-ttu-id="1d71a-140">The error message includes:</span><span class="sxs-lookup"><span data-stu-id="1d71a-140">The error message includes:</span></span>
    - <span data-ttu-id="1d71a-141">A CorrelationID and Timestamp.</span><span class="sxs-lookup"><span data-stu-id="1d71a-141">A CorrelationID and Timestamp.</span></span> <span data-ttu-id="1d71a-142">These values are important when you create a support case with Microsoft because they help the engineers to identify your problem and provide an accurate resolution to your issue.</span><span class="sxs-lookup"><span data-stu-id="1d71a-142">These values are important when you create a support case with Microsoft because they help the engineers to identify your problem and provide an accurate resolution to your issue.</span></span>
    - <span data-ttu-id="1d71a-143">A statement identifying the root cause of the problem.</span><span class="sxs-lookup"><span data-stu-id="1d71a-143">A statement identifying the root cause of the problem.</span></span>
2.  <span data-ttu-id="1d71a-144">Go back to Azure AD and find the **Test single sign-on** blade.</span><span class="sxs-lookup"><span data-stu-id="1d71a-144">Go back to Azure AD and find the **Test single sign-on** blade.</span></span>
3.  <span data-ttu-id="1d71a-145">In the text box above **Get resolution guidance**, paste the error message.</span><span class="sxs-lookup"><span data-stu-id="1d71a-145">In the text box above **Get resolution guidance**, paste the error message.</span></span>
3.  <span data-ttu-id="1d71a-146">Click **Get resolution guidance** to display steps for resolving the issue.</span><span class="sxs-lookup"><span data-stu-id="1d71a-146">Click **Get resolution guidance** to display steps for resolving the issue.</span></span> <span data-ttu-id="1d71a-147">The guidance might require information from the SAML request or SAML response.</span><span class="sxs-lookup"><span data-stu-id="1d71a-147">The guidance might require information from the SAML request or SAML response.</span></span> <span data-ttu-id="1d71a-148">If you’re not using the  MyApps Secure Sign-in Extension, you might need a tool such as [Fiddler](http://www.telerik.com/fiddler) to retrieve the SAML request and response.</span><span class="sxs-lookup"><span data-stu-id="1d71a-148">If you’re not using the  MyApps Secure Sign-in Extension, you might need a tool such as [Fiddler](http://www.telerik.com/fiddler) to retrieve the SAML request and response.</span></span>
4.  <span data-ttu-id="1d71a-149">Verify the destination in the SAML request corresponds to the SAML Single Sign-On Service URL obtained from Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d71a-149">Verify the destination in the SAML request corresponds to the SAML Single Sign-On Service URL obtained from Azure Active Directory</span></span>
5.  <span data-ttu-id="1d71a-150">Verify the issuer in the SAML request is the same identifier you have configured for the application in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d71a-150">Verify the issuer in the SAML request is the same identifier you have configured for the application in Azure Active Directory.</span></span> <span data-ttu-id="1d71a-151">Azure AD uses the issuer to find an application in your directory.</span><span class="sxs-lookup"><span data-stu-id="1d71a-151">Azure AD uses the issuer to find an application in your directory.</span></span>
6.  <span data-ttu-id="1d71a-152">Verify AssertionConsumerServiceURL is where the application expects to receive the SAML token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d71a-152">Verify AssertionConsumerServiceURL is where the application expects to receive the SAML token from Azure Active Directory.</span></span> <span data-ttu-id="1d71a-153">You can configure this value in Azure Active Directory, but it’s not mandatory if it’s part of the SAML request.</span><span class="sxs-lookup"><span data-stu-id="1d71a-153">You can configure this value in Azure Active Directory, but it’s not mandatory if it’s part of the SAML request.</span></span>


## <a name="resolve-a-sign-in-error-on-the-application-page"></a><span data-ttu-id="1d71a-154">Resolve a sign-in error on the application page</span><span class="sxs-lookup"><span data-stu-id="1d71a-154">Resolve a sign-in error on the application page</span></span>

<span data-ttu-id="1d71a-155">You might sign in successfully and then see an error on the application's page.</span><span class="sxs-lookup"><span data-stu-id="1d71a-155">You might sign in successfully and then see an error on the application's page.</span></span> <span data-ttu-id="1d71a-156">This occurs when Azure AD issued a token to the application, but the application does not accept the response.</span><span class="sxs-lookup"><span data-stu-id="1d71a-156">This occurs when Azure AD issued a token to the application, but the application does not accept the response.</span></span>   

<span data-ttu-id="1d71a-157">To resolve the error:</span><span class="sxs-lookup"><span data-stu-id="1d71a-157">To resolve the error:</span></span>

1. <span data-ttu-id="1d71a-158">If the application is in the Azure AD Gallery, verify you have followed all the steps for integrating the application with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1d71a-158">If the application is in the Azure AD Gallery, verify you have followed all the steps for integrating the application with Azure AD.</span></span> <span data-ttu-id="1d71a-159">To find the integration instructions for your application, see the [list of SaaS application integration tutorials](../saas-apps/tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="1d71a-159">To find the integration instructions for your application, see the [list of SaaS application integration tutorials](../saas-apps/tutorial-list.md).</span></span>
2. <span data-ttu-id="1d71a-160">Retrieve the SAML response.</span><span class="sxs-lookup"><span data-stu-id="1d71a-160">Retrieve the SAML response.</span></span>
    - <span data-ttu-id="1d71a-161">If the My Apps Secure Sign-in extension is installed, from the **Test single sign-on** blade, click **download the SAML response**.</span><span class="sxs-lookup"><span data-stu-id="1d71a-161">If the My Apps Secure Sign-in extension is installed, from the **Test single sign-on** blade, click **download the SAML response**.</span></span>
    - <span data-ttu-id="1d71a-162">If the extension is not installed, use a tool such as [Fiddler](http://www.telerik.com/fiddler) to retrieve the SAML response.</span><span class="sxs-lookup"><span data-stu-id="1d71a-162">If the extension is not installed, use a tool such as [Fiddler](http://www.telerik.com/fiddler) to retrieve the SAML response.</span></span> 
3. <span data-ttu-id="1d71a-163">Notice these elements in the SAML response token:</span><span class="sxs-lookup"><span data-stu-id="1d71a-163">Notice these elements in the SAML response token:</span></span>
    - <span data-ttu-id="1d71a-164">User unique identifier of NameID value and format</span><span class="sxs-lookup"><span data-stu-id="1d71a-164">User unique identifier of NameID value and format</span></span>
    - <span data-ttu-id="1d71a-165">Claims issued in the token</span><span class="sxs-lookup"><span data-stu-id="1d71a-165">Claims issued in the token</span></span>
    - <span data-ttu-id="1d71a-166">Certificate used to sign the token.</span><span class="sxs-lookup"><span data-stu-id="1d71a-166">Certificate used to sign the token.</span></span> <span data-ttu-id="1d71a-167">For information on how to review the SAML response, see [Single Sign-On SAML protocol](single-sign-on-saml-protocol.md).</span><span class="sxs-lookup"><span data-stu-id="1d71a-167">For information on how to review the SAML response, see [Single Sign-On SAML protocol](single-sign-on-saml-protocol.md).</span></span>
4. <span data-ttu-id="1d71a-168">For more information on the SAML response, see [Single Sign-on SAML protocol](single-sign-on-saml-protocol.md).</span><span class="sxs-lookup"><span data-stu-id="1d71a-168">For more information on the SAML response, see [Single Sign-on SAML protocol](single-sign-on-saml-protocol.md).</span></span>
5. <span data-ttu-id="1d71a-169">Now that you have reviewed the SAML response, see [Error on an application's page after signing in](../manage-apps/application-sign-in-problem-application-error.md) for guidance on resolving the problem.</span><span class="sxs-lookup"><span data-stu-id="1d71a-169">Now that you have reviewed the SAML response, see [Error on an application's page after signing in](../manage-apps/application-sign-in-problem-application-error.md) for guidance on resolving the problem.</span></span> 
6. <span data-ttu-id="1d71a-170">If you are still not able to sign in successfully, you can ask the application vendor what is missing from the SAML response.</span><span class="sxs-lookup"><span data-stu-id="1d71a-170">If you are still not able to sign in successfully, you can ask the application vendor what is missing from the SAML response.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d71a-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d71a-171">Next steps</span></span>
<span data-ttu-id="1d71a-172">Now that single sign-on is working to your application, you could [Automate user provisioning and deprovisioning to SaaS applications](../manage-apps/user-provisioning.md), or [get started with conditional access](../conditional-access/app-based-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="1d71a-172">Now that single sign-on is working to your application, you could [Automate user provisioning and deprovisioning to SaaS applications](../manage-apps/user-provisioning.md), or [get started with conditional access](../conditional-access/app-based-conditional-access.md).</span></span>


