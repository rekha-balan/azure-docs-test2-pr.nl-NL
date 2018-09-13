---
title: 'Tutorial: Azure Active Directory integration with ClickTime | Microsoft Docs'
description: Learn how to use ClickTime with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 336b6b1a4ddd2a45cf5c38baf5e32584b0fe9f1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552700"
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="8eaee-103">Tutorial: Azure Active Directory integration with ClickTime</span><span class="sxs-lookup"><span data-stu-id="8eaee-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>
<span data-ttu-id="8eaee-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8eaee-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8eaee-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8eaee-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8eaee-106">You can control in Azure AD who has access to ClickTime</span><span class="sxs-lookup"><span data-stu-id="8eaee-106">You can control in Azure AD who has access to ClickTime</span></span>
* <span data-ttu-id="8eaee-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8eaee-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8eaee-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8eaee-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8eaee-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8eaee-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8eaee-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8eaee-110">Prerequisites</span></span>
<span data-ttu-id="8eaee-111">To configure Azure AD integration with ClickTime, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8eaee-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

* <span data-ttu-id="8eaee-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8eaee-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8eaee-113">A ClickTime single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8eaee-113">A ClickTime single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8eaee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8eaee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8eaee-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8eaee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8eaee-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8eaee-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8eaee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8eaee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8eaee-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8eaee-118">Scenario description</span></span>
<span data-ttu-id="8eaee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8eaee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="8eaee-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8eaee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8eaee-121">Adding ClickTime from the gallery</span><span class="sxs-lookup"><span data-stu-id="8eaee-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="8eaee-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8eaee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="8eaee-123">Adding ClickTime from the gallery</span><span class="sxs-lookup"><span data-stu-id="8eaee-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="8eaee-124">The objective of this section is to outline how to enable the application integration for ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8eaee-124">The objective of this section is to outline how to enable the application integration for ClickTime.</span></span>

### <a name="to-enable-the-application-integration-for-clicktime-perform-the-following-steps"></a><span data-ttu-id="8eaee-125">To enable the application integration for ClickTime, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8eaee-125">To enable the application integration for ClickTime, perform the following steps:</span></span>
1. <span data-ttu-id="8eaee-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="8eaee-127">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8eaee-127">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8eaee-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8eaee-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8eaee-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8eaee-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="8eaee-130">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="8eaee-130">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic700994.png "Applications")</span></span>
4. <span data-ttu-id="8eaee-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8eaee-131">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="8eaee-132">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="8eaee-132">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic749321.png "Add application")</span></span>
5. <span data-ttu-id="8eaee-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="8eaee-134">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="8eaee-134">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8eaee-135">In the **search box**, type **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-135">In the **search box**, type **ClickTime**.</span></span>
   
   <span data-ttu-id="8eaee-136">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777275.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="8eaee-136">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777275.png "Application gallery")</span></span>
7. <span data-ttu-id="8eaee-137">In the results pane, select **ClickTime**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8eaee-137">In the results pane, select **ClickTime**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="8eaee-138">![ClickTime](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777276.png "ClickTime")</span><span class="sxs-lookup"><span data-stu-id="8eaee-138">![ClickTime](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777276.png "ClickTime")</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8eaee-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8eaee-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8eaee-140">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8eaee-140">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8eaee-141">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8eaee-141">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="8eaee-142">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8eaee-142">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="8eaee-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8eaee-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ClickTime.</span></span>

