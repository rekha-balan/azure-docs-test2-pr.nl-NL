---
title: 'Tutorial: Azure Active Directory integration with SD Elements | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SD Elements.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: c70ec94e65a4e83472919e4839b558846c0f9642
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550110"
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="8be33-103">Tutorial: Azure Active Directory integration with SD Elements</span><span class="sxs-lookup"><span data-stu-id="8be33-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>
<span data-ttu-id="8be33-104">The objective of this tutorial is to show you how to integrate SD Elements with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8be33-104">The objective of this tutorial is to show you how to integrate SD Elements with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="8be33-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8be33-105">Integrating SD Elements with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8be33-106">You can control in Azure AD who has access to SD Elements</span><span class="sxs-lookup"><span data-stu-id="8be33-106">You can control in Azure AD who has access to SD Elements</span></span>
* <span data-ttu-id="8be33-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8be33-107">You can enable your users to automatically get signed-on to SD Elements (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8be33-108">You can manage your accounts in one central location - the Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8be33-108">You can manage your accounts in one central location - the Azure Active Directory</span></span> 

<span data-ttu-id="8be33-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8be33-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8be33-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8be33-110">Prerequisites</span></span>
<span data-ttu-id="8be33-111">To configure Azure AD integration with SD Elements, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8be33-111">To configure Azure AD integration with SD Elements, you need the following items:</span></span>

* <span data-ttu-id="8be33-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8be33-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8be33-113">A SD Elements single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8be33-113">A SD Elements single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8be33-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8be33-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8be33-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8be33-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8be33-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8be33-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8be33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8be33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8be33-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="8be33-118">Scenario Description</span></span>
<span data-ttu-id="8be33-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8be33-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="8be33-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8be33-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8be33-121">Adding SD Elements from the gallery</span><span class="sxs-lookup"><span data-stu-id="8be33-121">Adding SD Elements from the gallery</span></span>
2. <span data-ttu-id="8be33-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8be33-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-the-gallery"></a><span data-ttu-id="8be33-123">Adding SD Elements from the gallery</span><span class="sxs-lookup"><span data-stu-id="8be33-123">Adding SD Elements from the gallery</span></span>
<span data-ttu-id="8be33-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8be33-124">To configure the integration of SD Elements into Azure AD, you need to add SD Elements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8be33-125">**To add SD Elements from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8be33-125">**To add SD Elements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8be33-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8be33-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="8be33-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8be33-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8be33-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8be33-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="8be33-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8be33-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="8be33-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8be33-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="8be33-135">In the search box, type **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="8be33-135">In the search box, type **SD Elements**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_01.png)

7. <span data-ttu-id="8be33-137">In the results pane, select **SD Elements**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8be33-137">In the results pane, select **SD Elements**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8be33-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8be33-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8be33-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8be33-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8be33-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="8be33-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SD Elements to an user in Azure AD is.</span></span> <span data-ttu-id="8be33-142">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8be33-142">In other words, a link relationship between an Azure AD user and the related user in SD Elements needs to be established.</span></span>  
<span data-ttu-id="8be33-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SD Elements.</span><span class="sxs-lookup"><span data-stu-id="8be33-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SD Elements.</span></span>

<span data-ttu-id="8be33-144">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8be33-144">To configure and test Azure AD single sign-on with SD Elements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8be33-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8be33-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8be33-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8be33-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8be33-147">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8be33-147">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - to have a counterpart of Britta Simon in SD Elements that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8be33-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8be33-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8be33-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8be33-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8be33-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8be33-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="8be33-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SD Elements application.</span><span class="sxs-lookup"><span data-stu-id="8be33-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="8be33-152">Your SD Elements application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="8be33-152">Your SD Elements application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> <span data-ttu-id="8be33-153">The following screenshot shows an example for this:</span><span class="sxs-lookup"><span data-stu-id="8be33-153">The following screenshot shows an example for this:</span></span>

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_14.png) 

<span data-ttu-id="8be33-155">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8be33-155">**To configure Azure AD single sign-on with SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="8be33-156">In the Azure classic portal, on the **SD Elements** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="8be33-156">In the Azure classic portal, on the **SD Elements** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="8be33-158">On the **How would you like users to sign on to SD Elements** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8be33-158">On the **How would you like users to sign on to SD Elements** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_03.png) 

