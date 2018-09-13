---
title: 'Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Ceridian Dayforce HCM.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 6925d347ef6d0625c41b7fd48b6d65bb02534069
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549773"
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="87ca7-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="87ca7-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>
<span data-ttu-id="87ca7-104">The objective of this tutorial is to show you how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87ca7-104">The objective of this tutorial is to show you how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="87ca7-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="87ca7-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="87ca7-106">You can control in Azure AD who has access to Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="87ca7-106">You can control in Azure AD who has access to Ceridian Dayforce HCM</span></span>
* <span data-ttu-id="87ca7-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="87ca7-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="87ca7-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="87ca7-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="87ca7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87ca7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87ca7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="87ca7-110">Prerequisites</span></span>
<span data-ttu-id="87ca7-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="87ca7-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

* <span data-ttu-id="87ca7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="87ca7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="87ca7-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="87ca7-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87ca7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="87ca7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="87ca7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="87ca7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="87ca7-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="87ca7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="87ca7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87ca7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87ca7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="87ca7-118">Scenario description</span></span>
<span data-ttu-id="87ca7-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="87ca7-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="87ca7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="87ca7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87ca7-121">Adding Ceridian Dayforce HCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="87ca7-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="87ca7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87ca7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="87ca7-123">Adding Ceridian Dayforce HCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="87ca7-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="87ca7-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="87ca7-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87ca7-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87ca7-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87ca7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="87ca7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="87ca7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="87ca7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="87ca7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="87ca7-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="87ca7-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="87ca7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="87ca7-135">In the search box, type **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-135">In the search box, type **Ceridian Dayforce HCM**.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_01.png)
7. <span data-ttu-id="87ca7-137">In the results pane, select **Ceridian Dayforce HCM**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="87ca7-137">In the results pane, select **Ceridian Dayforce HCM**, and then click **Complete** to add the application.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87ca7-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87ca7-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87ca7-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="87ca7-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87ca7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="87ca7-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM to an user in Azure AD is.</span></span> <span data-ttu-id="87ca7-142">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="87ca7-142">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="87ca7-143">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="87ca7-143">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87ca7-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="87ca7-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87ca7-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87ca7-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87ca7-146">**[Creating a Ceridian Dayforce HCM test user](#creating-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="87ca7-146">**[Creating a Ceridian Dayforce HCM test user](#creating-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="87ca7-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="87ca7-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87ca7-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="87ca7-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87ca7-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87ca7-149">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="87ca7-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="87ca7-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="87ca7-151">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="87ca7-151">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="87ca7-152">Please work with Dayforce HCM team first to identify the correct user identifier.</span><span class="sxs-lookup"><span data-stu-id="87ca7-152">Please work with Dayforce HCM team first to identify the correct user identifier.</span></span> <span data-ttu-id="87ca7-153">Microsoft recommends using the **"name"** attribute as user identifier.</span><span class="sxs-lookup"><span data-stu-id="87ca7-153">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="87ca7-154">You can manage the value of this attribute on the **"Atrribute"** dialog.</span><span class="sxs-lookup"><span data-stu-id="87ca7-154">You can manage the value of this attribute on the **"Atrribute"** dialog.</span></span> <span data-ttu-id="87ca7-155">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="87ca7-155">The following screenshot shows an example for this.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_02.png) 

<span data-ttu-id="87ca7-157">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87ca7-157">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="87ca7-158">In the Azure classic portal, on the **Ceridian Dayforce HCM** application integration page, in the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-158">In the Azure classic portal, on the **Ceridian Dayforce HCM** application integration page, in the menu on the top, click **Attributes**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_81.png) 
2. <span data-ttu-id="87ca7-160">In the attributes **saml token attributes** list, select the name attribute, and then click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-160">In the attributes **saml token attributes** list, select the name attribute, and then click **Edit**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_06.png) 
3. <span data-ttu-id="87ca7-162">On the **Edit User Attribute** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87ca7-162">On the **Edit User Attribute** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="87ca7-163">a.</span><span class="sxs-lookup"><span data-stu-id="87ca7-163">a.</span></span> <span data-ttu-id="87ca7-164">From the **Attribute Value** list, select the user attribute you want to use for your implementation.</span><span class="sxs-lookup"><span data-stu-id="87ca7-164">From the **Attribute Value** list, select the user attribute you want to use for your implementation.</span></span>  
    <span data-ttu-id="87ca7-165">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-165">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span> 
   
    <span data-ttu-id="87ca7-166">b.</span><span class="sxs-lookup"><span data-stu-id="87ca7-166">b.</span></span> <span data-ttu-id="87ca7-167">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-167">Click **Complete**.</span></span>    
