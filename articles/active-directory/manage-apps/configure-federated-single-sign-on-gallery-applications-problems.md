---
title: Problem configuring federated single sign-on for an Azure AD Gallery application | Microsoft Docs
description: Address some of the common problems you may encounter when configuring federated single sign-on using SAML for applications that are listed in the Azure AD Application Gallery
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: 2aee48d0d62321cd129e0e5480e3d31d644baba1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855849"
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="23bf9-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="23bf9-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="23bf9-104">If you encounter a problem when configuring an application.</span><span class="sxs-lookup"><span data-stu-id="23bf9-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="23bf9-105">Verify you have followed all the steps in the tutorial for the application.</span><span class="sxs-lookup"><span data-stu-id="23bf9-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="23bf9-106">In the application’s configuration, you have inline documentation on how to configure the application.</span><span class="sxs-lookup"><span data-stu-id="23bf9-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="23bf9-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span><span class="sxs-lookup"><span data-stu-id="23bf9-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="23bf9-108">Can’t add another instance of the application</span><span class="sxs-lookup"><span data-stu-id="23bf9-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="23bf9-109">To add a second instance of an application, you need to be able to:</span><span class="sxs-lookup"><span data-stu-id="23bf9-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="23bf9-110">Configure a unique identifier for the second instance.</span><span class="sxs-lookup"><span data-stu-id="23bf9-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="23bf9-111">You won’t be able to configure the same identifier used for the first instance.</span><span class="sxs-lookup"><span data-stu-id="23bf9-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="23bf9-112">Configure a different certificate than the one used for the first instance.</span><span class="sxs-lookup"><span data-stu-id="23bf9-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="23bf9-113">If the application doesn’t support any of the above.</span><span class="sxs-lookup"><span data-stu-id="23bf9-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="23bf9-114">Then, you won’t be able to configure a second instance.</span><span class="sxs-lookup"><span data-stu-id="23bf9-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="23bf9-115">Can’t add the Identifier or the Reply URL</span><span class="sxs-lookup"><span data-stu-id="23bf9-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="23bf9-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span><span class="sxs-lookup"><span data-stu-id="23bf9-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="23bf9-117">To know the patterns pre-configured for the application:</span><span class="sxs-lookup"><span data-stu-id="23bf9-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="23bf9-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go to step 7.</span><span class="sxs-lookup"><span data-stu-id="23bf9-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go to step 7.</span></span> <span data-ttu-id="23bf9-119">If you are already in the application configuration blade on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23bf9-119">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="23bf9-120">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="23bf9-120">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="23bf9-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="23bf9-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="23bf9-122">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="23bf9-122">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="23bf9-123">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="23bf9-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="23bf9-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="23bf9-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="23bf9-125">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="23bf9-125">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="23bf9-126">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="23bf9-126">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="23bf9-127">Select **SAML-based Sign-on** from the **Mode** dropdown.</span><span class="sxs-lookup"><span data-stu-id="23bf9-127">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="23bf9-128">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span><span class="sxs-lookup"><span data-stu-id="23bf9-128">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="23bf9-129">There are three ways to know the supported patterns for the application:</span><span class="sxs-lookup"><span data-stu-id="23bf9-129">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="23bf9-130">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span><span class="sxs-lookup"><span data-stu-id="23bf9-130">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="23bf9-131">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span><span class="sxs-lookup"><span data-stu-id="23bf9-131">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="23bf9-132">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span><span class="sxs-lookup"><span data-stu-id="23bf9-132">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="23bf9-133">In the tutorial for the application, you can also get information about the supported patterns.</span><span class="sxs-lookup"><span data-stu-id="23bf9-133">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="23bf9-134">Under the **Configure Azure AD single sign-on** section.</span><span class="sxs-lookup"><span data-stu-id="23bf9-134">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="23bf9-135">Go to the step for configured the values under the **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="23bf9-135">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="23bf9-136">If the values don’t match with the patterns pre-configured on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23bf9-136">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="23bf9-137">You can:</span><span class="sxs-lookup"><span data-stu-id="23bf9-137">You can:</span></span>

-   <span data-ttu-id="23bf9-138">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span><span class="sxs-lookup"><span data-stu-id="23bf9-138">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="23bf9-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span><span class="sxs-lookup"><span data-stu-id="23bf9-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="23bf9-140">Where do I set the EntityID (User Identifier) format</span><span class="sxs-lookup"><span data-stu-id="23bf9-140">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="23bf9-141">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span><span class="sxs-lookup"><span data-stu-id="23bf9-141">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="23bf9-142">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="23bf9-142">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="23bf9-143">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="23bf9-143">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="23bf9-144">Can’t find the Azure AD metadata to complete the configuration with the application</span><span class="sxs-lookup"><span data-stu-id="23bf9-144">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="23bf9-145">To download the application metadata or certificate from Azure AD, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="23bf9-145">To download the application metadata or certificate from Azure AD, follow these steps:</span></span>

1.  <span data-ttu-id="23bf9-146">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="23bf9-146">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="23bf9-147">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="23bf9-147">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="23bf9-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="23bf9-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="23bf9-149">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="23bf9-149">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="23bf9-150">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="23bf9-150">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="23bf9-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="23bf9-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="23bf9-152">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="23bf9-152">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="23bf9-153">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="23bf9-153">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="23bf9-154">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="23bf9-154">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="23bf9-155">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="23bf9-155">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="23bf9-156">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="23bf9-156">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="23bf9-157">The metadata can only be retrieved as a XML file.</span><span class="sxs-lookup"><span data-stu-id="23bf9-157">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="23bf9-158">Don't know how to customize SAML claims sent to an application</span><span class="sxs-lookup"><span data-stu-id="23bf9-158">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="23bf9-159">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span><span class="sxs-lookup"><span data-stu-id="23bf9-159">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23bf9-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="23bf9-160">Next steps</span></span>
[<span data-ttu-id="23bf9-161">Managing Applications with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23bf9-161">Managing Applications with Azure Active Directory</span></span>](what-is-application-management.md)