3. <span data-ttu-id="8be33-160">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="8be33-160">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_04.png) 

    <span data-ttu-id="8be33-162">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-162">a.</span></span> <span data-ttu-id="8be33-163">In the **Issuer** textbox, type your tenant's issuer URL using the following pattern: *https://\<your tenant name\>.sdelements.com/sso/saml2/metadata*</span><span class="sxs-lookup"><span data-stu-id="8be33-163">In the **Issuer** textbox, type your tenant's issuer URL using the following pattern: *https://\<your tenant name\>.sdelements.com/sso/saml2/metadata*</span></span>

    <span data-ttu-id="8be33-164">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-164">b.</span></span> <span data-ttu-id="8be33-165">In the **Reply URL** textbox, type your tenant's reply URL using the following pattern: *https://\<your tenant name\>.sdelements.com/sso/saml2/acs/*</span><span class="sxs-lookup"><span data-stu-id="8be33-165">In the **Reply URL** textbox, type your tenant's reply URL using the following pattern: *https://\<your tenant name\>.sdelements.com/sso/saml2/acs/*</span></span>       

    > [!NOTE] 
    > <span data-ttu-id="8be33-166">If you need the actual Issuer URL and Reply URL for your tenant, contact your [SD Elements support team](mailto:support@sdelements.com).</span><span class="sxs-lookup"><span data-stu-id="8be33-166">If you need the actual Issuer URL and Reply URL for your tenant, contact your [SD Elements support team](mailto:support@sdelements.com).</span></span>

    <span data-ttu-id="8be33-167">c.</span><span class="sxs-lookup"><span data-stu-id="8be33-167">c.</span></span> <span data-ttu-id="8be33-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8be33-168">Click **Next**.</span></span>


1. <span data-ttu-id="8be33-169">On the **Configure single sign-on at SD Elements** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-169">On the **Configure single sign-on at SD Elements** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_05.png) 
   
    <span data-ttu-id="8be33-171">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-171">a.</span></span> <span data-ttu-id="8be33-172">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8be33-172">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="8be33-173">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-173">b.</span></span> <span data-ttu-id="8be33-174">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8be33-174">Click **Next**.</span></span>
2. <span data-ttu-id="8be33-175">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="8be33-175">To get single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with the downloaded certificate file.</span></span>
3. <span data-ttu-id="8be33-176">In a different browser window, singn-on to your SD Elements tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8be33-176">In a different browser window, singn-on to your SD Elements tenant as an administrator.</span></span>
4. <span data-ttu-id="8be33-177">In the menu on the top, click System, and then Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="8be33-177">In the menu on the top, click System, and then Single Sign-on.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 
5. <span data-ttu-id="8be33-179">On the **Single Sign-On Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-179">On the **Single Sign-On Settings** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="8be33-181">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-181">a.</span></span> <span data-ttu-id="8be33-182">As **SSO Type**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8be33-182">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="8be33-183">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-183">b.</span></span> <span data-ttu-id="8be33-184">In the Azure classic portal, on the **Configure single sign-on at SD Elements** dialog page, copy the **Issuer URL** value, and then paste it into the **Identity Provider Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="8be33-184">In the Azure classic portal, on the **Configure single sign-on at SD Elements** dialog page, copy the **Issuer URL** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>
   
    <span data-ttu-id="8be33-185">c.</span><span class="sxs-lookup"><span data-stu-id="8be33-185">c.</span></span> <span data-ttu-id="8be33-186">In the Azure classic portal, on the **Configure single sign-on at SD Elements** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign-On Service** textbox.</span><span class="sxs-lookup"><span data-stu-id="8be33-186">In the Azure classic portal, on the **Configure single sign-on at SD Elements** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Identity Provider Single Sign-On Service** textbox.</span></span>
   
    <span data-ttu-id="8be33-187">d.</span><span class="sxs-lookup"><span data-stu-id="8be33-187">d.</span></span> <span data-ttu-id="8be33-188">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8be33-188">Click **Save**.</span></span>
6. <span data-ttu-id="8be33-189">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8be33-189">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="8be33-191">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8be33-191">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]
8. <span data-ttu-id="8be33-193">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span><span class="sxs-lookup"><span data-stu-id="8be33-193">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span> 
   
    ![Configure Single Sign-On][21]