4. <span data-ttu-id="87ca7-168">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-168">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hightail-tutorial/tutorial_general_83.png)  
5. <span data-ttu-id="87ca7-170">In the Azure classic portal, on the **Ceridian Dayforce HCM** application integration page, click **Configure single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-170">In the Azure classic portal, on the **Ceridian Dayforce HCM** application integration page, click **Configure single sign-on**.</span></span>
   
    ![Configure Single Sign-On][6] 
6. <span data-ttu-id="87ca7-172">On the **How would you like users to sign on to Ceridian Dayforce HCM** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-172">On the **How would you like users to sign on to Ceridian Dayforce HCM** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_03.png) 
7. <span data-ttu-id="87ca7-174">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="87ca7-174">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_04.png) 

    <span data-ttu-id="87ca7-176">a.</span><span class="sxs-lookup"><span data-stu-id="87ca7-176">a.</span></span> <span data-ttu-id="87ca7-177">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="87ca7-177">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span> <span data-ttu-id="87ca7-178">For production environments, use the following URL format: `https://sso.dayforcehcm.com/DayforcehcmNamespace`</span><span class="sxs-lookup"><span data-stu-id="87ca7-178">For production environments, use the following URL format: `https://sso.dayforcehcm.com/DayforcehcmNamespace`</span></span>

    <span data-ttu-id="87ca7-179">For clarity, replace DayforcehcmNamespace with the namespace of your environment or your Company ID; for example: `https://sso.dayforcehcm.com/contoso`</span><span class="sxs-lookup"><span data-stu-id="87ca7-179">For clarity, replace DayforcehcmNamespace with the namespace of your environment or your Company ID; for example: `https://sso.dayforcehcm.com/contoso`</span></span>

    <span data-ttu-id="87ca7-180">For test environments, use the following URL format: `https://ssotest.dayforcehcm.com/DayforcehcmNamespace`</span><span class="sxs-lookup"><span data-stu-id="87ca7-180">For test environments, use the following URL format: `https://ssotest.dayforcehcm.com/DayforcehcmNamespace`</span></span> 

    <span data-ttu-id="87ca7-181">b.</span><span class="sxs-lookup"><span data-stu-id="87ca7-181">b.</span></span> <span data-ttu-id="87ca7-182">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span><span class="sxs-lookup"><span data-stu-id="87ca7-182">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>  
    <span data-ttu-id="87ca7-183">For production environments, use: `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="87ca7-183">For production environments, use: `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2`</span></span>  
    <span data-ttu-id="87ca7-184">For test environments, use: `https://fs-test.dayforcehcm.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="87ca7-184">For test environments, use: `https://fs-test.dayforcehcm.com/sp/ACS.saml2`</span></span>  

1. <span data-ttu-id="87ca7-185">On the **Configure single sign-on at Ceridian Dayforce HCM** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87ca7-185">On the **Configure single sign-on at Ceridian Dayforce HCM** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_05.png) 
   
    <span data-ttu-id="87ca7-187">a.</span><span class="sxs-lookup"><span data-stu-id="87ca7-187">a.</span></span> <span data-ttu-id="87ca7-188">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="87ca7-188">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="87ca7-189">b.</span><span class="sxs-lookup"><span data-stu-id="87ca7-189">b.</span></span> <span data-ttu-id="87ca7-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-190">Click **Next**.</span></span>
2. <span data-ttu-id="87ca7-191">To get SSO configured for your application, contact your Ceridian Dayforce HCM support team via email, and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="87ca7-191">To get SSO configured for your application, contact your Ceridian Dayforce HCM support team via email, and provide them with the following:</span></span>
   
   * <span data-ttu-id="87ca7-192">The downloaded certificate file</span><span class="sxs-lookup"><span data-stu-id="87ca7-192">The downloaded certificate file</span></span>
   * <span data-ttu-id="87ca7-193">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="87ca7-193">The **Issuer URL**</span></span>
   * <span data-ttu-id="87ca7-194">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="87ca7-194">The **SAML SSO URL**</span></span> 
   * <span data-ttu-id="87ca7-195">The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="87ca7-195">The **Single Sign Out Service URL**</span></span> 