<span data-ttu-id="8eaee-144">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8eaee-144">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8eaee-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8eaee-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8eaee-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8eaee-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8eaee-147">**[Creating a ClickTime test user](#creating-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8eaee-147">**[Creating a ClickTime test user](#creating-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8eaee-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8eaee-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8eaee-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8eaee-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8eaee-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8eaee-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="8eaee-151">The objective of this section is to outline how to enable users to authenticate to ClickTime with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="8eaee-151">The objective of this section is to outline how to enable users to authenticate to ClickTime with their account in Azure AD using federation based on the SAML protocol.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="8eaee-152">In order to be able to configure single sign-on on your ClickTime tenant, you need to contact first the ClickTime technical support to get this feature enabled.</span><span class="sxs-lookup"><span data-stu-id="8eaee-152">In order to be able to configure single sign-on on your ClickTime tenant, you need to contact first the ClickTime technical support to get this feature enabled.</span></span>
> 
> 

<span data-ttu-id="8eaee-153">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8eaee-153">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="8eaee-154">In the Azure classic portal, on the **ClickTime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="8eaee-154">In the Azure classic portal, on the **ClickTime** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8eaee-155">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777277.png "Enable single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8eaee-155">![Enable single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777277.png "Enable single sign-on")</span></span>
2. <span data-ttu-id="8eaee-156">On the **How would you like users to sign on to ClickTime** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-156">On the **How would you like users to sign on to ClickTime** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="8eaee-157">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777278.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8eaee-157">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777278.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="8eaee-158">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8eaee-158">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777286.png) 
   
    <span data-ttu-id="8eaee-160">a.</span><span class="sxs-lookup"><span data-stu-id="8eaee-160">a.</span></span> <span data-ttu-id="8eaee-161">In the **IdentifierL** textbox, type the URL using the following pattern: **https://app.clicktime.com/sp/**</span><span class="sxs-lookup"><span data-stu-id="8eaee-161">In the **IdentifierL** textbox, type the URL using the following pattern: **https://app.clicktime.com/sp/**</span></span>
   
    <span data-ttu-id="8eaee-162">b.</span><span class="sxs-lookup"><span data-stu-id="8eaee-162">b.</span></span> <span data-ttu-id="8eaee-163">In the **Reply URL** textbox, type the URL using the following pattern: **https://app.clicktime.com/Login/**</span><span class="sxs-lookup"><span data-stu-id="8eaee-163">In the **Reply URL** textbox, type the URL using the following pattern: **https://app.clicktime.com/Login/**</span></span>
   
    <span data-ttu-id="8eaee-164">c.</span><span class="sxs-lookup"><span data-stu-id="8eaee-164">c.</span></span> <span data-ttu-id="8eaee-165">click **Next**</span><span class="sxs-lookup"><span data-stu-id="8eaee-165">click **Next**</span></span>
4. <span data-ttu-id="8eaee-166">On the **Configure single sign-on at ClickTime** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8eaee-166">On the **Configure single sign-on at ClickTime** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="8eaee-167">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777279.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8eaee-167">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777279.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="8eaee-168">In a different web browser window, log into your ClickTime company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8eaee-168">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>
6. <span data-ttu-id="8eaee-169">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-169">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>
7. <span data-ttu-id="8eaee-170">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8eaee-170">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="8eaee-171">![Security Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span><span class="sxs-lookup"><span data-stu-id="8eaee-171">![Security Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
   <span data-ttu-id="8eaee-172">a.</span><span class="sxs-lookup"><span data-stu-id="8eaee-172">a.</span></span>  <span data-ttu-id="8eaee-173">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-173">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
   <span data-ttu-id="8eaee-174">b.</span><span class="sxs-lookup"><span data-stu-id="8eaee-174">b.</span></span>  <span data-ttu-id="8eaee-175">In the Azure classic portal, on the **Configure single sign-on at ClickTime** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity Provider Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="8eaee-175">In the Azure classic portal, on the **Configure single sign-on at ClickTime** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity Provider Endpoint** textbox.</span></span>
   
   <span data-ttu-id="8eaee-176">c.</span><span class="sxs-lookup"><span data-stu-id="8eaee-176">c.</span></span>  <span data-ttu-id="8eaee-177">Open the base-64 encoded certificate in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="8eaee-177">Open the base-64 encoded certificate in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="8eaee-178">d.</span><span class="sxs-lookup"><span data-stu-id="8eaee-178">d.</span></span>  <span data-ttu-id="8eaee-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-179">Click **Save**.</span></span>
8. <span data-ttu-id="8eaee-180">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="8eaee-180">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8eaee-181">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777281.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="8eaee-181">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777281.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="8eaee-182">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="8eaee-182">Configuring user provisioning</span></span>
<span data-ttu-id="8eaee-183">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8eaee-183">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="8eaee-184">In the case of ClickTime, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="8eaee-184">In the case of ClickTime, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="8eaee-185">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8eaee-185">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="8eaee-186">Log in to your **ClickTime** tenant.</span><span class="sxs-lookup"><span data-stu-id="8eaee-186">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="8eaee-187">In the toolbar on the top, click **Company**, and then click **People**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-187">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
   <span data-ttu-id="8eaee-188">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span><span class="sxs-lookup"><span data-stu-id="8eaee-188">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="8eaee-189">Click **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-189">Click **Add Person**.</span></span>
   
   <span data-ttu-id="8eaee-190">![Add Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span><span class="sxs-lookup"><span data-stu-id="8eaee-190">![Add Person](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="8eaee-191">In the New Person section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8eaee-191">In the New Person section, perform the following steps:</span></span>
   
   <span data-ttu-id="8eaee-192">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span><span class="sxs-lookup"><span data-stu-id="8eaee-192">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
   <span data-ttu-id="8eaee-193">a.</span><span class="sxs-lookup"><span data-stu-id="8eaee-193">a.</span></span>  <span data-ttu-id="8eaee-194">In the **email address** textbox, type the email address of your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="8eaee-194">In the **email address** textbox, type the email address of your Azure AD account.</span></span>
   
   <span data-ttu-id="8eaee-195">b.</span><span class="sxs-lookup"><span data-stu-id="8eaee-195">b.</span></span>  <span data-ttu-id="8eaee-196">In the **full name** textbox, type the name of your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="8eaee-196">In the **full name** textbox, type the name of your Azure AD account.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="8eaee-197">If you want to, you can set additional properties of the new person object.</span><span class="sxs-lookup"><span data-stu-id="8eaee-197">If you want to, you can set additional properties of the new person object.</span></span>
   > 
   > 
   
   <span data-ttu-id="8eaee-198">c.</span><span class="sxs-lookup"><span data-stu-id="8eaee-198">c.</span></span>  <span data-ttu-id="8eaee-199">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-199">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="8eaee-200">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="8eaee-200">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8eaee-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8eaee-201">Assigning the Azure AD test user</span></span>
<span data-ttu-id="8eaee-202">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8eaee-202">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ClickTime.</span></span>

![Assign User][200]

<span data-ttu-id="8eaee-204">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="8eaee-204">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="8eaee-205">**To assign Britta Simon to ClickTime, perform the following steps**</span><span class="sxs-lookup"><span data-stu-id="8eaee-205">**To assign Britta Simon to ClickTime, perform the following steps**</span></span>

1. <span data-ttu-id="8eaee-206">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8eaee-206">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="8eaee-208">In the applications list, select **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-208">In the applications list, select **ClickTime**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_50.png) 
3. <span data-ttu-id="8eaee-210">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-210">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="8eaee-212">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-212">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8eaee-213">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8eaee-213">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

## <a name="testing-single-sign-on"></a><span data-ttu-id="8eaee-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8eaee-215">Testing single sign-on</span></span>
<span data-ttu-id="8eaee-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8eaee-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8eaee-217">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span><span class="sxs-lookup"><span data-stu-id="8eaee-217">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8eaee-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8eaee-218">Additional resources</span></span>
* [<span data-ttu-id="8eaee-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8eaee-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8eaee-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8eaee-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-clicktime-tutorial/tutorial_general_205.png




