9. <span data-ttu-id="8be33-195">For each row in the following table, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-195">For each row in the following table, perform the following steps:</span></span>
   
   | <span data-ttu-id="8be33-196">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="8be33-196">Attribute Name</span></span> | <span data-ttu-id="8be33-197">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="8be33-197">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8be33-198">email</span><span class="sxs-lookup"><span data-stu-id="8be33-198">email</span></span> |<span data-ttu-id="8be33-199">user.mail</span><span class="sxs-lookup"><span data-stu-id="8be33-199">user.mail</span></span> |
   | <span data-ttu-id="8be33-200">firstname</span><span class="sxs-lookup"><span data-stu-id="8be33-200">firstname</span></span> |<span data-ttu-id="8be33-201">user.givenname</span><span class="sxs-lookup"><span data-stu-id="8be33-201">user.givenname</span></span> |
   | <span data-ttu-id="8be33-202">lastname</span><span class="sxs-lookup"><span data-stu-id="8be33-202">lastname</span></span> |<span data-ttu-id="8be33-203">user.surname</span><span class="sxs-lookup"><span data-stu-id="8be33-203">user.surname</span></span> |

    <span data-ttu-id="8be33-204">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-204">a.</span></span> <span data-ttu-id="8be33-205">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="8be33-205">Click **add user attribute**.</span></span> 

    ![Configure Single Sign-On][23]

    <span data-ttu-id="8be33-207">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-207">b.</span></span> <span data-ttu-id="8be33-208">In the **Attribute Name** textbox, type the **Attribute Name** and as **Attribute Value**, select the Attribute Value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="8be33-208">In the **Attribute Name** textbox, type the **Attribute Name** and as **Attribute Value**, select the Attribute Value shown for that row.</span></span>

    ![Configure Single Sign-On][22]

    <span data-ttu-id="8be33-210">c.</span><span class="sxs-lookup"><span data-stu-id="8be33-210">c.</span></span> <span data-ttu-id="8be33-211">Click **add user attribute**.</span><span class="sxs-lookup"><span data-stu-id="8be33-211">Click **add user attribute**.</span></span> 

    ![Configure Single Sign-On][23]

1. <span data-ttu-id="8be33-213">Click **Apply Changes**.</span><span class="sxs-lookup"><span data-stu-id="8be33-213">Click **Apply Changes**.</span></span> 
   
    ![Configure Single Sign-On][24]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8be33-215">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8be33-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="8be33-216">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8be33-216">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="8be33-218">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8be33-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8be33-219">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8be33-219">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="8be33-221">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8be33-221">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8be33-222">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8be33-222">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="8be33-224">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="8be33-224">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="8be33-226">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-226">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="8be33-228">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-228">a.</span></span> <span data-ttu-id="8be33-229">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="8be33-229">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="8be33-230">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-230">b.</span></span> <span data-ttu-id="8be33-231">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8be33-231">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8be33-232">c.</span><span class="sxs-lookup"><span data-stu-id="8be33-232">c.</span></span> <span data-ttu-id="8be33-233">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8be33-233">Click **Next**.</span></span>
6. <span data-ttu-id="8be33-234">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-234">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="8be33-236">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-236">a.</span></span> <span data-ttu-id="8be33-237">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8be33-237">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="8be33-238">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-238">b.</span></span> <span data-ttu-id="8be33-239">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8be33-239">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="8be33-240">c.</span><span class="sxs-lookup"><span data-stu-id="8be33-240">c.</span></span> <span data-ttu-id="8be33-241">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8be33-241">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="8be33-242">d.</span><span class="sxs-lookup"><span data-stu-id="8be33-242">d.</span></span> <span data-ttu-id="8be33-243">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8be33-243">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="8be33-244">e.</span><span class="sxs-lookup"><span data-stu-id="8be33-244">e.</span></span> <span data-ttu-id="8be33-245">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8be33-245">Click **Next**.</span></span>
7. <span data-ttu-id="8be33-246">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="8be33-246">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="8be33-248">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-248">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="8be33-250">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-250">a.</span></span> <span data-ttu-id="8be33-251">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="8be33-251">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="8be33-252">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-252">b.</span></span> <span data-ttu-id="8be33-253">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8be33-253">Click **Complete**.</span></span>   

### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="8be33-254">Creating a SD Elements test user</span><span class="sxs-lookup"><span data-stu-id="8be33-254">Creating a SD Elements test user</span></span>
<span data-ttu-id="8be33-255">The objective of this section is to create a user called Britta Simon in SD Elements.</span><span class="sxs-lookup"><span data-stu-id="8be33-255">The objective of this section is to create a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="8be33-256">In the case of SD Elements, creating SD Elements users is a manual task.</span><span class="sxs-lookup"><span data-stu-id="8be33-256">In the case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="8be33-257">**To create Britta Simon in SD Elements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8be33-257">**To create Britta Simon in SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="8be33-258">In a web browser window, sign-on to your SD Elements company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8be33-258">In a web browser window, sign-on to your SD Elements company site as an administrator.</span></span>
2. <span data-ttu-id="8be33-259">In the menu on the top, click User Management, and then Users.</span><span class="sxs-lookup"><span data-stu-id="8be33-259">In the menu on the top, click User Management, and then Users.</span></span>
   
   ![Creating a SD Elements test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 
3. <span data-ttu-id="8be33-261">Click Add New User.</span><span class="sxs-lookup"><span data-stu-id="8be33-261">Click Add New User.</span></span>
   
   ![Creating a SD Elements test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png) 
4. <span data-ttu-id="8be33-263">On the Add New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8be33-263">On the Add New User dialog, perform the following steps:</span></span>
   
   ![Creating a SD Elements test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
   <span data-ttu-id="8be33-265">a.</span><span class="sxs-lookup"><span data-stu-id="8be33-265">a.</span></span> <span data-ttu-id="8be33-266">In the **E-mail** textbox, type Britta's email address in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8be33-266">In the **E-mail** textbox, type Britta's email address in Azure AD.</span></span>
   
   <span data-ttu-id="8be33-267">b.</span><span class="sxs-lookup"><span data-stu-id="8be33-267">b.</span></span> <span data-ttu-id="8be33-268">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8be33-268">In the **First Name** textbox, type **Britta**.</span></span>
   
   <span data-ttu-id="8be33-269">c.</span><span class="sxs-lookup"><span data-stu-id="8be33-269">c.</span></span> <span data-ttu-id="8be33-270">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8be33-270">In the **Last Name** textbox, type **Simon**.</span></span>
   
   <span data-ttu-id="8be33-271">d.</span><span class="sxs-lookup"><span data-stu-id="8be33-271">d.</span></span> <span data-ttu-id="8be33-272">As **Role**, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8be33-272">As **Role**, select **User**.</span></span> 
   
   <span data-ttu-id="8be33-273">e.</span><span class="sxs-lookup"><span data-stu-id="8be33-273">e.</span></span> <span data-ttu-id="8be33-274">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="8be33-274">Click **Create User**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8be33-275">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8be33-275">Assigning the Azure AD test user</span></span>
<span data-ttu-id="8be33-276">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SD Elements.</span><span class="sxs-lookup"><span data-stu-id="8be33-276">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SD Elements.</span></span>

![Assign User][200] 

<span data-ttu-id="8be33-278">**To assign Britta Simon to SD Elements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8be33-278">**To assign Britta Simon to SD Elements, perform the following steps:**</span></span>

1. <span data-ttu-id="8be33-279">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8be33-279">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="8be33-281">In the applications list, select **SD Elements**.</span><span class="sxs-lookup"><span data-stu-id="8be33-281">In the applications list, select **SD Elements**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_50.png) 
3. <span data-ttu-id="8be33-283">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8be33-283">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="8be33-285">In the **Users** list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8be33-285">In the **Users** list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8be33-286">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8be33-286">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8be33-288">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8be33-288">Testing Single Sign-On</span></span>
<span data-ttu-id="8be33-289">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8be33-289">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="8be33-290">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span><span class="sxs-lookup"><span data-stu-id="8be33-290">When you click the SD Elements tile in the Access Panel, you should get automatically signed-on to your SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8be33-291">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="8be33-291">Additional Resources</span></span>
* [<span data-ttu-id="8be33-292">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8be33-292">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8be33-293">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8be33-293">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_80.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_82.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_81.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_83.png


[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sd-elements-tutorial/tutorial_general_205.png



