3. <span data-ttu-id="87ca7-196">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-196">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="87ca7-198">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-198">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87ca7-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="87ca7-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="87ca7-201">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87ca7-201">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="87ca7-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87ca7-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87ca7-204">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-204">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="87ca7-206">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="87ca7-206">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="87ca7-207">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-207">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="87ca7-209">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-209">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="87ca7-211">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87ca7-211">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="87ca7-213">a.</span><span class="sxs-lookup"><span data-stu-id="87ca7-213">a.</span></span> <span data-ttu-id="87ca7-214">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="87ca7-214">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="87ca7-215">b.</span><span class="sxs-lookup"><span data-stu-id="87ca7-215">b.</span></span> <span data-ttu-id="87ca7-216">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-216">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="87ca7-217">c.</span><span class="sxs-lookup"><span data-stu-id="87ca7-217">c.</span></span> <span data-ttu-id="87ca7-218">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-218">Click **Next**.</span></span>
6. <span data-ttu-id="87ca7-219">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87ca7-219">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="87ca7-221">a.</span><span class="sxs-lookup"><span data-stu-id="87ca7-221">a.</span></span> <span data-ttu-id="87ca7-222">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-222">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="87ca7-223">b.</span><span class="sxs-lookup"><span data-stu-id="87ca7-223">b.</span></span> <span data-ttu-id="87ca7-224">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-224">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="87ca7-225">c.</span><span class="sxs-lookup"><span data-stu-id="87ca7-225">c.</span></span> <span data-ttu-id="87ca7-226">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-226">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="87ca7-227">d.</span><span class="sxs-lookup"><span data-stu-id="87ca7-227">d.</span></span> <span data-ttu-id="87ca7-228">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-228">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="87ca7-229">e.</span><span class="sxs-lookup"><span data-stu-id="87ca7-229">e.</span></span> <span data-ttu-id="87ca7-230">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-230">Click **Next**.</span></span>

7. <span data-ttu-id="87ca7-231">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-231">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="87ca7-233">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87ca7-233">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="87ca7-235">a.</span><span class="sxs-lookup"><span data-stu-id="87ca7-235">a.</span></span> <span data-ttu-id="87ca7-236">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-236">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="87ca7-237">b.</span><span class="sxs-lookup"><span data-stu-id="87ca7-237">b.</span></span> <span data-ttu-id="87ca7-238">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-238">Click **Complete**.</span></span>   

### <a name="creating-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="87ca7-239">Creating a Ceridian Dayforce HCM test user</span><span class="sxs-lookup"><span data-stu-id="87ca7-239">Creating a Ceridian Dayforce HCM test user</span></span>
<span data-ttu-id="87ca7-240">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="87ca7-240">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> 

<span data-ttu-id="87ca7-241">Please work with the Ceridian Dayforce HCM support team to get users added to your in the Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="87ca7-241">Please work with the Ceridian Dayforce HCM support team to get users added to your in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="87ca7-242">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="87ca7-242">Assigning the Azure AD test user</span></span>
<span data-ttu-id="87ca7-243">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Ceridian Dayforce HCM.</span><span class="sxs-lookup"><span data-stu-id="87ca7-243">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Ceridian Dayforce HCM.</span></span>

![Assign User][200] 

<span data-ttu-id="87ca7-245">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87ca7-245">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="87ca7-246">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="87ca7-246">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="87ca7-248">In the applications list, select **Ceridian Dayforce HCM**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-248">In the applications list, select **Ceridian Dayforce HCM**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_50.png) 
3. <span data-ttu-id="87ca7-250">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-250">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="87ca7-252">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-252">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="87ca7-253">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="87ca7-253">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="87ca7-255">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="87ca7-255">Testing single sign-on</span></span>
<span data-ttu-id="87ca7-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="87ca7-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="87ca7-257">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span><span class="sxs-lookup"><span data-stu-id="87ca7-257">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87ca7-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="87ca7-258">Additional resources</span></span>
* [<span data-ttu-id="87ca7-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87ca7-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87ca7-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87ca7-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_205.png





























